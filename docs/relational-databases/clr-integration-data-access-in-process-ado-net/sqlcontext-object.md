---
title: SqlContext 개체 | 마이크로 소프트 문서
description: 사용자 연결에서 SQL Server에서 관리 코드를 호출하면 호출자의 컨텍스트에 대한 액세스가 SqlContext 개체에서 추상화됩니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
author: rothja
ms.author: jroth
ms.openlocfilehash: cd6d3091b155ae829e368bdd182b3da8286c7194
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487542"
---
# <a name="sqlcontext-object"></a>SqlContext 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  프로시저 또는 함수를 호출하거나, CLR(공용 언어 런타임) 사용자 정의 형식의 메서드를 호출하거나, 사용자의 동작이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 언어로 정의된 트리거를 발생시키면 서버에서 관리 코드가 호출됩니다. 이러한 코드 실행은 사용자 연결의 일부로 요청되므로 서버에서 실행되는 코드에서 호출자의 컨텍스트에 대한 액세스가 필요합니다. 또한 특정 데이터 액세스 작업은 호출자의 컨텍스트에서 실행해야만 유효합니다. 예를 들어 트리거 작업에서 사용된 삽입되거나 삭제된 의사 테이블에 대한 액세스는 호출자의 컨텍스트에서만 유효합니다.  
  
 호출자의 컨텍스트는 **SqlContext** 개체에서 추상화됩니다. **SqlTriggerContext** 메서드 및 속성에 대한 자세한 내용은 SDK의 **Microsoft.SqlServer.Server.SqlTriggerContext** 클래스 참조 설명서를 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 참조하십시오.  
  
 **SqlContext는** 다음 구성 요소에 대한 액세스를 제공합니다.  
  
-   **SqlPipe**: **SqlPipe** 개체는 결과가 클라이언트로 흐르는 "파이프"를 나타냅니다. **SqlPipe** 개체에 대한 자세한 내용은 [SqlPipe 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)를 참조하십시오.  
  
-   **SqlTriggerContext**: **SqlTriggerContext** 개체는 CLR 트리거 내에서만 검색할 수 있습니다. 이 개체는 트리거를 발생시킨 작업에 대한 정보와 업데이트된 열의 맵을 제공합니다. **SqlTriggerContext** 개체에 대한 자세한 내용은 [SqlTriggerContext 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)를 참조하십시오.  
  
-   **사용 가능**: **IsAvailable** 속성은 컨텍스트 가용성을 결정하는 데 사용됩니다.  
  
-   **Windows Identity**: **WindowsIdentity** 속성은 호출자의 Windows ID를 검색하는 데 사용됩니다.  
  
## <a name="determining-context-availability"></a>컨텍스트 가용성 확인  
 **SqlContext** 클래스를 쿼리하여 현재 실행 중인 코드가 프로세스 에서 실행되고 있는지 확인합니다. 이렇게 하려면 **SqlContext** 개체의 **IsAvailable** 속성을 확인합니다. **IsAvailable** 속성은 읽기 전용이며 호출 코드가 내부에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행중이고 다른 **SqlContext** 멤버에 액세스할 수 있는 경우 **True를** 반환합니다. **IsAvailable** **속성이 False를**반환하는 경우 다른 모든 **SqlContext** 멤버는 **잘못된 OperationException을**throw합니다. **IsAvailable** **가 False를**반환하는 경우 연결 문자열에 "컨텍스트 연결=true"가 있는 연결 개체를 열려는 모든 시도가 실패합니다.  
  
## <a name="retrieving-windows-identity"></a>Windows ID 검색  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에서 실행되는 CLR 코드는 항상 프로세스 계정의 컨텍스트에서 호출됩니다. 코드가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 ID 대신 호출 하는 사용자의 ID를 사용 하 여 특정 작업을 수행 해야 하는 경우 가장 토큰 **은 WindowsIdentity** 개체의 **WindowsIdentity** 속성을 통해 가져와야 합니다. **WindowsIdentity** 속성은 호출자의 Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] ID를 나타내는 **WindowsIdentity** 인스턴스를 반환하거나 클라이언트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 인증된 경우 null을 반환합니다. **EXTERNAL_ACCESS** 또는 **안전하지 않은** 권한이 표시된 어셈블리만 이 속성에 액세스할 수 있습니다.  
  
 **WindowsIdentity** 개체를 얻은 후 호출자는 클라이언트 계정을 가장하고 해당 계정을 대신하여 작업을 수행할 수 있습니다.  
  
 호출자의 ID는 Windows 인증을 사용하여 서버에 연결된 저장 프로시저 또는 함수의 실행을 시작한 클라이언트인 경우 **SqlContext.WindowsIdentity를** 통해서만 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 사용된 경우 이 속성은 Null이며 코드는 호출자를 가장할 수 없습니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SqlPipe 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [SqlTrigger컨텍스트 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR 트리거](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [ADO.NET에 대한 SQL Server In-Process 전용 확장](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
