---
title: DROP INDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_INDEX_TSQL
- DROP INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- nonclustered indexes [SQL Server], removing
- MAXDOP index option, DROP INDEX statement
- index removal [SQL Server]
- spatial indexes [SQL Server], dropping
- removing indexes
- deleting indexes
- dropping indexes
- MOVE TO clause
- clustered indexes, removing
- indexes [SQL Server], dropping
- filtered indexes [SQL Server], dropping
- ONLINE option
- indexes [SQL Server], moving
- XML indexes [SQL Server], dropping
- DROP INDEX statement
ms.assetid: 2b1464c8-934c-405f-8ef7-2949346b5372
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3e151639595e181fb434e5144daa64cc84128892
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132453"
---
# <a name="drop-index-transact-sql"></a>DROP INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스에서 하나 이상의 관계형 인덱스, 공간 인덱스, 필터링된 인덱스 또는 XML 인덱스를 제거합니다. 클러스터형 인덱스를 삭제하고 MOVE TO 옵션을 지정하여 결과 테이블을 단일 트랜잭션으로 다른 파일 그룹이나 파티션 구성표로 이동할 수 있습니다.  
  
 DROP INDEX 문은 PRIMARY KEY 또는 UNIQUE 제약 조건을 정의함으로써 생성된 인덱스에는 적용되지 않습니다. 제약 조건과 해당 인덱스를 제거하려면 DROP CONSTRAINT 절과 함께 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)을 사용합니다.  
  
> [!IMPORTANT]
>  `<drop_backward_compatible_index>`에 정의된 구문은 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서 제거될 예정입니다. 새 개발 작업에서는 이 구문을 사용하지 말고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. 대신 `<drop_relational_or_xml_index>`에 지정된 구문을 사용하세요. XML 인덱스는 이전 버전과의 호환을 위한 구문을 사용하여 삭제할 수 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server (All options except filegroup and filestream apply to Azure SQL Database.)  
  
DROP INDEX [ IF EXISTS ]   
{ <drop_relational_or_xml_or_spatial_index> [ ,...n ]   
| <drop_backward_compatible_index> [ ,...n ]  
}  
  
<drop_relational_or_xml_or_spatial_index> ::=  
    index_name ON <object>   
    [ WITH ( <drop_clustered_index_option> [ ,...n ] ) ]  
  
<drop_backward_compatible_index> ::=  
    [ owner_name. ] table_or_view_name.index_name  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<drop_clustered_index_option> ::=  
{  
    MAXDOP = max_degree_of_parallelism  
  | ONLINE = { ON | OFF }  
  | MOVE TO { partition_scheme_name ( column_name )   
            | filegroup_name  
            | "default"   
            }  
  [ FILESTREAM_ON { partition_scheme_name   
            | filestream_filegroup_name   
            | "default" } ]  
}  
```  
  
```  
-- Syntax for Azure SQL Database  
  
DROP INDEX  
{ <drop_relational_or_xml_or_spatial_index> [ ,...n ]   
}  
  
<drop_relational_or_xml_or_spatial_index> ::=   
    index_name ON <object>  
  
<object> ::=   
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP INDEX index_name ON [ database_name . [schema_name ] . | schema_name . ] table_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 이미 있는 경우에만 인덱스를 조건부로 삭제합니다.  
  
 *index_name*  
 삭제할 인덱스의 이름입니다.  
  
 *database_name*  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이나 뷰가 속한 스키마의 이름입니다.  
  
 *table_or_view_name*  
 인덱스와 관련된 테이블이나 뷰의 이름입니다. 공간 인덱스는 테이블에서만 지원됩니다.  
  
 개체에 대한 인덱스 보고서를 표시하려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰를 사용합니다.  
  
 database_name이 현재 데이터베이스이거나 database_name이 tempdb이고 object_name이 #으로 시작하는 경우 Microsoft Azure SQL Database는 세 부분으로 구성된 이름 형식 database_name.[schema_name].object_name을 지원합니다.  
  
 \<drop_clustered_index_option>  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 클러스터형 인덱스 옵션을 제어합니다. 다른 인덱스 유형에는 이 옵션을 사용할 수 없습니다.  
  
 MAXDOP = *max_degree_of_parallelism*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)](성능 수준 P2 및 P3만 해당)  
  
 인덱스 작업 기간 동안 **max degree of parallelism** 구성 옵션을 재정의합니다. 자세한 내용은 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
