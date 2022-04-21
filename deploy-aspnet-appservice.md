# Deploy ASP.NET to Azure App Service

## 1. Create  Windows Server 2019 VM
```console
$ az group create --name Win-Server-RG --location japanwest
$ az vm create -g Win-Server-RG --name Win-Svr2019-VM --image win2019datacenter --admin-username xxxxxx --admin-password XXXXXXX
$ az vm show -g Win-Server-RG --name Win-Svr2019-VM -d --query [publicIps] -o tsv
```
>**Attention: please change to your username and password.**

## 2. Install Docker

Connect to VM by RDP

### 2.1 Install Windows Feature: containers 
Open a PowerShell terminal as Administrator 
```console
PS C:\Users\azureuser> Install-WindowsFeature containers

Success Restart Needed Exit Code      Feature Result
------- -------------- ---------      --------------
True    Yes            SuccessRest... {Containers}
WARNING: You must restart this server to finish the installation process.
```
>**Important: Restart VM after installing docker.**

### 2.2 Install Docker
Open a PowerShell terminal as Administrator 
```console
PS C:\Users\azureuser> Install-Module -Name DockerMsftProvider -Repository PSGallery -Force

PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\azureuser\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by
running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install
and import the NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
```

```console
PS C:\Users\azureuser> Install-Package -Name docker -ProviderName DockerMsftProvider

The package(s) come(s) from a package source that is not marked as trusted.
Are you sure you want to install software from 'DockerDefault'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A

Name                           Version          Source           Summary
----                           -------          ------           -------
Docker                         20.10.9          DockerDefault    Contains Docker EE for use with Windows Server.
```
>**Important: Restart VM after installing this feature.**

### 2.3 Verify Docker Installation

```console
PS C:\Users\azureuser> docker version

Client: Mirantis Container Runtime
 Version:           20.10.9
 API version:       1.41
 Go version:        go1.16.12m2
 Git commit:        591094d
 Built:             12/21/2021 21:34:30
 OS/Arch:           windows/amd64
 Context:           default
 Experimental:      true

Server: Mirantis Container Runtime
 Engine:
  Version:          20.10.9
  API version:      1.41 (minimum version 1.24)
  Go version:       go1.16.12m2
  Git commit:       9b96ce992b
  Built:            12/21/2021 21:33:06
  OS/Arch:          windows/amd64
  Experimental:     false
```

```console
PS C:\Users\azureuser> docker info

Client:
 Context:    default
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  cluster: Manage Mirantis Container Cloud clusters (Mirantis Inc., v1.9.0)
  registry: Manage Docker registries (Docker Inc., 0.1.0)

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 20.10.9
 Storage Driver: windowsfilter
  Windows:
 Logging Driver: json-file
 Plugins:
  Volume: local
  Network: ics internal l2bridge l2tunnel nat null overlay private transparent
  Log: awslogs etwlogs fluentd gcplogs gelf json-file local logentries splunk syslog
 Swarm: inactive
 Default Isolation: process
 Kernel Version: 10.0 17763 (17763.1.amd64fre.rs5_release.180914-1434)
 Operating System: Windows Server 2019 Datacenter Version 1809 (OS Build 17763.2803)
 OSType: windows
 Architecture: x86_64
 CPUs: 1
 Total Memory: 3.5GiB
 Name: Win-Svr2019-VM
 ID: EZB6:HNFF:CKRT:45PX:5TM4:GQJW:JTKV:BF7P:Q3XY:L4RC:4OVZ:VRZP
 Docker Root Dir: C:\ProgramData\docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
```

## 3. Docker Run

```console
PS C:\Users\azureuser> docker run -it mcr.microsoft.com/windows/servercore:ltsc2019
...
C:\> dir
 Volume in drive C has no label.
 Volume Serial Number is 4059-0A8C

 Directory of C:\

05/07/2020  04:48 AM             5,510 License.txt
04/04/2022  11:22 AM    <DIR>          Program Files
04/04/2022  11:20 AM    <DIR>          Program Files (x86)
04/04/2022  11:23 AM    <DIR>          Users
04/20/2022  12:03 PM    <DIR>          Windows
               1 File(s)          5,510 bytes
               4 Dir(s)  21,237,743,616 bytes free
C:\> exit
```

```console
PS C:\Users\azureuser> docker run --name aspnetapp --rm -it -p 8000:80 mcr.microsoft.com/dotnet/framework/aspnet:4.8

Unable to find image 'mcr.microsoft.com/dotnet/framework/aspnet:4.8' locally
4.8: Pulling from dotnet/framework/aspnet
4612f6d0b889: Already exists
ba8181afd426: Already exists
02ca74b83f10: Pull complete
5766b0ca35fc: Extracting [========>                                          ]  164.9MB/937.2MB
5de5a64e826d: Download complete
1138ad773a4b: Download complete
bdfef305d21d: Download complete
557c3762bd5b: Download complete
9ad16d6663a0: Download complete
2609e2178f13: Download complete
9991dcecae92: Download complete

Service 'w3svc' has been stopped

Service 'w3svc' started
```
Visit http://localhost:8000

## Reference
- [Containers on Windows documentation](https://docs.microsoft.com/en-us/virtualization/windowscontainers/)
- [Windows Server Core](https://hub.docker.com/_/microsoft-windows-servercore)
- [ASP.NET](https://hub.docker.com/_/microsoft-dotnet-framework-aspnet)
