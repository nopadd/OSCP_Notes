# General
When you find a new software / service:
1. Identify any NSE scripts that may work with the service.
```
locate .nse | grep -i [service name]
```
2. Identify if there are any MSF scripts / auxillary modules.
```
searchsploit [service name]
```
