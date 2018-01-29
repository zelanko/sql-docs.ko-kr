---
title: "SQL Server 에이전트 프록시 삭제 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting SQL Server Agent proxies
- proxies [SQL Server Agent], deleting
- removing SQL Server Agent proxies
ms.assetid: 9248841d-7294-47d4-94f3-b34a0521fabc
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79937166e8bbd119f2bb5d5e98b7a49dd969047b
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="delete-a-sql-server-agent-proxy"></a>Delete a SQL Server Agent Proxy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql_md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 프록시 계정을 삭제하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **다음을 사용하여 SQL Server 에이전트 프록시 계정을 삭제합니다.**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 프록시 계정을 삭제할 때 프록시가 활성 작업 단계를 참조하지 않는지 확인합니다. 프록시를 참조하는 작업 단계를 확인하려면 프록시를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 후 *proxy_name***프록시 계정 속성** 대화 상자에서 **참조** 페이지를 선택합니다. 프록시를 삭제한 경우 **개체 삭제** 대화 상자에서 해당 프록시를 사용하는 모든 작업 단계를 재할당할 수 있는 옵션이 제공됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 프록시는 자격 증명을 사용하여 Windows 사용자 계정에 대한 정보를 저장합니다. 자격 증명에 지정된 사용자에게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 가 실행 중인 컴퓨터에 대한 "일괄 작업으로 로그온" 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트는 프록시에 대한 하위 시스템 액세스 권한을 확인하고 작업 단계가 실행될 때마다 프록시에 대한 액세스 권한을 부여합니다. 프록시에 하위 시스템에 대한 액세스 권한이 없으면 작업 단계가 실패합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 프록시에 지정된 사용자를 가장하여 작업 단계를 실행합니다.  
  
-   사용자의 로그인에 프록시에 대한 액세스 권한이 있거나 사용자가 프록시에 대한 액세스 권한이 있는 역할에 속하는 경우 해당 사용자는 작업 단계에서 프록시를 사용할 수 있습니다.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
**sysadmin** 고정 서버 역할의 멤버만 프록시 계정을 만들거나 수정하거나 삭제할 수 있습니다.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>SQL Server 에이전트 프록시 계정을 삭제하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 삭제하려는 프록시 계정이 포함된 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **프록시** 폴더를 확장합니다.  
  
4.  더하기 기호를 클릭하여 삭제하려는 프록시 계정이 포함된 하위 시스템을 확장합니다(예: **ActiveX 스크립트**).  
  
5.  삭제하려는 프록시 계정을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
6.  **개체 삭제** 대화 상자에서 올바른 프록시 계정이 선택되었는지 확인합니다. **재할당 대상** 확인란을 선택하여 이 프록시 계정을 참조하는 작업 단계를 다른 계정에 재할당합니다.  
  
7.  **확인**을 클릭합니다.  
  
## <a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>SQL Server 에이전트 프록시 계정을 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- deletes the proxy "Catalog application proxy"  
    USE msdb ;  
    GO  
    EXEC dbo.sp_delete_proxy  
        @proxy_name = N'Catalog application proxy' ;  
    GO  
    ```  
  
자세한 내용은 [sp_delete_proxy(Transact-SQL)](http://msdn.microsoft.com/en-us/44a1db13-b7f2-4dab-a1b5-b8dafb41737c)를 참조하세요.  
  
