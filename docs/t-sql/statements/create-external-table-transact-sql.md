---
title: CREATE EXTERNAL TABLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fc04195092a1371be93410cc77d8d06460c957da
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="create-external-table-transact-sql"></a>CREATE EXTERNAL TABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  PolyBase 또는 Elastic Database 쿼리에 대한 외부 테이블을 만듭니다. 시나리오에 따라 구문은 크게 다릅니다. PolyBase용으로 만든 외부 테이블은 Elastic Database 쿼리에 사용할 수 없습니다.  마찬가지로 Elastic Database 쿼리용으로 만든 외부 테이블은 PolyBase 등에 사용할 수 없습니다. 
  
> [!NOTE]  
>  PolyBase는 SQL Server 2016(또는 그 이상), Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스에서만 지원됩니다. Elastic Database 쿼리는 Azure SQL Database v12 이상에서만 지원됩니다.  


- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 외부 테이블을 사용하여 Hadoop 클러스터나 Azure Blob 저장소에 저장된 데이터를 참조하는 Hadoop 클러스터나 Azure Blob 저장소 PolyBase 외부 테이블에 저장된 데이터에 액세스합니다. [Elastic Database 쿼리](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)에 대한 외부 테이블을 만드는 데에도 사용할 수 있습니다.  
  
 외부 테이블을 사용하여 다음을 수행합니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 통해 Hadoop 또는 Azure Blob Storage 데이터를 쿼리합니다.  
  
-   Hadoop 또는 Azure Blob Storage의 데이터를 가져와서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장합니다.  
  
-   Elastic Database에 사용할 외부 테이블   
     쿼리를 만듭니다.  
     
- Azure Data Lake Store의 데이터를 가져와서 Azure SQL Data Warehouse에 저장합니다.
  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) 및 [DROP EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-table-transact-sql.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  

```  
-- Syntax for SQL Server 
  
-- Create a new external table  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  

```  
-- Syntax for Azure SQL Database
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  


```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Create a new external table in SQL Server PDW  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'hdfs_folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
```  
  
## <a name="arguments"></a>인수  
 *database_name* . [ schema_name ] . | schema_name. ] *table_name*  
 만들려는 테이블의 한 부분에서 세 부분으로 이루어진 이름입니다. 외부 테이블의 경우 테이블 메타데이터만이 Hadoop 또는 Azure Blob Storage에 참조된 파일 또는 폴더에 관한 기본 통계와 함께 SQL에 저장됩니다. 실제 데이터가 이동되거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장되지 않습니다.  
  
 \<column_definition> [ ,...*n* ] CREATE EXTERNAL TABLE을 통해 하나 이상의 열 정의를 사용할 수 있습니다. CREATE EXTERNAL TABLE과 CREATE TABLE 모두 열을 정의하는 데 같은 구문을 사용합니다. 이에 대한 예외는 외부 테이블에 DEFAULT CONSTRAINT를 사용할 수 없다는 것입니다. 열 정의 및 해당 데이터 형식에 대한 자세한 내용은 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 및 [Azure SQL Database에 대한 CREATE TABLE](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1)을 참조하세요.  
  
 데이터 형식 및 열 수를 포함한 열 정의는 외부 파일의 데이터와 일치해야 합니다. 불일치가 있는 경우 실제 데이터를 쿼리할 때 파일 행이 거부됩니다.  
  
 외부 데이터 원본의 파일을 참조하는 외부 테이블의 경우 열 및 형식 정의는 외부 파일의 정확한 스키마에 매핑해야 합니다. Hadoop/Hive에 저장된 데이터를 참조하는 데이터 형식을 정의하는 경우 SQL과 Hive 데이터 형식 간에 다음 매핑을 사용하고 그로부터 선택할 때 형식을 SQL 데이터 형식으로 캐스팅합니다. 형식은 달리 명시하지 않은 한 Hive의 모든 버전을 포함합니다.

