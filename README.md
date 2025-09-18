# Optimizely:

This is just going to be things about optimizely, EPiserver.

## Installation:

Source: https://www.nuget.org/packages/EPiServer.Templates/

Open console and type:

```console
dotnet new install EPiServer.Templates
```

After having installed the package, create a new project and make sure the optimizely package is in the nuget source.

## Database and appsettings.json file:

Create a database in Microsoft SQL Server Management Studio.

Connection string for your own database in Microsoft SQL Server Management Studio. Switch out the servername and databasename.

```json
{
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "EPiServerDB": "Data Source=SERVERNAME;Initial Catalog=DATABASENAME;Integrated Security=true;Connect Timeout=60;Persist Security Info=False;MultipleActiveResultSets=True;TrustServerCertificate=true;"
  }
}
```

## Licence:

Request a licence from this url: https://license.optimizely.com/

The mac adress can be found under network settings on your computer or you can type "ipconfig /all" in the command console.

After sending the request, you will recieve an email. Download the file and add it to the solutions root folder. Should show up in the Setting > Licence Information in the optimizely backoffice if done correctly.

To reach the backoffice, start the project and go to https://localhost:5000/episerver/cms 

## Logging:

Source: https://www.jondjones.com/learn-optimizely/cms/setting-up-logging-with-optimizely-cms-12/

Start by installing the following packages:

```console
Install-Package Serilog
Install-Package Serilog.AspNetCore
Install-Package Microsoft.Extensions.Logging
Install-Package Serilog.Formatting.Compact
Install-Package Serilog.Sinks.File
```


















