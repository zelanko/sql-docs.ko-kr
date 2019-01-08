---
title: sys.internal_partitions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a86c559adeeca787ac0e278eed5fb832b8c00bfd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537900"
---
# <a name="sysinternalpartitions-transact-sql"></a>sys.internal_partitions (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  디스크 기반 테이블의 columnstore 인덱스에 대 한 내부 데이터를 추적 하는 각 행 집합에 대해 하나의 행을 반환 합니다. 이러한 행 집합은 columnstore 인덱스의 내부 및 삭제 하는 추적 행, 행 그룹 매핑 및 델타 rowgroup을 저장 합니다. 각 테이블 파티션이;에 대해 각 데이터 추적 모든 테이블에는 하나 이상의 파티션이 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] columnstore 인덱스를 다시 작성 될 때마다 행 집합을 다시 만듭니다.   
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|이 파티션에 대 한 파티션 ID입니다. 데이터베이스 내에서 고유합니다.|  
|object_id|**int**|파티션이 포함 된 테이블에 대 한 개체 ID입니다.|  
|index_id|**int**|테이블에 정의 하 여 columnstore 인덱스의 인덱스 ID입니다.<br /><br /> 1 = 클러스터형된 columnstore 인덱스<br /><br /> 2 = 비클러스터형 columnstore 인덱스|  
|partition_number|**int**|파티션 번호입니다.<br /><br /> 1 = 분할된 된 테이블의 첫 번째 파티션 또는 분할 되지 않은 테이블의 단일 파티션에 합니다.<br /><br /> 2 = 두 번째 파티션 및 등입니다.|  
|internal_object_type|**tinyint**|Columnstore 인덱스에 대 한 내부 데이터를 추적 하는 행 집합 개체입니다.<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP-이 비트맵 인덱스는 columnstore에서 삭제 된 것으로 표시 되는 행을 추적 합니다. 비트맵은 파티션을 여러 rowgroup의 행을 가질 수 있으므로 모든 행 그룹입니다. 행이 columnstore에서 여전히 실제로 있는 공간을 차지 사용 중인 합니다.<br /><br /> COLUMN_STORE_DELTA_STORE-저장소 행 그룹, 열 형식 저장소에 없습니다 압축 된 rowgroup을 호출 합니다. 각 테이블 파티션이 0 개 이상의 deltastore 행 그룹에 있을 수 있습니다.<br /><br /> COLUMN_STORE_DELETE_BUFFER-업데이트 가능한 비클러스터형 columnstore 인덱스에 대 한 삭제를 유지 관리 합니다. 기본 rowstore 테이블에서 행을 삭제 하는 쿼리를 경우 삭제 버퍼 columnstore에서 삭제를 추적 합니다. 삭제 된 행 수가 1048576를 초과 하는 경우 병합 된 다시 삭제 비트맵 Tuple Mover 스레드가 백그라운드 또는 명시적 Reorganize 명령을 합니다.  지정 된 시점에서 비트맵을 삭제 하 고 삭제 버퍼의 합집합 모든 삭제 된 행을 나타냅니다.<br /><br /> COLUMN_STORE_MAPPING_INDEX-클러스터형된 columnstore 인덱스는 비클러스터형된 인덱스를 보조 하는 경우에 사용 합니다. 비클러스터형 인덱스 키의 올바른 행 그룹 및 columnstore의 행 ID에 매핑됩니다. 다른; 행 그룹으로 이동 하는 행에 대 한 키만 저장 이 델타 rowgroup을 columnstore로 압축 됩니다 시간과 병합 작업을 서로 다른 두 rowgroup의 행을 병합 하는 경우 발생 합니다.|  
|Row_group_id|**int**|Deltastore 행 그룹에 대 한 ID입니다. 각 테이블 파티션이 0 개 이상의 deltastore 행 그룹에 있을 수 있습니다.|  
|hobt_id|**bigint**|내부 행 집합 개체의 ID입니다. 이것이 내부 행 집합의 물리적 특성에 대 한 자세한 정보를 보려면 다른 Dmv와 조인 하는 데 적절 한 키입니다.|  
|rows|**bigint**|이 파티션에 있는 행의 대략적인 수입니다.|  
|data_compression|**tinyint**|상태 행 집합에 대 한 압축입니다.<br /><br /> 0 = 없음<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|각 파티션의 압축 상태입니다. rowstore 테이블의 가능한 값은 NONE, ROW 및 PAGE입니다. columnstore 테이블의 가능한 값은 COLUMNSTORE 및 COLUMNSTORE_ARCHIVE입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다시 새 columnstore 내부 인덱스를 만들거나 columnstore 인덱스를 다시 작성 될 때마다 만들어집니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>1. 모든 테이블에 대 한 내부 행 집합 보기  
 이 예제에서는 모든 테이블에 대 한 내부 columnstore 행 집합을 반환합니다. 특정 행 집합에 대 한 자세한 내용을 보려면 hobt_id를 이용할 수 있습니다.  
  
```  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
