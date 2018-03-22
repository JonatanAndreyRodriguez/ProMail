# Monitoreo de Correos Electrónicos
### Iniciar servicio de monitoreo

Para el monitoreo de correo electrónico se cuenta con un servicio que al ser iniciado utiliza la función :
```powershell
Start-Monitor
```
<h2 align="center"><img src="Start Service.png" /></h2>

Una vez iniciado el proceso de monitoreo se espera que un correo recibido cumpla con alguna de las reglas asociadas a alguna de las cuentas monitoreadas para ser procesado.
En cuanto se detecte un correo que cumpla con la regla se iniciará el proceso pertinente indicado en la regla como [Plugin](Plugin-Manager.md).

Para validar el estado de ejecución del monitoreo:
```powershell
Get-MonitorState
```
Para validar el proceso de un correo recibido se puede utilizar el siguiente comando.

```powershell
Get-JobState
```
- **Nota:**
después de completado el proceso del plugin la información del job será eliminada de la base de datos pero no del log del proceso.

Para detener el monitoreo se detendrá el servicio de Windows el cual internamente ejecutará la función:
```powershell
Stop-Monitor
```
<h2 align="center"><img src="Stop Service.png" /></h2>

Con esto terminará el monitoreo de los correo electrónicos.
