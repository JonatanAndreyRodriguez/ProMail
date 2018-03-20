# ¿ProMail?

![Curent release](https://img.shields.io/badge/Version-1.0.0.0-orange.svg)

ProMail es un módulo de PowerShell que permite la automatización de procesos por correo electrónico, permitiendo crear reglas para la ejecución de procesos posteriores mediante de [Plugins](Setuo/Plugin-Manager.md), esto cuando se reciba un correo que coincida con una regla creada.
Para registrar una cuenta a monitorear :
- **Nota:**
En caso de no enviar los parametros EmailAddress y Pasword aparecera una ventana emergente solicitando las credenciales.
Todas las combinaciones del comando anterior permiten el parametro -Force el cual permite registrar una cuenta sin validar la conexion .
```powershell
Register-EmailAccount
Register-EmailAccount -Name $FileName -Force
```
<h2 align="center"><img src="Credential Dialog.png" /></h2>

```powershell
Register-EmailAccount -EmailAddress 'MyMail@Domain.com' Password $SecureString -Force
Register-EmailAccount -Name $FileName -EmailAddress 'MyMail@Domain.com' -Password $SecureString -Force
```
Con el comando Get-EmailAccount se puede validar la informacion de la cuenta creada.
```powershell
Get-EmailAccount -EmailAddress 'MyMail@Domain.com'
```
<h2 align="center"><img src="Get Account.png" /></h2>

Una vez registrada una cuenta es necesario crear una regla para obtener un correo especifico de la bandeja de entrada.

- **Nota:**
El Nombre de la regla debe ser Intuitivo ya que permite que varias reglas puedan tener el mismo nombre.

```powershell
$RuleInformation = @{
  Name             = $RuleName 
  AuthorizedSender = 'MyMail@MyDomain.com'
  Subject          = 'Subject To Process' 
  AttachmentsName  = '*.txt','AttachmentToProcess.txt' 
  PluginName       = $Plugin
}
Register-Rule @RuleInformation
```
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
Con el comando Get-Rule se puede validar la informacion con la cual se creo la regla:

```powershell
Get-Rule -Name MyRuleName
```
<h2 align="center"><img src="Get RuleName.png" /> </h2>

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
Esta es la configuracion basica para iniciar el proceso de [Monitoreo de correos](Monitor-Emails.md) del modulo. Para validar mas opciones de configuracion como agregar y quitar asuntos, aduntos, correos autorizados y cambios de contraseña puede validar las demas funciones del modulo.

## Estructura de la documentación
Las carpetas corresponden a los siguientes recursos de información:

| Carpeta  | Descripción  |
|:---|---|
| [Setup](Setup)  | Describe el proceso de instalación|
| [Funciones](Functions)  | Contiene las ayudas de las funciones publicas del módulo|