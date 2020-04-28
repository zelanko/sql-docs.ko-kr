---
title: 데이터 수집기 뷰 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- data collector [SQL Server], views
ms.assetid: a005e885-7813-4c7e-b332-b01d9e9d4054
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9e412f796a5b04f980557b5a3131763811aa78da
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68033176"
---
# <a name="data-collector-views-transact-sql"></a>데이터 수집기 뷰(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  데이터 수집기는 수집기 유형 속성, 컬렉션 집합, 컬렉션 집합 항목과 같은 데이터 수집기 구성에 대한 정보와 컬렉션 집합이 실행될 때 얻은 실행 통계에 대한 정보를 표시하기 위한 다음과 같은 뷰를 제공합니다. **Msdb** 데이터베이스에 있는 이러한 뷰는 기본 테이블에 대 한 추상화 계층도 제공 합니다. 이 추상화는 테이블에 대한 직접 액세스를 차단하고 관련 애플리케이션에 영향을 주지 않으면서 테이블의 변경을 허용함으로써 보안을 강화합니다.  
  
|||  
|-|-|  
|[syscollector_collection_items&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|[syscollector_collection_sets&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|  
|[syscollector_collector_types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|[syscollector_config_store&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|  
|[syscollector_execution_log&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|[syscollector_execution_log_full&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|  
|[syscollector_execution_stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)||  
  
## <a name="see-also"></a>참고 항목  
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)   
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
