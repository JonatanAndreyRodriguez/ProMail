# Monitoreo de Correos Electronicos
**Inicio de Monitoreo de Correo Electronico**

Para el monitoreo de correo electronico se cuenta con un servicio que al ser iniciado utiliza la funcion :
```powershell
Start-Monitor
```
<h2 align="center"><img src="Start Service.png" /></h2>

Una vez iniciado el proceso de monitoreo se espera que un correo recibido cumpla con alguna de las reglas asociadas a alguna de las cuentas monitoreadas para ser procesado.
En cuanto se detecte un correo que cumpla con la regla se iniciara el proceso pertinente indicado en la regla como [Plugin](Plugin-Manager.md).

Para validar el estado de ejecucion del monitoreo:
```powershell
Get-MonitorState
```
Para validar el proceso de un correo recibido se puede utilizar el sigueinte comando.
- **Nota:**
despues de completado el proceso del plugin la informacion del job sera eliminada de la base de datos pero no del log del proceso.

```powershell
Get-JobState
```

Para detener el monitoreo se dentendra el servicio de windows el cual internamente ejecutara la funcion:
```powershell
Stop-Monitor
```
<h2 align="center"><img src="Stop Service.png" /></h2>

Con esto terminara el monitoreo de los correo electronicos.