> [!IMPORTANT]  
>  공간 인덱스 또는 XML 인덱스에서는 MAXDOP를 사용할 수 없습니다.  
  
 *max_degree_of_parallelism*은 다음 중 하나일 수 있습니다.  
  
 1  
 병렬 계획이 생성되지 않습니다.  
  
 \>1  
 병렬 인덱스 작업에 사용되는 최대 프로세서 수를 지정된 값으로 제한합니다.  
  
 0(기본값)  
 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]  
>  병렬 인덱스 작업은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ONLINE = ON | **OFF**  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]까지  
  
 인덱스 작업 중 쿼리 및 데이터 수정에 기본 테이블과 관련 인덱스를 사용할 수 있는지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 장기 테이블 잠금이 유지되지 않습니다. 따라서 기본 테이블에 대한 쿼리나 업데이트를 계속할 수 있습니다.  
  
 OFF  
 테이블 잠금이 적용되어 인덱스 작업 중에 테이블을 사용할 수 없습니다.  
  
 ONLINE 옵션은 클러스터형 인덱스를 삭제할 때만 지정할 수 있습니다. 자세한 내용은 주의 섹션을 참조하세요.  
  
> [!NOTE]  
>  온라인 인덱스 작업은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 MOVE TO { _partition\_scheme\_name_**(**_column\_name_**)** | _filegroup\_name_ | **"** default **"**  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에서는 파일 그룹 이름으로 "default"를 지원합니다.  
  
 현재 클러스터형 인덱스의 리프 수준에 있는 데이터 행을 옮길 위치를 지정합니다. 데이터는 힙 형태로 새 위치로 옮겨집니다. 파티션 구성표 또는 파일 그룹을 새 위치로 지정할 수도 있지만 이미 존재하는 파티션 구성표 또는 파일 그룹이어야 합니다. 인덱싱된 뷰나 비클러스터형 인덱스에는 MOVE TO를 사용할 수 없습니다. 파티션 구성표 또는 파일 그룹을 지정하지 않으면 결과 테이블은 클러스터형 인덱스와 동일한 파티션 구성표 또는 파일 그룹에 위치합니다.  
  
 MOVE TO를 사용하여 클러스터형 인덱스를 삭제하면 기본 테이블의 모든 비클러스터형 인덱스는 다시 작성되지만 원본 파일 그룹 또는 파티션 구성표에는 그대로 남습니다. 기본 테이블을 다른 파일 그룹 또는 파티션 구성표로 옮기면 비클러스터형 인덱스는 기본 테이블의 새 위치(힙)에 일치하게 옮겨지지 않습니다. 따라서 비클러스터형 인덱스가 전에 클러스터형 인덱스에 맞추어 정렬되었다 하더라도 더 이상 힙에 정렬되지는 않습니다. 분할된 인덱스 정렬에 대한 자세한 내용은 [분할된 테이블 및 인덱스](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하세요.  
  
 _partition_scheme_name_ **(** _column_name_ **)**  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
 파티션 구성표를 결과 테이블의 위치로 지정합니다. 파티션 구성표는 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) 또는 [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md) 문을 실행하여 이미 생성되어 있어야 합니다. 지정된 위치가 없고 테이블이 분할되어 있다면 해당 테이블은 기존 클러스터형 인덱스와 동일한 파티션에 포함됩니다.  
  
 구성표의 열 이름으로 인덱스 정의의 열만 사용할 필요는 없으며 기본 테이블의 모든 열을 지정할 수 있습니다.  
  
 *filegroup_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 파일 그룹을 결과 테이블의 위치로 지정합니다. 지정된 위치가 없고 테이블이 분할되지 않으면 결과 테이블은 클러스터형 인덱스와 동일한 파일 그룹에 포함됩니다. 파일 그룹은 이미 존재해야 합니다.  
  
 **"** default **"**  
 결과 테이블의 기본 위치를 지정합니다.  
  
> [!NOTE]
>  이 컨텍스트에서 default는 키워드가 아니라 기본 파일 그룹에 대한 식별자이므로 MOVE TO **"** default **"** 또는 MOVE TO **[** default **]** 와 같이 구분되어야 합니다. **"** default **"** 를 지정하면 현재 세션에 대한 QUOTED_IDENTIFIER 옵션이 ON으로 설정되어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
 FILESTREAM_ON { *partition_scheme_name* | *filestream_filegroup_name* | **"** default **"** }  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 현재 클러스터형 인덱스의 리프 수준에 있는 FILESTREAM 테이블을 옮길 위치를 지정합니다. 데이터는 힙 형태로 새 위치로 옮겨집니다. 파티션 구성표 또는 파일 그룹을 새 위치로 지정할 수도 있지만 이미 존재하는 파티션 구성표 또는 파일 그룹이어야 합니다. FILESTREAM ON은 인덱싱된 뷰나 비클러스터형 인덱스에는 사용할 수 없습니다. 파티션 구성표를 지정하지 않으면 데이터가 클러스터형 인덱스에 대해 정의된 것과 동일한 파티션 구성표에 위치하게 됩니다.  
  
 *partition_scheme_name*  
 FILESTREAM 데이터의 파티션 구성표를 지정합니다. 파티션 구성표는 [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) 또는 [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md) 문을 실행하여 이미 생성되어 있어야 합니다. 지정된 위치가 없고 테이블이 분할되어 있다면 해당 테이블은 기존 클러스터형 인덱스와 동일한 파티션에 포함됩니다.  
  
 MOVE TO에 대한 파티션 구성표를 지정하는 경우 FILESTREAM ON과 동일한 파티션 구성표를 사용해야 합니다.  
  
 *filestream_filegroup_name*  
 FILESTREAM 데이터의 FILESTREAM 파일 그룹을 지정합니다. 지정된 위치가 없고 테이블이 분할되지 않으면 데이터는 기본 FILESTREAM 파일 그룹에 포함됩니다.  
  
 **"** default **"**  
 FILESTREAM 데이터의 기본 위치를 지정합니다.  
  
> [!NOTE]
>  이 컨텍스트에서 default는 키워드가 아니라 기본 파일 그룹에 대한 식별자이므로 MOVE TO **"** default **"** 또는 MOVE TO **[** default **]** 와 같이 구분되어야 합니다. "default"를 지정하면 현재 세션의 QUOTED_IDENTIFIER 옵션이 ON이어야 합니다. 이 값은 기본 설정입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 비클러스터형 인덱스를 삭제하면 인덱스 정의가 메타데이터에서 제거되고 인덱스 데이터 페이지(B-트리)가 데이터베이스 파일에서 제거됩니다. 클러스터형 인덱스가 삭제되면 인덱스 정의가 메타데이터에서 제거되고 클러스터형 인덱스의 리프 수준에 저장된 데이터 행은 정렬되지 않은 결과 테이블인 힙에 저장됩니다. 인덱스가 이전에 점유하고 있던 모든 공간은 반환됩니다. 반환된 공간은 다른 데이터베이스 개체에서 사용할 수 있습니다.  
  
 인덱스가 있는 파일 그룹이 오프라인이거나 읽기 전용으로 설정되어 있으면 파일 그룹에서 인덱스를 삭제할 수 없습니다.  
  
 인덱싱된 뷰의 클러스터형 인덱스를 삭제하면 해당 뷰의 모든 비클러스터형 인덱스와 자동 생성된 통계가 자동으로 삭제됩니다. 수동으로 생성된 통계는 삭제되지 않습니다.  
  
 _table\_or\_view\_name_**.**_index\_name_ 구문은 이전 버전과의 호환성을 위해 유지 관리됩니다. XML 인덱스 또는 공간 인덱스는 이전 버전과 호환되는 구문을 사용하여 삭제할 수 없습니다.  
  
 128개 이상의 익스텐트를 가진 인덱스가 삭제되면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 트랜잭션이 커밋될 때까지 실제 페이지 할당 취소 및 관련 잠금을 연기합니다.  
  
 인덱스를 다시 구성 또는 다시 작성하기 위해 인덱스를 삭제하고 다시 만드는 경우도 있습니다. 예를 들면 새 채우기 비율 값을 적용하거나 대량 로드 후 데이터를 다시 구성하기 위해서입니다. 이렇게 하려면 [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)를 사용하는 것이 더 효율적이며 특히 클러스터형 인덱스의 경우 매우 효율적입니다. ALTER INDEX REBUILD는 비클러스터형 인덱스를 다시 작성하는 데 따른 오버헤드를 막기 위한 최적화 기능을 갖고 있습니다.  
  
## <a name="using-options-with-drop-index"></a>DROP INDEX에 옵션 사용  
 클러스터형 인덱스를 삭제할 때 MAXDOP, ONLINE 및 MOVE TO와 같은 인덱스 옵션을 설정할 수 있습니다.  
  
 한 번의 트랜잭션으로 클러스터형 인덱스를 삭제하고 결과 테이블을 다른 파일 그룹 또는 파티션 구성표로 옮기려면 MOVE TO 옵션을 사용합니다.  
  
 ONLINE = ON으로 지정하면 기본 데이터 및 연결된 비클러스터형 인덱스에 대한 쿼리 및 수정 사항은 DROP INDEX 트랜잭션에 의해 차단되지 않습니다. 클러스터형 인덱스는 한 번에 한 개씩만 온라인으로 삭제할 수 있습니다. ONLINE 옵션에 대한 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
 뷰에서 인덱스가 비활성화되어 있거나 리프 수준 데이터 행에 **text**, **ntext**, **image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)** 또는 **xml** 열이 포함되어 있으면 클러스터형 인덱스를 온라인으로 삭제할 수 없습니다.  
  
 ONLINE = ON 및 MOVE TO 옵션을 사용하려면 임시 디스크 공간이 더 필요합니다.  
  
 인덱스가 삭제된 후 결과 힙은 **sys.indexes** 카탈로그 뷰에 표시되며 **name** 열에 NULL이 포함됩니다. 테이블 이름을 보려면 **object_id**에서 **sys.indexes**와 **sys.tables**을 조인합니다. 쿼리 예는 예 1을 참조하세요.  
  
 다중 프로세서 컴퓨터에서 [!INCLUDE[ssEnterpriseEd2005](../../includes/ssenterpriseed2005-md.md)] 이상을 실행하는 경우 DROP INDEX는 다른 쿼리와 마찬가지로 클러스터형 인덱스 삭제와 관련된 검색 및 정렬 작업을 수행하기 위해 더 많은 프로세서를 사용할 수 있습니다. MAXDOP 인덱스 옵션을 지정하여 DROP INDEX 문을 실행하기 위해 사용되는 프로세서 개수를 수동으로 구성할 수 있습니다. 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
 클러스터형 인덱스를 삭제한 경우 파티션 구성표를 수정하지 않으면 해당 힙 파티션에서 데이터 압축 설정이 유지됩니다. 파티션 구성표가 변경되면 모든 파티션이 압축되지 않은 상태(DATA_COMPRESSION = NONE)로 다시 작성됩니다. 클러스터형 인덱스를 삭제하고 파티션 구성표를 변경하려면 다음 두 단계를 수행해야 합니다.  
  
