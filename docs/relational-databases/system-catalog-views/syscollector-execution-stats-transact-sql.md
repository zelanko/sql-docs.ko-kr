---
title: syscollector_execution_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_execution_stats
- syscollector_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_execution_stats view
- data collector view
ms.assetid: 23e35ac5-fbbf-4922-970c-f4fac44c1263
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b89823af1295b329046395a8f3c345401ca61805
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779721"
---
# <a name="syscollectorexecutionstats-transact-sql"></a>syscollector_execution_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  컬렉션 집합 또는 패키지에 대한 태스크 실행 정보를 제공합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**log_id**|**bigint**|각 컬렉션 집합의 실행을 식별합니다. 이 뷰와 자세한 다른 로그를 조인하는 데 사용됩니다. Null을 허용하지 않습니다.|  
|**task_name**|**nvarchar(128)**|이 정보의 대상인 컬렉션 집합 또는 패키지 태스크의 이름입니다. Null을 허용하지 않습니다.|  
|**execution_row_count_in**|**int**|데이터 흐름의 시작 부분에서 처리되는 행 수입니다. Null을 허용합니다.|  
|**execution_row_count_out**|**int**|데이터 흐름의 종료 부분에서 처리되는 행 수입니다. Null을 허용합니다.|  
|**execution_row_count_errors**|**int**|데이터 흐름 도중 실패한 행 수입니다. Null을 허용합니다.|  
|**execution_time_ms**|**int**|태스크가 완료되는 데 필요한 시간(밀리초)입니다. Null을 허용합니다.|  
|**log_time**|**datetime**|이 정보가 기록된 시간입니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 에 대 한 SELECT 권한이 필요 **dc_operator**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 수집기 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