> [!NOTE]  
>  SQL Server는 어떤 변환에서도 Hive _무한대_ 데이터 값을 지원하지 않습니다. PolyBase는 데이터 형식 변환 오류가 있으면 실패합니다.


|SQL 데이터 형식|.NET 데이터 형식|Hive 데이터 형식|Hadoop/Java 데이터 형식|주석|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|TINYINT|Byte|TINYINT|ByteWritable|부호 없는 숫자의 경우만.|  
|SMALLINT|Int16|SMALLINT|ShortWritable||  
|ssNoversion|Int32|ssNoversion|IntWritable||  
|BIGINT|Int64|BIGINT|LongWritable||  
|bit|Boolean|boolean|BooleanWritable||  
|FLOAT|Double|double|DoubleWritable||  
|REAL|단일|FLOAT|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|SMALLMONEY|Decimal|double|DoubleWritable||  
|NCHAR|String<br /><br /> Char[]|string|text||  
|NVARCHAR|String<br /><br /> Char[]|string|텍스트 모드||  
|char|String<br /><br /> Char[]|string|텍스트 모드||  
|varchar|String<br /><br /> Char[]|string|텍스트 모드||  
|BINARY|Byte[]|BINARY|BytesWritable|Hive 0.8 이상에 적용됩니다.|  
|varbinary|Byte[]|BINARY|BytesWritable|Hive 0.8 이상에 적용됩니다.|  
|날짜|DateTime|TIMESTAMP|TimestampWritable||  
|smalldatetime|DateTime|TIMESTAMP|TimestampWritable||  
|Datetime2|DateTime|TIMESTAMP|TimestampWritable||  
|DATETIME|DateTime|TIMESTAMP|TimestampWritable||  
|Time|TimeSpan|TIMESTAMP|TimestampWritable||  
|Decimal|Decimal|Decimal|BigDecimalWritable|Hive 0.11 이상에 적용됩니다.|  
  
 LOCATION =  '*folder_or_filepath*'  
 Hadoop 또는 Azure Blob Storage의 실제 데이터에 대한 폴더 또는 파일 경로 및 파일 이름을 지정합니다. 위치는 루트 폴더에서 시작하며, 루트 폴더는 외부 데이터 원본에 지정된 데이터 위치입니다.  


SQL Server에서는 CREATE EXTERNAL TABLE 문이 경로 및 폴더가 없으면 만듭니다. 그런 다음, INSERT INTO를 사용하여 로컬 SQL Server 테이블에서 외부 데이터 원본으로 데이터를 내보냅니다. 자세한 내용은 [PolyBase 쿼리](/sql/relational-databases/polybase/polybase-queries)를 참조하세요. 

