---
title: EF Core tools for Package Manager Console (Visual Studio) - EF Core
author: bricelam
ms.author: bricelam
ms.date: 09/18/2018
---

# Entity Framework Core tools for Package Manager Console (Visual Studio)

The EF Core Package Manager Console (PMC) tools run inside of Visual Studio using the [Package Manager Console](https://docs.microsoft.com/nuget/tools/package-manager-console). These tools work with both .NET Framework and .NET Core projects.

If you aren't using Visual Studio, we recommend the [EF Core Command-line Tools](dotnet.md) instead. The CLI tools are cross-platform and run inside a command prompt.

## Installing the tools

Install the EF Core Package Manager Console tools by installing the `Microsoft.EntityFrameworkCore.Tools` NuGet package. Run the following command in **Package Manager Console**.

``` powershell
Install-Package Microsoft.EntityFrameworkCore.Tools
```

Verify successful installation by running this command:

``` powershell
Get-Help about_EntityFrameworkCore
```

## Before using the tools

If your startup project targets .NET Standard, [cross-target a supported framework][3] before using the tools.

> [!IMPORTANT]
> If you're using **Universal Windows** or **Xamarin**, move your EF code to a .NET Standard class library and
> [cross-target a supported framework][3] before using the tools. Specify the class library as your startup project.

## Target and startup project

Whenever you invoke a command, there are two projects involved:

* The *target project* is where any files are added (or in some cases removed). The target project defaults to the project in the current directory, but can be changed using the <nobr>**`--project`**</nobr> option.

* The *startup project* is the one emulated by the tools when executing your project's code. It also defaults to the project in the current directory, but can be changed using the <nobr>**`--startup-project`**</nobr> option.

For instance, here's a command to update the database of a web application that has EF Core installed in a different project. In this example, *WebProj* and *EFCoreProj* are projects at the same folder level. The command prompt is running in the *WebProj* folder.


```console
dotnet ef database update --project ./EFCoreProj
```
The target project is where any files are added (or in some cases removed). The target project defaults to the
**Default project** selected in Package Manager Console, but can also be specified using the -Project parameter.

The startup project is the one emulated by the tools when executing your project's code. It defaults to one
**Set as StartUp Project** in Solution Explorer. It can also be specified using the -StartupProject parameter.

Common parameters:

|                           |                             |
|:--------------------------|:----------------------------|
| -Context \<String>        | The DbContext to use.       |
| -Project \<String>        | The project to use.         |
| -StartupProject \<String> | The startup project to use. |
| -Verbose                  | Show verbose output.        |

To show help information about a command, use PowerShell's `Get-Help` command.

> [!TIP]
> The Context, Project, and StartupProject parameters support tab-expansion.

> [!TIP]
> Set **env:ASPNETCORE_ENVIRONMENT** before running to specify the ASP.NET Core environment.

Commands
--------

### Add-Migration

Adds a new migration.

Parameters:

|                                   |                                                                                                                  |
|:----------------------------------|:-----------------------------------------------------------------------------------------------------------------|
| ***-Name*** \<String>             | The name of the migration.                                                                                       |
| <nobr>-OutputDir \<String></nobr> | The directory (and sub-namespace) to use. Paths are relative to the project directory. Defaults to "Migrations". |

> [!NOTE]
> Parameters in **bold** are required, and ones in *italics* are positional.

### Drop-Database

Drops the database.

Parameters:

|         |                                                          |
|:--------|:---------------------------------------------------------|
| -WhatIf | Show which database would be dropped, but don't drop it. |

### Get-DbContext

Gets information about a DbContext type.

### Remove-Migration

Removes the last migration.

Parameters:

|        |                                                              |
|:-------|:-------------------------------------------------------------|
| -Force | Revert the migration if it has been applied to the database. |

### Scaffold-DbContext

Scaffolds a DbContext and entity types for a database.

Parameters:

|                                          |                                                                                                  |
|:-----------------------------------------|:-------------------------------------------------------------------------------------------------|
| <nobr>***-Connection*** \<String></nobr> | The connection string to the database.                                                           |
| ***-Provider*** \<String>                | The provider to use. (for example, Microsoft.EntityFrameworkCore.SqlServer)                      |
| -OutputDir \<String>                     | The directory to put files in. Paths are relative to the project directory.                      |
| -ContextDir \<String>                    | The directory to put DbContext file in. Paths are relative to the project directory.             |
| -Context \<String>                       | The name of the DbContext to generate.                                                           |
| -Schemas \<String[]>                     | The schemas of tables to generate entity types for.                                              |
| -Tables \<String[]>                      | The tables to generate entity types for.                                                         |
| -DataAnnotations                         | Use attributes to configure the model (where possible). If omitted, only the fluent API is used. |
| -UseDatabaseNames                        | Use table and column names directly from the database.                                           |
| -Force                                   | Overwrite existing files.                                                                        |

### Script-Migration

Generates a SQL script from migrations.

Parameters:

|                   |                                                                    |
|:------------------|:-------------------------------------------------------------------|
| *-From* \<String> | The starting migration. Defaults to 0 (the initial database).      |
| *-To* \<String>   | The ending migration. Defaults to the last migration.              |
| -Idempotent       | Generate a script that can be used on a database at any migration. |
| -Output \<String> | The file to write the result to.                                   |

> [!TIP]
> The To, From, and Output parameters support tab-expansion.

### Update-Database

|                                     |                                                                                                |
|:------------------------------------|:-----------------------------------------------------------------------------------------------|
| <nobr>*-Migration* \<String></nobr> | The target migration. If '0', all migrations will be reverted. Defaults to the last migration. |

> [!TIP]
> The Migration parameter supports tab-expansion.



  [3]: index.md#frameworks
