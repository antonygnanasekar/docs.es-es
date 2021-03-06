---
title: Comando dotnet-new | Microsoft Docs
description: El comando dotnet-new crea nuevos proyectos de .NET Core en el directorio actual.
keywords: dotnet-new, CLI, comando de CLI, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fcc3ed2e-9265-4d50-b59e-dc2e5c190b34
translationtype: Human Translation
ms.sourcegitcommit: 99254f84873003496ee00214d55ff908f9fd47d3
ms.openlocfilehash: f0df2efe732912abbdb2d63e918b7ee1a4178b07
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-new"></a>dotnet-new

## <a name="name"></a>Name
`dotnet-new`: crea un nuevo proyecto, archivo de configuración o solución según la plantilla especificada.

## <a name="synopsis"></a>Sinopsis
```
dotnet new <TEMPLATE> [-lang|--language] [-n|--name] [-o|--output] [-all|--show-all] [-h|--help] [Template arguments]
dotnet new <TEMPLATE> [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```

## <a name="description"></a>Descripción
El comando `dotnet new` proporciona una manera cómoda de inicializar un proyecto de .NET Core válido, junto con código fuente de ejemplo para probar el conjunto de herramientas de la interfaz de la línea de comandos (CLI). 

Cuando se invoca, el comando llama al [motor de plantillas](https://github.com/dotnet/templating) para crear los artefactos en el disco basándose en las opciones y la plantilla especificadas.

## <a name="arguments"></a>Argumentos

`<TEMPLATE>`

La plantilla de la que se va a crear una instancia cuando se invoca el comando. Cada plantilla puede tener opciones específicas que puede pasar. Para obtener más información, vea [Opciones de plantilla](#template-options).

El comando contiene una lista predeterminada de plantillas. Use `dotnet new -all` para ver todas.

En la siguiente tabla se muestran las plantillas que vienen preinstaladas con el SDK. El lenguaje predeterminado de la plantilla se muestra entre corchetes como `[C#]`.

|Descripción de plantilla  | Nombre de plantilla  | Lenguajes |
|----------------------|----------------|-----------|
| Aplicación de consola  | consola        | [C#], F#  |
| Biblioteca de clases        | classlib       | [C#], F#  |
| Proyecto de prueba unitaria    | mstest         | [C#], F#  |
| Proyecto de prueba xUnit   | xunit          | [C#], F#  |
| Vacío de ASP.NET Core   | web            | [C#]      |
| Aplicación web de ASP.NET Core | mvc            | [C#], F#  |
| API web de ASP.NET Core | webapi         | [C#]      |
| Configuración de NuGet         | nugetconfig    |           |
| Configuración de la Web           | webconfig      |           |
| Archivo de solución        | sln            |           |

## <a name="options"></a>Opciones

`-h|--help`

Imprime la ayuda para el comando. Puede invocarse para el propio comando `dotnet new` o para cualquier plantilla, como `dotnet new mvc --help`.

`-l|--list`

Muestra las plantillas que contienen el nombre especificado. Si se ha invocado para el propio comando `dotnet new`, muestra las plantillas posibles que se van a usar en el directorio determinado.
Por ejemplo, si el directorio ya contiene un proyecto, no mostrará todas las plantillas del proyecto.

`-lang|--language <C#|F#>`

El lenguaje de la plantilla que se va a crear. El lenguaje aceptado cambia según la plantilla (vea los valores predeterminados en la sección [argumentos](#arguments)). No es válido para algunas plantillas.

`-n|--name <OUTPUT_NAME>`

El nombre de la salida que se va a crear. Si no se especifica ningún nombre, se usa el nombre del directorio actual.

`-o|--output <OUTPUT_DIRECTORY>`

La ubicación para colocar la salida generada. El valor predeterminado es el directorio actual.

`-all|--show-all`

Muestra todas las plantillas de un tipo de proyecto específico cuando se ejecuta en el contexto del comando `dotnet new` por sí solo. Cuando se ejecuta en el contexto de una plantilla específica, como `dotnet new web -all`, `-all` se interpreta como una marca de creación de fuerza. Esto puede suceder cuando el directorio de salida ya contiene un proyecto.

## <a name="template-options"></a>Opciones de plantilla
Cada plantilla de proyecto puede tener opciones adicionales disponibles. Las plantillas principales tienen las siguientes opciones:

**console, xunit, mstest, web, webapi **

`-f|--framework`: especifica la plataforma de destino. Valores: netcoreapp1.0 o netcoreapp1.1 (Valor predeterminado: netcoreapp1.0)

**mvc**

`-f|--framework`: especifica la plataforma de destino. Valores: netcoreapp1.0 o netcoreapp1.1 (Valor predeterminado: netcoreapp1.0)

`-au|--authentication`: el tipo de autenticación que se va a usar. Valores: None o Individual (predeterminado: None)

`-uld|--use-local-db`: si se va a usar o no LocalDB en lugar de SQLite. Valores: true o false (valor predeterminado: false)

**classlib**

`-f|--framework`: especifica la plataforma de destino. Valores: netcoreapp1.0, netcoreapp1.1 y netstandard1.0 - 1.6 (Valor predeterminado: netstandard1.4).

## <a name="examples"></a>Ejemplos

Cree un proyecto de aplicación de consola con F# en el directorio actual:

`dotnet new console -lang f#` 
   
Cree un nuevo proyecto de aplicación MVC de ASP.NET Core C# en el directorio actual sin autenticación destinado a .NET Core 1.0:  

`dotnet new mvc -au None -f netcoreapp1.0`
 
Cree una nueva aplicación de XUnit destinada a .NET Core 1.1:

`dotnet new xunit --Framework netcoreapp1.1`

Enumere todas las plantillas disponibles para MVC:

`dotnet new mvc -l`

