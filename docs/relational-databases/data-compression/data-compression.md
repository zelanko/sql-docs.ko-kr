---
title: 데이터 압축 | Microsoft 문서
description: SQL Server 및 Azure SQL Database를 사용하여 행 및 페이지 데이터 압축 또는 columnstore 및 columnstore 보관 압축을 적용합니다.
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- page compression [Database Engine]
- indexes [SQL Server], compressed
- compressed indexes [SQL Server]
- storage compression [Database Engine]
- tables [SQL Server], compressed
- storage [SQL Server], compressed
- compression [SQL Server]
- row compression [Database Engine]
- compression [SQL Server], about compressed tables and indexes
- data compression [Database Engine]
- compressed tables [SQL Server]
ms.assetid: 5f33e686-e115-4687-bd39-a00c48646513
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5da071f378edb771d4b1dc70ac8257febd78a522
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86459015"
---
# <a name="data-compression"></a>Data Compression
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 rowstore 테이블 및 인덱스를 위해 행 및 페이지 압축을 지원하며 columnstore 테이블 및 인덱스를 위해 columnstore 및 columnstore 보관 압축을 지원합니다.  
  
 rowstore 테이블 및 인덱스의 경우 데이터베이스 크기를 줄이려면 데이터 압축 기능을 사용하십시오. 데이터를 압축하면 공간을 절약할 수 있을 뿐만 아니라 데이터가 보다 적은 수의 페이지에 저장되어 쿼리가 디스크에서 읽어야 하는 페이지가 적어지므로 I/O가 많은 작업의 성능을 향상시킬 수 있습니다. 그러나 데이터를 애플리케이션과 교환하는 동안 데이터를 압축하고 압축 해제하기 위해 데이터베이스 서버에 추가 CPU 리소스가 필요합니다. 다음 데이터베이스 개체에 대해 행 및 페이지 압축을 구성할 수 있습니다.   
-   힙으로 저장되는 전체 테이블  
-   클러스터형 인덱스로 저장되는 전체 테이블  
-   전체 비클러스터형 인덱스  
-   전체 인덱싱된 뷰  
-   분할된 테이블과 인덱스의 경우 파티션별로 압축 옵션을 구성할 수 있고 개체의 다양한 파티션에 동일한 압축 설정을 구성할 필요가 없습니다.  
  
columnstore 테이블 및 인덱스의 경우 모든 columnstore 테이블 및 인덱스는 항상 columnstore 압축을 사용하며 이것은 사용자가 구성할 수 없습니다. 데이터를 저장하고 검색할 추가 시간과 CPU 리소스가 있는 상황에서 데이터 크기를 더 줄이려면 columnstore 보관 압축을 사용하십시오.  다음 데이터베이스 개체에 대해 columnstore 보관 압축을 구성할 수 있습니다.  
-   전체 columnstore 테이블 또는 전체 클러스터형 columnstore 인덱스  columnstore 테이블은 클러스터형 columnstore 인덱스로 저장되므로 둘 다 같은 결과를 가져옵니다.  
-   전체 비클러스터형 columnstore 인덱스  
-   분할된 columnstore 테이블과 columnstore 인덱스의 경우 파티션별로 보관 압축 옵션을 구성할 수 있고 다양한 파티션에 동일한 보관 압축 설정을 구성할 필요가 없습니다.  
  
