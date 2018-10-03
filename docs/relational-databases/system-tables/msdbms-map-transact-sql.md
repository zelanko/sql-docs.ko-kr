---
title: MSdbms_map (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: a718cd7130e13ed5e9afddadddf7c1b5e3ee0ccf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832961"
---
# <a name="msdbmsmap-transact-sql"></a>MSdbms_map(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSdbms_map** 테이블 원본 및 대상 DBMS 쌍에 대 한 기본 대상 데이터 형식 정보에 대 한 링크 뿐만 아니라 원본 데이터 형식 정보를 포함 합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스 및 다른 유형의 게시에 사용 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**map_id**|**int**|데이터 형식 매핑을 고유하게 식별합니다.|  
|**src_dbms_id**|**int**|지정 하 여 원본 DBMS를 식별 합니다. 해당 **dbms_id** 에 [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) 테이블입니다.|  
|**dest_dbms_id**|**int**|지정 하 여 대상 DBMS를 식별 합니다. 해당 **dbms_id** 에 [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) 테이블입니다.|  
|**src_datatype_id**|**int**|식별 된 **datatype_id** 에서 [MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md) 원본 데이터 형식에 대 한 테이블입니다.|  
|**src_len_min**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최소 길이입니다. NULL 값은 길이가 사용되지 않음을 나타냅니다.|  
|**src_len_max**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최대 길이입니다. NULL 값은 길이가 사용되지 않음을 나타냅니다.|  
|**src_prec_min**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최소 전체 자릿수입니다. NULL 값은 전체 자릿수가 사용되지 않음을 나타냅니다.|  
|**src_prec_max**|**bigint**|원본 DBMS에서 해당 데이터 형식의 최대 전체 자릿수입니다. NULL 값은 전체 자릿수가 사용되지 않음을 나타냅니다.|  
|**src_scale_min**|**int**|원본 DBMS에서 해당 데이터 형식의 최소 소수 자릿수입니다. NULL 값은 소수 자릿수가 사용되지 않음을 나타냅니다.|  
|**src_scale_max**|**int**|원본 DBMS에서 해당 데이터 형식의 최대 소수 자릿수입니다. NULL 값은 소수 자릿수가 사용되지 않음을 나타냅니다.|  
|**src_nullable**|**bit**|매핑의 대상 열이 NULL 값을 허용하는지 여부를 나타냅니다. 여기서 NULL 값은 이 정의가 필요하지 않음을 의미합니다.|  
|**default_datatype_mapping_id**|**int**|지정 하 여 기본 데이터 형식 매핑을 식별 해당 **map_id** 표에 [MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md)합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle 게시자에 대 한 데이터 형식 매핑 지정](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