SQL Data Warehouse 및 Analytics Platform System에서는 [CREATE EXTERNAL TABLE AS SELECT](create-external-table-as-select-transact-sql.md) 문이 존재하지 않는 경로 및 폴더를 만듭니다. 이 두 제품에서는 CREATE EXTERNAL TABLE이 경로와 폴더를 만들지 않습니다.

  
 위치(LOCATION)를 폴더로 지정할 경우, 외부 테이블에서 선택하는 PolyBase 쿼리는 폴더 및 해당 폴더의 모든 하위 폴더에서 파일을 검색합니다. Hadoop과 마찬가지로 PolyBase도 숨겨진 폴더를 반환하지 않습니다. 또한 파일 이름이 밑줄(_) 또는 마침표(.)로 시작하는 파일을 반환하지 않습니다.  
  
 이 예제에서 LOCATION='/webdata/'이면 PolyBase 쿼리는 mydata.txt 및 mydata2.txt에서 행을 반환합니다.  mydata3.txt는 숨겨진 폴더의 하위 폴더이므로 반환하지 않습니다. _hidden.txt는 숨겨진 파일이므로 반환하지 않습니다.  
  
 ![외부 테이블에 대한 재귀적 데이터](../../t-sql/statements/media/aps-polybase-folder-traversal.png "외부 테이블에 대한 재귀적 데이터")  
  
 기본값을 변경하고 루트 폴더에서 읽기만 하려면 core-site.xml 구성 파일에서 특성 \<polybase.recursive.traversal>을 'false'로 설정합니다. 이 파일은 `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server` 아래에 있습니다. `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`)을 입력합니다.  
  
 DATA_SOURCE = *external_data_source_name*  
 외부 데이터의 위치를 포함하는 외부 데이터 원본의 이름을 지정합니다. 이 위치는 Hadoop 또는 Azure Blob Storage입니다. 외부 데이터 원본을 만들려면 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)을 사용합니다.  
  
 FILE_FORMAT = *external_file_format_name*  
 외부 데이터에 대한 파일 형식 및 압축 방법을 저장하는 외부 파일 형식 개체의 이름을 지정합니다. 외부 파일 형식을 만들려면 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)을 사용합니다.  
  
 거부 옵션  
 PolyBase가 외부 데이터 원본에서 검색하는 *더티* 레코드를 처리하는 방법을 결정하는 거부 매개 변수를 지정할 수 있습니다. 데이터 레코드는 실제 데이터 형식 또는 열 수가 외부 테이블의 열 정의와 일치하지 않으면 '더티'로 간주됩니다.  
  
 거부 값을 지정하거나 변경하지 않으면 PolyBase는 기본값을 사용합니다. 거부 매개 변수에 관한 이 정보는 CREATE EXTERNAL TABLE 문을 사용하여 외부 테이블을 만들 때 추가 메타데이터로 저장됩니다.   후속 SELECT 문 또는 SELECT INTO SELECT 문이 외부 데이터에서 데이터를 선택하는 경우, PolyBase는 거부 옵션을 사용하여 실제 쿼리가 실패할 때까지 거부될 수 있는 행의 개수 또는 비율을 결정합니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다. 이 쿼리는 거부된 임계값이 초과될 때까지 (부분) 결과를 반환하며, 그 후 해당 오류 메시지가 발생하면 실패합니다.  
  
 REJECT_TYPE = **value** | percentage  
 REJECT_VALUE 옵션이 리터럴 값으로 지정되는지 또는 백분율로 지정되는지 구체화합니다.  
  
 value  
 REJECT_VALUE는 백분율이 아닌 리터럴 값입니다. PolyBase 쿼리는 거부된 행 수가 *reject_value*를 초과하면 실패합니다.  
  
 예를 들어 REJECT_VALUE = 5이고 REJECT_TYPE = value인 경우, PolyBase SELECT 쿼리는 행 5개가 거부된 후 실패합니다.  
  
 percentage  
 REJECT_VALUE는 리터럴 값이 아닌 백분율입니다. PolyBase 쿼리는 실패한 행의 백분율(*percentage*)이 *reject_value*를 초과하면 실패합니다. 실패한 행의 백분율은 일정 간격으로 계산됩니다.  
  
 REJECT_VALUE = *reject_value*  
 쿼리가 실패할 때까지 거부될 수 있는 값 또는 행의 백분율을 지정합니다.  
  
 REJECT_TYPE = value인 경우, *reject_value*는 0에서 2,147,483,647 사이의 정수여야 합니다.  
  
 REJECT_TYPE = percentage인 경우, *reject_value*는 0에서 100 사이의 부동 소수점 수이어야 합니다.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 이 특성은 REJECT_TYPE = percentage를 지정한 경우에 필요하며 PolyBase가 거부된 행의 백분율을 다시 계산하기 전까지 검색을 시도하는 행 수를 결정합니다.  
  
 *reject_sample_value* 매개 변수는 0에서 2,147,483,647 사이의 정수여야 합니다.  
  
 예를 들어 REJECT_SAMPLE_VALUE = 1000인 경우, PolyBase는 외부 데이터 파일에서 행 1000개 가져오기를 시도한 후 실패한 행의 백분율을 계산합니다. 실패한 행의 백분율이 *reject_value*보다 작은 경우, PolyBase는 또 다른 행 1000개의 검색을 시도합니다. 계속해서 추가로 행 1000개의 가져오기를 시도한 후마다 실패한 행의 백분율을 다시 계산합니다.  
  
