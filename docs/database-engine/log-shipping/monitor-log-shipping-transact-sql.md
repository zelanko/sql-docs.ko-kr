---
title: 로그 전달 모니터링(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], status
- history tables [SQL Server]
- historical information [SQL Server], log shipping
- log shipping [SQL Server], monitoring
- alerts [SQL Server], log shipping
- status information [SQL Server], log shipping
- monitoring log shipping [SQL Server]
ms.assetid: acf3cd99-55f7-4287-8414-0892f830f423
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: cd0527188ebdf3bbe5f0e2504ddd696f92038faa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794613"
---
# <a name="monitor-log-shipping-transact-sql"></a>로그 전달 모니터링(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  로그 전달을 구성한 후 모든 로그 전달 서버의 상태에 대한 정보를 모니터링할 수 있습니다. 로그 전달 작업의 기록과 상태는 항상 로그 전달 작업에 의해 로컬에 저장됩니다. 백업 작업의 기록과 상태는 주 서버에 저장되고 복사 및 복원 작업의 기록과 상태는 보조 서버에 저장됩니다. 원격 모니터 서버를 구현한 경우 이 정보는 모니터 서버에도 저장됩니다.  
  
 로그 전달 작업이 예약된 대로 수행되지 않으면 경고가 발생하도록 구성할 수 있습니다. 오류는 백업 및 복원 작업 상태를 감시하는 경고 작업에 의해 발생합니다. 이러한 오류가 발생할 때 운영자에게 알리는 경고를 정의할 수 있습니다. 모니터 서버가 구성되어 있는 경우 모니터 서버에서 로그 전달 구성의 모든 작업에 대해 오류를 발생시키는 하나의 경고 작업이 실행됩니다. 모니터 서버가 지정되지 않은 경우 경고 작업은 주 서버 인스턴스에서 실행되어 백업 작업을 모니터링합니다. 모니터 서버가 지정되어 있지 않으면 각 보조 서버 인스턴스에서도 경고 작업이 실행되어 로컬 복사 및 복원 작업을 모니터링합니다.  
  
> [!IMPORTANT]  
>  로그 전달 구성을 모니터링하려면 로그 전달을 설정할 때 모니터 서버를 추가해야 합니다. 나중에 모니터 서버를 추가하는 경우 로그 전달 구성을 제거한 다음 모니터 서버가 포함된 새 구성으로 바꾸어야 합니다. 자세한 내용은 [로그 전달 구성&#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)에서 도입되었습니다. 또한 모니터 서버를 구성한 후에는 로그 전달을 먼저 제거하지 않으면 모니터 서버를 변경할 수 없습니다.  
  
## <a name="history-tables-containing-monitoring-information"></a>모니터링 정보가 들어 있는 기록 테이블  
 모니터링 기록 테이블에는 모니터 서버에 저장된 메타데이터가 있습니다. 지정된 주 서버 또는 보조 서버에 대한 정보의 복사본도 로컬에 저장됩니다.  
  
 이러한 테이블을 쿼리하여 로그 전달 세션의 상태를 모니터링할 수 있습니다. 예를 들어 로그 전달 상태를 알려면 백업 작업, 복사 작업 및 복원 작업의 상태와 기록을 확인합니다. 다음의 모니터링 테이블을 쿼리하여 특정 로그 전달 기록 및 오류 정보를 볼 수 있습니다.  
  
|Table|설명|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](../../relational-databases/system-tables/log-shipping-monitor-alert-transact-sql.md)|경고 작업 ID를 저장합니다.|  
|[log_shipping_monitor_error_detail](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)|로그 전달 작업에 대한 오류 정보를 저장합니다. 이 테이블을 쿼리하여 에이전트 세션에 대한 오류를 볼 수 있습니다. 필요에 따라 각 오류가 로그된 날짜 및 시간별로 오류를 정렬할 수 있습니다. 각 오류는 예외순으로 로그되고 에이전트 세션당 여러 개의 오류(시퀀스)가 로그될 수 있습니다.|  
|[log_shipping_monitor_history_detail](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)|로그 전달 에이전트에 대한 기록 세부 정보가 들어 있습니다. 이 테이블을 쿼리하여 에이전트 세션에 대한 기록 세부 정보를 볼 수 있습니다.|  
|[log_shipping_monitor_primary](../../relational-databases/system-tables/log-shipping-monitor-primary-transact-sql.md)|모니터링에 유용한 마지막 복원 파일과 마지막 백업 파일에 대한 정보를 포함하여 각 로그 전달 구성에 주 데이터베이스에 대한 하나의 모니터 레코드를 저장합니다.|  
|[log_shipping_monitor_secondary](../../relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)|모니터링에 유용한 마지막 복원 파일과 마지막 백업 파일에 대한 정보를 포함하여 각 보조 데이터베이스에 대한 하나의 모니터 레코드를 저장합니다.|  
  
## <a name="stored-procedures-for-monitoring-log-shipping"></a>로그 전달 모니터링을 위한 저장 프로시저  
 로그 전달 저장 프로시저를 사용하여 액세스할 수 있는 **msdb**의 테이블에 모니터링 및 기록 정보가 저장됩니다. 다음 표에 표시된 서버에서 이러한 저장 프로시저를 실행합니다.  
  
|저장 프로시저|설명|프로시저 실행 위치|  
|----------------------|-----------------|---------------------------|  
|[sp_help_log_shipping_monitor_primary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)|**log_shipping_monitor_primary** 테이블에서 지정한 주 데이터베이스에 대한 모니터 레코드를 반환합니다.|모니터 서버 또는 주 서버|  
|[sp_help_log_shipping_monitor_secondary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)|**log_shipping_monitor_secondary** 테이블에서 지정한 보조 데이터베이스에 대한 모니터 레코드를 반환합니다.|모니터 서버 또는 보조 서버|  
|[sp_help_log_shipping_alert_job](../../relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql.md)|경고 작업의 작업 ID를 반환합니다.|모니터 서버 또는 정의된 모니터가 없으면 주 서버 또는 보조 서버|  
|[sp_help_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)|주 데이터베이스 설정을 검색하고 **log_shipping_primary_databases** 및 **log_shipping_monitor_primary** 테이블의 값을 표시합니다.|주 서버|  
|[sp_help_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql.md)|주 데이터베이스의 보조 데이터베이스 이름을 검색합니다.|주 서버|  
|[sp_help_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)|**log_shipping_secondary**, **log_shipping_secondary_databases** 및 **log_shipping_monitor_secondary** 테이블에서 보조 데이터베이스 설정을 검색합니다.|보조 서버|  
|[sp_help_log_shipping_secondary_primary&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql.md)|이 저장 프로시저는 보조 서버에서 지정된 주 데이터베이스의 설정을 검색합니다.|보조 서버|  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 보고서 보기&#40;SQL Server Management Studio&#41;](../../database-engine/log-shipping/view-the-log-shipping-report-sql-server-management-studio.md)   
 [로그 전달 저장 프로시저 및 테이블](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  
