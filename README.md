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

Add the following to the program file:

```csharp
using Serilog;

namespace Optimizely002;

public class Program
{
    public static IConfiguration Configuration { get; } =
        new ConfigurationBuilder()
        .AddJsonFile("appSettings.json", false, true)
        .AddJsonFile($"appsettings.{Environment.GetEnvironmentVariable("ASPNETCORE_ENVIRONMENT")}.json", true, true)
        .AddJsonFile($"appsettings.{Environment.MachineName}.json", true, true)
        .AddEnvironmentVariables()
        .Build();

    public static void Main(string[] args)
    {
        Log.Logger = new LoggerConfiguration()
            .ReadFrom.Configuration(Configuration).WriteTo.Console().CreateLogger();

        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureCmsDefaults()
            .UseSerilog()   
            .ConfigureWebHostDefaults(webBuilder => webBuilder.UseStartup<Startup>());
}

```

Add in the appsetting:

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
  "Serilog": {
    "Using": [],
    "MinimumLevel": {
      "Default": "Warning",
      "Override": {
        "Microsoft": "Warning",
        "System": "Warning"
      }
    },
    "Enrich": [ "FromLogContext", "WithMachineName", "WithProcessId", "WithThreadId" ],
    "WriteTo": [
      {
        "Name": "File",
        "Args": {
          "path": "Logs/log.json",
          "rollingInterval": "Day",
          "formatter": "Serilog.Formatting.Json.JsonFormatter, Serilog"
        }
      }
    ]
  }
```



## Limiting page creation under root:

This is to lock down so that only certain types of pages can be created under the root.

```csharp
[InitializableModule]
[ModuleDependency(typeof(CmsCoreInitialization))]
public class RootPageInitialization : IInitializableModule
{
    public void Initialize(InitializationEngine context)
    {
        var contentTypeRepository = context.Locate.Advanced.GetInstance<IContentTypeRepository>();
        var sysRoot = contentTypeRepository.Load("SysRoot") as PageType;
        var setting = new AvailableSetting { Availability = Availability.Specific };

        setting.AllowedContentTypeNames.Add(contentTypeRepository.Load<StartPage>().Name);

        var avaliableSettingsRepository = context.Locate.Advanced.GetInstance<IAvailableSettingsRepository>();
        avaliableSettingsRepository.RegisterSetting(sysRoot, setting);
    }

    public void Uninitialize(InitializationEngine context)
    {
    }
}
```

## Adding icons to pages/blocks:

You create a wwwroot file. (Should have the globe next to it after creation)

Add images into folders. And then add the indicated line below:

```csharp
[ContentType(
    GUID = "623CEBCD-6DD4-47F2-B454-1C7E578AF466",
    GroupName = Globals.GroupNames.Specialized
    )]

[ImageUrl("/pages/CMS-icon-page-02.png")]    <===== This line.
public class StartPage : SitePageData
{
    [Display(
        GroupName = SystemTabNames.Content,
        Order = 10
        )]
    [CultureSpecific]
    
    public virtual string Heading { get; set; } = string.Empty;
}
```

And it should look like this after:

<img src="https://github.com/user-attachments/assets/72f5d374-98de-42ff-877e-1168bd3f61d4" width="400">


## Allowing image upload for pages:

In the models folder, create a class named ImageFile

```csharp
[ContentType(GUID = "7C62645B-4170-4415-A45A-2440FED397B4")]
[MediaDescriptor(ExtensionString = "jpg,jpeg,jpe,ico,gif,bmp,png,webp")]
public class ImageFile : ImageData
{
}
```




