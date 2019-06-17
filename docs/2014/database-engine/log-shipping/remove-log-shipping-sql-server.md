---
title: 로그 전달 제거(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], removing
- removing log shipping
- deleting log shipping
ms.assetid: 859373db-c744-4a4b-8479-45163f61e8cb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 270ca92b723aa67938dc1f56d72425d7e1c98040
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774997"
---
# <a name="remove-log-shipping-sql-server"></a>로그 전달 제거(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 로그 전달을 제거하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **로그 전달을 제거하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 로그 전달 저장 프로시저를 사용하려면 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-remove-log-shipping"></a>로그 전달을 제거하려면  
  
1.  현재 로그 전달 주 서버인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 연결하고 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 로그 전달 주 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **페이지 선택**에서 **트랜잭션 로그 전달**을 클릭합니다.  
  
4.  **이 데이터베이스를 로그 전달 구성의 주 데이터베이스로 사용** 확인란의 선택을 취소합니다.  
  
5.  **확인** 을 클릭하여 주 데이터베이스의 로그 전달을 제거합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-remove-log-shipping"></a>로그 전달을 제거하려면  
  
1.  로그 전달 주 서버에서 [sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql) 를 실행하여 주 서버에서 보조 데이터베이스에 대한 정보를 삭제합니다.  
  
2.  로그 전달 보조 서버에서 [sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql) 를 실행하여 보조 데이터베이스를 삭제합니다.  
  
    > [!NOTE]  
    >  보조 ID가 같은 보조 데이터베이스가 없는 경우 **sp_delete_log_shipping_secondary_database** 에서 **sp_delete_log_shipping_secondary_primary** 가 호출되어 보조 ID에 대한 항목과 복사 및 복원 작업이 삭제됩니다.  
  
3.  로그 전달 주 서버에서 **sp_delete_log_shipping_primary_database** 를 실행하여 주 서버에서 로그 전달 구성에 대한 정보를 삭제합니다. 이렇게 하면 백업 작업도 삭제됩니다.  
  
4.  로그 전달 주 서버에서 백업 작업을 사용하지 않도록 설정합니다. 자세한 내용은 [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)을 참조하세요.  
  
5.  로그 전달 보조 서버에서 복사 및 복원 작업을 사용하지 않도록 설정합니다.  
  
6.  로그 전달 보조 데이터베이스를 더 이상 사용하지 않으려는 경우 선택적으로 보조 서버에서 해당 로그 전달 보조 데이터베이스를 삭제할 수 있습니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [SQL Server 2014로 로그 전달 업그레이드 &#40;TRANSACT-SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [로그 전달 구성&#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [로그 전달 구성에 보조 데이터베이스 추가&#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [로그 전달 구성에서 보조 데이터베이스 제거&#40;SQL Server&#41;](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [로그 전달 모니터링&#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [로그 전달 보조 데이터베이스로 장애 조치(failover)&#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [로그 전달 테이블 및 저장 프로시저](log-shipping-tables-and-stored-procedures.md)  
  
  
