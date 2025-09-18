# Optimizely:

This is just going to be things about optimizely, EPiserver.

## Installation:

https://www.nuget.org/packages/EPiServer.Templates/

Open console and type:

```console
dotnet new install EPiServer.Templates
```


## Licence:

Request a licence from this url:

https://license.optimizely.com/

Download it from the email and add it to the solutions root folder. Should show up in the Setting > Licence Information if done correctly.

## AppSettings.Json file:

Connection strings for your own database in Microsoft SQL Server Management Studio.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning",
      "Microsoft": "Warning",
      "EPiServer": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "EPiServerDB": "Data Source=SERVERNAME;Initial Catalog=DATABASENAME;Integrated Security=true;Connect Timeout=60;Persist Security Info=False;MultipleActiveResultSets=True;TrustServerCertificate=true;"
  }
}
```


