# ProMail

![Curent release](https://img.shields.io/badge/Version-1.0.0.0-orange.svg)

ProMail es un Módulo de PowerShell que permite la automatización de procesos por medio de la recepción de mensajes en una o varias cuentas de correo electrónico. Para su funcionamiento es necesario crear una o varias reglas asociadas a las cuentas de correo, que a su vez ejecutarán un proceso o acción mediante un [Plugins](Setup/Plugin-Manager.md), esto cuando se reciba un correo que coincida con una regla creada.

# Para registrar una cuenta a monitorear

1. Registrar cuenta de correo
```powershell
Register-EmailAccount
Register-EmailAccount -Name $FileName -Force
```
- **Nota:**
En caso de no enviar los parametros EmailAddress y Password aparecerá una ventana emergente solicitando las credenciales.
Todas las combinaciones del comando anterior permiten el parametro -Force el cual permite registrar una cuenta sin validar la conexión .

<h2 align="center"><img src="Setup/Credential Dialog.png" /></h2>

```powershell
Register-EmailAccount -EmailAddress 'MyMail@Domain.com' Password $SecureString -Force
Register-EmailAccount -Name $FileName -EmailAddress 'MyMail@Domain.com' -Password $SecureString -Force
```
Con el comando Get-EmailAccount se puede validar la informacion de la cuenta creada.
```powershell
Get-EmailAccount -EmailAddress 'MyMail@Domain.com'
```
<h2 align="center"><img src="Setup/Get Account.png" /></h2>

2. Creación de Regla
```powershell
$RuleInformation = @{
  Name             = $RuleName 
  AuthorizedSender = 'MyMail@MyDomain.com'
  Subject          = 'Subject To Process' 
  AttachmentsName  = '*.txt','AttachmentToProcess.txt' 
  PluginName       = $Plugin
  ResponseTemplatePath = 'C:\PathFileCustomTemplate.html'
}
Register-Rule @RuleInformation
```
La regla debe estar asociada a una cuenta de correo electrónico registrada anteriormente, adicionalmente contempla una serie de parámetros de configuración para la ejecución de un proceso específico.

- **Nota:**
El nombre de la regla debe ser intuitivo y pueden existir varias reglas con el mismo nombre.

Ejemplo:
```powershell
$RuleInformation = @{
  Name                 = $RuleName 
  AuthorizedSenderPath = 'C:\PathFileAuthorizedEmails.txt'
  Subject              = 'Subject To Process' 
  AttachmentsName      = '*.txt','AttachmentToProcess.txt' 
  PluginName           = $Plugin
  ResponseTemplatePath = 'C:\PathFileCustomTemplate.html'
}
Register-Rule @RuleInformation
```
Use el cmdlet Get-InboxRule para ver las propiedades de la regla de Bandeja de entrada. Las reglas de la bandeja de entrada se utilizan para procesar los mensajes en la Bandeja de entrada en función de las condiciones especificadas y tomar medidas como mover un mensaje a una carpeta específica o eliminar un mensaje

Sintaxis
```powershell
Get-Rule -Name MyRuleName
```
<h2 align="center"><img src="Setup/Get RuleName.png" /> </h2>

Cuando se tenga la regla creada se debe asociar la regla a la cuenta.

```powershell
Get-EmailAccount -EmailAddress 'MyMail@MyDomain.com' | 
Add-RuleToEmailAccount -IdRule 14
```

Para validar que reglas tiene asociada una cuenta se puede utilizar el siguiente comando :
```powershell
Get-EmailAccount -EmailAddress 'MyMail@MyDomain.com' | Get-Rule
```
Para remover la asociacion de la regla a una cuenta:
```powershell
Get-EmailAccount -EmailAddress 'MyMail@MyDomain.com' | 
Remove-RuleFromEmailAccount -IdRule 1
```

- **Nota:**
Esta es la configuracion básica para iniciar el proceso de [Monitoreo de correos](Setup/Monitor-Emails.md) del modulo. Para validar mas opciones de configuracion como agregar y quitar asuntos, aduntos, correos autorizados y cambios de contraseña puede validar las demas funciones del modulo.

## Estructura de la documentación
Las carpetas corresponden a los siguientes recursos de información:

| Carpeta  | Descripción  |
|:---|---|
| [Setup](Setup)  | Describe el proceso de instalación|
| [Funciones](Functions)  | Contiene las ayudas de las funciones publicas del módulo|
