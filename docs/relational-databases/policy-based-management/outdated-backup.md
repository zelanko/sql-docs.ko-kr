---
title: "오래된 백업 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "최선의 방법 [데이터베이스 엔진]"
ms.assetid: 307a4ad0-675a-4f97-9a3c-cedd61bdfae5
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 오래된 백업
  이 규칙은 최근 데이터베이스 백업이 있는지 검사합니다. 여러 가지 오류로 인한 데이터 손실로부터 데이터베이스를 보호하기 위해서는 정기적인 백업을 예약하는 것이 중요합니다. 적절한 데이터 백업 빈도는 데이터베이스의 복구 모델, 가능한 데이터 손실에 대한 비즈니스 요구 사항 및 데이터베이스 업데이트 빈도에 따라 달라집니다. 자주 업데이트되는 데이터베이스의 경우 백업 사이의 작업 손실 가능성이 빠르게 증가합니다.  
  
## 최선의 구현 방법 권장 사항  
 데이터 손실로부터 데이터베이스를 보호하는 데 충분한 빈도로 백업을 수행하는 것이 좋습니다.  
  
 단순 복구 모델과 전체 복구 모델 모두 데이터 백업이 필요합니다. 두 복구 모델에서 모두 전체 백업을 보충하는 차등 백업을 통해 데이터 손실 위험을 효과적으로 줄일 수 있습니다.  
  
 전체 복구 모델을 사용하는 데이터베이스의 경우 로그 백업을 자주 수행하는 것이 좋습니다. 매우 중요한 데이터가 포함된 프로덕션 데이터베이스의 경우 일반적으로 1분에서 15분 사이의 간격으로 로그 백업을 수행합니다.  
  
> [!NOTE]  
>  백업 예약을 위해서는 데이터베이스 유지 관리 계획을 사용하는 것이 좋습니다.  
  
## 참조 항목  
 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
 [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)  
  
## 참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  