> [!NOTE]  
> 데이터는 GZIP 알고리즘 형식을 사용하여 압축될 수도 있습니다. 이는 추가 단계이며 장기 스토리지에 이전 데이터를 보관하는 경우 데이터의 일부를 압축하는 데 가장 적합합니다. `COMPRESS` 함수를 사용하여 압축된 데이터는 인덱싱할 수 없습니다. 자세한 내용은 [COMPRESS&#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)를 참조하세요.  
  
## <a name="considerations-for-when-you-use-row-and-page-compression"></a>행 및 페이지 압축 시 고려 사항  
 행 및 페이지 압축을 사용할 때 다음 사항을 고려해야 합니다.  
-   데이터 압축의 세부 사항은 서비스 팩이나 후속 릴리스에서 예고 없이 변경될 수 있습니다.
-   [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]에서 압축을 사용할 수 있습니다.  
-   일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 압축을 사용할 수 없습니다. 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
-   시스템 테이블에는 압축을 사용할 수 없습니다.  
-   압축하면 한 페이지에 더 많은 행을 저장할 수 있지만 테이블 또는 인덱스의 최대 행 크기는 변경되지 않습니다.  
-   최대 행 크기와 압축 오버헤드를 더한 값이 최대 행 크기 8060바이트를 초과하는 테이블에서는 압축을 사용할 수 없습니다. 예를 들어 `c1 CHAR(8000)` 및 `c2 CHAR(53)` 열이 있는 테이블은 추가 압축 오버헤드 때문에 압축할 수 없습니다. vardecimal 스토리지 형식이 사용되는 경우 해당 형식을 사용하면 행 크기 검사가 수행됩니다. 행 및 페이지 압축의 경우 개체가 처음 압축될 때 행 크기 검사가 수행된 다음 각 행을 삽입하거나 수정할 때 검사됩니다. 압축에는 다음 두 가지 규칙이 적용됩니다.  
    -   고정 길이 형식으로의 업데이트가 항상 성공해야 합니다.  
    -   데이터 압축 비활성화에 항상 성공해야 합니다. 압축된 행이 8060바이트 미만으로 페이지에 맞더라도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 압축하지 않을 경우 행에 맞지 않는 업데이트 내용을 적용할 수 없도록 합니다.  
-   파티션 목록을 지정하는 경우 개별 파티션에 대한 압축 유형을 ROW, PAGE 또는 NONE으로 설정할 수 있습니다. 파티션 목록을 지정하지 않은 경우에는 모든 파티션이 문에 지정된 데이터 압축 속성을 사용하여 설정됩니다. 테이블이나 인덱스를 만들 때 달리 지정하지 않는 한 데이터 압축이 NONE으로 설정됩니다. 테이블을 수정할 경우에는 달리 지정하지 않는 한 기존 압축이 유지됩니다.  
-   범위를 벗어난 파티션 목록 또는 파티션을 지정하면 오류가 생성됩니다.  
-   비클러스터형 인덱스는 테이블의 압축 속성을 상속하지 않습니다. 인덱스를 압축하려면 인덱스의 압축 속성을 명시적으로 설정해야 합니다. 기본적으로 인덱스를 만들 때 인덱스의 압축 설정은 NONE으로 설정됩니다.  
-   힙에 클러스터형 인덱스를 만드는 경우 이 클러스터형 인덱스는 다른 압축 상태를 지정하지 않는 한 힙의 압축 상태를 상속합니다.  
-   힙이 페이지 수준 압축을 사용하도록 구성된 경우 페이지는 다음과 같은 방식으로만 페이지 수준 압축을 받습니다.  
    -   대량 최적화가 사용하도록 설정된 상태로 데이터를 대량으로 가져옵니다.  
    -   `INSERT INTO ... WITH (TABLOCK)` 구문을 사용하여 데이터를 삽입하고, 테이블에 비클러스터형 인덱스가 없습니다.  
    -   페이지 압축 옵션과 함께 `ALTER TABLE ... REBUILD` 문을 실행하여 테이블을 다시 작성합니다.  
-   DML 작업의 일부로 힙에 할당된 새 페이지에서는 힙이 다시 작성될 때까지 PAGE 압축을 사용하지 않습니다. 압축을 제거하고 다시 적용하거나, 클러스터형 인덱스를 만들거나 제거하여 힙을 다시 작성하십시오.  
-   힙의 압축 설정을 변경하는 경우 힙의 새 행 위치에 대한 포인터를 포함하도록 테이블의 모든 비클러스터형 인덱스를 다시 작성해야 합니다.  
-   온라인이나 오프라인으로 ROW 또는 PAGE 압축을 사용하거나 사용하지 않도록 설정할 수 있습니다. 힙에서 압축을 사용하도록 설정하는 것은 온라인 작업의 경우 단일 스레드입니다.  
-   행 또는 페이지 압축을 사용하거나 사용하지 않도록 설정하기 위한 디스크 공간 요구 사항은 인덱스를 만들거나 다시 작성하는 경우와 같습니다. 분할된 데이터의 경우 한 번에 하나의 파티션에 대해 압축을 사용하거나 사용하지 않도록 설정하여 필요한 공간을 줄일 수 있습니다.  
-   분할된 테이블에서 파티션의 압축 상태를 확인하려면 sys.partitions 카탈로그 뷰의 data_compression 열을 쿼리합니다.  
-   인덱스를 압축하는 경우 리프 수준 페이지는 행 압축과 페이지 압축을 모두 사용하여 압축될 수 있습니다. 리프 수준이 아닌 페이지는 페이지 압축을 받지 않습니다.  
-   큰 값 데이터 형식은 해당 크기 때문에 일반 행 데이터와 별도로 특수 용도 페이지에 저장되기도 합니다. 별도로 저장되는 데이터에는 데이터 압축을 사용할 수 없습니다.  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 vardecimal 스토리지 형식을 구현한 테이블을 업그레이드해도 해당 설정은 유지됩니다. vardecimal 스토리지 형식의 테이블에 행 압축을 적용할 수 있습니다. 그러나 행 압축이 vardecimal 스토리지 형식의 상위 집합이므로 vardecimal 스토리지 형식을 유지할 필요가 없습니다. vardecimal 스토리지 형식과 행 압축을 함께 사용해도 10진수 값이 추가로 압축되지 않습니다. vardecimal 스토리지 형식의 테이블에 페이지 압축을 적용할 수 있지만 vardecimal 스토리지 형식 열이 추가로 압축되지는 않습니다.  
  
    > [!NOTE]  
    > [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 vardecimal 스토리지 형식을 지원하지만 행 수준 압축으로 동일한 결과를 얻을 수 있으므로 vardecimal 스토리지 형식은 더 이상 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="using-columnstore-and-columnstore-archive-compression"></a>Columnstore 및 Columnstore 보관 압축 사용  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]  
  
### <a name="basics"></a>기본 사항  
 Columnstore 테이블 및 인덱스는 항상 columnstore 압축으로 저장됩니다. 보관 압축이라고 하는 추가 압축을 구성하여 columnstore 데이터 크기를 더 줄일 수 있습니다.  보관 압축을 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터에 대해 Microsoft XPRESS 압축 알고리즘을 실행합니다. 다음 데이터 압축 유형을 사용하여 보관 압축을 추가하거나 제거합니다.  
-   보관 압축으로 columnstore 데이터를 압축하려면 **COLUMNSTORE_ARCHIVE** 데이터 압축을 사용하세요.  
-   보관 압축을 풀려면 **COLUMNSTORE** 데이터 압축을 사용하십시오. 결과 데이터는 columnstore 압축으로 계속해서 압축됩니다.  
  
보관 압축을 추가하려면 REBUILD 옵션 및DATA COMPRESSION = COLUMNSTORE_ARCHIVE와 함께 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 또는 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)을 사용하세요.  
  
