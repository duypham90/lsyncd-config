# lsyncd-config

## Document: 
- https://axkibe.github.io/lsyncd/manual/config/layer4/

## Setup ssh key for both servers
- https://vnsys.wordpress.com/2016/12/10/ssh-keys-2-chieu-tren-servers/

## Install lsyncd and required packages
- apt-get -y update
- apt-get -y install lsyncd

## Config lsync on both servers

 Server 1: 
  - create file: /etc/lsyncd.conf and add content below
 ```JS
settings {
    logfile = "/var/log/lsyncd.log",
    statusFile = "/var/log/lsyncd-status.log",
    statusInterval = 20
}

sync {
   default.rsync,
   delete = true,
   source = "/var/www/mulodo/",
   target = "18.222.133.152:/var/www/mulodo/",
   delay = 1,
   rsync = {
   archive =  true,
   perms = true,
   owner =  true,
   _extra = {"-a"},
    rsh = "/usr/bin/ssh -l ubuntu -i /home/ubuntu/.ssh/id_rsa -o StrictHostKeyChecking=no"
   }
}
```

### Server 2
- create file: /etc/lsyncd.conf and add content below

```JS
settings {
    logfile = "/var/log/lsyncd.log",
    statusFile = "/var/log/lsyncd-status.log",
    statusInterval = 20
}

sync {
   default.rsync,
   delete = true,
   source = "/var/www/mulodo/",
   target = "13.58.126.1:/var/www/mulodo/",
   delay = 1,
   rsync = {
   archive =  true,
   perms = true,
   owner =  true,
   _extra = {"-a"},
    rsh = "/usr/bin/ssh -i /home/ubuntu/.ssh/id_rsa -o StrictHostKeyChecking=no"
   }
}
```

## Restart and check log lsyncd on both servers
- Start: systemctl start lsyncd
- Restart: service lsyncd restart

## Test
 -  create file on server 1 and check on server 2 and reverse