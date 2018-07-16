---
title: SMO 예외 처리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], exceptions
- exceptions [SMO]
- SQL Server Management Objects, exceptions
- inner exceptions [SMO]
ms.assetid: 4c725ff2-6588-44ca-b86a-87979e164153
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2d8e121a9fdc76073a016041f102fa36e6685f72
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299843"
---
# <a name="handling-smo-exceptions"></a>SMO 예외 처리
  관리 코드에서 오류가 발생하면 예외가 throw됩니다. SMO 메서드와 속성은 반환 값에 성공 또는 실패를 보고하지 않습니다. 대신 예외 처리기에서 예외를 catch하고 처리할 수 있습니다.  
  
 SMO에는 여러 예외 클래스가 있습니다. 예외에 대한 텍스트 메시지를 제공하는 `Message` 속성과 같은 예외 속성에서 예외 정보를 추출할 수 있습니다.  
  
 예외 처리 문은 프로그래밍 언어와 관련이 있습니다. 예를 들어 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic에서는 `Catch` 문입니다.  
  
## <a name="inner-exceptions"></a>내부 예외  
 예외는 일반 예외나 특정 예외일 수 있습니다. 일반 예외에는 특정 예외 집합이 포함됩니다. 여러 `Catch` 문은 예상된 오류를 처리 하 고 나머지 오류가 일반 예외 처리 코드를 사용할 수 있습니다. 예외는 연계 시퀀스로 발생하는 경우가 많습니다. 대체로 SQL 예외로 인해 SMO 예외가 발생했을 수 있습니다. 이 감지 하는 방법은 사용 하는 것을 `InnerException` 속성 연속 해 서 최종 최상위 예외를 발생 시킨 원래 예외를 확인 합니다.  
  
> [!NOTE]  
>  합니다 `SQLException` 예외에 선언 된 합니다 **System.Data.SqlClient** 네임 스페이스입니다.  
  
 ![올 수준을 보여 주는 다이어그램 예외 수준을](../../../database-engine/dev-guide/media/exception-flow.gif "올 수준을 보여 주는 다이어그램 예외 수준을")  
  
 다음 다이어그램은 응용 프로그램 계층을 통한 예외 흐름을 보여 줍니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md) 또는 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="catching-an-exception-in-visual-basic"></a>Visual Basic에서 예외 catch  
 이 코드 예제에서는 사용 하는 `Try…Catch…Finally` [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] SMO 예외를 catch 하는 문입니다. 모든 SMO 예외는 SmoException 유형이며 SMO 참조에 표시됩니다. 내부 예외의 시퀀스가 표시되어 오류의 근원을 보여 줍니다. 자세한 내용은 참조는 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET 설명서.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBExceptions1](SMO How to#SMO_VBExceptions1)]  -->  
  
## <a name="catching-an-exception-in-visual-c"></a>Visual C#에서 예외 catch  
 이 코드 예제에서는 `Try…Catch…Finally` Visual C# 문을 사용하여 SMO 예외를 catch하는 방법을 보여 줍니다. 모든 SMO 예외는 SmoException 유형이며 SMO 참조에 표시됩니다. 내부 예외의 시퀀스가 표시되어 오류의 근원을 보여 줍니다. 자세한 내용은 Visual C# 설명서를 참조하십시오.  
  
```  
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
  
  
