Run command in background 
`[command] &`

list Jobs
`jobs -l`
result:
```
[1]+  Stopped                 bash
```

resume job in background
`bg %[n]` 

## jobs command options

Table 1: From the bash command man page

|Option|Description|
|---|---|
|**-l**|Show process id’s in addition to the normal information.|
|**-p**|Show process id’s only.|
|**-n**|Show only processes that have changed status since the last notification are printed.|
|**-r**|Restrict output to running jobs only.|
|**-s**|Restrict output to stopped jobs only.|
|**-x**|COMMAND is run after all job specifications that appear in ARGS have been replaced with the process ID of that job’s process group leader.|
