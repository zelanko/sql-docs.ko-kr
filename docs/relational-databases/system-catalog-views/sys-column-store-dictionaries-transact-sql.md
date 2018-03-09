---
title: sys.column_store_dictionaries (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.column_store_dictionaries_TSQL
- column_store_dictionaries
- column_store_dictionaries_TSQL
- sys.column_store_dictionaries
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_dictionaries catalog view
ms.assetid: 56efd563-2f72-4caf-94e3-8a182385c173
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e540f8bea10bb627554ebee15254112e3e4d71c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="syscolumnstoredictionaries-transact-sql"></a>sys.column_store_dictionaries(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  xVelocity 메모리 최적화 columnstore 인덱스에 사용되는 각 사전에 대한 행을 포함합니다. 사전은 일부 데이터 형식을 인코딩하는 데 사용되므로 columnstore 인덱스의 일부 열에만 사전이 있습니다. 사전은 모든 세그먼트의 기본 사전으로 있을 수 있으며 열 세그먼트의 하위 집합에 사용되는 다른 보조 사전으로 있을 수도 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**hobt_id**|**bigint**|이 Columnstore 인덱스를 가진 테이블의 B-트리 인덱스(hobt) 또는 힙의 ID입니다.|  
|**column_id**|**int**|1부터 시작 하는 columnstore 열의 ID입니다. 첫 번째 열에 ID = 1, 두 번째 열에 ID = 2, 등입니다.|  
|**dictionary_id**|**int**|두 가지 사전, 전역 및 로컬, 열 세그먼트와 연결 된 있을 수 있습니다. 0 dictionary_id에 모든 열 세그먼트 (각 행 그룹에 대해 하나씩) 해당 열에 대해에서 공유 되는 전역 사전을 나타냅니다.|  
|**version**|**int**|사전 형식의 버전입니다.|  
|**유형**|**int**|사전 종류입니다.<br /><br /> 1-포함 하는 해시 사전 **int** 값<br /><br /> 2 – 사용되지 않음<br /><br /> 3 – 문자열 값을 포함하는 해시 사전<br /><br /> 4-포함 하는 해시 사전 **float** 값<br /><br /> 사전에 대 한 자세한 내용은 참조 [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)합니다.|  
|**last_id**|**int**|사전의 마지막 데이터 ID입니다.|  
|**entry_count 개**|**bigint**|사전에 있는 항목의 개수입니다.|  
|**on_disc_size**|**bigint**|사전의 크기(바이트)입니다.|  
|**partition_id**|**bigint**|파티션 ID를 나타냅니다. 데이터베이스 내에서 고유합니다.|  
  
## <a name="permissions"></a>Permissions  
 모든 열에 테이블에 대한 VIEW DEFINITION 이상의 권한이 필요합니다. 해당 사용자에 게 하지 않는 한 다음과 같은 열은 null을 반환 **선택** 권한: last_id, entry_count, data_ptr 등입니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_segments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

