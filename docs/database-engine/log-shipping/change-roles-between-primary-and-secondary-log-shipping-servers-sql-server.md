---
title: 주 로그 전달 역할 및 보조 로그 전달 역할 변경
description: SQL Server 로그 전달 솔루션의 주 데이터베이스 역할을 하도록 보조 데이터베이스를 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], role changes
- secondary data files [SQL Server], roles changed between
- primary databases [SQL Server]
- initial role changes [SQL Server]
- log shipping [SQL Server], failover
- failover [SQL Server], log shipping
ms.assetid: 2d7cc40a-47e8-4419-9b2b-7c69f700e806
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b2a032663343223bcfab58075343e61c72e1df7c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85696783"
---
# <a name="change-roles-between-primary-and-secondary-log-shipping-servers-sql-server"></a>주 로그 전달 서버와 보조 로그 전달 서버 간 역할 변경(SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  보조 서버로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 전달 구성에 대해 장애 조치(Failover)를 수행한 후에 주 데이터베이스로 작동하도록 보조 데이터베이스를 구성할 수 있습니다. 그러면 필요할 때 주 데이터베이스와 보조 데이터베이스를 바꿀 수 있습니다.  
  
## <a name="performing-the-initial-role-change"></a>초기 역할 변경 수행  
 처음으로 보조 데이터베이스로 장애 조치(Failover)를 하고 이 데이터베이스를 새로운 주 데이터베이스로 만들 때 일련의 단계를 수행해야 합니다. 이러한 초기 단계를 수행한 후에는 주 데이터베이스와 보조 데이터베이스의 역할을 쉽게 바꿀 수 있습니다.  
  
1.  수동으로 주 데이터베이스에서 보조 데이터베이스로 장애 조치(Failover)를 합니다. NORECOVERY를 사용하여 주 서버의 활성 트랜잭션 로그를 백업해야 합니다. 자세한 내용은 [로그 전달 보조 데이터베이스로 장애 조치(failover)&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)를 참조하세요.  
  
2.  원래 주 서버에서 로그 전달 백업 작업을 비활성화하고 원래 보조 서버에서 복사 및 복원 작업을 비활성화합니다.  
  
3.  새로운 주 데이터베이스로 만들 보조 데이터베이스에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 로그 전달을 구성합니다. 자세한 내용은 [로그 전달 구성&#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)에서 도입되었습니다. 다음 단계를 수행합니다.  
  
    1.  원래의 주 서버용으로 만든 공유와 같은 공유를 백업 생성에 사용합니다.  
  
    2.  보조 데이터베이스를 추가할 때 **보조 데이터베이스 설정** 대화 상자에서 **보조 데이터베이스** 상자에 원래의 주 데이터베이스 이름을 입력합니다.  
  
    3.  **보조 데이터베이스 설정** 대화 상자에서 **아니요, 보조 데이터베이스가 초기화되었습니다.** 를 선택합니다.  
  
4.  이전 로그 전달 구성에서 로그 전달 모니터링을 사용하도록 설정한 경우에는 새 로그 전달 구성을 모니터링하도록 로그 전달 모니터링을 다시 구성합니다.  threshold_alert_enabled를 1로 설정하면 restore_threshold가 초과될 때 경고가 발생하도록 지정됩니다. *database_name* 을 사용자 데이터베이스 이름으로 바꾸어 다음 명령을 실행합니다.  
  
    1.  **새 주 서버에서 다음을 수행합니다.**  
  
         다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
        ```sql  
        -- Statement to execute on the new primary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_secondary_database @secondary_database = N'database_name', @threshold_alert_enabled = 1;  
        GO  
        ```  
  
    2.  **새 보조 서버에서 다음을 수행합니다.**  
  
         다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
        ```sql  
        -- Statement to execute on the new secondary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_primary_database @database=N'database_name', @threshold_alert_enabled = 1;  
        GO  
        ```  
  
## <a name="swapping-roles"></a>역할 바꾸기  
 초기 역할 변경을 위해 위의 단계를 완료한 후에 이 섹션의 단계에 따라 주 데이터베이스와 보조 데이터베이스의 역할을 변경할 수 있습니다. 역할을 변경하려면 아래의 일반적인 단계를 따르십시오.  
  
1.  보조 데이터베이스를 온라인 상태로 만들고 NORECOVERY를 사용하여 주 서버의 트랜잭션 로그를 백업합니다.  
  
2.  원래 주 서버에서 로그 전달 백업 작업을 비활성화하고 원래 보조 서버에서 복사 및 복원 작업을 비활성화합니다.  
  
3.  보조 서버(새로운 주 서버)의 로그 전달 백업 작업을 활성화하고 주 서버(새로운 보조 서버)의 복사 및 복원 작업을 활성화합니다.  
  
> [!IMPORTANT]  
>  보조 데이터베이스를 주 데이터베이스로 변경하는 경우 사용자와 애플리케이션에 일관된 환경을 제공하려면 로그인, 작업 등 데이터베이스의 일부 또는 모든 메타데이터를 새로운 주 서버 인스턴스에서 다시 만들어야 할 수도 있습니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)을 참조하세요.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [로그 전달 보조 데이터베이스로 장애 조치(failover)&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [역할 전환 후 로그인 및 작업 관리&#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 테이블 및 저장 프로시저](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
