# Optimizely:

This is just going to be things about optimizely, EPiserver.

## Installation:

https://www.nuget.org/packages/EPiServer.Templates/

Open console and type:

```console
dotnet new install EPiServer.Templates
```

After having installed the package, create a new project and make sure the optimizely package is in the nuget source.

## Licence:

Request a licence from this url:

https://license.optimizely.com/

Download it from the email and add it to the solutions root folder. Should show up in the Setting > Licence Information in the optimizely backoffice if done correctly.

To reach the backoffice go to https://localhost:5000/episerver/cms 

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



