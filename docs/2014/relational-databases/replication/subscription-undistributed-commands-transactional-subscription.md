---
title: 구독, 배포 되지 않은 명령 (트랜잭션 구독, SQL Server 2005 이상) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a1f957c417c5c63766dfbffa923edd6935d1eb5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151487"
---
# <a name="subscription-undistributed-commands-transactional-subscription-sql-server-2005-and-later"></a>구독, 배포되지 않은 명령(트랜잭션 구독, SQL Server 2005 이상)
  **배포되지 않은 명령** 탭에는 선택한 구독자에 배달되지 않은 배포 데이터베이스의 명령 수와 해당 명령의 예상 배달 시간에 대한 정보가 표시됩니다. 배포 데이터베이스의 명령을 보는 방법은 [sp_replshowcmds&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql)를 참조하세요.  
  
## <a name="options"></a>변수  
 **이 구독자에 적용되기를 기다리는 배포 데이터베이스의 명령 수**  
 선택한 구독자에 배달되지 않은 배포 데이터베이스의 명령 수. 명령은 하나의 Transact-SQL DML(데이터 조작 언어) 문이나 하나의 DDL(데이터 정의 언어) 문으로 구성됩니다.  
  
 **과거 성능을 기준으로 이 명령 적용에 소요될 예상 시간**  
 명령을 구독자에 배달하는 데 걸리는 예상 시간. 이 값이 스냅숏을 생성하여 구독자에 적용하는 데 필요한 시간 값보다 더 큰 경우 구독자를 다시 초기화하십시오. 자세한 내용은 [구독 다시 초기화](reinitialize-subscriptions.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [복제 모니터 시작](monitor/start-the-replication-monitor.md)   
 [복제 모니터로 성능 모니터링](monitor/monitor-performance-with-replication-monitor.md)   
 [복제 모니터링](monitoring-replication.md)  
  
  
