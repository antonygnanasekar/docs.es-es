---
title: '#pragma checksum (Referencia de C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '#pragma checksum'
dev_langs:
- CSharp
helpviewer_keywords:
- '#pragma checksum [C#]'
ms.assetid: 3673e4ca-6098-4ec1-890f-8fceb2a794a2
caps.latest.revision: 11
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5daf71faea5736036e9e3e0178e84ea03c314ff6
ms.lasthandoff: 03/13/2017

---
# <a name="pragma-checksum-c-reference"></a>#pragma checksum (Referencia de C#)
Genera las sumas de comprobación para archivos de código fuente para ayudar en la depuración de páginas [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
#pragma checksum "filename" "{guid}" "checksum bytes"  
```  
  
#### <a name="parameters"></a>Parámetros  
 `"filename"`  
 El nombre del archivo que requiere la supervisión para cambios o actualizaciones.  
  
 `"{guid}"`  
 El identificador único global (GUID) del archivo.  
  
 `"checksum_bytes"`  
 La cadena de dígitos hexadecimales que representa los bytes de la suma de comprobación. Debe ser un número par de dígitos hexadecimales. Un número impar de dígitos produce una advertencia de tiempo de compilación y la directiva se ignora.  
  
## <a name="remarks"></a>Comentarios  
 El depurador de Visual Studio usa una suma de comprobación para asegurarse de que siempre encuentra el código fuente correcto. El compilador calcula la suma de comprobación para un archivo de origen y, después, emite el resultado en el archivo de base de datos del programa (PDB). Después, el depurador usa el archivo PDB para comparar la suma de comprobación que calcula para el archivo de origen.  
  
 Esta solución no funciona para proyectos de [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)], ya que la suma de comprobación calculada es para el archivo de código fuente generado, no para el archivo .aspx. Para solucionar este problema, `#pragma checksum` proporciona compatibilidad con la suma de comprobación para páginas [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)].  
  
 Cuando se crea un proyecto de [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] en [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)], el archivo de código fuente generado contiene una suma de comprobación para el archivo .aspx, desde el que se genera el código fuente. Después, el compilador escribe esta información en el archivo PDB.  
  
 Si el compilador no encuentra ninguna directiva `#pragma checksum` en el archivo, calcula la suma de comprobación y escribe el valor en el archivo PDB.  
  
## <a name="example"></a>Ejemplo  
  
```  
class TestClass  
{  
    static int Main()  
    {  
        #pragma checksum "file.cs" "{3673e4ca-6098-4ec1-890f-8fceb2a794a2}" "{012345678AB}" // New checksum  
    }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de C#](../../../csharp/language-reference/index.md)   
 [Guía de programación de C#](../../../csharp/programming-guide/index.md)   
 [Directivas de preprocesador de C#](../../../csharp/language-reference/preprocessor-directives/index.md)
