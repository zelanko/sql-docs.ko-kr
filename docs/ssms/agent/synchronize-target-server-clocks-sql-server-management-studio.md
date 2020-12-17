---
description: 대상 서버 클록 동기화
title: 대상 서버 클록 동기화
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 01294938af5e2d1813a371091e89b03321268637
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478784"
---
# <a name="synchronize-target-server-clocks"></a>대상 서버 클록 동기화

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 대상 서버 클럭을 마스터 서버 클럭과 동기화하는 방법에 대해 설명합니다. 이러한 시스템 클럭의 동기화는 사용자의 작업 일정을 지원합니다.  

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
**sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-synchronize-target-server-clocks"></a>대상 서버 클럭을 동기화하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 대상 서버 클럭을 마스터 서버 클럭과 동기화하려는 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리** 를 가리킨 다음 **대상 서버 관리** 를 선택합니다.  
  
3.  **대상 서버 관리** 대화 상자에서 **명령 게시** 를 클릭합니다.  
  
4.  **명령 유형** 목록에서 **클럭 동기화** 를 선택합니다.  
  
5.  **받는 사람** 에서 다음 중 하나를 수행합니다.  
  
    -   모든 대상 서버 클럭을 마스터 서버 클럭과 동기화하려면 **모든 대상 서버** 를 클릭합니다.  
  
    -   **대상 서버 지정** 을 클릭하여 특정 서버 클럭을 동기화하고 마스터 서버 클럭과 동기화할 클럭의 대상 서버를 각각 선택합니다.  
  
6.  완료되었으면 **확인** 을 클릭합니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-synchronize-target-server-clocks"></a>대상 서버 클럭을 동기화하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
자세한 내용은 [sp_resync_targetserver(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)를 참조하세요.  
