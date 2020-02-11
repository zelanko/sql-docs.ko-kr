---
title: 로그 전달 구성(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], enabling
- log shipping [SQL Server], configuring
ms.assetid: c42aa04a-4945-4417-b4c7-50589d727e9c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7533eb253ba32dd8ef2d57c3182096b36a6e47b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774587"
---
# <a name="configure-log-shipping-sql-server"></a>로그 전달 구성(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 로그 전달을 구성하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서는 백업 압축을 지원합니다. 로그 전달 구성을 만들 때 로그 백업의 백업 압축 동작을 제어할 수 있습니다. 자세한 내용은 [백업 압축&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **로그 전달을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 조건  
  
-   주 데이터베이스는 전체 또는 대량 로그 복구 모델이어야 합니다. 데이터베이스를 단순 복구로 전환하면 로그 전달이 작동하지 않습니다.  
  
-   로그 전달을 구성하려면 먼저 공유를 만들어 트랜잭션 로그 백업을 보조 서버에서 사용할 수 있도록 설정해야 합니다. 이 공유는 트랜잭션 로그 백업이 생성될 디렉터리의 공유입니다. 예를 들어 트랜잭션 로그를 c:\data\tlogs\\디렉터리로 백업할 경우 이 디렉터리의 \\\\*primaryserver*\tlogs 공유를 만들 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 로그 전달 저장 프로시저를 사용하려면 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-log-shipping"></a>로그 전달을 구성하려면  
  
1.  로그 전달 구성에서 주 데이터베이스로 사용하려는 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **페이지 선택**에서 **트랜잭션 로그 전달**을 클릭합니다.  
  
3.  **이 데이터베이스를 로그 전달 구성의 주 데이터베이스로 사용** 확인란을 선택합니다.  
  
4.  **트랜잭션 로그 백업**에서 **백업 설정**을 클릭합니다.  
  
5.  **백업 폴더의 네트워크 경로** 입력란에 트랜잭션 로그 백업 폴더용으로 만든 공유의 네트워크 경로를 입력합니다.  
  
6.  백업 폴더가 주 서버에 있는 경우 **백업 폴더가 주 서버에 있는 경우 폴더의 로컬 경로를 입력하세요** 입력란에 백업 폴더의 로컬 경로를 입력합니다. 백업 폴더가 주 서버에 있지 않은 경우 이 입력란을 비워 둘 수 있습니다.  
  
    > [!IMPORTANT]  
    >  주 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정이 로컬 시스템 계정으로 실행 중인 경우 주 서버에 백업 폴더를 만들고 해당 폴더의 로컬 경로를 지정해야 합니다.  
  
7.  **다음보다 오래된 파일 삭제** 및 **다음 기간 내에 백업이 발생하지 않으면 경고** 매개 변수를 구성합니다.  
  
8.  백업 일정은 **백업 작업** 의 **일정**상자에 나열됩니다. 설치 일정을 사용자 지정하려면 **일정** 을 클릭한 다음 필요에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 일정을 조정합니다.  
  
9. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 지원합니다. 로그 전달 구성을 만들 때 **기본 서버 설정 사용**, **백업 압축**또는 **백업 압축 안 함**중 하나를 선택하여 로그 백업에 대한 백업 압축 동작을 제어할 수 있습니다. 자세한 내용은 [Log Shipping Transaction Log Backup Settings](../../relational-databases/databases/log-shipping-transaction-log-backup-settings.md)을 참조하세요.  
  
10. **확인**을 클릭합니다.  
  
11. **보조 서버 인스턴스 및 데이터베이스**에서 **추가**를 클릭합니다.  
  
12. **연결** 을 클릭하여 보조 서버로 사용하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
13. **보조 데이터베이스** 입력란의 목록에서 데이터베이스를 선택하거나 만들 데이터베이스의 이름을 입력합니다.  
  
14. **보조 데이터베이스 초기화** 탭에서 보조 데이터베이스 초기화에 사용하려는 옵션을 선택합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 가 데이터베이스 백업에서 보조 데이터베이스를 초기화하도록 선택하면 보조 데이터베이스의 데이터 및 로그 파일이 **master** 데이터베이스의 데이터 및 로그 파일과 동일한 위치에 배치됩니다. 이 위치는 주 데이터베이스 데이터 및 로그 파일의 위치와 다를 수 있습니다.  
  
15. **파일 복사** 탭의 **복사한 파일의 대상 폴더** 입력란에 트랜잭션 로그 백업을 복사할 대상 폴더의 경로를 입력합니다. 이 폴더는 대개 보조 서버에 위치합니다.  
  
