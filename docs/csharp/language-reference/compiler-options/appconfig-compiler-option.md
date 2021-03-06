---
title: "/appconfig (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/appconfig"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/appconfig compiler option [C#]"
ms.assetid: 1cdbcbcc-7813-4010-b5b8-e67c107c5a98
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# /appconfig (C# Compiler Options)
La opción del compilador **\/appconfig** permite a una aplicación de C\# especificar la ubicación del archivo de configuración de la aplicación de un ensamblado \(app.config\) al Common Language Runtime \(CLR\) en tiempo de enlace del ensamblado.  
  
## Sintaxis  
  
```  
/appconfig:file  
```  
  
## Argumentos  
 `file`  
 Obligatorio.  El archivo de configuración de la aplicación que contiene los valores de enlace del ensamblado.  
  
## Comentarios  
 Un uso de **\/appconfig** es escenarios avanzadas en las que un ensamblado tiene que hacer referencia a la versión de .NET Framework y la versión de .NET Framework para Silverlight de un ensamblado determinado de la referencia al mismo tiempo.  Por ejemplo, un diseñador de XAML escrito en Windows Presentation Foundation \(WPF\) podría tener que hacer referencia al escritorio de WPF, de la interfaz de usuario del diseñador, y al subconjunto de WPF que se incluye con Silverlight.  El mismo ensamblado del diseñador tiene que tener acceso a ambos ensamblados.  De forma predeterminada, las referencias independientes producen un error del compilador, ya que el enlace del ensamblado considera los dos ensamblados equivalentes.  
  
 La opción del compilador **\/appconfig** le permite especificar la ubicación de un archivo app.config que deshabilita el comportamiento predeterminado utilizando una etiqueta `<supportPortability>`, como se muestra en el siguiente ejemplo.  
  
 `<supportPortability PKT="7cec85d7bea7798e" enable="false"/>`  
  
 El compilador pasa la ubicación del archivo a la lógica de enlace del ensamblado de CLR.  
  
> [!NOTE]
>  Si está usando Microsoft Build Engine \(MSBuild\) para compilar su aplicación, puede establecer la opción del compilador **\/appconfig** mediante la adición de una etiqueta de propiedad al archivo .csproj.  Para utilizar el archivo app.config que ya está establecida en el proyecto, agregue la etiqueta `<UseAppConfigForCompiler>` de propiedades al archivo .csproj y establezca su valor en `true`.  Para especificar otro archivo app.config, agregue la etiqueta `<AppConfigForCompiler>` y establezca su valor en la ubicación del archivo.  
  
## Ejemplo  
 En el siguiente ejemplo se muestra un archivo app.config que permite a una aplicación tener referencias a la implementación de .NET Framework y de .NET Framework para Silverlight de cualquier ensamblado de .NET Framework que exista en ambas implementaciones.  La opción del compilador **\/appconfig** especifica la ubicación de este archivo app.config.  
  
```  
<configuration>  
      <runtime>  
      <assemblyBinding>  
            <supportPortability PKT="7cec85d7bea7798e" enable="false"/>  
            <supportPortability PKT="31bf3856ad364e35" enable="false"/>  
      </assemblyBinding>  
      </runtime>  
</configuration>  
```  
  
## Vea también  
 [.NET Framework Assembly Unification Overview](http://msdn.microsoft.com/es-es/8d8cc65e-031d-463b-bde3-2c6dc2e3bc48)   
 [\<supportPortability\> \(Elemento\)](../Topic/%3CsupportPortability%3E%20Element.md)   
 [C\# Compiler Options Listed Alphabetically](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)