#### <a name="examples"></a>예제:  

```sql  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE ON PARTITIONS (2,4)) ;  
```  
  
보관 압축을 제거하고 데이터를 columnst또는e 압축으로 복원하려면 REBUILD 옵션 및 DATA COMPRESSION = COLUMNSTORE와 함께 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 또는 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) 를 사용하세요.  
  
#### <a name="examples"></a>예제:  
  
```sql  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (2,4) ) ;  
```  
  
다음 예에서는 데이터 압축을 일부 파티션의 경우 columnstore로 설정하고 다른 파티션의 경우 columnstore 보관으로 설정합니다.  
  
```sql  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (  
    DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (4,5),  
    DATA COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (1,2,3)  
) ;  
```  
  
### <a name="performance"></a>성능  
 보관 압축으로 columnstore 인덱스를 압축하면 보관 압축을 사용하지 않는 columnstore 인덱스보다 인덱스가 느리게 수행됩니다. 데이터를 압축하고 검색할 추가 시간과 CPU 리소스가 있는 상황에서만 보관 압축을 사용하십시오.  
  
 보관 압축의 이점은 자주 액세스하지 않는 데이터에 대해 유용한 스토리지 용량 감소입니다. 예를 들어, 월별 데이터에 대해 파티션이 있고 대부분의 작업이 가장 최근 월에 대한 작업인 경우 스토리지 요구 사항을 줄이기 위해 이전 월을 보관할 수 있습니다.  
  