1.  클러스터형 인덱스를 삭제합니다.  
  
2.  압축 옵션을 지정하는 ALTER TABLE ... REBUILD ... 옵션을 사용하여 테이블을 수정합니다.  
  
클러스터형 인덱스가 OFFLINE으로 삭제되면 클러스터형 인덱스의 상위 수준만 제거되므로 작업이 상당히 빠르게 수행됩니다. 클러스터형 인덱스를 ONLINE으로 삭제하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 1단계와 2단계에서 한 번씩, 총 두 번에 걸쳐 힙을 다시 작성합니다. 데이터 압축에 대한 자세한 내용은 [데이터 압축](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
## <a name="xml-indexes"></a>XML 인덱스  
 XML 인덱스를 삭제할 때는 옵션을 지정할 수 없습니다. 또한 _table\_or\_view\_name_**.**_index\_name_ 구문을 사용할 수 없습니다. 기본 XML 인덱스가 삭제되면 연결된 모든 보조 XML 인덱스는 자동으로 삭제됩니다. 자세한 내용은 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)를 참조하세요.  
  
## <a name="spatial-indexes"></a>공간 인덱스  
 공간 인덱스는 테이블에서만 지원됩니다. 공간 인덱스를 삭제하는 경우 옵션을 지정하거나 **.**_index\_name_을 사용할 수 없습니다. 올바른 구문은 다음과 같습니다.  
  
 DROP INDEX *spatial_index_name* ON *spatial_table_name*;  
  
 공간 인덱스에 대한 자세한 내용은 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)를 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 DROP INDEX를 실행하려면 최소한 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할에 부여됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-an-index"></a>1. 인덱스 삭제  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `ProductVendor` 테이블의 `IX_ProductVendor_VendorID` 인덱스를 삭제합니다.  
  
