---
title: sys.dm_fts_semantic_similarity_population (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_fts_semantic_similarity_population_TSQL
- sys.dm_fts_semantic_similarity_population
- dm_fts_semantic_similarity_population
- sys.dm_fts_semantic_similarity_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_semantic_similarity_population dynamic management view
ms.assetid: 33666f28-c370-47e2-a932-190316ed5f69
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0e28dfafb637aebf7e22f4b61f595f02de0f1284
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmftssemanticsimilaritypopulation-transact-sql"></a>sys.dm_fts_semantic_similarity_population(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  연결된 의미 체계 인덱스가 있는 각 테이블의 각 유사성 인덱스에 대해 문서 유사성 인덱스 채우기와 관련된 상태 정보가 들어 있는 하나의 행을 반환합니다.  
  
 채우기 단계는 추출 단계 이후에 수행됩니다. 유사성 추출 단계에 대 한 상태 정보를 참조 하십시오. [sys.dm_fts_index_population &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)합니다.  
    
||||  
|-|-|-|  
|**열 이름**|**형식**|**설명**|  
|**database_id**|**int**|채우기가 진행되고 있는 전체 텍스트 인덱스를 포함하는 데이터베이스의 ID입니다.|  
|**catalog_id**|**int**|이 전체 텍스트 인덱스를 포함하는 전체 텍스트 카탈로그의 ID입니다.|  
|**table_id**|**int**|전체 텍스트 인덱스가 채워지고 있는 테이블의 ID입니다.|  
|**document_count**|**int**|채우기의 총 문서 수입니다.|  
|**document_processed_count**|**int**|이 채우기 주기가 시작된 이후 처리된 문서 수입니다.|  
|**completion_type**|**int**|이 채우기의 완료 상태입니다.|  
|**completion_type_description**|**nvarchar(120)**|완료 유형에 대한 설명입니다.|  
|**worker_count**|**int**|유사성 추출과 관련된 작업자 스레드 수입니다.|  
|**상태**|**int**|이 채우기의 상태입니다. 참고: 일부 상태는 일시적입니다. 다음 중 하나일 수 있습니다.<br /><br /> 3 = 시작 중<br /><br /> 5 = 정상적으로 처리 중<br /><br /> 7 = 처리가 중지됨<br /><br /> 11 = 채우기 중단됨|  
|**status_description**|**nvarchar(120)**|채우기 상태에 대한 설명입니다.|  
|**start_time**|**datetime**|채우기가 시작된 시간입니다.|  
|**incremental_timestamp**|**timestamp**|전체 채우기의 시작 타임스탬프를 나타냅니다. 다른 모든 채우기 유형의 경우 이 값은 마지막으로 커밋된 검사점으로, 채우기의 진행 상태를 나타냅니다.|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 참조 [검색 관리 및 모니터링 의미 체계](../../relational-databases/search/manage-and-monitor-semantic-search.md)합니다.  
  
## <a name="metadata"></a>메타데이터  
 쿼리 의미 체계 인덱싱의 상태에 대 한 자세한 내용은 [sys.dm_fts_index_population &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)합니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 연결된 의미 체계 인덱스가 있는 모든 테이블에 대한 문서 유사성 인덱스 채우기의 상태를 쿼리하는 방법을 보여 줍니다.  
  
```  
SELECT * FROM sys.dm_fts_semantic_similarity_population;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