> [!NOTE]  
>  PolyBase는 실패한 행의 백분율을 일정 간격으로 계산하므로 실패한 행의 실제 백분율은 *reject_value*를 초과할 수 있습니다.  
  
 예:  
  
 이 예제에서는 REJECT 옵션 세 개가 서로 상호 작용하는 방법을 보여 줍니다. 예를 들어REJECT_TYPE = percentage, REJECT_VALUE = 30 및 REJECT_SAMPLE_VALUE = 100인 경우 다음과 같은 시나리오가 일어날 수 있습니다.  
  
-   PolyBase가 처음 100개 행의 검색을 시도하며, 25개가 실패하고 75개가 성공합니다.  
  
-   실패한 행의 백분율은 25%로 계산되며, 이는 거부 값 30%보다 작습니다. 그러므로 PolyBase는 외부 데이터 소스에서 데이터 검색을 계속합니다.  
  
-   PolyBase는 다음 100개 행의 로드를 시도하며, 이번에는 25개가 성공하고 75개가 실패합니다.  
  
-   실패한 행의 백분율은 50%로 다시 계산됩니다. 실패한 행의 이 백분율은 30% 거부 값을 초과했습니다.  
  
-   PolyBase 쿼리는 처음 200개 행의 반환을 시도한 후 거부된 행이 50%여서 실패합니다. 참고로 PolyBase 쿼리에서 거부 임계값이 초과되었음을 감지하기 전에 일치하는 행 수가 반환되었습니다.  
  
 분할된 데이터베이스 외부 테이블 옵션  
 [Elastic Database 쿼리](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)에 대한 외부 데이터 원본(SQL Server 데이터 원본이 아닌) 및 배포 방법을 지정합니다.  
  
 DATA_SOURCE  
 Hadoop 파일 시스템, Azure Blob Storage 또는 [분할된 데이터베이스 맵 관리자](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/)에 저장된 데이터 같은 외부 데이터 원본입니다.  
  
 SCHEMA_NAME  
 SCHEMA_NAME 절은 외부 테이블 정의를 원격 데이터베이스의 다른 스키마의 테이블에 매핑하는 기능을 제공합니다. 이 기능을 사용하여 로컬과 원격 데이터베이스에 모두 존재하는 스키마 사이를 구분합니다.  
  
 OBJECT_NAME  
 OBJECT_NAME 절은 외부 테이블 정의를 원격 데이터베이스의 다른 이름을 가진 테이블에 매핑하는 기능을 제공합니다. 이 기능을 사용하여 로컬과 원격 데이터베이스에 모두 존재하는 개체 이름 사이를 구분합니다.  
  
 DISTRIBUTION  
 (선택 사항) 이 절은 SHARD_MAP_MANAGER 형식의 데이터베이스에 대해서만 필요합니다. 이 절은 테이블이 분할된 데이터베이스 테이블로 처리되는지 아니면 복제된 테이블로 처리되는지를 제어합니다. **SHARDED**(*열 이름*) 테이블에서는 서로 다른 테이블의 데이터가 겹치지 않습니다. **REPLICATED**는 테이블이 모든 분할된 데이터베이스에서 같은 데이터를 갖도록 지정합니다. **ROUND_ROBIN**은 응용 프로그램 관련 방법을 사용하여 데이터를 배포하도록 지정합니다.  
  
## <a name="permissions"></a>사용 권한  
 다음과 같은 권한이 필요합니다.  
  
-   **CREATE TABLE**  
  
-   **ALTER ANY SCHEMA**  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**  

-   **CONTROL DATABASE**
  
 참고로 외부 데이터 원본을 만드는 로그인은 Hadoop 또는 Azure Blob Storage에 있는 외부 데이터 원본에 대한 읽기 및 쓰기 권한을 가져야 합니다.  


 > [!IMPORTANT]  

