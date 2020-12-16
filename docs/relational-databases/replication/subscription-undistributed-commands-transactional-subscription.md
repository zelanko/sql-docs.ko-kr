---
title: 배포되지 않은 명령(복제 모니터)
description: SSMS(SQL Server Management Studio) 복제 모니터의 ‘배포되지 않은 명령’ 탭을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: eec70665ef299b54c07ee74a4189ff3a10d00482
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460166"
---
# <a name="subscription-undistributed-commands-transactional-subscription"></a>구독, 배포되지 않은 명령(트랜잭션 구독)
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  **배포되지 않은 명령** 탭에는 선택한 구독자에 배달되지 않은 배포 데이터베이스의 명령 수와 해당 명령의 예상 배달 시간에 대한 정보가 표시됩니다. 배포 데이터베이스의 명령을 보는 방법은 [sp_replshowcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)를 참조하세요.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>옵션  
 **이 구독자에 적용되기를 기다리는 배포 데이터베이스의 명령 수**  
 선택한 구독자에 배달되지 않은 배포 데이터베이스의 명령 수. 명령은 하나의 Transact-SQL DML(데이터 조작 언어) 문이나 하나의 DDL(데이터 정의 언어) 문으로 구성됩니다.  
  
 **과거 성능을 기준으로 이 명령 적용에 소요될 예상 시간**  
 명령을 구독자에 배달하는 데 걸리는 예상 시간. 이 값이 스냅샷을 생성하여 구독자에 적용하는 데 필요한 시간 값보다 더 큰 경우 구독자를 다시 초기화하십시오. 자세한 내용은 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [복제 모니터로 성능 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
