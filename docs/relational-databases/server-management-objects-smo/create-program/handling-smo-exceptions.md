---
description: SMO 예외 처리
title: SMO 예외 처리 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], exceptions
- exceptions [SMO]
- SQL Server Management Objects, exceptions
- inner exceptions [SMO]
ms.assetid: 4c725ff2-6588-44ca-b86a-87979e164153
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 66956ff6d6b8d904ba20cb68ce012194d6069e75
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463034"
---
# <a name="handling-smo-exceptions"></a>SMO 예외 처리
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  관리 코드에서 오류가 발생하면 예외가 throw됩니다. SMO 메서드와 속성은 반환 값에 성공 또는 실패를 보고하지 않습니다. 대신 예외 처리기에서 예외를 catch하고 처리할 수 있습니다.  
  
 SMO에는 여러 예외 클래스가 있습니다. 예외에 대한 텍스트 메시지를 제공하는 **Message** 속성과 같은 예외 속성에서 예외 정보를 추출할 수 있습니다.  
  
 예외 처리 문은 프로그래밍 언어와 관련이 있습니다. 예를 들어 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic에서는 **Catch** 문입니다.  
  
## <a name="inner-exceptions"></a>내부 예외  
 예외는 일반 예외나 특정 예외일 수 있습니다. 일반 예외에는 특정 예외 집합이 포함됩니다. 여러 개의 **Catch** 문을 사용하여 예상 오류를 처리하고 나머지 오류가 일반 예외 처리 코드로 이동되게 할 수 있습니다. 예외는 연계 시퀀스로 발생하는 경우가 많습니다. 대체로 SQL 예외로 인해 SMO 예외가 발생했을 수 있습니다. 이를 검색하려면 연속해서 **InnerException** 속성을 사용하여 최종 최상위 예외를 발생시킨 원래 예외를 확인합니다.  
  
> [!NOTE]  
>  **SQLException** 예외는 **system.object** 네임 스페이스에서 선언 됩니다.  
  
 ![예외 수준을 보여 주는 다이어그램](../../../relational-databases/server-management-objects-smo/create-program/media/exception-flow.gif "예외 수준을 보여 주는 다이어그램")  
  
 다음 다이어그램은 애플리케이션 계층을 통한 예외 흐름을 보여 줍니다.  
  
## <a name="example"></a>예  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.
  
## <a name="catching-an-exception-in-visual-basic"></a>Visual Basic에서 예외 catch  
 이 코드 예제에서는 Try ...를 사용 하는 방법을 보여 줍니다. **Catch ...** [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] SMO 예외를 catch 하는 Finally 문입니다. 모든 SMO 예외는 SmoException 유형이며 SMO 참조에 표시됩니다. 내부 예외의 시퀀스가 표시되어 오류의 근원을 보여 줍니다. 자세한 내용은 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET 설명서를 참조하십시오.  
  
```VBNET
'This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace is included.
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.
'Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.
Dim op As [Operator]
op = New [Operator](srv.JobServer, "Test_Operator")
op.Create()
'Start exception handling.
Try
    'Create the operator again to cause an SMO exception.
    Dim opx As OperatorCategory
    opx = New OperatorCategory(srv.JobServer, "Test_Operator")
    opx.Create()
    'Catch the SMO exception
Catch smoex As SmoException
    Console.WriteLine("This is an SMO Exception")
    'Display the SMO exception message.
    Console.WriteLine(smoex.Message)
    'Display the sequence of non-SMO exceptions that caused the SMO exception.
    Dim ex As Exception
    ex = smoex.InnerException
    Do While ex.InnerException IsNot (Nothing)
        Console.WriteLine(ex.InnerException.Message)
        ex = ex.InnerException
    Loop
    'Catch other non-SMO exceptions.
Catch ex As Exception
    Console.WriteLine("This is not an SMO exception.")
End Try
``` 
  
## <a name="catching-an-exception-in-visual-c"></a>Visual C#에서 예외 catch  
 이 코드 예제에서는 Try ...를 사용 하는 방법을 보여 줍니다. **Catch ... 마지막으로** SMO 예외를 catch 하는 Visual c # 문입니다. 모든 SMO 예외는 SmoException 유형이며 SMO 참조에 표시됩니다. 내부 예외의 시퀀스가 표시되어 오류의 근원을 보여 줍니다. 자세한 내용은 Visual C# 설명서를 참조하십시오.  
  
```csharp  
{   
//This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace to be included.   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.   
//Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.   
op = new Operator(srv.JobServer, "Test_Operator");   
op.Create();   
//Start exception handling.   
try {   
    //Create the operator again to cause an SMO exception.   
    OperatorCategory opx;   
    opx = new OperatorCategory(srv.JobServer, "Test_Operator");   
    opx.Create();   
}   
//Catch the SMO exception   
catch (SmoException smoex) {   
    Console.WriteLine("This is an SMO Exception");   
   //Display the SMO exception message.   
   Console.WriteLine(smoex.Message);   
   //Display the sequence of non-SMO exceptions that caused the SMO exception.   
   Exception ex;   
   ex = smoex.InnerException;   
   while (!object.ReferenceEquals(ex.InnerException, (null))) {   
      Console.WriteLine(ex.InnerException.Message);   
      ex = ex.InnerException;   
    }   
    }   
   //Catch other non-SMO exceptions.   
   catch (Exception ex) {   
      Console.WriteLine("This is not an SMO exception.");   
}   
}  
```  
  
  