16. 복사 일정은 **복사 작업** 의 **일정**상자에 나열됩니다. 설치 일정을 사용자 지정하려면 **일정** 을 클릭한 다음 필요에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 일정을 조정합니다. 이 일정은 백업 일정과 비슷해야 합니다.  
  
17. **트랜잭션 로그 복원** 탭의 **백업 복원 시 데이터베이스 상태**에서 **복구 안 함 모드** 또는 **대기 모드** 옵션을 선택합니다.  
  
18. **대기 모드** 옵션을 선택한 경우 복원 작업을 진행하는 동안 보조 데이터베이스에서 사용자와의 연결을 끊을지 여부를 선택합니다.  
  
19. 보조 서버에서 복원 프로세스를 지연시키려면 **최소 다음 기간 동안 백업 복원 지연**에서 지연 시간을 선택합니다.  
  
20. **다음 기간 내에 복원이 발생하지 않으면 경고**에서 경고 임계값을 선택합니다.  
  
21. 복원 일정은 **복원 작업** 의 **일정**상자에 나열됩니다. 설치 일정을 사용자 지정하려면 **일정** 을 클릭한 다음 필요에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 일정을 조정합니다. 이 일정은 백업 일정과 비슷해야 합니다.  
  
22. **확인**을 클릭합니다.  
  
23. **모니터 서버 인스턴스**에서 **모니터 서버 인스턴스 사용** 확인란을 선택하고 **설정**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  이 로그 전달 구성을 모니터링하려면 지금 모니터 서버를 추가해야 합니다. 나중에 모니터 서버를 추가하려면 이 로그 전달 구성을 제거한 다음 모니터 서버가 포함된 새 구성으로 바꾸어야 합니다.  
  
24. **연결** 을 클릭하여 모니터 서버로 사용하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
25. **모니터 연결**에서 백업, 복사 및 복원 작업을 모니터 서버에 연결하는 데 사용할 연결 방법을 선택합니다.  
  
26. **기록 보존**에서 로그 전달 기록을 보관할 기간을 선택합니다.  
  
27. **확인**을 클릭합니다.  
  
28. **데이터베이스 속성** 대화 상자에서 **확인** 을 눌러 구성 프로세스를 시작합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-log-shipping"></a>로그 전달을 구성하려면  
  
1.  보조 서버에서 주 데이터베이스의 전체 백업을 복원하는 방법으로 보조 데이터베이스를 시작합니다.  
  
2.  주 서버에서 [sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql) 를 실행하여 주 데이터베이스를 추가합니다. 저장 프로시저는 백업 작업 ID 및 주 ID를 반환합니다.  
  
3.  주 서버에서 [sp_add_jobschedule](/sql/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql) 을 실행하여 백업 작업에 대한 일정을 추가합니다.  
  
4.  모니터 서버에서 [sp_add_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql) 을 실행하여 경고 작업을 추가합니다.  
  
5.  주 서버에서 백업 작업을 활성화합니다.  
  
6.  보조 서버에서 [sp_add_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql) 를 실행하여 주 서버와 데이터베이스에 대한 세부 정보를 제공합니다. 이 저장 프로시저는 보조 ID와 복사 및 복원 작업 ID를 반환합니다.  
  
7.  보조 서버에서 [sp_add_jobschedule](/sql/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql) 을 실행하여 복사 및 복원 작업의 일정을 설정합니다.  
  
8.  보조 서버에서 [sp_add_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql) 를 실행하여 보조 데이터베이스를 추가합니다.  
  
9. 주 서버에서 [sp_add_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql) 를 실행하여 새 보조 데이터베이스에 대한 필요 정보를 주 서버에 추가합니다.  
  
10. 보조 서버에서 복사 및 복원 작업을 활성화합니다. 자세한 내용은 [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [SQL Server 2014 &#40;Transact-sql&#41;로그 전달 업그레이드](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [로그 전달 구성에 보조 데이터베이스 추가&#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [로그 전달 구성에서 보조 데이터베이스 제거&#40;SQL Server&#41;](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [로그 전달 제거&#40;SQL Server&#41;](remove-log-shipping-sql-server.md)  
  
-   [로그 전달 보고서 보기&#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [로그 전달 모니터링&#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [로그 전달 보조 데이터베이스로 장애 조치(failover)&#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [로그 전달 테이블 및 저장 프로시저](log-shipping-tables-and-stored-procedures.md)  
  
  