### <a name="metadata"></a>메타데이터  
다음 시스템 뷰에는 클러스터형 인덱스의 데이터 압축 정보가 포함되어 있습니다.  
-   [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) - **type**과 **type_desc** 열에는 CLUSTERED COLUMNSTORE 및 NONCLUSTERED COLUMNSTORE가 포함됩니다.  
-   [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) – **data_compression**과 **data_compression_desc** 열에는 COLUMNSTORE 및 COLUMNSTORE_ARCHIVE가 포함됩니다.  
  
[sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) 프로시저는 columnstore 인덱스에도 적용할 수 있습니다.  
  
## <a name="how-compression-affects-partitioned-tables-and-indexes"></a>압축이 분할된 테이블 및 인덱스에 주는 영향  
 분할된 테이블 및 인덱스에서 데이터 압축을 사용할 때는 다음 사항을 고려해야 합니다.  
-   `ALTER PARTITION` 문을 사용하여 파티션을 분할할 경우 두 파티션이 모두 원래 파티션의 데이터 압축 특성을 상속합니다.  
-   두 파티션을 병합할 경우 결과 파티션이 대상 파티션의 데이터 압축 특성을 상속합니다.  
-   파티션을 전환하려면 파티션의 데이터 압축 속성이 테이블의 압축 속성과 일치해야 합니다.  
-   분할된 테이블 또는 인덱스의 압축을 수정하는 데에는 다음과 같은 두 가지 구문 변형을 사용할 수 있습니다.  
    -   다음 구문에서는 참조된 파티션만 다시 작성합니다.  
    
        ```sql  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  <option>)  
        ```  
    
    -   다음 구문에서는 참조되지 않는 파티션의 기존 압축 설정을 사용하여 전체 테이블을 다시 작성합니다.  
    
        ```sql  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = ALL   
        WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(<range>),  
        ... )  
        ```  
  
     분할된 인덱스에서는 같은 원칙에 따라 `ALTER INDEX`를 사용합니다.  
  
-   클러스터형 인덱스를 삭제한 경우 파티션 구성표를 수정하지 않으면 해당 힙 파티션에서 데이터 압축 설정이 유지됩니다. 파티션 구성표를 변경하는 경우 모든 파티션이 압축되지 않은 상태로 다시 작성됩니다. 클러스터형 인덱스를 삭제하고 파티션 구성표를 변경하려면 다음 단계를 수행해야 합니다.  
     1. 클러스터형 인덱스를 삭제합니다.  
     2. 압축 옵션을 지정하는 `ALTER TABLE ... REBUILD` 옵션을 사용하여 테이블을 수정합니다.  
  
     클러스터형 인덱스를 OFFLINE으로 삭제하면 클러스터형 인덱스의 상위 수준만 제거되므로 작업이 상당히 빠르게 수행됩니다. 클러스터형 인덱스를 ONLINE으로 삭제하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 1단계와 2단계에서 한 번씩, 총 두 번에 걸쳐 힙을 다시 작성해야 합니다.  
  
## <a name="how-compression-affects-replication"></a>압축이 복제에 주는 영향 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])   

