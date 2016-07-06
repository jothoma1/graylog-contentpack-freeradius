# Freeradius 3 Accounting Content Pack for Graylog (https://www.graylog.org/)

Tested with nxLog/freeradius3/Graylog 2

This content pack provides useful dashboard for auditing freeradius accounting :
* Access from last week
* Top hourly accounting users
* Top hourly callingstation
* Start/Stop/Interim-Update
* VLAN
* NAS

## Includes

* Freeradius 3 linelog accounting configuration (in order to format log in JSON)
* NXLog configuration
* Stream (unconfigured)
* Dashboard

## Requirements

* Freeradius 3 with linelog accounting
* NXLog collecting freeradius logs, other log collectors will work but may require modifying the searches to match the different fields outputted by other collectors

## NXLog Example
```
define ROOT C:\Program Files (x86)\nxlog

Moduledir %ROOT%\modules
CacheDir %ROOT%\data
Pidfile %ROOT%\data\nxlog.pid
SpoolDir %ROOT%\data
LogFile %ROOT%\data\nxlog.log

<Extension gelf>
    Module xm_gelf
</Extension>
<Input in>
    # For windows vista/2008 and above use:
    Module      im_msvistalog

    # For windows 2003 and earlier use the following:
    #   Module      im_mseventlog
</Input>

<Output out> 
    Module      om_udp
    Host        graylog.server.com
    Port        5414
    OutputType  GELF
</Output>

<Route 1>
    Path        in => out
</Route>
```

## Screenshots

![Dashboard](http://www.ohjeah.net/wp-content/uploads/2015/09/ad_audit.png)