```  
DROP INDEX IX_ProductVendor_BusinessEntityID   
    ON Purchasing.ProductVendor;  
GO  
```  
  
### <a name="b-dropping-multiple-indexes"></a>2. 여러 인덱스 삭제  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 하나의 트랜잭션으로 두 개의 인덱스를 삭제합니다.  
  
```  
DROP INDEX  
    IX_PurchaseOrderHeader_EmployeeID ON Purchasing.PurchaseOrderHeader,  
    IX_Address_StateProvinceID ON Person.Address;  
GO  
```  
  
### <a name="c-dropping-a-clustered-index-online-and-setting-the-maxdop-option"></a>3. 온라인으로 클러스터형 인덱스 삭제 및 MAXDOP 옵션 설정  
 다음 예에서는 `ONLINE` 옵션을 `ON`으로 설정하고 `MAXDOP`를 `8`로 설정해 클러스터형 인덱스를 삭제합니다. MOVE TO 옵션을 지정하지 않았기 때문에 결과 테이블은 인덱스와 동일한 파일 그룹에 저장됩니다. 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]까지  
  
```  
DROP INDEX AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate   
    ON Production.BillOfMaterials WITH (ONLINE = ON, MAXDOP = 2);  
GO  
```  
  
### <a name="d-dropping-a-clustered-index-online-and-moving-the-table-to-a-new-filegroup"></a>D. 온라인으로 클러스터형 인덱스 삭제 및 새 파일 그룹으로 테이블 이동  
 다음 예에서는 `NewGroup` 절을 사용하여 온라인으로 클러스터형 인덱스를 삭제하고 결과 테이블을 `MOVE TO` 파일 그룹으로 옮깁니다. 테이블을 이동하기 전과 이동한 후에 파일 그룹에서의 인덱스 및 테이블 배치를 확인하기 위해 `sys.indexes`, `sys.tables`및 `sys.filegroups` 카탈로그 뷰를 쿼리합니다. ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 DROP INDEX IF EXISTS 구문을 사용할 수 있습니다.)  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
