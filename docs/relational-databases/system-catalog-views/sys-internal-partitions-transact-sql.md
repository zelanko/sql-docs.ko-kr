---
title: sys. internal_partitions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c4f0ff3a5cc18845bc2fcc2bec682c6bd8e2db4e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724663"
---
# <a name="sysinternal_partitions-transact-sql"></a>sys. internal_partitions (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asdw.md)]

  디스크 기반 테이블의 columnstore 인덱스에 대 한 내부 데이터를 추적 하는 각 행 집합에 대해 하나의 행을 반환 합니다. 이러한 행 집합은 columnstore 인덱스에 대 한 내부 이며 삭제 된 행, 행 그룹 매핑 및 델타 저장소 행 그룹을 추적 합니다. 각 테이블 파티션에 대 한 데이터를 추적 합니다. 모든 테이블에는 하나 이상의 파티션이 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]columnstore 인덱스를 다시 작성할 때마다 행 집합을 다시 만듭니다.   
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|이 파티션의 파티션 ID입니다. 데이터베이스 내에서 고유합니다.|  
|object_id|**int**|파티션을 포함 하는 테이블의 개체 ID입니다.|  
|index_id|**int**|테이블에 정의 된 columnstore 인덱스의 인덱스 ID입니다.<br /><br /> 1 = 클러스터형 columnstore 인덱스<br /><br /> 2 = 비클러스터형 columnstore 인덱스|  
|partition_number|**int**|파티션 번호입니다.<br /><br /> 1 = 분할 된 테이블의 첫 번째 파티션 또는 분할 되지 않은 테이블의 단일 파티션입니다.<br /><br /> 2 = 두 번째 파티션 등|  
|internal_object_type|**tinyint**|Columnstore 인덱스에 대 한 내부 데이터를 추적 하는 행 집합 개체입니다.<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP-이 비트맵 인덱스는 columnstore에서 삭제 된 것으로 표시 된 행을 추적 합니다. 파티션은 여러 행 그룹에 행을 포함할 수 있기 때문에 모든 행 그룹에 대 한 비트맵입니다. 행은 여전히 물리적으로 존재 하며 columnstore에서 공간을 차지 합니다.<br /><br /> COLUMN_STORE_DELTA_STORE-칼럼 형식 저장소로 압축 되지 않은 행 그룹 이라는 행 그룹을 저장 합니다. 각 테이블 파티션에는 0 개 이상의 deltastore 행 그룹이 있을 수 있습니다.<br /><br /> COLUMN_STORE_DELETE_BUFFER-업데이트 가능한 비클러스터형 columnstore 인덱스에 대 한 삭제를 유지 관리 합니다. 쿼리가 기본 rowstore 테이블에서 행을 삭제 하면 삭제 버퍼는 columnstore에서 삭제를 추적 합니다. 삭제 된 행 수가 1048576을 초과 하면 백그라운드 튜플 이동 기 스레드나 명시적 다시 구성 명령에 의해 삭제 된 행이 다시 병합 됩니다.  지정 된 시점에서 delete 비트맵과 삭제 버퍼의 합집합은 모든 삭제 된 행을 나타냅니다.<br /><br /> COLUMN_STORE_MAPPING_INDEX-클러스터형 columnstore 인덱스에 보조 비클러스터형 인덱스가 있는 경우에만 사용 됩니다. 이렇게 하면 비클러스터형 인덱스 키가 columnstore의 올바른 행 그룹 및 행 ID에 매핑됩니다. 다른 행 그룹 이동 하는 행의 키만 저장 합니다. 이는 델타 행 그룹이 columnstore로 압축 되 고 병합 작업이 서로 다른 두 행 그룹의 행을 병합 하는 경우에 발생 합니다.|  
|Row_group_id|**int**|Deltastore 행 그룹의 ID입니다. 각 테이블 파티션에는 0 개 이상의 deltastore 행 그룹이 있을 수 있습니다.|  
|hobt_id|**bigint**|내부 행 집합 개체의 ID입니다 (HoBT). 이 키는 내부 행 집합의 물리적 특성에 대 한 자세한 정보를 얻기 위해 다른 Dmv와 조인 하는 데 유용 합니다.|  
|rows|**bigint**|이 파티션에 있는 행의 대략적인 수입니다.|  
|data_compression|**tinyint**|행 집합에 대 한 압축 상태:<br /><br /> 0 = 없음<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|각 파티션에 대 한 압축 상태입니다. rowstore 테이블의 가능한 값은 NONE, ROW 및 PAGE입니다. columnstore 테이블의 가능한 값은 COLUMNSTORE 및 COLUMNSTORE_ARCHIVE입니다.|  
|optimize_for_sequential_key|**bit**|1 = 파티션에서 마지막 페이지 삽입 최적화를 사용 하도록 설정 했습니다.<br><br>0 = 기본값 파티션에서 마지막 페이지 삽입 최적화를 사용 하지 않도록 설정 했습니다.|
  
## <a name="permissions"></a>사용 권한  
 `public` 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]columnstore 인덱스를 만들거나 다시 작성할 때마다 새 columnstore 내부 인덱스를 다시 만듭니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. 테이블에 대 한 내부 행 집합 모두 보기  
 이 예에서는 테이블에 대 한 모든 내부 columnstore 행 집합을 반환 합니다. Hobt_id를 사용 하 여 특정 행 집합에 대 한 자세한 정보를 찾을 수도 있습니다.  
  
```sql  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
