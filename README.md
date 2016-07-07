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
* NXLog configuration (change with your graylog server or LB)
* Stream (dont forget to change MyRadiusServer with your host)
* Dashboard

## Requirements

* Freeradius 3 with linelog accounting
* NXLog collecting freeradius logs, other log collectors will work but may require modifying the searches to match the different fields outputted by other collectors

## NXLog Example
```
########################################
# Global directives                    #
########################################
User nxlog
Group nxlog

LogFile /var/log/nxlog/nxlog.log
LogLevel WARNING

########################################
# Modules                              #
########################################
<Extension gelf>
    Module      xm_gelf
</Extension>

<Extension json>
    Module      xm_json
</Extension>

<Input in1>
    Module      im_file
    File        '/var/log/radius/linelog-accounting'
    SavePos TRUE
    ReadFromLast TRUE
    Exec        parse_json();
</Input>

<Output out1>
    Module      om_tcp
    Host        graylog.server.com
    Port        12201
    OutputType  GELF_TCP
</Output>

########################################
# Routes                               #
########################################
<Route 1>
    Path        in1 => out1
</Route>

```

## Screenshots

![Dashboard](http://www.ohjeah.net/wp-content/uploads/2015/09/ad_audit.png)
