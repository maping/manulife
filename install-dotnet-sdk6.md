## 1. Install .NET SDK 6 

Download [dotnet-sdk-6.0.202-win-x64.exe](https://download.visualstudio.microsoft.com/download/pr/e4f4bbac-5660-45a9-8316-0ffc10765179/8ade57de09ce7f12d6411ed664f74eca/dotnet-sdk-6.0.202-win-x64.exe)

Double click dotnet-sdk-6.0.202-win-x86.exe file to install.

## 2. Verify Installation
Open a cmd terminal, type in
```console
$ dotnet --version
6.0.202
```

## 3. Create a Console App
```console
$ dotnet new console -o MyApp -f net6.0

Welcome to .NET 6.0!
---------------------
SDK Version: 6.0.202

Telemetry
---------
The .NET tools collect usage data in order to help us improve your experience. It is collected by Microsoft and shared with the community. You can opt-out of telemetry by setting the DOTNET_CLI_TELEMETRY_OPTOUT environment variable to '1' or 'true' using your favorite shell.

Read more about .NET CLI Tools telemetry: https://aka.ms/dotnet-cli-telemetry

----------------
Installed an ASP.NET Core HTTPS development certificate.
To trust the certificate run 'dotnet dev-certs https --trust' (Windows and macOS only).
Learn about HTTPS: https://aka.ms/dotnet-https
----------------
Write your first app: https://aka.ms/dotnet-hello-world
Find out what's new: https://aka.ms/dotnet-whats-new
Explore documentation: https://aka.ms/dotnet-docs
Report issues and find source on GitHub: https://github.com/dotnet/core
Use 'dotnet --help' to see available commands or visit: https://aka.ms/dotnet-cli
--------------------------------------------------------------------------------------
The template "Console App" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on C:\code\dotnet\MyApp\MyApp.csproj...
  Determining projects to restore...
  Restored C:\code\dotnet\MyApp\MyApp.csproj (in 96 ms).
Restore succeeded.
```

## 4. Run App
```console
$ cd MyApp
$ dotnet run
Hello, World!
```

## Reference
- [.NET Tutorial - Hello World in 5 minutes](https://dotnet.microsoft.com/en-us/learn/dotnet/hello-world-tutorial/install)