--Create a clustered index on the PRIMARY filegroup if the index does not exist.  
CREATE UNIQUE CLUSTERED INDEX  
    AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate   
        ON Production.BillOfMaterials (ProductAssemblyID, ComponentID,   
        StartDate)  
    ON 'PRIMARY';  
GO  
-- Verify filegroup location of the clustered index.  
SELECT t.name AS [Table Name], i.name AS [Index Name], i.type_desc,  
    i.data_space_id, f.name AS [Filegroup Name]  
FROM sys.indexes AS i  
    JOIN sys.filegroups AS f ON i.data_space_id = f.data_space_id  
    JOIN sys.tables as t ON i.object_id = t.object_id  
        AND i.object_id = OBJECT_ID(N'Production.BillOfMaterials','U')  
GO  
--Create filegroup NewGroup if it does not exist.  
IF NOT EXISTS (SELECT name FROM sys.filegroups  
                WHERE name = N'NewGroup')  
    BEGIN  
    ALTER DATABASE AdventureWorks2012  
        ADD FILEGROUP NewGroup;  
    ALTER DATABASE AdventureWorks2012  
        ADD FILE (NAME = File1,  
            FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\File1.ndf')  
        TO FILEGROUP NewGroup;  
    END  
GO  
--Verify new filegroup  
SELECT * from sys.filegroups;  
GO  
-- Drop the clustered index and move the BillOfMaterials table to  
-- the Newgroup filegroup.  
-- Set ONLINE = OFF to execute this example on editions other than Enterprise Edition.  
DROP INDEX AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate   
    ON Production.BillOfMaterials   
    WITH (ONLINE = ON, MOVE TO NewGroup);  
GO  
-- Verify filegroup location of the moved table.  
SELECT t.name AS [Table Name], i.name AS [Index Name], i.type_desc,  
    i.data_space_id, f.name AS [Filegroup Name]  
FROM sys.indexes AS i  
    JOIN sys.filegroups AS f ON i.data_space_id = f.data_space_id  
    JOIN sys.tables as t ON i.object_id = t.object_id  
        AND i.object_id = OBJECT_ID(N'Production.BillOfMaterials','U');  
GO  
```  
  
### <a name="e-dropping-a-primary-key-constraint-online"></a>E. 온라인으로 PRIMARY KEY 제약 조건 삭제  
 PRIMARY KEY 또는 UNIQUE 제약 조건 생성 결과로 생성된 인덱스는 DROP INDEX를 사용하여 삭제할 수 없습니다. 이러한 인덱스는 ALTER TABLE DROP CONSTRAINT 문을 사용하여 삭제할 수 있습니다. 자세한 내용은 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
 다음 예에서는 제약 조건을 삭제하여 PRIMARY KEY 제약 조건을 가진 클러스터형 인덱스를 삭제합니다. `ProductCostHistory` 테이블에는 FOREIGN KEY 제약 조건이 없습니다. 제약 조건이 있을 경우 제약 조건을 먼저 제거해야 합니다.  
  
```  
-- Set ONLINE = OFF to execute this example on editions other than Enterprise Edition.  
ALTER TABLE Production.TransactionHistoryArchive  
DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID  
WITH (ONLINE = ON);  
```  
  
### <a name="f-dropping-an-xml-index"></a>F. XML 인덱스 삭제  
 다음 예에서는 `ProductModel` 데이터베이스에서 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 테이블의 XML 인덱스를 삭제합니다.  
  
```  
DROP INDEX PXML_ProductModel_CatalogDescription   
    ON Production.ProductModel;  
```  
  
### <a name="g-dropping-a-clustered-index-on-a-filestream-table"></a>G. FILESTREAM 테이블에서 클러스터형 인덱스 삭제  
 다음 예에서는 클러스터형 인덱스를 온라인으로 삭제하고 `MyPartitionScheme` 절과 `MOVE TO` 절을 모두 사용하여 테이블(힙) 결과 및 FILESTREAM 데이터를 `FILESTREAM ON` 파티션 구성표로 이동합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
DROP INDEX PK_MyClusteredIndex   
    ON dbo.MyTable   
    WITH (MOVE TO MyPartitionScheme,  
          FILESTREAM_ON MyPartitionScheme);  
GO  
```  

  
## <a name="see-also"></a>참고 항목  
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [ALTER PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
  
  


