**&larr; [Back to Project 2 README](../project2-csharp/README.md)**
# Development Environment and Setup

<!-- TOC -->
  * [Creating the C# ASP.NET MVC API Project](#creating-the-C#-ASP-NET-API-project)
  * [Using Microsoft SQL Server Database](#using-Microsoft-SQL-Server-database)
<!-- TOC -->

---
## Creating the C# ASP NET API Project
Create project via Visual Studio as an ASP.NET Core Web API 

## Using Microsoft SQL Server Database

The full application requires a database for data storage. The reference code uses a Microsoft SQL Server database. The connection string can use a Trusted Connection rather than specifying a user id and password.
The following shows the DB configuration that needs to be added to the Visual Studio project's appsettings.json file

```json
  "ConnectionStrings": {
    "EstateAgent": "Server=(local);Database=estateagent;Trusted_Connection=True;MultipleActiveResultSets=true;Encrypt=False"
  },
```

