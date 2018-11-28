# Logs

ProMail utiliza el módulo [NLog](https://github.com/RD-Processa/NLog) el cual permite visualizar y registrar las etapas de ejecución de los módulos registrados, con información útil para el seguimiento de incidencias que se puedan presentar en cada ejecución.

**Visor de eventos**

Use el comando **Get-Source** para visualizar los módulos registrados en NLog.

```powershell
PS X> Get-Source

ID Name          Descripción
-- ------        -----------
1  PluginManager Descripción del origen PluginManager
2  ProMail       Descripción del origen ProMail
```

Para visualizar los últimos 10 eventos registrados en NLog para el modulo ProMail puede utilizar el siguiente ejemplo:

```powershell
Get-Source -Name 'ProMail' | Get-Log -Last 10
```
