# Installing Docker, PostgreSQL and DBeaver.


## 1.0 Installing Docker Hub in Windows Home 11.

### 1.1 Enabling virtualization on my home computer.

I ran into some problems first, as Windows Home is limited when it comes to virtualization. Had to enable virtualization from BIOS. Rebooted

### 1.2 Running script to 

Ran a script that allowed me to install HyperV. Found this from [MakeUseOf](https://www.makeuseof.com/install-hyper-v-windows-11-home/)

HYPERV.BAT

```
pushd "%~dp0"

dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt

for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"

del hyper-v.txt

Dism /online /enable-feature /featurename:Microsoft-Hyper-V -All /LimitAccess /ALL

Pause

```

Ran the script and rebooted the computer.

### 1.2 Updating WSL

Also for I had to update WSL (Windows Subsystem for Linux). This was only one line in CMD. After command I rebooted.

```
wsl --install
```

### 1.3 Installing Docker Hub and PostgreSQL on the docker hub.

These previous steps prevented me to install docker. Finally when everything was installed and updated. Installing docker was fairly easy. I downloaded the hub from their official [website](https://hub.docker.com/). Searched "postgre" and selected the right image.

## 2.0 Logging in and creating a instance

To access my docker, i had to login. At this point, I was already logged in as I had my hub open on my computer. 

```
$ docker login
```
![image](https://github.com/WindoCode/PostgresDocker/assets/110290723/c8dec2b5-c929-4ec9-9bb3-06df3de4bfec)


To create a instance, we use following command from the official documentation.

```
$ docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

-- name = name of the instance, we can edit this how we like. I used: windo-postgres,
-e = stands for enviromental variable, in this case "POSTGRES_PASSWORD", which is set to: mysecretpassword. This works as a root password to our instance.
-d = means detached mode, which means that container runs in the background and we can use terminal for other commands.
postgres = path to image in the official docker hub, where the image is downloaded. You can also add the version number, if you want to use some specific version.

I also added **-p 5432:5432**. -p stands for port. I want to use Dbeaver to connect to database, thats why we need a port.

![image](https://github.com/WindoCode/PostgresDocker/assets/110290723/3154417f-af9d-4d0e-8858-fd72b9801983)

![image](https://github.com/WindoCode/PostgresDocker/assets/110290723/bfc67b87-ca31-4ddd-b56c-c82874d128c4)

As we can see in the hub, the container is running. Alternatively we can use command ```docker ps``` to see, if the container is online.

![image](https://github.com/WindoCode/PostgresDocker/assets/110290723/46bdc5b6-2ff3-4d9d-8a0e-3ea6038341ef)







