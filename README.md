# sbfspot-collector
SBFspot collector image

## Pre requisites
* solarexplorer/sbfspot-sqlite3-pi-base is available
* bluetooth is setup in your docker host / raspberry pi
* a user sbfspot is created with uid 2000

## Building
```
docker build -t solarexplorer/sbfspot-collector .
```

## Running SBFspot collector
```
docker run -it -v /etc/localtime:/etc/localtime:ro -v /home/sbfspot/data:/var/smadata -v /home/sbfspot/config/SBFspot.cfg:/opt/sbfspot/SBFspot.cfg --net=host --privileged --name sbfspot-collector solarexplorer/sbfspot-collector
```

N.B. in this run command the config file for SBFspot is externalized as well as de data directory. This way an update of the container will retain your data.

## Configure crontab on Docker host

If you want the SBFspot collector container to be run automatically you can use standard crontab functionality to run it at set intervals;

Run the following command as root:

```
(crontab -u sbfspot -l 2>/dev/null; echo "*/5 5-23 * * * docker start -a sbfspot-collector > /dev/null 2>&1") | crontab -u sbfspot -
```