데이터 압축과 복제를 함께 사용할 때는 다음 사항을 고려해야 합니다.  
-   스냅샷 에이전트에서 초기 스키마 스크립트를 생성할 때 새 스키마는 테이블과 해당 인덱스 모두에 대해 동일한 압축 설정을 사용합니다. 압축을 인덱스에 사용하지 않고 테이블에만 사용할 수는 없습니다.  
-   트랜잭션 복제의 경우 아티클 스키마 옵션에 따라 스크립팅할 종속 개체 및 속성이 결정됩니다. 자세한 내용은 [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 참조하세요.  
     배포 에이전트에서는 스크립트를 적용할 때 하위 구독자를 확인하지 않습니다. 압축 복제를 선택하는 경우 하위 구독자에서 테이블을 만들 수 없습니다. 혼합 토폴로지의 경우 압축 복제를 사용하지 마십시오.  
-   병합 복제의 경우 게시 호환성 수준이 스키마 옵션을 재정의하며 스크립팅될 스키마 개체를 결정합니다.  
     혼합 토폴로지의 경우 새 압축 옵션을 지원할 필요가 없으면 게시 호환성 수준을 하위 구독자 버전으로 설정해야 합니다. 새 압축 옵션이 필요하면 테이블을 만든 후 구독자에서 테이블을 압축합니다.  
  
다음 표에서는 복제하는 동안 압축을 제어하는 복제 설정을 보여 줍니다.  
  
|사용자 의도|테이블 또는 인덱스에 대한 파티션 구성표 복제|압축 설정 복제|스크립팅 동작|  
|-----------------|-----------------------------------------------------|------------------------------------|------------------------|  
|파티션 구성표를 복제하고 파티션의 구독자에서 압축 사용|True|True|파티션 구성표와 압축 설정을 모두 스크립팅합니다.|  
|파티션 구성표를 복제하지만 구독자에서 데이터를 압축하지 않음|True|False|파티션 구성표를 스크립팅하지만 파티션의 압축 설정은 스크립팅하지 않습니다.|  
|파티션 구성표를 복제하지 않고 구독자에서 데이터를 압축하지 않음|False|False|파티션이나 압축 설정을 스크립팅하지 않습니다.|  
|게시자에서 모든 파티션이 압축된 경우 구독자에서 테이블을 압축하지만 파티션 구성표를 복제하지 않음|False|True|모든 파티션에서 압축을 사용할 수 있는지 확인합니다.<br /><br /> 테이블 수준에서 압축을 스크립팅합니다.|  
  
## <a name="how-compression-affects-other-sql-server-components"></a>압축이 다른 SQL Server 구성 요소에 주는 영향 
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])  
   
 압축은 스토리지 엔진에서 발생하므로 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 다른 구성 요소 대부분에 압축되지 않은 상태로 제공됩니다. 따라서 압축이 다른 구성 요소에 주는 영향은 다음으로 제한됩니다.  
-   대량 가져오기 및 내보내기 작업  
     데이터를 내보낼 때는 네이티브 형식으로 내보내더라도 데이터가 압축되지 않는 행 형식으로 출력됩니다. 따라서 내보낸 데이터 파일의 크기가 원본 데이터보다 훨씬 커질 수 있습니다.  
     데이터를 가져올 때는 대상 테이블이 압축을 사용하도록 설정된 경우 스토리지 엔진에서 데이터를 압축된 행 형식으로 변환합니다. 이로 인해 데이터를 압축되지 않은 테이블로 가져올 때보다 CPU 사용량이 증가할 수 있습니다.  
     페이지 압축을 사용하여 힙으로 데이터를 대량으로 가져오는 경우 대량 가져오기 작업에서는 데이터를 삽입할 때 페이지 압축을 사용하여 데이터를 압축하려고 합니다.  
-   백업 및 복원에는 압축이 영향을 주지 않습니다.  
-   로그 전달에는 압축이 영향을 주지 않습니다.  
-   스파스 열에서는 데이터 압축이 호환되지 않습니다. 따라서 스파스 열이 포함된 테이블은 압축할 수 없으며 스파스 열을 압축된 테이블에 추가할 수도 없습니다.  
-   데이터는 서로 다른 페이지 수 및 페이지당 행 수를 사용하여 저장되므로 압축을 사용하도록 설정하면 쿼리 계획이 변경될 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 압축 구현](../../relational-databases/data-compression/row-compression-implementation.md)   
 [페이지 압축 구현](../../relational-databases/data-compression/page-compression-implementation.md)   
 [유니코드 압축 구현](../../relational-databases/data-compression/unicode-compression-implementation.md)   
 [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  

