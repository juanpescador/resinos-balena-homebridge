# ResinOS balena Homebridge

This Docker image lets you run oznu's Docker Homebridge image on a Raspberry Pi
with ResinOS by disabling Avahi.

## Usage

    balena run \
    --net=host \
    -e TZ=Europe/Madrid \
    -e HOMEBRIDGE_CONFIG_UI=1 \
    -e HOMEBRIDGE_CONFIG_UI_PORT=8080 \
    -v /mnt/data/resin-data/homebridge:/homebridge \
    -v /var/run/dbus:/var/run/dbus \
    oznu/homebridge:raspberry-pi

Mounting `/var/run/dbus` allows the docker container to use the host ResinOS'
Avahi daemon.

Mounting `/mnt/data/resin-data/homebridge` allows homebridge's configuration to
be stored outside the container, following ResinOS' convention.

## Details

ResinOS already provides an Avahi daemon which conflicts with the Avahi daemon
running in oznu's Docker Homebridge, resulting in log messages like this:

    Node00b01973d6c8 daemon.notice avahi-daemon[1624]: Service name conflict for "%h" (/services/ssh.service), retrying with "Node00b01973d6c8 #2".