>  ALTER ANY EXTERNAL DATA SOURCE 권한은 주체에 대해 외부 데이터 원본 개체를 만들고 수정하는 권한을 부여하며, 따라서 데이터베이스의 모든 데이터베이스 범위 자격 증명에 액세스하는 권한도 부여합니다. 이 권한은 높은 수준의 권한으로 간주되어야 하므로, 시스템의 신뢰할 수 있는 보안 주체에만 부여되어야 합니다.

## <a name="error-handling"></a>오류 처리  
 CREATE EXTERNAL TABLE 문을 실행하는 동안 PolyBase는 외부 데이터 원본에 연결을 시도합니다. 연결 시도가 실패하면 이 문이 실패하고 외부 테이블이 만들어지지 않습니다. PolyBase는 쿼리가 결국 실패할 때까지 연결을 다시 시도하므로 이 명령이 실패하려면 1분 이상 걸릴 수 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 임시 쿼리 시나리오, 즉 SELECT FROM EXTERNAL TABLE에서 PolyBase는 외부 데이터 원본에서 검색된 행을 임시 테이블에 저장합니다. 쿼리가 완료된 후 PolyBase는 임시 테이블을 제거하고 삭제합니다. 영구적 데이터가 SQL 테이블에 저장되지 않습니다.  
  
 이에 비해 가져오기 시나리오, 즉 SELECT INTO FROM EXTERNAL TABLE에서 PolyBase는 외부 데이터 원본에서 검색된 행을 영구 데이터로 SQL 테이블에 저장합니다. 새 테이블은 PolyBase가 외부 데이터를 검색할 때 쿼리를 실행하는 동안 만들어집니다.  
  
 PolyBase는 쿼리 성능을 향상시키기 위해 쿼리 계산 중 일부를 Hadoop에 푸시할 수 있습니다. 이 기능을 조건자 푸시 다운이라 합니다. 이 기능을 활성화하려면 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)에 Hadoop 리소스 관리자 위치 옵션을 지정합니다.  
  
 같은 또는 서로 다른 외부 데이터 원본을 참조하는 수많은 외부 테이블을 만들 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 CTP2에서 내보내기 기능은 지원되지 않습니다. 즉, SQL 데이터를 외부 데이터 원본에 영구적으로 저장합니다. 이 기능은 CTP3에서 사용할 수 있습니다.  
  
 외부 테이블에 대한 데이터는 어플라이언스 외부에 상주하므로 PolyBase의 제어를 받지 않으며 언제든지 외부 프로세스에 의해 변경 또는 제거될 수 있습니다. 이러한 이유 때문에 외부 테이블에 대한 쿼리 결과는 결정적인 것으로 보증되지 않습니다. 즉, 외부 테이블에 대해 실행할 때마다 같은 쿼리가 서로 다른 결과를 반환할 수 있습니다. 마찬가지로 외부 데이터가 제거되거나 이동되면 쿼리가 실패할 수 있습니다.  
  
 각각 서로 다른 외부 데이터 원본을 참조하는 여러 개의 외부 테이블을 만들 수 있습니다. 그러나 서로 다른 Hadoop 데이터 원본에 대해 동시에 쿼리를 실행하는 경우 각 Hadoop 원본이 같은 'hadoop 연결' 서버 구성 설정을 사용해야 합니다. 예를 들어 Cloudera Hadoop 클러스터 및 Hortonworks Hadoop 클러스터는 서로 다른 구성 설정을 사용하므로 이들에 대해 하나의 쿼리를 동시에 실행할 수 없습니다. 구성 설정 및 지원되는 결합에 대해서는 [PolyBase 연결 구성&#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요.  
  
 다음 DDL(Data Definition Language) 문은 외부 테이블에 대해 허용됩니다.  
  
-   CREATE TABLE 및 DROP TABLE  
  
-   CREATE STATISTICS 및 DROP STATISTICS  
참고: 외부 테이블에 대한 CREATE 및 DROP STATISTICS는 Azure SQL Database에서 지원되지 않습니다. 
  
-   CREATE VIEW 및 DROP VIEW  
  
 지원되지 않는 구문 및 작업:  
  
-   외부 테이블 열에 대한 DEFAULT 제약 조건  
  
-   삭제, 삽입 및 업데이트의 DML(데이터 조작 언어) 작업  
  
 쿼리 제한 사항:  
  
 PolyBase는 32개의 동시 PolyBase 쿼리를 실행할 때 폴더당 최대 33k 파일을 사용할 수 있습니다. 이 최대 개수는 각 HDFS 폴더의 파일과 하위 폴더를 모두 포함합니다. 동시성 수준이 32보다 작은 경우 사용자는 33k보다 많은 파일을 포함하는 HDFS의 폴더에 대해 PolyBase 쿼리를 실행할 수 있습니다. 외부 파일 경로를 짧게 유지하고 HDFS 폴더당 30k 이하의 파일을 사용하는 것이 좋습니다. 너무 많은 파일이 참조되면 JVM(Java Virtual Machine) 메모리 부족 예외가 발생할 수 있습니다.  

테이블 너비 제한 사항: SQL Server 2016의 PolyBase에는 테이블 정의에 의해 유효한 단일 행의 최대 크기를 기반으로 32KB의 행 너비 한도가 적용됩니다. 열 스키마의 합계가 32KB보다 큰 경우, PolyBase는 데이터를 쿼리할 수 없습니다. 

SQL Data Warehouse에서 이 제한 사항은 1MB로 증가되었습니다.


## <a name="locking"></a>잠금  
 SCHEMARESOLUTION 개체에 대한 공유 잠금입니다.  
  
## <a name="security"></a>보안  
 외부 테이블에 대한 데이터 파일은 Hadoop 또는 Azure Blob Storage에 저장됩니다. 이러한 데이터 파일은 사용자 고유의 프로세스에 의해 만들어지고 관리됩니다. 외부 데이터의 보안을 관리하는 것은 사용자의 책임입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>1. 텍스트로 구분된 형식의 데이터를 사용하여 외부 테이블을 만듭니다.  
 이 예제에서는 텍스트로 구분된 파일 형식의 데이터를 가진 외부 테이블을 만드는 데 필요한 모든 단계를 보여 줍니다. 즉, 외부 데이터 원본 *mydatasource* 및 외부 파일 형식 *myfileformat*을 만듭니다. 이러한 데이터베이스 수준 개체는 나중에 CREATE EXTERNAL TABLE 문에 참조됩니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) 및 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)을 참조하세요.  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,   
    FORMAT_OPTIONS (FIELD_TERMINATOR ='|')  
);  
  
