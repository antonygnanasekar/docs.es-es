---
title: Crear agentes de escucha de registro personalizados (Visual Basic) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- custom log listeners
- My.Application.Log object, custom log listeners
ms.assetid: 0e019115-4b25-4820-afb1-af8c6e391698
caps.latest.revision: 19
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 98cec8d5077e777f18c18ad1af0040b3359151f7
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-creating-custom-log-listeners-visual-basic"></a>Tutorial: Crear agentes de escucha de registro personalizados (Visual Basic)
En este tutorial se muestra cómo crear un agente de escucha de registro personalizado y configurarlo para escuchar la salida del objeto `My.Application.Log`.  
  
## <a name="getting-started"></a>Introducción  
 Los agentes de escucha de registro deben heredarse de la clase <xref:System.Diagnostics.TraceListener>.  
  
#### <a name="to-create-the-listener"></a>Para crear el agente de escucha  
  
-   En la aplicación, cree una clase denominada `SimpleListener` que herede de <xref:System.Diagnostics.TraceListener>.  
  
     [!code-vb[VbVbalrMyApplicationLog#16](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-creating-custom-log-listeners_1.vb)]  
  
     Los métodos <xref:System.Diagnostics.TraceListener.Write%2A> y <xref:System.Diagnostics.TraceListener.WriteLine%2A>, requeridos por la clase base, llaman a `MsgBox` para mostrar su entrada.  
  
     El atributo <xref:System.Security.Permissions.HostProtectionAttribute> se aplica a los métodos <xref:System.Diagnostics.TraceListener.Write%2A> y <xref:System.Diagnostics.TraceListener.WriteLine%2A> para que sus atributos coincidan con los métodos de clase base. El atributo <xref:System.Security.Permissions.HostProtectionAttribute> permite al host que ejecuta el código determinar que el código expone sincronización de protección de host.  
  
    > [!NOTE]
    >  El atributo <xref:System.Security.Permissions.HostProtectionAttribute> solo es eficaz en aplicaciones no administradas que hospedan Common Language Runtime e implementan protección de host, como SQL Server.  
  
 Para asegurarse de que `My.Application.Log` usa su agente de escucha de registro, debe asignar un nombre seguro al ensamblado que contiene el agente de escucha de registro.  
  
 En el procedimiento siguiente se proporcionan algunos pasos sencillos para crear un ensamblado de agente de escucha de registro con nombre seguro. Para obtener más información, vea [Crear y utilizar ensamblados con nombre seguro](https://msdn.microsoft.com/library/xwb8f617).  
  
#### <a name="to-strongly-name-the-log-listener-assembly"></a>Para asignar un nombre seguro al ensamblado de agente de escucha de registro  
  
1.  Seleccione un proyecto en el **Explorador de soluciones**. En el menú **Proyecto** , elija **Propiedades**. Para obtener más información, consulte [Introducción al Diseñador de proyectos](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Haga clic en la pestaña **Firma**.  
  
3.  Active la casilla **Firmar el ensamblado**.  
  
4.  Seleccione **\<Nuevo>** en la lista desplegable **Elija un archivo de clave de nombre seguro**.  
  
     Se abre el cuadro de diálogo **Crear clave de nombre seguro**.  
  
5.  Especifique un nombre para el archivo de clave en el cuadro **Nombre del archivo de clave**.  
  
6.  Escriba una contraseña en los cuadros **Escribir contraseña** y **Confirmar contraseña**.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Vuelva a compilar la aplicación.  
  
## <a name="adding-the-listener"></a>Agregar el agente de escucha  
 Ahora que el ensamblado tiene un nombre seguro, debe determinar el nombre seguro del agente de escucha para que `My.Application.Log` use el agente de escucha de registro.  
  
 El formato de un tipo con nombre seguro es el siguiente.  
  
 \<nombre de tipo>, \<nombre de ensamblado>, \<número de versión>, \<referencia cultural>, \<nombre seguro>  
  
#### <a name="to-determine-the-strong-name-of-the-listener"></a>Para determinar el nombre seguro del agente de escucha  
  
-   En el código siguiente se muestra cómo determinar el nombre de tipo seguro para `SimpleListener`.  
  
     [!code-vb[VbVbalrMyApplicationLog#17](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-creating-custom-log-listeners_2.vb)]  
  
     El nombre seguro del tipo depende de su proyecto.  
  
 Con el nombre seguro, puede agregar el agente de escucha a la colección de agente de escucha de registro de `My.Application.Log`.  
  
#### <a name="to-add-the-listener-to-myapplicationlog"></a>Para agregar el agente de escucha a My.Application.Log  
  
1.  Haga clic con el botón derecho en app.config en el **Explorador de soluciones** y seleccione **Abrir**.  
  
     O bien  
  
     Si hay un archivo app.config:  
  
    1.  En el menú **Proyecto** , elija **Agregar nuevo elemento**.  
  
    2.  En el cuadro de diálogo **Agregar nuevo elemento** , seleccione **Archivo de configuración de aplicación**.  
  
    3.  Haga clic en **Agregar**.  
  
2.  Busque la sección `<listeners>` , en la sección `<source>` con el atributo `name` el "DefaultSource", ubicada en la sección `<sources>` . La sección `<sources>` se encuentra en la sección `<system.diagnostics>` , en la sección de nivel superior `<configuration>` .  
  
3.  Agregue este elemento a la sección `<listeners>`:  
  
    ```  
    <add name="SimpleLog" />  
    ```  
  
4.  Busque la sección `<sharedListeners>` , en la sección `<system.diagnostics>` , en la sección de nivel superior `<configuration>` .  
  
5.  Agregue este elemento a dicha sección `<sharedListeners>` :  
  
    ```  
    <add name="SimpleLog" type="SimpleLogStrongName" />  
    ```  
  
     Cambie el valor de `SimpleLogStrongName` para que sea el nombre seguro del agente de escucha.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [Trabajar con registros de aplicaciones](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [Cómo: Registrar excepciones](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)   
 [Cómo: Escribir mensajes de registro](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [Tutorial: Cambiar el lugar donde My.Application.Log escribe información](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)
