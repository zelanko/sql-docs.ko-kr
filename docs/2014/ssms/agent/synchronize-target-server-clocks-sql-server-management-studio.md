---
title: 대상 서버 클럭 동기화(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8e7150cd42699503ab22cdd89fb6206194bd64e1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067500"
---
# <a name="synchronize-target-server-clocks-sql-server-management-studio"></a>Synchronize Target Server Clocks (SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 대상 서버 클럭을 마스터 서버 클럭과 동기화하는 방법에 대해 설명합니다. 이러한 시스템 클럭의 동기화는 사용자의 작업 일정을 지원합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 대상 서버 클럭을 동기화합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-synchronize-target-server-clocks"></a>대상 서버 클럭을 동기화하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 대상 서버 클럭을 마스터 서버 클럭과 동기화하려는 서버를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리**를 가리킨 다음 **대상 서버 관리**를 선택합니다.  
  
3.  **대상 서버 관리** 대화 상자에서 **명령 게시**를 클릭합니다.  
  
4.  **명령 유형** 목록에서 **클럭 동기화**를 선택합니다.  
  
5.  **받는 사람**에서 다음 중 하나를 수행합니다.  
  
    -   모든 대상 서버 클럭을 마스터 서버 클럭과 동기화하려면 **모든 대상 서버** 를 클릭합니다.  
  
    -   **대상 서버 지정** 을 클릭하여 특정 서버 클럭을 동기화하고 마스터 서버 클럭과 동기화할 클럭의 대상 서버를 각각 선택합니다.  
  
6.  작업을 완료한 후 **확인**을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-synchronize-target-server-clocks"></a>대상 서버 클럭을 동기화하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
 자세한 내용은 [sp_resync_targetserver &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)를 참조 하세요.  
  
  
