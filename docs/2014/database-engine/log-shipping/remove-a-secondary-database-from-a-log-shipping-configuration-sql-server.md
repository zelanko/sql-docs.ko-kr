---
title: 로그 전달 구성에서 보조 데이터베이스 제거(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- deleting secondary databases
- secondary databases [SQL Server], in log shipping
- removing secondary databases
- secondary data files [SQL Server], removing
- log shipping [SQL Server], secondary databases
ms.assetid: ebe368a4-ca1c-45d0-9a71-3ddbd5b26a8e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0849d4e10df746dd98e271bb3eb35696cb20337b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157843"
---
# <a name="remove-a-secondary-database-from-a-log-shipping-configuration-sql-server"></a>로그 전달 구성에서 보조 데이터베이스 제거(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 로그 전달 보조 데이터베이스를 제거하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **로그 전달 보조 데이터베이스를 제거하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 로그 전달 저장 프로시저를 사용하려면 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-remove-a-log-shipping-secondary-database"></a>로그 전달 보조 데이터베이스를 제거하려면  
  
1.  현재 로그 전달 주 서버인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 연결하고 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 로그 전달 주 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **페이지 선택**에서 **트랜잭션 로그 전달**을 클릭합니다.  
  
4.  **보조 서버 인스턴스 및 데이터베이스**에서 제거할 데이터베이스를 클릭합니다.  
  
5.  **제거**를 클릭합니다.  
  
6.  **확인** 을 클릭하여 구성을 업데이트합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-remove-a-secondary-database"></a>보조 데이터베이스를 제거하려면  
  
1.  주 서버에서 [sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql) 를 실행하여 주 서버에서 보조 데이터베이스에 대한 정보를 삭제합니다.  
  
2.  보조 서버에서 [sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql) 를 실행하여 보조 데이터베이스를 삭제합니다.  
  
    > [!NOTE]  
    >  보조 ID가 같은 보조 데이터베이스가 없는 경우 **sp_delete_log_shipping_secondary_database** 에서 **sp_delete_log_shipping_secondary_primary** 가 호출되어 보조 ID에 대한 항목과 복사 및 복원 작업이 삭제됩니다.  
  
3.  보조 서버에서 복사 및 복원 작업을 사용하지 않도록 설정합니다. 자세한 내용은 [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [SQL Server 2014로 로그 전달 업그레이드 &#40;TRANSACT-SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [로그 전달 구성&#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [로그 전달 구성에 보조 데이터베이스 추가&#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [로그 전달 제거&#40;SQL Server&#41;](remove-log-shipping-sql-server.md)  
  
-   [로그 전달 보고서 보기&#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [로그 전달 모니터링&#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [로그 전달 보조 데이터베이스로 장애 조치(Failover)&#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [로그 전달 테이블 및 저장 프로시저](log-shipping-tables-and-stored-procedures.md)  
  
  
