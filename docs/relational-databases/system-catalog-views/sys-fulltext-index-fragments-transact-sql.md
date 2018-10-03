---
title: sys.fulltext_index_fragments (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_index_fragments
- sys.fulltext_index_fragments_TSQL
- fulltext_index_fragments_TSQL
- sys.fulltext_index_fragments
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], fragments
- full-text indexes [SQL Server], metadata
- troubleshooting [SQL Server], full-text search
- sys.fulltext_index_fragments catalog view
ms.assetid: a82e5018-5d88-45c0-9a47-c251e17a6cdb
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dbf3affc922eeddd0b27d15df1177bad30bb185f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646271"
---
# <a name="sysfulltextindexfragments-transact-sql"></a>sys.fulltext_index_fragments(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  라고 하는 내부 테이블을 사용 하 여 전체 텍스트 인덱스 *전체 텍스트 인덱스 조각* 반전 된 인덱스 데이터를 저장 합니다. 이 뷰를 사용하면 이러한 조각에 대한 메타데이터를 쿼리할 수 있습니다. 이 뷰에는 전체 텍스트 인덱스를 포함하는 모든 테이블의 각 전체 인덱스 조각에 대한 행이 들어 있습니다.  
 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|table_id|**int**|전체 텍스트 인덱스 조각을 포함하는 테이블의 개체 ID입니다.|  
|fragment_object_id|**int**|조각과 연결된 내부 테이블의 개체 ID입니다.|  
|fragment_id|**int**|전체 텍스트 인덱스 조각의 논리적 ID입니다. 이는 이 테이블의 모든 조각에서 고유합니다.|  
|TIMESTAMP|**timestamp**|조각 생성과 연결된 타임스탬프입니다. 최신 세그먼트의 타임스탬프가 이전 세그먼트의 타임스탬프보다 큽니다.|  
|data_size|**int**|조각의 논리적 크기(바이트)입니다.|  
|row_count|**int**|조각의 개별 행 수입니다.|  
|상태|**int**|조각의 상태로, 다음 중 하나입니다.<br /><br /> 0 = 새로 만들었지만 아직 사용하지 않음<br /><br /> 1 = 전체 텍스트 인덱스 채우기 또는 병합 동안 삽입에 사용됨<br /><br /> 4 = 닫힘 쿼리를 준비함<br /><br /> 6 = 병합 입력에 사용되며 쿼리를 준비함<br /><br /> 8 = 삭제용으로 표시되며 쿼리 및 병합 원본에 사용되지 않음<br /><br /> 상태 4 또는 6은 조각이 논리적 전체 텍스트 인덱스의 일부 이며 쿼리할 수 있습니다. 즉, 한 *쿼리 가능한* 조각.|  
  
## <a name="remarks"></a>Remarks  
 sys.fulltext_index_fragments 카탈로그 뷰를 사용하면 전체 텍스트 인덱스를 구성하는 조각 수를 쿼리할 수 있습니다. 느린 전체 텍스트 쿼리 성능을 경험하는 경우 다음과 같이 sys.fulltext_index_fragments를 사용하여 전체 텍스트 인덱스에서 쿼리 가능 조각(상태 = 4 또는 6) 수를 쿼리할 수 있습니다.  
  
```  
SELECT table_id, status FROM sys.fulltext_index_fragments  
   WHERE status=4 OR status=6;  
```  
  
 쿼리 가능 조각이 많이 있는 경우 조각을 모두 병합하도록 전체 텍스트 인덱스를 포함하는 전체 텍스트 카탈로그를 다시 구성하는 것이 좋습니다. 다시 구성 하는 전체 텍스트 카탈로그 사용 [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)*catalog_name* 다시 구성 합니다. 예를 들어 `ftCatalog` 데이터베이스에서 `AdventureWorks2012`라는 전체 텍스트 카탈로그를 다시 구성하려면 다음을 입력합니다.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog REORGANIZE;  
GO  
```  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