CREATE EXTERNAL TABLE ClickStream (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee.tbl',  
        DATA_SOURCE = mydatasource,  
        FILE_FORMAT = myfileformat  
    )  
;  
  
```  
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>2. RCFile 형식의 데이터를 사용하여 외부 테이블을 만듭니다.  
 이 예제에서는 RCFile 형식의 데이터를 가진 외부 테이블을 만드는 데 필요한 모든 단계를 보여 줍니다. 즉, 외부 데이터 원본 *mydatasource_rc* 및 외부 파일 형식 *myfileformat_rc*를 만듭니다. 이러한 데이터베이스 수준 개체는 나중에 CREATE EXTERNAL TABLE 문에 참조됩니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) 및 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)을 참조하세요.  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_rc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee_rc.tbl',  
        DATA_SOURCE = mydatasource_rc,  
        FILE_FORMAT = myfileformat_rc  
    )  
;  
  
```  
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>3. ORC 형식의 데이터를 사용하여 외부 테이블을 만듭니다.  
 이 예제에서는 ORC 형식의 데이터를 가진 외부 테이블을 만드는 데 필요한 모든 단계를 보여 줍니다. 즉, 외부 데이터 원본 mydatasource_orc 및 외부 파일 형식 myfileformat_orc를 만듭니다. 이러한 데이터베이스 수준 개체는 나중에 CREATE EXTERNAL TABLE 문에 참조됩니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) 및 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)을 참조하세요.  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_orc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_orc  
