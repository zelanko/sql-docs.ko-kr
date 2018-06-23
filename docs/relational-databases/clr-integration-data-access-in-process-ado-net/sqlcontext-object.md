---
title: SqlContext 개체 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
caps.latest.revision: 54
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1aa4e7dce28a9bf0b15c40843db13d7d75d5327a
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35697774"
---
# <a name="sqlcontext-object"></a>SqlContext 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  프로시저 또는 함수를 호출하거나, CLR(공용 언어 런타임) 사용자 정의 형식의 메서드를 호출하거나, 사용자의 동작이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 언어로 정의된 트리거를 발생시키면 서버에서 관리 코드가 호출됩니다. 이러한 코드 실행은 사용자 연결의 일부로 요청되므로 서버에서 실행되는 코드에서 호출자의 컨텍스트에 대한 액세스가 필요합니다. 또한 특정 데이터 액세스 작업은 호출자의 컨텍스트에서 실행해야만 유효합니다. 예를 들어 트리거 작업에서 사용된 삽입되거나 삭제된 의사 테이블에 대한 액세스는 호출자의 컨텍스트에서만 유효합니다.  
  
 호출자의 컨텍스트로에 추상화 됩니다는 **SqlContext** 개체입니다. 에 대 한 자세한 내용은 **SqlTriggerContext** 메서드 및 속성 참조는 **Microsoft.SqlServer.Server.SqlTriggerContext** 클래스 참조 문서에서는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK입니다.  
  
 **SqlContext** 다음 구성 요소에 대 한 액세스를 제공 합니다.  
  
-   **SqlPipe**:는 **SqlPipe** 개체를 통해 결과를 클라이언트로 전달 하는 "파이프"를 나타냅니다. 에 대 한 자세한 내용은 **SqlPipe** 개체, 참조 [SqlPipe 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)합니다.  
  
-   **SqlTriggerContext**:는 **SqlTriggerContext** 개체는 CLR 트리거에서 검색할 수 있습니다. 이 개체는 트리거를 발생시킨 작업에 대한 정보와 업데이트된 열의 맵을 제공합니다. 에 대 한 자세한 내용은 **SqlTriggerContext** 개체, 참조 [SqlTriggerContext 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)합니다.  
  
-   **IsAvailable**:는 **IsAvailable** 속성은 컨텍스트 가용성을 확인 하는 데 사용 됩니다.  
  
-   **WindowsIdentity**:는 **WindowsIdentity** 속성은 호출자의 Windows id를 검색 하는 데 사용 합니다.  
  
## <a name="determining-context-availability"></a>컨텍스트 가용성 확인  
 쿼리는 **SqlContext** 현재 실행 중인 코드가 프로세스에서 실행 되 고 있는지 확인 하려면 클래스입니다. 이 작업을 수행 하려면 확인는 **IsAvailable** 의 속성은 **SqlContext** 개체입니다. **IsAvailable** 속성이 읽기 전용 이므로 반환 **True** 호출 코드 내에서 실행 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 다른 **SqlContext** 멤버에 액세스할 수 있습니다. 경우는 **IsAvailable** 속성에서 반환 **False**, 다른 모든 **SqlContext** 멤버를 throw 한 **InvalidOperationException**사용 하는 경우, . 경우 **IsAvailable** 반환 **False**, 시도 된 연결 개체를 "컨텍스트 연결 = true" 연결 문자열에는 실패 합니다.  
  
## <a name="retrieving-windows-identity"></a>Windows ID 검색  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에서 실행되는 CLR 코드는 항상 프로세스 계정의 컨텍스트에서 호출됩니다. 코드 대신 호출 하는 사용자의 id를 사용 하 여 특정 작업을 수행 해야 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 통해 가장 토큰을 얻어야 하는 다음 프로세스 id는 **WindowsIdentity** 는 의속성 **SqlContext** 개체입니다. **WindowsIdentity** 속성에서 반환 된 **WindowsIdentity** 인스턴스를 나타내는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 호출자 또는 클라이언트를 사용 하 여 인증 된 경우에 null의 Windows id [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증입니다. 으로 표시 된 어셈블리만 **EXTERNAL_ACCESS** 또는 **UNSAFE** 사용 권한을이 속성에 액세스할 수 있습니다.  
  
 가져온 후의 **WindowsIdentity** 개체 호출자는 클라이언트 계정을 가장 하 고을 대신해 작업을 수행할 수 있습니다.  
  
 호출자의 id를 통해 사용할 수만 **SqlContext.WindowsIdentity** 함수나 저장 프로시저의 실행을 시작한 클라이언트가 Windows 인증을 사용 하 여 서버에 연결 하는 경우. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 사용된 경우 이 속성은 Null이며 코드는 호출자를 가장할 수 없습니다.  
  
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
 [SqlPipe 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [SqlTriggerContext 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR 트리거](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [ADO.NET에 대한 SQL Server In-Process 전용 확장](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
