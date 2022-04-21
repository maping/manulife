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

## Reference
- [ASP.NET Tutorial - Hello World in 5 minutes](https://dotnet.microsoft.com/en-us/learn/aspnet/hello-world-tutorial/intro)
- [Quickstart: Deploy an ASP.NET web app](https://docs.microsoft.com/en-us/azure/app-service/quickstart-dotnetcore?tabs=net60&pivots=development-environment-cli)
