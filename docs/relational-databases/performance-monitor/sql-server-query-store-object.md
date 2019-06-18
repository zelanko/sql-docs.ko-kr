---
title: SQL Server, Query Store 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store object
- SQL Server:Query Store
ms.assetid: b4a04acd-0b66-44a5-b72d-1a45b49e13e6
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: aba8942612be6c7b33883bb109146170583b5b95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62649420"
---
# <a name="sql-server-query-store-object"></a>SQL Server, 쿼리 저장소 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  쿼리 저장소 개체는 저장 프로시저, 임시 및 준비된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문, 트리거 등의 개체에 대한 쿼리 텍스트, 실행 계획 및 런타임 통계를 저장하기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 리소스 사용률을 모니터링하는 카운터를 제공합니다.  
  
 다음 표에서는 **SQLServer:Query Store**카운터에 대해 설명합니다.  
  
|SQL Server 쿼리 저장소 카운터|설명|  
|-------------------------------------|-----------------|  
|**Query Store CPU usage**|쿼리 저장소의 CPU 사용량을 나타냅니다.|  
|**Query Store logical reads**|쿼리 저장소에서 수행된 논리적 읽기 수를 나타냅니다.|  
|**Query Store logical writes**|쿼리 저장소에서 플러시되도록 대기된 데이터의 양을 나타냅니다. 런타임 통계를 나타내는 항목을 큐에 추가하는 작업의 빈도와 연기 시간은 데이터 플러시 간격 설정에 따라 제어됩니다.|  
|**Query Store physical reads**|쿼리 저장소에서 수행된 물리적 읽기 수를 나타냅니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|쿼리 저장소 인스턴스|설명|  
|--------------------------|-----------------|  
|**_Total**|이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 쿼리 저장소의 정보입니다.|  
|\<데이터베이스 이름>|이 데이터베이스에 대한 쿼리 저장소 정보입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [쿼리 저장소 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
