---
title: MSSQLSERVER_14421 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 14421 (Database Engine error)
ms.assetid: 03e76d4a-d463-4673-8843-08e4ecaefe27
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2977fa37871ea3a9ecb47d4b4931fa8349e38123
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver14421"></a>MSSQLSERVER_14421
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14421|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum14421|  
|메시지 텍스트|로그 전달 보조 데이터베이스 %s.%s은(는) 복원 임계값이 %d분이며 동기화되지 않았습니다. %d분 동안 복원이 수행되지 않았습니다. 복원 대기 시간은 %d분입니다. 에이전트 로그 및 로그 전달 모니터 정보를 확인하십시오.|  
  
## <a name="explanation"></a>설명  
이 메시지는 로그 전달이 복원 임계값을 초과하여 동기화되지 않았음을 나타냅니다. 복원 임계값은 메시지가 생성되기 전에 복원 작업 간에 경과된 시간(분)입니다.  
  
### <a name="possible-causes"></a>가능한 원인  
이 메시지가 반드시 로그 전달 문제를 나타내는 것은 아닙니다. 대신 이 메시지는 다음 문제 중 하나를 나타낼 수 있습니다.  
  
-   복원 작업이 실행되고 있지 않습니다.  
  
    이는 보조 서버 인스턴스의 SQL Server 에이전트 서비스가 실행되고 있지 않거나 작업이 해제되었거나 작업 일정이 변경되었기 때문일 수 있습니다.  
  
-   복원 작업이 실패했습니다.  
  
    복원 폴더 경로가 유효하지 않거나 디스크가 꽉 찼거나 RESTORE 문이 실패할 수 있는 다른 원인으로 인해 작업이 실패했을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 메시지의 문제를 해결하려면  
  
-   SQL Server 에이전트 서비스가 보조 서버 인스턴스에 대해 실행되고 있는지 그리고 이 보조 데이터베이스에 대한 복원 작업이 설정되어 적절한 빈도로 실행되도록 예약되어 있는지 확인합니다.  
  
-   보조 서버의 복원 작업이 실패할 수 있습니다. 이 경우 원인을 찾을 수 있도록 복원 작업에 대한 작업 기록을 확인합니다.  
  
-   보조 서버 인스턴스에서 실행되는 로그 전달 복원 작업의 경우 **log_shipping_monitor_secondary** 테이블을 업데이트하기 위한 모니터 서버 인스턴스로의 연결이 불가능할 수 있습니다. 이는 모니터 서버 인스턴스와 보조 서버 인스턴스 간의 인증 문제로 인해 발생할 수 있습니다.  
  
-   백업 경고 임계값에 잘못된 값이 있을 수 있습니다. 이 값은 복원 작업 빈도의 세 배 이상으로 설정되는 것이 좋습니다. 로그 전달을 구성하여 작동한 후에 복원 작업의 빈도를 변경하는 경우 백업 경고 임계값을 이에 맞게 업데이트해야 합니다.  
  
-   모니터 서버 인스턴스가 오프라인 상태가 된 후 다시 온라인 상태로 돌아오는 경우 경고 메시지 작업이 실행되기 전에는 **log_shipping_monitor_secondary** 테이블이 현재 값으로 업데이트되지 않습니다. "보조 데이터베이스에 적용할 수 있는 로그 백업 파일을 찾을 수 없습니다"라는 메시지와 함께 복원 작업이 실행되는 경우 오류 14421이 발생할 수 있습니다. 이러한 오류가 발생하면 복원 시간은 업데이트되지 않습니다. 이 경우 오류는 복사 작업 문제로 인한 것일 수 있습니다.  
  
    보조 데이터베이스에 대한 최신 데이터를 사용하여 모니터 테이블을 업데이트하려면 보조 서버 인스턴스에서 **sp_refresh_log_shipping_monitor**를 실행합니다.  
  
-   보조 인스턴스나 모니터 서버 인스턴스의 날짜 또는 시간이 올바르지 않습니다. 이로 인해 경고 메시지가 생성될 수 있습니다. 두 서버 인스턴스 중 하나에서 시스템 날짜나 시간이 수정되었을 수 있습니다.  
  
    > [!NOTE]  
    > 두 서버 인스턴스의 서로 다른 표준 시간대로 인해 문제가 발생하지 않아야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[log_shipping_monitor_secondary&#40;Transact-SQL&#41;](~/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)  
[로그 전달 정보&#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
[sp_help_log_shipping_monitor_secondary&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)  
[sp_refresh_log_shipping_monitor&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql.md)  
[로그 전달 정보&#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