WITH (  
    FORMAT = ORC,  
    COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_orc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/',  
        DATA_SOURCE = mydatasource_orc,  
        FILE_FORMAT = myfileformat_orc  
    )  
;  
  
```  
  
### <a name="d-querying-hadoop-data"></a>4. Hadoop 데이터 쿼리  
 Clickstream은 Hadoop 클러스터의 텍스트로 구분된 파일 employee.tbl에 연결하는 외부 테이블입니다. 다음 쿼리는 표준 테이블에 대한 쿼리와 유사해 보입니다. 그러나 이 쿼리는 Hadoop에서 데이터를 검색한 다음, 결과를 계산합니다.  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>5. Hadoop 데이터를 SQL 데이터와 조인  
 이 쿼리는 SQL 테이블 두 개에 대한 표준 JOIN과 유사해 보입니다. 차이점은 PolyBase이 Hadoop에서 Clickstream 데이터를 검색한 다음, UrlDescription 테이블에 조인한다는 것입니다. 한 테이블은 외부 테이블이며 다른 테이블은 표준 SQL 테이블입니다.  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>6. SQL 테이블로 Hadoop의 데이터 가져오기  
 이 예제에서는 표준 SQL 테이블 *user*와 외부 테이블 *ClickStream* 간 조인의 결과를 영구적으로 저장하는 새 SQL 케이블 ms_user입니다.  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>7. 분할된 데이터베이스 데이터 원본에 대한 외부 테이블 만들기  
 이 예제에서는 SCHEMA_NAME 및 OBJECT_NAME 절을 사용하여 원격 DMV를 외부 테이블에 다시 매핑합니다.  
  
```  
CREATE EXTERNAL TABLE [dbo].[all_dm_exec_requests]([session_id] smallint NOT NULL,  
  [request_id] int NOT NULL,  
  [start_time] datetime NOT NULL,   
  [status] nvarchar(30) NOT NULL,  
  [command] nvarchar(32) NOT NULL,  
  [sql_handle] varbinary(64),  
  [statement_start_offset] int,  
  [statement_end_offset] int,  
  [cpu_time] int NOT NULL)  
WITH  
(  
  DATA_SOURCE = MyExtSrc,  
  SCHEMA_NAME = 'sys',  
  OBJECT_NAME = 'dm_exec_requests',  
  DISTRIBUTION=ROUND_ROBIN  
);   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>8. Azure [!INCLUDE[ssDW](../../includes/ssdw-md.md)]로 ADLS의 데이터 가져오기  
 
  
```  

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@\<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = 'adl://pbasetr.azuredatalakestore.net'
)



CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH ( FORMATTYPE = DELIMITEDTEXT 
     , FORMATOPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
    )


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH ( LOCATION='/DimProduct/' , 
       DATA_SOURCE = AzureDataLakeStore , 
       FILE_FORMAT = TextFileFormat , 
       REJECT_TYPE = VALUE ,
       REJECT_VALUE = 0 ) ;


CREATE TABLE [dbo].[DimProduct] 
WITH (DISTRIBUTION = HASH([ProductKey] ) ) 
AS SELECT * FROM 
[dbo].[DimProduct_external] ; 
     
```  
  
### <a name="i-join-external-tables"></a>9. 외부 테이블 조인  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>10. HDFS 데이터를 PDW 데이터와 조인  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>11. HDFS의 행 데이터를 배포된 PDW 테이블에 가져오기  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>12. HDFS의 행 데이터를 복제된 PDW 테이블에 가져오기  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>참고 항목  
 [일반적인 메타데이터 쿼리 예제(SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



