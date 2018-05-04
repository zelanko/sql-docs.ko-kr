---
title: sys.internal_partitions (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 525e98f4fe0a5096e7a75242174d84f38084e696
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysinternalpartitions-transact-sql"></a>sys.internal_partitions (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  디스크 기반 테이블에서 columnstore 인덱스에 대 한 내부 데이터를 추적 하는 각 행 집합에 대해 한 행을 반환 합니다. 이러한 행 집합은 columnstore 인덱스를 내부 및 추적 삭제 된 행, 행 그룹 매핑 및 델타 행 그룹을 저장 합니다. 각 테이블 파티션이;에 대 한 각에 대 한 데이터를 추적 모든 테이블에 파티션이 하나 이상 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] columnstore 인덱스를 다시 작성 될 때마다 행 집합을 다시 만듭니다.   
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|이 파티션에 대 한 파티션 ID입니다. 데이터베이스 내에서 고유합니다.|  
|object_id|**int**|파티션이 포함 된 테이블에 대 한 개체 ID입니다.|  
|index_id|**int**|테이블에 정의 된 columnstore 인덱스에 대 한 인덱스 ID입니다.<br /><br /> 1 = 클러스터형된 columnstore 인덱스<br /><br /> 2 = 비클러스터형 columnstore 인덱스|  
|partition_number|**int**|파티션 번호입니다.<br /><br /> 1 = 분할된 된 테이블의 첫 번째 파티션에 또는 분할 되지 않은 테이블의 단일 파티션에 합니다.<br /><br /> 2 = 두 번째 파티션 등에입니다.|  
|internal_object_type|**tinyint**|Columnstore 인덱스에 대 한 내부 데이터를 추적 하는 행 집합 개체입니다.<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP –이 비트맵 인덱스는 columnstore에서 삭제 된 것으로 표시 된 행을 추적 합니다. 비트맵은 모든 행 그룹에 대해 없으므로 파티션에 여러 행 그룹의 행을 사용할 수 있습니다. 행은 columnstore 여전히 물리적으로 존재 하 고 공간을 가져오는 표시 됩니다.<br /><br /> COLUMN_STORE_DELTA_STORE – 저장소 행 그룹, 하지 열 형식 저장소에 압축 된 rowgroup을 호출 합니다. 각 테이블 파티션이 0 개 이상의 deltastore rowgroup을 사용할 수 있습니다.<br /><br /> COLUMN_STORE_DELETE_BUFFER – 삭제 업데이트 가능한 비클러스터형 columnstore 인덱스를 유지 관리 합니다. 쿼리는 기본 rowstore 테이블에서 행을 삭제, 삭제 버퍼 columnstore에서 삭제를 추적 합니다. 삭제 된 행 수가 1048576를 초과 하는 경우 때 백그라운드 Tuple Mover 스레드 또는 명시적 Reorganize 명령을 삭제 비트맵에 다시 병합 됩니다.  특정 시점에 delete 비트맵과 삭제 버퍼의 합집합 모든 삭제 된 행을 나타냅니다.<br /><br /> COLUMN_STORE_MAPPING_INDEX – 클러스터형된 columnstore 인덱스에는 보조 비클러스터형된 인덱스에 경우에 사용 합니다. 비클러스터형 인덱스 키의 올바른 행 그룹 및 columnstore에서 행 ID에 매핑됩니다. 다른 열 그룹;으로 이동 하는 행에 대 한 키만 저장 델타 행 그룹을 columnstore로 압축 및 병합 작업은 두 개의 서로 다른 행 그룹에서 행을 병합 하는 경우 발생 합니다.|  
|Row_group_id|**int**|Deltastore 행 그룹에 대 한 ID입니다. 각 테이블 파티션이 0 개 이상의 deltastore rowgroup을 사용할 수 있습니다.|  
|hobt_id|**bigint**|내부 행 집합 개체의 ID입니다. 내부 행 집합의 물리적 특성에 대 한 자세한 정보를 보려면 다른 Dmv와 조인에 대 한 좋은 키입니다.|  
|rows|**bigint**|이 파티션에 있는 행의 대략적인 수입니다.|  
|data_compression|**tinyint**|행 집합에 대 한 압축 상태:<br /><br /> 0 = 없음<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|각 파티션에 대해 압축의 상태입니다. rowstore 테이블의 가능한 값은 NONE, ROW 및 PAGE입니다. columnstore 테이블의 가능한 값은 COLUMNSTORE 및 COLUMNSTORE_ARCHIVE입니다.|  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만들거나 columnstore 인덱스를 다시 작성 될 때마다 새 columnstore 내부 인덱스를 다시 만듭니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>1. 테이블에 대 한 내부 행 집합의 모든 보기  
 이 예에서는 모든 테이블에 대 한 내부 columnstore 행 집합을 반환합니다. 또한 특정 행 집합에 대 한 자세한 내용을 보려면 hobt_id를 사용할 수 있습니다.  
  
```  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
