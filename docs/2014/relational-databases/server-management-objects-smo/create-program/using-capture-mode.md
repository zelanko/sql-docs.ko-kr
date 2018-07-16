---
title: 캡처 모드를 사용 하 여 | Microsoft Docs
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
- SQL Server Management Objects, capture mode
- capture mode [SMO]
- SMO [SQL Server], capture mode
ms.assetid: ace29bf0-705a-434f-82e4-db99d01c5008
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7df68a5dc1718924bc12c17f69703bb4ede01058
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232953"
---
# <a name="using-capture-mode"></a>캡처 모드 사용
  SMO 프로그램은 프로그램에서 실행하는 문 대신 실행하거나 문과 함께 실행한 해당 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 캡처하고 기록할 수 있습니다. <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 사용하거나 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Server> 속성을 사용하여 캡처 모드를 설정합니다.  
  
## <a name="example"></a>예제  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="enabling-capture-mode-in-visual-basic"></a>Visual Basic에서 캡처 모드 설정  
 다음 코드 예에서는 캡처 모드를 설정한 다음 캡처 버퍼에 보관된 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령을 표시합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCapture1](SMO How to#SMO_VBCapture1)]  -->  
  
## <a name="enabling-capture-mode-in-visual-c"></a>Visual C#에서 캡처 모드 설정  
 다음 코드 예에서는 캡처 모드를 설정한 다음 캡처 버퍼에 보관된 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령을 표시합니다.  
  
```  
{   
// Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
// Set the execution mode to CaptureSql for the connection.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.CaptureSql;   
// Make a modification to the server that is to be captured.   
srv.UserOptions.AnsiNulls = true;   
srv.Alter();   
// Iterate through the strings in the capture buffer and display the captured statements.   
string s;   
foreach ( String p_s in srv.ConnectionContext.CapturedSql.Text ) {   
   Console.WriteLine(p_s);   
}   
// Execute the captured statements.   
srv.ConnectionContext.ExecuteNonQuery(srv.ConnectionContext.CapturedSql.Text);   
// Revert to immediate execution mode.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
  
