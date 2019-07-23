---
title: 로그 전달 구성에 보조 데이터베이스 추가(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- adding secondary databases
- secondary databases [SQL Server], in log shipping
- secondary data files [SQL Server], adding
- log shipping [SQL Server], secondary databases
ms.assetid: b02eba13-f8e6-4684-b7e4-75ea038ea473
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f1a2f3c2149a089b4fe62564fae1278690ba4420
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057897"
---
# <a name="add-a-secondary-database-to-a-log-shipping-configuration-sql-server"></a>로그 전달 구성에 보조 데이터베이스 추가(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 기존의 로그 전달 구성에 보조 데이터베이스를 추가하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **로그 전달 보조 데이터베이스를 추가하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 로그 전달 저장 프로시저를 사용하려면 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-add-a-log-shipping-secondary-database"></a>로그 전달 보조 데이터베이스를 추가하려면  
  
1.  로그 전달 구성에서 주 데이터베이스로 사용하려는 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **페이지 선택**에서 **트랜잭션 로그 전달**을 클릭합니다.  
  
3.  **보조 서버 인스턴스 및 데이터베이스**에서 **추가**를 클릭합니다.  
  
4.  **연결** 을 클릭하여 보조 서버로 사용하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
5.  **보조 데이터베이스** 상자의 목록에서 데이터베이스를 선택하거나 만들려는 데이터베이스의 이름을 입력합니다.  
  
6.  **보조 데이터베이스 초기화** 탭에서 보조 데이터베이스 초기화에 사용하려는 옵션을 선택합니다.  
  
7.  **파일 복사**탭의 **복사한 파일의 대상 폴더** 입력란에 트랜잭션 로그 백업을 복사할 대상 폴더의 경로를 입력합니다. 이 폴더는 대개 보조 서버에 위치합니다.  
  
8.  복사 일정은 **복사 작업** 의 **일정**상자에 나열됩니다. 설치 일정을 사용자 지정하려면 **일정** 을 클릭한 다음 필요에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 일정을 조정합니다. 이 일정은 백업 일정과 비슷해야 합니다.  
  
9. **트랜잭션 로그 복원** 탭의 **백업 복원 시 데이터베이스 상태**에서 **복구 안 함 모드** 또는 **대기 모드** 옵션을 선택합니다.  
  
10. **대기 모드** 옵션을 선택한 경우 복원 작업을 진행하는 동안 보조 데이터베이스에서 사용자와의 연결을 끊을지 여부를 선택합니다.  
  
11. 보조 서버에서 복원 프로세스를 지연시키려면 **최소 다음 기간 동안 백업 복원 지연**에서 지연 시간을 선택합니다.  
  
12. **다음 기간 내에 복원이 발생하지 않으면 경고**에서 경고 임계값을 선택합니다.  
  
13. 복원 일정은 **복원 작업** 의 **일정**상자에 나열됩니다. 설치 일정을 사용자 지정하려면 **일정** 을 클릭한 다음 필요에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 일정을 조정합니다. 이 일정은 백업 일정과 비슷해야 합니다.  
  
14. **확인**을 클릭합니다.  
  
15. 데이터베이스 속성 대화 상자에서 **확인** 을 클릭하여 구성 프로세스를 시작합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-add-a-log-shipping-secondary-database"></a>로그 전달 보조 데이터베이스를 추가하려면  
  
1.  보조 서버에서 [sp_add_log_shipping_secondary_primary](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql.md) 를 실행하여 주 서버와 데이터베이스에 대한 세부 정보를 제공합니다. 이 저장 프로시저는 보조 ID와 복사 및 복원 작업 ID를 반환합니다.  
  
2.  보조 서버에서 [sp_add_jobschedule](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md) 을 실행하여 복사 및 복원 작업의 일정을 설정합니다.  
  
3.  보조 서버에서 [sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md) 를 실행하여 보조 데이터베이스를 추가합니다.  
  
4.  주 서버에서 [sp_add_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql.md) 를 실행하여 새 보조 데이터베이스에 대한 필요 정보를 주 서버에 추가합니다.  
  
5.  보조 서버에서 복사 및 복원 작업을 활성화합니다. 자세한 내용은 [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [SQL Server 2016으로 로그 전달 업그레이드&#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [로그 전달 구성&#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
-   [로그 전달 구성에서 보조 데이터베이스 제거&#40;SQL Server&#41;](../../database-engine/log-shipping/remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [로그 전달 제거&#40;SQL Server&#41;](../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
-   [로그 전달 보고서 보기&#40;SQL Server Management Studio&#41;](../../database-engine/log-shipping/view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [로그 전달 모니터링&#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
-   [로그 전달 보조 데이터베이스로 장애 조치(Failover)&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [로그 전달 테이블 및 저장 프로시저](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
