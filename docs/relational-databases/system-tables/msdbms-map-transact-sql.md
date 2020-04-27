---
title: MSdbms_map (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_map
- MSdbms_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_map system table
ms.assetid: df67e691-3a50-450a-99c5-8c4a041749ae
author: stevestein
ms.author: sstein
ms.openlocfilehash: fffa30d0e252392c41cee34c1875b12b5b7a53b4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907497"
---
# <a name="msdbms_map-transact-sql"></a>MSdbms_map(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_map** 테이블에는 원본 데이터 형식 정보와 원본 및 대상 DBMS 쌍의 기본 대상 데이터 형식 정보에 대 한 링크가 포함 되어 있습니다. 이 테이블은 **msdb** 데이터베이스에 저장 되며 유형이 다른 게시에 사용 됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**map_id**|**int**|데이터 형식 매핑을 고유하게 식별합니다.|  
|**src_dbms_id**|**int**|[Msdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) 테이블에서 해당 **dbms_id** 을 지정 하 여 원본 DBMS를 식별 합니다.|  
|**dest_dbms_id**|**int**|[Msdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) 테이블에서 해당 **dbms_id** 을 지정 하 여 대상 DBMS를 식별 합니다.|  
|**src_datatype_id**|**int**|[MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md) 테이블에서 원본 데이터 형식에 대 한 **datatype_id** 를 식별 합니다.|  
|**src_len_min**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최소 길이입니다. NULL 값은 길이가 사용되지 않음을 나타냅니다.|  
|**src_len_max**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최대 길이입니다. NULL 값은 길이가 사용되지 않음을 나타냅니다.|  
|**src_prec_min**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최소 전체 자릿수입니다. NULL 값은 전체 자릿수가 사용되지 않음을 나타냅니다.|  
|**src_prec_max**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최대 전체 자릿수입니다. NULL 값은 전체 자릿수가 사용되지 않음을 나타냅니다.|  
|**src_scale_min**|**int**|원본 DBMS에서 해당 데이터 형식의 최소 소수 자릿수입니다. NULL 값은 소수 자릿수가 사용되지 않음을 나타냅니다.|  
|**src_scale_max**|**int**|원본 DBMS에서 해당 데이터 형식의 최대 소수 자릿수입니다. NULL 값은 소수 자릿수가 사용되지 않음을 나타냅니다.|  
|**src_nullable**|**bit**|매핑의 대상 열이 NULL 값을 허용하는지 여부를 나타냅니다. 여기서 NULL 값은 이 정의가 필요하지 않음을 의미합니다.|  
|**default_datatype_mapping_id**|**int**|테이블 [MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md)에서 **map_id** 를 지정 하 여 기본 데이터 형식 매핑을 식별 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
