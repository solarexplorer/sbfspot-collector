# sbfspot-collector
SBFspot collector image

## Building
```
docker build explorer/sbfspot-collector .
```

## Running SBFspot collector
docker run -it -v /etc/localtime:/etc/localtime:ro -v /home/sbfspot/data:/var/smadata -v /home/sbfspot/config/SBFspot.cfg:/opt/sbfspot/SBFspot.cfg --net=host --privileged --name sbfspot-collector explorer/sbfspot-collector

## Configure crontab on Docker host

If you want the SBFspot collector container to be run automatically you can use standard crontab functionality to run it at set intervals;

Run the following command as root:

```
(crontab -u sbfspot -l 2>/dev/null; echo "*/5 5-23 * * * docker start -a sbfspot-collector > /dev/null 2>&1") | crontab -u sbfspot -
```

