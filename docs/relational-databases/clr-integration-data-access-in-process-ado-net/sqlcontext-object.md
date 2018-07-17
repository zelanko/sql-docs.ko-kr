---
title: SqlContext 개체 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
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
ms.openlocfilehash: fd8bcd270794394bcb576c42657c2d9cd831fc98
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37359545"
---
# <a name="sqlcontext-object"></a>SqlContext 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  프로시저 또는 함수를 호출하거나, CLR(공용 언어 런타임) 사용자 정의 형식의 메서드를 호출하거나, 사용자의 동작이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 언어로 정의된 트리거를 발생시키면 서버에서 관리 코드가 호출됩니다. 이러한 코드 실행은 사용자 연결의 일부로 요청되므로 서버에서 실행되는 코드에서 호출자의 컨텍스트에 대한 액세스가 필요합니다. 또한 특정 데이터 액세스 작업은 호출자의 컨텍스트에서 실행해야만 유효합니다. 예를 들어 트리거 작업에서 사용된 삽입되거나 삭제된 의사 테이블에 대한 액세스는 호출자의 컨텍스트에서만 유효합니다.  
  
 호출자의 컨텍스트와에서 추상화 되는 **SqlContext** 개체입니다. 에 대 한 자세한 내용은 합니다 **SqlTriggerContext** 메서드 및 속성을 참조 하세요 합니다 **Microsoft.SqlServer.Server.SqlTriggerContext** 클래스 참조 설명서를 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 **SqlContext** 다음 구성 요소에 대 한 액세스를 제공 합니다.  
  
-   **SqlPipe**: 합니다 **SqlPipe** 개체는 클라이언트에 흐름을 통해 "파이프"를 나타냅니다. 에 대 한 자세한 내용은 합니다 **SqlPipe** 개체를 참조 하십시오 [SqlPipe 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)합니다.  
  
-   **SqlTriggerContext**: 합니다 **SqlTriggerContext** 개체는 CLR 트리거에서 검색할 수 있습니다. 이 개체는 트리거를 발생시킨 작업에 대한 정보와 업데이트된 열의 맵을 제공합니다. 에 대 한 자세한 내용은 합니다 **SqlTriggerContext** 개체를 참조 하십시오 [SqlTriggerContext 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)합니다.  
  
-   **IsAvailable**: 합니다 **IsAvailable** 속성 상황에 맞는 가용성을 확인 하는 데 사용 됩니다.  
  
-   **WindowsIdentity**: 합니다 **WindowsIdentity** 속성 호출자의 Windows id를 검색 하는 데 사용 됩니다.  
  
## <a name="determining-context-availability"></a>컨텍스트 가용성 확인  
 쿼리는 **SqlContext** 클래스 코드를 현재 실행 중인 프로세스에서 실행 되 고 있는지 확인 합니다. 이 작업을 수행 하려면 확인 합니다 **IsAvailable** 의 속성을 **SqlContext** 개체. 합니다 **IsAvailable** 반환 하는 속성은 읽기 전용 **True** 호출 하는 코드 내에서 실행 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 다른 **SqlContext** 멤버에 액세스할 수 있습니다. 경우는 **IsAvailable** 속성이 반환 **False**, 다른 모든 **SqlContext** 멤버 throw를 **InvalidOperationException**사용 되는 경우 . 하는 경우 **IsAvailable** 반환 **False**를 가진 연결 개체를 열려고 "컨텍스트 연결 = true" 연결 문자열에 실패 합니다.  
  
## <a name="retrieving-windows-identity"></a>Windows ID 검색  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에서 실행되는 CLR 코드는 항상 프로세스 계정의 컨텍스트에서 호출됩니다. 코드를 대신 호출 하는 사용자의 id를 사용 하 여 특정 작업을 수행 해야 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 통해 가장 토큰을 가져와야 하는 다음 프로세스 id는 **WindowsIdentity** 속성을  **SqlContext** 개체입니다. **WindowsIdentity** 속성이 반환을 **WindowsIdentity** 인스턴스를 나타내는 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 사용 하 여 클라이언트를 인증 하는 경우 null을 호출자의 Windows id [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. 로 표시 된 어셈블리만 **EXTERNAL_ACCESS** 또는 **UNSAFE** 권한을이 속성에 액세스할 수 있습니다.  
  
 가져온 후 합니다 **WindowsIdentity** 개체를 호출자에 게는 클라이언트 계정을 가장 하 본인을 대신해 작업을 수행 합니다.  
  
 호출자의 id를 통해서만 제공 됩니다 **SqlContext.WindowsIdentity** 저장 프로시저 또는 함수의 실행을 시작한 클라이언트의 경우 Windows 인증을 사용 하 여 서버에 연결 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 사용된 경우 이 속성은 Null이며 코드는 호출자를 가장할 수 없습니다.  
  
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
  
  
