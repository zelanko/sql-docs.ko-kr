---
title: sys. pdw_nodes_column_store_row_groups (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 17a4c925-d4b5-46ee-9cd6-044f714e6f0e
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b1cbdc63907933f173c7d32a2dde3151dd4db7af
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399871"
---
# <a name="syspdw_nodes_column_store_row_groups-transact-sql"></a>sys. pdw_nodes_column_store_row_groups (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  에서는 클러스터 된 columnstore 인덱스 정보를 사용 하 여 관리자가에서 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]시스템 관리를 결정 하도록 지원 합니다. **pdw_nodes_column_store_row_groups** 에는 실제로 저장 된 총 행 수 (삭제 된 것으로 표시 된 행 수 포함)와 삭제 된 것으로 표시 된 행 수에 대 한 열이 있습니다. **Pdw_nodes_column_store_row_groups** 를 사용 하 여 삭제 된 행의 비율이 높은 행 그룹을 확인 하 고 다시 작성 해야 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|기본 테이블의 ID입니다. 이는 계산 노드의 물리적 테이블 이며, 컨트롤 노드의 논리 테이블에 대 한 object_id이 아닙니다. 예를 들어 object_id은 sys. tables의 object_id와 일치 하지 않습니다.<br /><br /> Sys. tables에 조인 하려면 pdw_index_mappings를 사용 합니다.|  
|**index_id**|**int**|*Object_id* 테이블에 대 한 클러스터형 columnstore 인덱스의 ID입니다.|  
|**partition_number**|**int**|행 그룹 *row_group_id*를 보유 하는 테이블 파티션의 ID입니다. *Partition_number* 를 사용 하 여이 DMV를 sys 파티션에 조인할 수 있습니다.|  
|**row_group_id**|**int**|이 행 그룹의 ID입니다. 이 번호는 파티션 내에서 고유합니다.|  
|**dellta_store_hobt_id**|**bigint**|델타 행 그룹은 hobt_id, 행 그룹 유형이 델타가 아니면 NULL입니다. 델타 행 그룹이란 새 레코드를 수락하는 읽기/쓰기 행 그룹입니다. 델타 행 그룹은 **열림** 상태를 가집니다. 델타 행 그룹은 columnstore 형식으로 압축되지 않았고 여전히 rowstore 형식입니다.|  
|**state**|**tinyint**|state_description과 연결된 ID 번호입니다.<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED|  
|**state_desccription**|**nvarchar(60)**|행 그룹의 영구 상태 설명:<br /><br /> OPEN-새 레코드를 수락 하는 읽기/쓰기 행 그룹입니다. 열린 행 그룹은 columnstore 형식으로 압축되지 않았고 여전히 rowstore 형식입니다.<br /><br /> CLOSED-튜플 이동 프로세스가 아직 압축 하지 않은 채 채워져 있지만 아직 압축 하지 않은 행 그룹입니다.<br /><br /> 압축-채워지고 압축 된 행 그룹입니다.|  
|**total_rows**|**bigint**|행 그룹에 물리적으로 저장된 총 행 수입니다. 일부는 삭제되었을 수도 있지만 그대로 저장되어 있습니다. 행 그룹의 최대 행 수는 1,048,576개(16진수 FFFFF)입니다.|  
|**deleted_rows**|**bigint**|삭제 되도록 표시 된 행 그룹에 물리적으로 저장 된 행의 수입니다.<br /><br /> 델타 행 그룹의 경우 항상 0입니다.|  
|**size_in_bytes**|**int**|이 행 그룹에 있는 모든 페이지의 조합 된 크기 (바이트)입니다. 이 크기에는 메타 데이터 또는 공유 사전을 저장 하는 데 필요한 크기가 포함 되지 않습니다.|  
|**pdw_node_id**|**int**|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 노드의 고유 id입니다.|  
|**distribution_id**|**int**|분포의 고유 id입니다.|
  
## <a name="remarks"></a>설명  
 클러스터형 또는 비클러스터형 columnstore 인덱스가 있는 각 테이블에 대해 columnstore 행 그룹당 한 행을 표시합니다.  
  
 **Pdw_nodes_column_store_row_groups** 를 사용 하 여 행 그룹에 포함 되는 행 수와 행 그룹의 크기를 확인 합니다.  
  
 행 그룹에서 삭제된 행 수가 총 행 수 대비 큰 비율로 증가하면 테이블의 효율성이 저하됩니다. columnstore 인덱스를 다시 작성하여 테이블 크기를 줄이면 테이블을 읽는 데 필요한 디스크 I/O가 줄어듭니다. Columnstore 인덱스를 다시 작성 하려면 **ALTER index** 문의 **rebuild** 옵션을 사용 합니다.  
  
 업데이트 가능한 columnstore는 먼저 rowstore 형식으로 된 **OPEN** 행 그룹에 새 데이터를 삽입 하며,이를 델타 테이블이 라고도 합니다.  열린 행 그룹 가득 차면 상태가 **CLOSED**로 변경 됩니다. 폐쇄형 행 그룹은 튜플 이동 기에 의해 columnstore 형식으로 압축 되 고 상태는 **압축**됨으로 변경 됩니다.  Tuple mover는 정기적으로 켜지는 백그라운드 프로세스로, 닫힌 열 그룹 중 columnstore 행 그룹으로 압축할 수 있는 그룹이 있는지 확인합니다.  또한 Tuple mover는 모든 행이 삭제된 행 그룹에 대한 할당을 취소합니다. 할당 취소 된 행 그룹은 사용 **중지**됨으로 표시 됩니다. 튜플 이동 기를 즉시 실행 하려면 **ALTER INDEX** 문의 다시 **구성 옵션을 사용 합니다.**  
  
 다 채워진 columnstore 행 그룹은 압축되며, 새 행을 수락하지 않습니다. 압축된 그룹에서 행을 삭제하면 삭제된 것으로 표시되고 행 자체는 그대로 유지됩니다. 압축된 그룹을 업데이트할 때는 압축된 그룹의 삭제 또는 열린 그룹에 대한 삽입을 이용합니다.  
  
## <a name="permissions"></a>사용 권한  
 **VIEW SERVER STATE** 권한이 필요합니다.  
  
## <a name="examples-sssdw-and-sspdw"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 다른 시스템 테이블에 **pdw_nodes_column_store_row_groups** 테이블을 조인 하 여 특정 테이블에 대 한 정보를 반환 합니다. 계산된 `PercentFull` 열은 행 그룹의 효율성 예상치입니다. 단일 테이블에 대 한 정보를 찾으려면 WHERE 절 앞에 주석 하이픈을 제거 하 고 테이블 이름을 제공 합니다.  
  
```  
SELECT IndexMap.object_id,   
  object_name(IndexMap.object_id) AS LogicalTableName,   
  i.name AS LogicalIndexName, IndexMap.index_id, NI.type_desc,   
  IndexMap.physical_name AS PhyIndexNameFromIMap,   
  CSRowGroups.*,  
  100*(ISNULL(deleted_rows,0))/total_rows AS PercentDeletedRows   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.pdw_index_mappings AS IndexMap  
    ON i.object_id = IndexMap.object_id  
    AND i.index_id = IndexMap.index_id  
JOIN sys.pdw_nodes_indexes AS NI  
    ON IndexMap.physical_name = NI.name  
    AND IndexMap.index_id = NI.index_id  
JOIN sys.pdw_nodes_column_store_row_groups AS CSRowGroups  
    ON CSRowGroups.object_id = NI.object_id   
    AND CSRowGroups.pdw_node_id = NI.pdw_node_id  
AND CSRowGroups.index_id = NI.index_id      
--WHERE t.name = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, IndexMap.physical_name, pdw_node_id;  
```  

다음 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 예에서는 클러스터 된 열 저장소에 대 한 파티션당 행 수 뿐만 아니라 열려 있는 행, 닫힌 행 또는 압축 된 행 그룹의 행 수를 계산 합니다.  

```
SELECT
    s.name AS [Schema Name]
    ,t.name AS [Table Name]
    ,rg.partition_number AS [Partition Number]
    ,SUM(rg.total_rows) AS [Total Rows]
    ,SUM(CASE WHEN rg.State = 1 THEN rg.Total_rows Else 0 END) AS [Rows in OPEN Row Groups]
    ,SUM(CASE WHEN rg.State = 2 THEN rg.Total_Rows ELSE 0 END) AS [Rows in Closed Row Groups]
    ,SUM(CASE WHEN rg.State = 3 THEN rg.Total_Rows ELSE 0 END) AS [Rows in COMPRESSED Row Groups]
FROM sys.pdw_nodes_column_store_row_groups rg
JOIN sys.pdw_nodes_tables pt
ON rg.object_id = pt.object_id AND rg.pdw_node_id = pt.pdw_node_id AND pt.distribution_id = rg.distribution_id
JOIN sys.pdw_table_mappings tm
ON pt.name = tm.physical_name
INNER JOIN sys.tables t
ON tm.object_id = t.object_id
INNER JOIN sys.schemas s
ON t.schema_id = s.schema_id
GROUP BY s.name, t.name, rg.partition_number
ORDER BY 1, 2
```
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Transact-sql&#41;&#40;COLUMNSTORE 인덱스 만들기](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [pdw_nodes_column_store_segments &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [pdw_nodes_column_store_dictionaries &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  
