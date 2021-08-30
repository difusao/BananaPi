## TightVNCserver

> Setup
Install package.
```
sudo apt-get install -y tightvncserver
```

> Service install
Save file `/etc/server/init.d/vncserver`

```
#!/bin/bash
### BEGIN INIT INFO
# Provides:          vncserver
# Required-Start:
# Required-Stop:
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: vncserver
### END INIT INFO
# update-rc.d vncserver defaults

PATH="$PATH:/usr/bin/"
export USER="bananapi"
DISPLAY="1"
DEPTH="16"
GEOMETRY="1360x740"
OPTIONS="-depth ${DEPTH} -geometry ${GEOMETRY} :${DISPLAY} -desktop 'bCNC'"

. /lib/lsb/init-functions

PATH=/sbin:/usr/sbin:/bin:/usr/bin
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

. /lib/lsb/init-functions

case "$1" in
    start)
                log_action_begin_msg "Iniciando vncserver pelo usuario '${USER}' no display:${DISPLAY}"
                su ${USER} -c "vncserver ${OPTIONS}"
                ;;
    stop)
                log_action_begin_msg "Parando vncserver pelo usuario '${USER}' no display:${DISPLAY}"
                su ${USER} -c "vncserver -kill :${DISPLAY}"
                ;;
    restart)
                $0 stop
                $0 start
                ;;
    status)
                ;;
    *)
                echo "Usage: $0 start|stop|restart" >&2
                ;;
esac
```

Set file `/etc/init.d/vncserver` with exec.
```
sudo chmod 755 /etc/init.d/vncserver
```

Set start service on initialization system.
```
sudo update-rc.d vncserver defaults
```
or exec with user `bananapi`.
```
su bananapi -c 'vncserver'
```
> 
> Optionaly
Disable `lightdm` for most perfomance.
```
sudo update-rc.d -f lightdm disable
```
