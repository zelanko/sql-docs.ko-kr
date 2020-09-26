---
description: sys.column_store_segments(Transact-SQL)
title: sys. column_store_segments (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_store_segments
- sys.column_store_segments_TSQL
- sys.column_store_segments
- column_store_segments_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_segments catalog view
ms.assetid: 1253448c-2ec9-4900-ae9f-461d6b51b2ea
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3957a13e4d3e7f5eff32b0417e65d33a573e5510
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364200"
---
# <a name="syscolumn_store_segments-transact-sql"></a>sys.column_store_segments(Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

Columnstore 인덱스의 각 열 세그먼트에 대해 하나의 행을 반환 합니다. 행 그룹 당 열 마다 하나의 열 세그먼트가 있습니다. 예를 들어 10 개의 행 그룹 및 34 열이 있는 테이블은 340 행을 반환 합니다. 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|파티션 ID를 나타냅니다. 데이터베이스 내에서 고유합니다.|  
|**hobt_id**|**bigint**|이 columnstore 인덱스가 있는 테이블에 대 한 힙 또는 B-트리 인덱스 (HoBT)의 ID입니다.|  
|**column_id**|**int**|Columnstore 열의 ID입니다.|  
|**segment_id**|**int**|행 그룹의 ID입니다. 이전 버전과의 호환성을 위해 행 그룹 ID 인 경우에도 열 이름은 segment_id 계속 호출 됩니다. <segment_id>를 사용 하 여 세그먼트를 고유 하 게 식별할 수 있습니다 \<hobt_id, partition_id, column_id> .|  
|**version**|**int**|열 세그먼트 형식의 버전입니다.|  
|**encoding_type**|**int**|해당 세그먼트에 사용 되는 인코딩 유형입니다.<br /><br /> 1 = VALUE_BASED-사전 없이 문자열이 아닌/이진 (일부 내부 변형이 있는 4와 유사)<br /><br /> 2 = VALUE_HASH_BASED-사전에 공통 값이 있는 문자열이 아닌/이진 열<br /><br /> 3 = STRING_HASH_BASED-사전에 공통 값이 있는 문자열/이진 열<br /><br /> 4 = STORE_BY_VALUE_BASED-사전이 없는 문자열/이진<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-사전 없는 문자열/이진<br /><br /> 자세한 내용은 [설명](#remarks) 섹션을 참조하세요.|  
|**row_count**|**int**|행 그룹의 행 수입니다.|  
|**has_nulls**|**int**|열 세그먼트에 Null 값이 있으면 1입니다.|  
|**base_id**|**bigint**|인코딩 유형 1을 사용 하는 경우 기준 값 ID입니다. 인코딩 유형 1을 사용 하지 않는 경우 base_id은-1로 설정 됩니다.|  
|**magnitude**|**float**|인코딩 유형 1을 사용 하는 경우 크기입니다. 인코딩 유형 1을 사용 하지 않는 경우 크기는-1로 설정 됩니다.|  
|**primary_dictionary_id**|**int**|값 0은 전역 사전을 나타냅니다. 값-1은이 열에 대해 생성 된 전역 사전이 없음을 나타냅니다.|  
|**secondary_dictionary_id**|**int**|0이 아닌 값은 현재 세그먼트 (즉, 행 그룹)의이 열에 대 한 로컬 사전을 가리킵니다. 값-1은이 세그먼트에 대 한 로컬 사전이 없음을 나타냅니다.|  
|**min_data_id**|**bigint**|열 세그먼트의 최소 데이터 ID입니다.|  
|**max_data_id**|**bigint**|열 세그먼트의 최대 데이터 ID입니다.|  
|**null_value**|**bigint**|Null을 나타내는 데 사용되는 값입니다.|  
|**on_disk_size**|**bigint**|세그먼트의 크기(바이트)입니다.|  
  
## <a name="remarks"></a>설명  
에서 columnstore 세그먼트 인코딩 유형을 선택 하면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 세그먼트 데이터를 분석 하 여 저장소 비용을 가장 적게 달성할 수 있습니다. 데이터가 대부분 고유한 경우는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 값 기반 인코딩을 사용 합니다. 데이터가 대부분 고유 하지 않은 경우는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 해시 기반 인코딩을 사용 합니다. 문자열 기반 인코딩과 값 기반 인코딩 중에서 선택 하는 것은 문자열 데이터 인지 또는 이진 데이터 인지에 관계 없이 저장 되는 데이터의 형식과 관련이 있습니다. 모든 인코딩은 가능 하면 비트 압축 및 실행 길이 인코딩을 활용 합니다.
 
## <a name="permissions"></a>사용 권한  
 모든 열에는 적어도 `VIEW DEFINITION` 테이블에 대 한 권한이 있어야 합니다. 다음 열은 사용자에 게,,,, `SELECT` `has_nulls` `base_id` `magnitude` `min_data_id` `max_data_id` 및 `null_value` 권한이 없는 경우 null을 반환 합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  

## <a name="examples"></a>예제

### <a name="the-following-query-returns-information-about-segments-of-a-columnstore-index"></a>다음 쿼리는 columnstore 인덱스의 세그먼트에 대한 정보를 반환합니다.  
  
```sql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 5 OR i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
GO  
```  

## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [all_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [computed_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)    
 [sys.column_store_dictionaries&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
 
