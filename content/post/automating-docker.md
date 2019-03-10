---
title: "Automating Docker"
date: 2018-12-31T00:00:00-06:00
draft: false
tags: [docker]
---


If you do something more than once it should be automated or scripted in a repeatable manner. You likely have heard this before, and it applies across various task that support commands being run via any scripting language.

Docker is no different and has been picking up speed. Many post I have seen folks show how to run individual commands to pull down images. Microsoft has started publishing beta releases of Windows Server, SQL Server and even PowerShell via Docker images. This mechanism gives you the opportunity to play with features more quickly than having to go through constant install and uninstall process.

The talk around town right now is SQL Server 2019 preview releases. So to pull the latest CTP release of SQL Server you would see the following commands be issued in a command prompt:

```
PS C:\> docker pull mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
PS C:\> docker run -p 1416:1433 -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=P@ssword12345 -d mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
```

The output of the pull command will look something like this:

![](/images/dockerctppull.png)

The second command starts a new container and output of this is:

![](img/dockerrun.png)

The output includes use of the docker logs command where I can see SQL Server starting up to know when it is ready.

Once it starts up and accepts connections I can make a connection using SSMS or command line scripts. The server will be `localhost,1416` with the associated sa login and password set.

# Repeatable and automated

All of the above is nice but it is so time consuming to do this each time I want to get a full development playground up and running as a new CTP version is released.

There are two main files used with automating Docker:

- dockerfile
- docker-compose.yml

These two files can work together to build a custom image and then create the container(s). Note I can use the docker-compose file to create one container or multiple. Since the image is already built for us by Microsoft, I am just going to show the docker-compose file that can be used to automate rebuilding a container as each CTP is released for 2019.

# Docker-Compose

Docker compose gets deeper into deploying application services, but in laymen terms it is creating containers. You can use it to also create storage mounts and networking, but I’m just going to cover creating the containers in this post.

The contents of my file `C:\temp\sql19\docker-compose.yml` file are below:

```
version: '3.2'

services:

  sql19-01:
    image: mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
    environment:
      - ACCEPT_EULA=Y
      - SA_PASSWORD=db@t00ls12345
    ports:
      - '1417:1433'
    container_name: sql19-01

  sql19-02:
    image: mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
    environment:
      - ACCEPT_EULA=Y
      - SA_PASSWORD=db@t00ls12345
    ports:
      - '1418:1433'
    container_name: sql19-02
```

After I save this file I simply issue the following and it will create two containers for me based on the CTP2.2 release image:

```
docker-compose -f "docker-compose.yml" up -d --no-build
```

The output of this command:

![](/images/dockercompose.png)

As you can see one simple command does all that work for me. If you check docker network ls you will also see that a network for the containers is created as `sql19_network`, so whether you create 2 or 20 they will all be on the same network and be able to see each other.

I can now just throw that into my PowerShell profile, with a few adjustments:

```
function New-SqlContainer {
    param(
        [string]$path = 'c:\temp\sql19\docker-compose.yml'
    )

    docker-compose -f $path up -d --build --force-recreate
}
```

If tomorrow Microsoft releases CTP 2.3, I simply update that docker-compose file, to increment the version, and issue the command `New-SqlContainer` in my PowerShell prompt. Docker will go through pull the latest image and then recreate the containers for me:

![](/images/dockercompose2.png)

_If a new image had to be pulled down you would see the output for that as well._