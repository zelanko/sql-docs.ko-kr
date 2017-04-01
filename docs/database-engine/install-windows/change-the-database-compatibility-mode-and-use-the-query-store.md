---
title: "데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용 | Microsoft Docs"
ms.custom: ""
ms.date: "09/22/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "쿼리 계획 [SQL Server], 마이그레이션"
  - "SQL Server 업그레이드, 쿼리 계획 마이그레이션"
  - "계획 지침 [SQL Server], 쿼리 계획 마이그레이션"
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 19
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 17
---
# 데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용
  SQL Server 2016에서 데이터베이스에 대한 DATABASE_COMPATIBILITY 수준이 130으로 변경된 후에 일부 변경 내용이 활성화됩니다.  이 작업은 여러 가지 이유로 수행되었습니다.  
  
-   업그레이드는 단방향 작업이므로(파일 형식을 다운그레이드할 수 없음) 데이터베이스 내에서 별도 작업에 대한 새로운 기능의 사용을 분리하는 값이 있습니다.  이전 DATABASE_COMPATIBILITY 수준으로 설정을 되돌릴 수는 있습니다.  새 모델은 중단 창 동안 발생해야 하는 것의 수를 줄입니다.  
  
-   쿼리 프로세서에 대한 변경 내용에는 복잡한 영향이 있을 수 있습니다.  대부분의 고객에게 유용할 수 있는 시스템에 대한 “올바른" 변경이더라도 다른 위치의 중요한 쿼리에 예상치 못한 회귀가 발생할 수 있습니다.  업그레이드 프로세스에서 이 논리를 분리하는 작업은 쿼리 저장소와 같은 기능이 계획 선택 회귀를 신속하게 완화하거나 프로덕션 서버에서 완전히 방지할 수 있도록 합니다.  
  
> [!NOTE]  
>  사용자 데이터베이스의 호환성 수준이 업그레이드 이전에 100 이상이었다면 업그레이드 후에도 동일하게 유지됩니다. 업그레이드 이전에 호환성 수준이 90이었다면 업그레이드된 데이터베이스에서는 호환성 수준이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되는 가장 낮은 호환성 수준인 100으로 설정됩니다.  
  
 새 쿼리 프로세서 기능을 활성화하는 업그레이드 프로세스는 제품의 릴리스 이후 서비스 모델과 관련이 있습니다.  이러한 수정의 일부는 추적 플래그 4199에서 릴리스됩니다.  수정이 필요한 고객은 다른 고객에 대한 예기치 않은 회귀를 일으키지 않고 이러한 수정을 선택할 수 있습니다.  쿼리 프로세서 핫픽스에 대한 릴리스 이후 서비스 모델은 [여기](https://support.microsoft.com/en-us/kb/974006)에 설명되어 있습니다. SQL Server 2016년 현재 새로운 호환성 수준으로의 이동은 해당 수정은 이제 최신 호환 모드(130)에서 기본적으로 사용할 수 있으므로 4199 추적 플래그가 더 이상 필요하지 않다는 것을 의미합니다.  따라서 업그레이드 프로세스의 일부로 업그레이드 프로세스가 완료되면 4199가 활성화되지 않는 것을 확인하는 것이 중요합니다.  
  
 쿼리 프로세서를 코드의 최신 버전으로 업그레이드하기 위해 권장되는 워크플로는 다음과 같습니다.  
  
1.  데이터베이스 호환성 수준을 변경하지 않고(이전 수준에서 유지) 데이터베이스를 SQL Server 2016으로 업그레이드  
  
2.  데이터베이스에서 쿼리 저장소를 활성화합니다. 쿼리 저장소 활성화 및 사용에 대한 자세한 내용은 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)을(를) 참조하세요.  
  
3.  작업의 대표 데이터를 수집할 수 있도록 충분한 시간을 기다립니다.  
  
4.  데이터베이스의 호환성 수준을 130으로 변경  
  
5.  SQL Server Management Studio를 사용하여 호환성 수준 변경 후에 특정 쿼리에 대한 성능 저하가 있는지 평가  
  
6.  회귀가 있는 경우 쿼리 저장소에서 이전 계획을 강제로 적용합니다.  
  
7.  강제 적용에 실패하는 쿼리 계획이 있는 경우 또는 성능이 여전히 충분하지 않은 경우 호환성 수준을 이전 설정으로 되돌린 다음 Microsoft 고객 지원 서비스에 연락하는 것이 좋습니다.  
  
## 참고 항목  
 [데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)  
  
  