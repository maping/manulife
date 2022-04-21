# Deploy a ASP.NET App to Azure App Service

## 1. Create a Web App
```console
$ dotnet new webapp -o MyWebApp --no-https -f net6.0
The template "ASP.NET Core Web App" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore/6.0-third-party-notices for details.

Processing post-creation actions...
Running 'dotnet restore' on C:\code\dotnet\MyWebApp\MyWebApp.csproj...
  Determining projects to restore...
  Restored C:\code\dotnet\MyWebApp\MyWebApp.csproj (in 81 ms).
Restore succeeded.
```

## 2. Run Web App Locally
```console
$ cd MyWebApp
$ dotnet watch
watch : Hot reload enabled. For a list of supported edits, see https://aka.ms/dotnet/hot-reload. Press "Ctrl + R" to restart.
watch : Building...
  Determining projects to restore...
  All projects are up-to-date for restore.
  MyWebApp -> C:\code\dotnet\MyWebApp\bin\Debug\net6.0\MyWebApp.dll
watch : Started
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://localhost:5276
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Development
info: Microsoft.Hosting.Lifetime[0]
      Content root path: C:\code\dotnet\MyWebApp\
```
Visit http://localhost:5276/

## 3. Deploy the Web App to Azure App Service
```console
$ cd MyWebApp
$ az webapp up -g ASPNET-RG -p mapingaspnet --sku F1 --name mapingaspnet --os-type windows -l japanwest
The webapp 'mapingaspnet' doesn't exist
Creating Resource group 'ASPNET-RG' ...
Resource group creation complete
Creating AppServicePlan 'mapingaspnet' ...
Creating webapp 'mapingaspnet' ...
Configuring default logging for the app, if not already enabled
Creating zip with contents of dir C:\code\dotnet\MyWebApp ...
Getting scm site credentials for zip deployment
Starting zip deployment. This operation can take a while to complete ...
Deployment endpoint responded with status code 202
You can launch the app at http://mapingaspnet.azurewebsites.net
Setting 'az webapp up' default arguments for current directory. Manage defaults with 'az configure --scope local'
--resource-group/-g default: ASPNET-RG
--sku default: F1
--plan/-p default: mapingaspnet
--location/-l default: japanwest
--name/-n default: mapingaspnet
Parameter persistence is turned on. Its information is saved in working directory C:\code\dotnet\MyWebApp. You can run `az config param-persist off` to turn it off.
Your preference of --resource-group: ASPNET-RG, --name: mapingaspnet, --location: japanwest are now saved as persistent parameter. To learn more, type in `az config param-persist --help`
{
  "URL": "http://mapingaspnet.azurewebsites.net",
  "appserviceplan": "mapingaspnet",
  "location": "japanwest",
  "name": "mapingaspnet",
  "os": "Windows",
  "resourcegroup": "ASPNET-RG",
  "runtime_version": "dotnet|5",
  "runtime_version_detected": "6.0",
  "sku": "FREE",
  "src_path": "C:\\code\\dotnet\\MyWebApp"
}
```
Visit http://mapingaspnet.azurewebsites.net

## Reference
- [ASP.NET Tutorial - Hello World in 5 minutes](https://dotnet.microsoft.com/en-us/learn/aspnet/hello-world-tutorial/intro)
- [Quickstart: Deploy an ASP.NET web app](https://docs.microsoft.com/en-us/azure/app-service/quickstart-dotnetcore?tabs=net60&pivots=development-environment-cli)
