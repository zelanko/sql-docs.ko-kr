---
title: sys.internal_tables (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.internal_tables
- internal_tables
- sys.internal_tables_TSQL
- internal_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- internal tables
- sys.internal_tables catalog view
ms.assetid: a5821c70-f150-4676-8476-3a31f7403dca
caps.latest.revision: 52
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ef44b01d4c0a5ca20d728c37240a2feb9a2a046
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028661"
---
# <a name="sysinternaltables-transact-sql"></a>sys.internal_tables(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  내부 테이블인 각 개체당 한 개의 행을 반환합니다. 내부 테이블은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 다양한 기능을 지원하기 위해 자동으로 생성됩니다. 예를 들어 기본 XML 인덱스를 만들면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 자동으로 내부 테이블을 만들어 단편 형태의 XML 문서 데이터를 저장합니다. 내부 테이블에 표시 된 **sys** 모든 데이터베이스의 스키마, 고유한 시스템 생성 이름을 예를 들어, 해당 기능을 나타내는 있고 **xml_index_nodes_2021582240_32001** 또는  **queue_messages_1977058079**  
  
 내부 테이블에는 사용자가 액세스할 수 있는 데이터가 포함되지 않으며 스키마가 고정되어 변경할 수 없습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서는 내부 테이블 이름을 참조할 수 없습니다. 예를 들어 선택과 같은 문은 실행할 수 없습니다 \* FROM  *\<sys.internal_table_name >* 합니다. 그러나 카탈로그 뷰를 쿼리하여 내부 테이블의 메타데이터를 볼 수 있습니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Sys.objects에서 상속 된 열 >**||이 뷰가 상속 하는 열 목록은 참조 하세요 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.|  
|**internal_type**|**tinyint**|내부 테이블의 유형입니다.<br /><br /> 201 = **queue_messages**<br /><br /> 202 = **xml_index_nodes**<br /><br /> 203 = **fulltext_catalog_freelist**<br /><br /> 205 = **query_notification**<br /><br /> 206 = **service_broker_map**<br /><br /> 207 = **extended_indexes** (예: 공간 인덱스)<br /><br /> 208 = **filestream_tombstone**<br /><br /> 209 = **change_tracking**<br /><br /> 210 = **tracked_committed_transactions**<br /><br /> 236 = **selective_xml_index_node_table**|  
|**internal_type_desc**|**nvarchar(60)**|내부 테이블의 유형에 대한 설명입니다.<br /><br /> QUEUE_MESSAGES<br /><br /> XML_INDEX_NODES<br /><br /> FULLTEXT_CATALOG_FREELIST<br /><br /> FULLTEXT_CATALOG_MAP<br /><br /> QUERY_NOTIFICATION<br /><br /> SERVICE_BROKER_MAP<br /><br /> EXTENDED_INDEXES<br /><br /> FILESTREAM_TOMBSTONE<br /><br /> CHANGE_TRACKING<br /><br /> TRACKED_COMMITTED_TRANSACTIONS<br /><br /> SELECTIVE_XML_INDEX_NODE_TABLE|  
|**parent_id**|**int**|부모의 ID입니다(스키마 범위 여부에 관계없이). 부모가 없는 경우 0입니다.<br /><br /> **queue_messages** = **object_id** 큐<br /><br /> **xml_index_nodes** = **object_id** xml 인덱스<br /><br /> **fulltext_catalog_freelist** = **fulltext_catalog_id** 전체 텍스트 카탈로그의<br /><br /> **fulltext_index_map** = **object_id** 전체 텍스트 인덱스<br /><br /> **query_notification**, 또는 **service_broker_map** = 0<br /><br /> **extended_indexes** = **object_id** 의 공간 인덱스와 같은 확장된 인덱스<br /><br /> **object_id** = 테이블에 대 한 추적이 설정 된 테이블의 **change_tracking**|  
|**parent_minor_id**|**int**|부모의 보조 ID입니다.<br /><br /> **xml_index_nodes** = **index_id** XML 인덱스<br /><br /> **extended_indexes** = **index_id** 의 공간 인덱스와 같은 확장된 인덱스<br /><br /> 0 = **queue_messages**, **fulltext_catalog_freelist**를 **fulltext_index_map**하십시오 **query_notification**,  **service_broker_map**, 또는 **change_tracking**|  
|**lob_data_space_id**|**int**|0이 아닌 값은 이 테이블의 LOB(Large Object) 데이터를 보관하는 데이터 공간(파일 그룹 또는 파티션 구성표)의 ID입니다.|  
|**filestream_data_space_id**|**int**|나중에 사용하도록 예약되어 있습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 내부 테이블은 부모 엔터티와 동일한 파일 그룹에 저장됩니다. 아래의 예 6에 표시된 카탈로그 쿼리를 사용하여 내부 테이블에서 행 내부, 행 외부 및 LOB(Large Object) 데이터에 사용되는 페이지 수를 반환할 수 있습니다.  
  
 사용할 수는 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 시스템 프로시저를 내부 테이블에 대 한 공간 사용 현황 데이터를 반환 합니다. **sp_spaceused** 다음과 같은 방법으로 내부 테이블 공간을 보고 합니다.  
  
-   큐 이름을 지정하면 큐와 연결된 기본 내부 테이블을 참조하여 해당 저장소 사용을 보고합니다.  
  
-   XML 인덱스, 공간 인덱스 및 전체 텍스트 인덱스의 내부 테이블에서 사용 되는 페이지에 포함 되는 **index_size** 열입니다. XML 인덱스, 공간 인덱스 및 해당 개체에 대 한 전체 텍스트 인덱스에 대 한 페이지를 열에 포함 된 테이블 또는 인덱싱된 뷰 이름을 지정 하면 **예약** 하 고 **index_size**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 카탈로그 뷰를 사용하여 내부 테이블 메타데이터를 쿼리하는 방법을 보여 줍니다.  
  
### <a name="a-show-internal-tables-that-inherit-columns-from-the-sysobjects-catalog-view"></a>1. sys.objects 카탈로그 뷰에서 열을 상속하는 내부 테이블 표시  
  
```  
SELECT * FROM sys.objects WHERE type = 'IT';  
```  
  
### <a name="b-return-all-internal-table-metadata-including-that-which-is-inherited-from-sysobjects"></a>2. 모든 내부 테이블 메타데이터 반환(sys.objects에서 상속된 메타데이터 포함)  
  
```  
SELECT * FROM sys.internal_tables;  
```  
  
### <a name="c-return-internal-table-columns-and-column-data-types"></a>3. 내부 테이블 열과 열 데이터 형식 반환  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,typ.name AS column_data_type   
    ,col.*  
FROM sys.internal_tables AS itab  
JOIN sys.columns AS col ON itab.object_id = col.object_id  
JOIN sys.types AS typ ON typ.user_type_id = col.user_type_id  
ORDER BY itab.name, col.column_id;  
```  
  
### <a name="d-return-internal-table-indexes"></a>4. 내부 테이블 인덱스 반환  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    , itab.name AS internal_table_name  
    , idx.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx ON itab.object_id = idx.object_id  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="e-return-internal-table-statistics"></a>5. 내부 테이블 통계 반환  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    , s.*  
FROM sys.internal_tables AS itab  
JOIN sys.stats AS s ON itab.object_id = s.object_id  
ORDER BY itab.name, s.stats_id;  
```  
  
### <a name="f-return-internal-table-partition-and-allocation-unit-information"></a>6. 내부 테이블 파티션 및 할당 단위 정보 반환  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,idx.name AS heap_or_index_name  
    ,p.*  
    ,au.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx  
--     JOIN to the heap or the clustered index  
    ON itab.object_id = idx.object_id AND idx.index_id IN (0,1)  
JOIN   sys.partitions AS p   
    ON p.object_id = idx.object_id AND p.index_id = idx.index_id  
JOIN   sys.allocation_units AS au  
--     IN_ROW_DATA (type 1) and ROW_OVERFLOW_DATA (type 3) => JOIN to partition's Hobt  
--     else LOB_DATA (type 2) => JOIN to the partition ID itself.  
ON au.container_id =    
    CASE au.type   
        WHEN 2 THEN p.partition_id   
        ELSE p.hobt_id   
    END  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="g-return-internal-table-metadata-for-xml-indexes"></a>7. XML 인덱스에 대한 내부 테이블 메타데이터 반환  
  
```  
SELECT t.name AS parent_table  
    ,t.object_id AS parent_table_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
    ,xi.name AS primary_XML_index_name  
    ,xi.index_id as primary_XML_index_id  
FROM sys.internal_tables AS it  
JOIN sys.tables AS t   
    ON it.parent_id = t.object_id  
JOIN sys.xml_indexes AS xi   
    ON it.parent_id = xi.object_id  
    AND it.parent_minor_id  = xi.index_id  
WHERE it.internal_type_desc = 'XML_INDEX_NODES';  
GO  
```  
  
### <a name="h-return-internal-table-metadata-for-service-broker-queues"></a>8. Service Broker 큐에 대한 내부 테이블 메타데이터 반환  
  
```  
SELECT q.name AS queue_name  
    ,q.object_id AS queue_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.service_queues  AS  q ON it.parent_id = q.object_id  
WHERE it.internal_type_desc = 'QUEUE_MESSAGES';  
GO  
```  
  
## <a name="i-return-internal-table-metadata-for-all-service-broker-services"></a>9. 모든 Service Broker 서비스에 대한 내부 테이블 메타데이터 반환  
  
```  
SELECT *   
FROM tempdb.sys.internal_tables   
WHERE internal_type_desc = 'SERVICE_BROKER_MAP';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
