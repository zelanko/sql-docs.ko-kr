---
title: SqlContext 개체 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
caps.latest.revision: 54
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ea7cd3ca105fd599f3b157f64189210b539de4ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181354"
---
# <a name="sqlcontext-object"></a>SqlContext 개체
  프로시저 또는 함수를 호출하거나, CLR(공용 언어 런타임) 사용자 정의 형식의 메서드를 호출하거나, 사용자의 동작이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 언어로 정의된 트리거를 발생시키면 서버에서 관리 코드가 호출됩니다. 이러한 코드 실행은 사용자 연결의 일부로 요청되므로 서버에서 실행되는 코드에서 호출자의 컨텍스트에 대한 액세스가 필요합니다. 또한 특정 데이터 액세스 작업은 호출자의 컨텍스트에서 실행해야만 유효합니다. 예를 들어 트리거 작업에서 사용된 삽입되거나 삭제된 의사 테이블에 대한 액세스는 호출자의 컨텍스트에서만 유효합니다.  
  
 호출자의 컨텍스트는 `SqlContext` 개체에 추상화됩니다. `SqlTriggerContext` 메서드 및 속성에 대한 자세한 내용은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK의 `Microsoft.SqlServer.Server.SqlTriggerContext` 클래스 참조 설명서를 참조하십시오.  
  
 `SqlContext`는 다음 구성 요소에 대한 액세스를 제공합니다.  
  
-   `SqlPipe`: `SqlPipe` 개체를 통해 결과를 클라이언트로 전달 하는 "파이프"를 나타냅니다. 에 대 한 자세한 내용은 `SqlPipe` 개체, 참조 [SqlPipe 개체](sqlpipe-object.md)합니다.  
  
-   `SqlTriggerContext`: `SqlTriggerContext` 개체는 CLR 트리거에서 검색할 수 있습니다. 이 개체는 트리거를 발생시킨 작업에 대한 정보와 업데이트된 열의 맵을 제공합니다. 에 대 한 자세한 내용은 `SqlTriggerContext` 개체, 참조 [SqlTriggerContext 개체](sqltriggercontext-object.md)합니다.  
  
-   `IsAvailable`: `IsAvailable` 속성은 컨텍스트 가용성을 확인 하는 데 사용 됩니다.  
  
-   `WindowsIdentity`: `WindowsIdentity` 속성은 호출자의 Windows id를 검색 하는 데 사용 합니다.  
  
## <a name="determining-context-availability"></a>컨텍스트 가용성 확인  
 `SqlContext` 클래스를 쿼리하면 현재 실행 중인 코드가 in-process로 실행 중인지 확인할 수 있습니다. 이렇게 하려면 `IsAvailable` 개체의 `SqlContext` 속성을 확인합니다. `IsAvailable` 속성은 읽기 전용이며, 호출 코드가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에서 실행 중이고 다른 `True` 멤버에 액세스가 허용되면 `SqlContext`를 반환합니다. `IsAvailable` 속성이 `False`를 반환하는 경우 다른 모든 `SqlContext` 멤버를 사용하면 `InvalidOperationException`이 throw됩니다. `IsAvailable`이 `False`를 반환하는 경우 연결 문자열에 "context connection=true"가 있는 연결 개체를 열려고 하면 오류가 발생합니다.  
  
## <a name="retrieving-windows-identity"></a>Windows ID 검색  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에서 실행되는 CLR 코드는 항상 프로세스 계정의 컨텍스트에서 호출됩니다. 코드에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 ID 대신 호출 사용자의 ID를 사용하여 특정 동작을 수행해야 하는 경우 `WindowsIdentity` 개체의 `SqlContext` 속성을 통해 가장 토큰을 얻어야 합니다. `WindowsIdentity` 속성은 호출자의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ID를 나타내는 `WindowsIdentity` 인스턴스를 반환하며, 클라이언트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 인증된 경우에는 Null을 반환합니다. `EXTERNAL_ACCESS` 또는 `UNSAFE` 권한으로 표시된 어셈블리만 이 속성에 액세스할 수 있습니다.  
  
 `WindowsIdentity` 개체를 얻으면 호출자는 클라이언트 계정을 가장하고 이를 대신해 동작을 수행할 수 있습니다.  
  
 호출자 ID는 저장 프로시저 또는 함수 실행을 시작한 클라이언트가 Windows 인증을 사용하여 서버에 연결된 경우 `SqlContext.WindowsIdentity`를 통해서만 얻을 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 사용된 경우 이 속성은 Null이며 코드는 호출자를 가장할 수 없습니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 호출 클라이언트의 Windows ID를 얻고 클라이언트를 가장하는 방법을 보여 줍니다.  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void WindowsIDTestProc()  
{  
    WindowsIdentity clientId = null;  
    WindowsImpersonationContext impersonatedUser = null;  
  
    // Get the client ID.  
    clientId = SqlContext.WindowsIdentity;  
  
    // This outer try block is used to thwart exception filter   
    // attacks which would prevent the inner finally   
    // block from executing and resetting the impersonation.  
    try  
    {  
        try  
        {  
            impersonatedUser = clientId.Impersonate();  
            if (impersonatedUser != null)  
            {  
                // Perform some action using impersonation.  
            }  
        }  
        finally  
        {  
            // Undo impersonation.  
            if (impersonatedUser != null)  
                impersonatedUser.Undo();  
        }  
    }  
    catch  
    {  
        throw;  
    }  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  WindowsIDTestProcVB ()  
    Dim clientId As WindowsIdentity  
    Dim impersonatedUser As WindowsImpersonationContext  
  
    ' Get the client ID.  
    clientId = SqlContext.WindowsIdentity  
  
    ' This outer try block is used to thwart exception filter   
    ' attacks which would prevent the inner finally   
    ' block from executing and resetting the impersonation.  
  
    Try  
        Try  
  
            impersonatedUser = clientId.Impersonate()  
  
            If impersonatedUser IsNot Nothing Then  
                ' Perform some action using impersonation.  
            End If  
  
        Finally  
            ' Undo impersonation.  
            If impersonatedUser IsNot Nothing Then  
                impersonatedUser.Undo()  
            End If  
        End Try  
  
    Catch e As Exception  
  
        Throw e  
  
    End Try  
End Sub  
```  
  
## <a name="see-also"></a>관련 항목  
 [SqlPipe 개체](sqlpipe-object.md)   
 [SqlTriggerContext 개체](sqltriggercontext-object.md)   
 [CLR 트리거](../../database-engine/dev-guide/clr-triggers.md)   
 [ADO.NET에 대한 SQL Server In-Process 전용 확장](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  