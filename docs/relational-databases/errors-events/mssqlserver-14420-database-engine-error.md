---
title: MSSQLSERVER_14420 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 14420 (Database Engine error)
ms.assetid: 4a1d72b1-ab1b-4119-a11b-a8a05c6fdb45
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1bd13e793e1ceed7a898267de84b8c0b2bbe0646
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323084"
---
# <a name="mssqlserver14420"></a>MSSQLSERVER_14420
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14420|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum14420|  
|메시지 텍스트|로그 전달 주 데이터베이스 %s.%s은(는) 백업 임계값이 %d분이며 %d분 동안 백업 로그 작업을 수행하지 않았습니다. 에이전트 로그 및 로그 전달 모니터 정보를 확인하십시오.|  
  
## <a name="explanation"></a>설명  
로그 전달이 백업 임계값을 초과하여 동기화되지 않았습니다. 백업 임계값은 로그 전달 백업 작업 간에 허용되는 시간(분)이며 이 시간이 지나면 경고가 발생합니다. 이 메시지가 반드시 로그 전달 문제를 나타내는 것은 아닙니다. 대신 이 메시지는 다음 문제 중 하나를 나타낼 수 있습니다.  
  
-   백업 작업이 실행되고 있지 않습니다. 이는 주 서버 인스턴스의 SQL Server 에이전트 서비스가 실행되고 있지 않거나 작업이 해제되었거나 작업 일정이 변경되었기 때문일 수 있습니다.  
  
-   백업 작업이 실패했습니다. 이는 백업 폴더 경로가 유효하지 않거나 디스크가 꽉 찼거나 BACKUP 문이 실패할 수 있는 다른 원인으로 인한 것일 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 메시지의 문제를 해결하려면  
  
-   SQL Server 에이전트 서비스가 주 서버 인스턴스에 대해 실행되고 있는지 그리고 주 데이터베이스에 대한 백업 작업이 설정되어 적절한 빈도로 실행되도록 예약되어 있는지 확인합니다.  
  
-   주 서버의 백업 작업이 실패할 수 있습니다. 이 경우 원인을 찾을 수 있도록 백업 작업에 대한 작업 기록을 확인합니다.  
  
-   주 서버 인스턴스에서 실행되는 로그 전달 백업 작업의 경우 **log_shipping_monitor_primary** 테이블을 업데이트하기 위한 모니터 서버 인스턴스에 대한 연결이 불가능할 수 있습니다. 이는 모니터 서버 인스턴스와 주 서버 인스턴스 간의 인증 문제로 인해 발생할 수 있습니다.  
  
-   백업 경고 임계값에 잘못된 값이 있을 수 있습니다. 이 값은 백업 작업 빈도의 세 배 이상으로 설정되는 것이 좋습니다. 로그 전달을 구성하여 작동한 후에 백업 작업의 빈도를 변경하는 경우 백업 경고 임계값을 이에 맞게 업데이트해야 합니다.  
  
-   모니터 서버 인스턴스가 오프라인 상태가 된 후 다시 온라인 상태로 돌아오는 경우 경고 메시지 작업이 실행되기 전에는 **log_shipping_monitor_primary** 테이블이 현재 값으로 업데이트되지 않습니다. 주 데이터베이스에 대한 최신 데이터를 사용하여 모니터 테이블을 업데이트하려면 주 서버 인스턴스에서 **sp_refresh_log_shipping_monitor**를 실행합니다.  
  
-   주 서버 인스턴스나 모니터 서버 인스턴스의 날짜 또는 시간이 올바르지 않습니다. 이로 인해 경고 메시지가 생성될 수 있습니다. 두 서버 인스턴스 중 하나에서 시스템 날짜나 시간이 수정되었을 수 있습니다.  
  
    > [!NOTE]  
    > 두 서버 인스턴스의 서로 다른 표준 시간대로 인해 문제가 발생하지 않아야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[log_shipping_monitor_primary&#40;Transact-SQL&#41;](~/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql.md)  
[로그 전달 정보&#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
[sp_help_log_shipping_monitor_primary&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)  
[sp_refresh_log_shipping_monitor&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql.md)  
[로그 전달 정보&#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
