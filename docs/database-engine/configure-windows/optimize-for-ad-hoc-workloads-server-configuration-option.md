---
title: "optimize for ad hoc workloads 서버 구성 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 11/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 207ca8c64cd20e8e98093960bd68ad23b770ea24
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>optimize for ad hoc workloads 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **optimize for ad hoc workloads** 옵션은 여러 개의 일회용 임시 일괄 처리를 포함하는 작업에서 계획 캐시의 효율성을 높이는 데 사용됩니다. 이 옵션을 1로 설정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 일괄 처리가 처음으로 컴파일되었을 때 전체 컴파일된 계획 대신 계획 캐시에 포함된 작은 컴파일된 계획 스텁을 저장합니다. 이렇게 하면 계획 캐시에 다시 사용할 수 없는 컴파일된 계획이 채워지지 않게 되므로 메모리 가중을 줄일 수 있습니다.  
  
 컴파일된 계획 스텁은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 이러한 임시 일괄 처리가 이전에 컴파일되었지만 컴파일된 계획 스텁만 저장했다는 것을 인식하게 함으로써 이 일괄 처리(컴파일 또는 실행된)가 다시 호출될 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 일괄 처리를 컴파일하고, 계획 캐시에서 컴파일된 계획 스텁을 제거하고, 계획 캐시에 전체 컴파일된 계획을 추가하도록 합니다. 
  
 컴파일된 계획 스텁은 sys.dm_exec_cached_plans 카탈로그 뷰로 표시되는 cacheobjtype 중 하나입니다. 여기에는 고유한 SQL 핸들 및 계획 핸들이 포함됩니다. 컴파일된 계획 스텁에는 연결된 실행 계획이 없으며 계획 핸들을 쿼리해도 XML 실행 계획이 반환되지 않습니다.  
  
 [추적 플래그 8032](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)는 일반적으로 캐시가 더 커지도록 허용하는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM 설정으로 캐시 제한 매개 변수를 복구합니다. 자주 재사용되는 캐시 항목이 캐시에 맞지 않고 임시 작업을 위해 최적화 서버 구성 옵션으로 계획 캐시 관련 문제를 해결하지 못한 경우 이 설정을 사용합니다.  
  
> [!WARNING]  
>  추적 플래그 8032는 대형 캐시로 버퍼 풀과 같은 다른 메모리 소비자에 제공되는 메모리가 줄어들 수 있는 성능 문제를 일으킬 수 있습니다.  

## <a name="recommendations"></a>권장 사항
일회 사용 계획의 수가 OLTP 서버의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 메모리의 상당 부분을 차지하고 이러한 계획이 임시 계획인 경우 이 서버 옵션을 사용하여 이들 개체의 메모리 사용을 줄입니다.
단일 사용으로 캐시된 계획의 수를 찾으려면 다음 쿼리를 실행합니다.

```t-sql
SELECT objtype, cacheobjtype, 
  AVG(usecounts) AS Avg_UseCount, 
  SUM(refcounts) AS AllRefObjects, 
  SUM(CAST(size_in_bytes AS bigint))/1024/1024 AS Size_MB
FROM sys.dm_exec_cached_plans
WHERE objtype = 'Adhoc' AND usecounts = 1
GROUP BY objtype, cacheobjtype;
```

> [!IMPORTANT]
> **optimize for ad hoc workloads** 를 1로 설정하면 새 계획만 영향을 받으며, 이미 계획 캐시에 있던 계획은 영향을 받지 않습니다.
> 이미 캐치된 계획에 즉시 영향을 주려면 [ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)를 사용하여 계획 캐시를 지우거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작해야 합니다.

## <a name="see-also"></a>관련 항목:  
 [sys.dm_exec_cached_plans&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
