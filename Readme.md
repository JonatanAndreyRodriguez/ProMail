# ProMail

![Curent release](https://img.shields.io/badge/Version-1.0.6682.62258-orange.svg)

ProMail es un Módulo de PowerShell que permite la automatización de procesos por medio de la recepción de mensajes en una o varias cuentas de correo electrónico. Para su funcionamiento es necesario crear una o varias reglas asociadas a las cuentas de correo, que a su vez ejecutarán un proceso o acción mediante un [Plugin](Setup/Plugin-Manager.md).

**Para monitorear una cuenta de correo**

**1. Registrar cuenta de correo**
```powershell
Register-EmailAccount
Register-EmailAccount -Name $AccountName -Force
```
- **Nota:**
En caso de no enviar los parámetros **EmailAddress** y **Password** aparecerá una ventana emergente solicitando las credenciales.
Todas las combinaciones del comando anterior permiten el parámetro **-Force** el cual permite registrar una cuenta sin validar la conexión .

<h2 align="center"><img src="Setup/Credential Dialog.png" /></h2>
Ejemplos:

```powershell
Register-EmailAccount -EmailAddress 'MyMail@Domain.com' -Password $SecureString -Force
Register-EmailAccount -Name $AccountName -EmailAddress 'MyMail@Domain.com' -Password $SecureString -Force
```

Use el comando **Get-EmailAccount** para ver las propiedades de la cuenta creada.

```powershell
Get-EmailAccount -EmailAddress 'MyMail@Domain.com'
```
<h2 align="center"><img src="Setup/Get Account.png" /></h2>

**2. Creación de Regla**

La regla debe estar asociada a una cuenta de correo electrónico registrada anteriormente, Las reglas de la bandeja de entrada se utilizan para procesar los mensajes entrantes en función de las condiciones especificadas.

Ejemplo 1:
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

- **Nota:**
El nombre de la regla debe ser intuitivo y pueden existir varias reglas con el mismo nombre.

Ejemplo 2:
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
Use el comando **Get-Rule** para ver las propiedades de la regla de bandeja de entrada.

```powershell
Get-Rule -Name 'MyRuleName'
```
Ejemplo:
<h2 align="center"><img src="Setup/Get RuleName.png" /> </h2>

Cada regla tiene asignado un número identificador el cual se denomina **Id de Regla**, para el ejemplo anterior el número identificador tiene el valor de 14, el cual se utilizará para relacionar la cuenta de correo con la regla.

**3. Asociar una cuenta de correo con una regla**

Para asociar se debe establecer como parámetros la cuenta de correo y el número identificador de la regla, para el siguiente ejemplo, el número identificador de la regla tiene el valor de 14

Ejemplo:
```powershell
Get-EmailAccount -EmailAddress 'MyMail@MyDomain.com' | Add-RuleToEmailAccount -IdRule 14
```

Use el comando **Get-EmailAccount** para ver las reglas asociadas una cuenta:
```powershell
Get-EmailAccount -EmailAddress 'MyMail@MyDomain.com' | Get-Rule
```
Use el comando **Remove-RuleFromEmailAccount** para remover la regla asociadas a una cuenta, se debe tener presente la cuenta de correo y el número identificador de la regla, para el siguiente ejemplo, el número identificador de la regla tiene el valor de 1:
```powershell
Get-EmailAccount -EmailAddress 'MyMail@MyDomain.com' | Remove-RuleFromEmailAccount -IdRule 1
```

- **Nota:**
Los comandos y parámetros anteriormente señalados del módulo corresponden a la configuración básica para iniciar el proceso de [Monitoreo de correos](Setup/Monitor-Emails.md). Para ver mas opciones de configuración, ingresar a los link de Setup y Funciones expuestos en la estructura de la documentación.

## Estructura de la documentación
Las carpetas corresponden a los siguientes recursos de información:

| Carpeta  | Descripción  |
|:---|---|
| [Setup](Setup)  | Describe el proceso de instalación|
| [Funciones](Functions)  | Contiene las ayudas de las funciones públicas del módulo|
