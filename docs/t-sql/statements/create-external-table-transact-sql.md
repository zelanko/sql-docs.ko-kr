---
title: "외부 테이블 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 11/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs: TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: "30"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 638708265e79ff0f3a927e9e049f3985cfe2752a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="create-external-table-transact-sql"></a>외부 테이블 (Transact SQL) 만들기
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Hadoop 클러스터 또는 Azure blob 저장소에 저장 된 데이터를 참조 하는 PolyBase 외부 테이블을 만듭니다. 에 대 한 외부 테이블을 만들려면 사용할 수도 있습니다 [탄력적 데이터베이스 쿼리](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)합니다.  
  
 외부 테이블을 사용 합니다.  
  
-   사용 하 여 Hadoop 또는 Azure blob 저장소 데이터를 쿼리 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.  
  
-   가져오기 및에 Hadoop 또는 Azure blob 저장소에서 데이터를 저장 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
-   탄력적 데이터베이스와 함께 사용 하기 위해 외부 테이블 만들기  
     쿼리입니다.  
     
- 가져오기 및 Azure SQL 데이터 웨어하우스로 Azure 데이터 레이크 저장소에서 데이터를 저장 합니다.
  
 참고 항목 [외부 데이터 원본 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) 및 [외부 테이블 &#40; 삭제 Transact SQL &#41; ](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
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
 *a s e _* 합니다. [schema_name]입니다. | schema_name 합니다. ] *table_name*  
 1 ~ 3 년 부분 이름 만들 테이블의입니다. 따라서 외부 테이블에 대 한 테이블 메타 데이터 파일 및 또는 Hadoop 또는 Azure blob 저장소에서 참조 되는 폴더에 대 한 기본 통계와 함께 SQL에 저장 됩니다. 실제 데이터가 없는 옮겨졌거나에 저장 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 \<column_definition > [,...  *n*  ] CREATE EXTERNAL TABLE이 하나 이상의 열 정의 허용 합니다. CREATE EXTERNAL TABLE과 CREATE TABLE 모두 열을 정의 하기 위한 동일한 구문을 사용 합니다. 이 예외를 외부 테이블에서 기본 제약 조건을 사용할 수 없습니다. 열 정 및 데이터 형식에 대 한 전체 세부 정보를 참조 하세요. [CREATE table&#40; Transact SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md) 및 [Azure SQL 데이터베이스에 새 테이블 만들기](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1)합니다.  
  
 열 정의 외부 파일의 데이터를 데이터 형식 및 열 개수를 포함 하 여 같아야 합니다. 불일치가 있을 경우에 실제 데이터를 쿼리할 때 파일 행 거부 됩니다.  
  
 외부 데이터 원본에 대 한 파일 참조 하는 외부 테이블에 대 한 열 및 형식 정의가 외부 파일의 정확한 스키마에 매핑해야 합니다. Hadoop/Hive에 저장 된 데이터를 참조 하는 데이터 형식에 정의할 때 하이브 또는 SQL 데이터 형식에서 다음 매핑을 사용 하 고 여기에서 선택 하는 경우 SQL 데이터 형식으로 형식을 캐스팅 합니다. 유형은 별도 설명이 없으면 하이브의 모든 버전을 포함 합니다.

> [!NOTE]  
>  SQL Server는 하이브를 지원 하지 않습니다 _무한대_ 변환의 데이터 값입니다. PolyBase는 데이터 형식 변환 오류와 함께 실패 합니다.


|SQL 데이터 형식|.NET 데이터 형식|하이브 데이터 형식|Hadoop/Java 데이터 형식|설명|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|tinyint|Byte|tinyint|ByteWritable|부호 없는 숫자입니다.|  
|smallint|Int16|smallint|ShortWritable||  
|int|Int32|int|IntWritable||  
|bigint|Int64|bigint|LongWritable||  
|bit|Boolean|boolean|BooleanWritable||  
|float|Double|double|DoubleWritable||  
|real|단일|float|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|smallmoney|Decimal|double|DoubleWritable||  
|nchar|문자열<br /><br /> Char]|string|text||  
|nvarchar|문자열<br /><br /> Char]|string|텍스트||  
|char|문자열<br /><br /> Char]|string|텍스트||  
|varchar|문자열<br /><br /> Char]|string|텍스트||  
|binary|Byte[]|binary|BytesWritable|하이브 0.8 이상에 적용 됩니다.|  
|varbinary|Byte[]|binary|BytesWritable|하이브 0.8 이상에 적용 됩니다.|  
|date|DateTime|timestamp|TimestampWritable||  
|smalldatetime|DateTime|timestamp|TimestampWritable||  
|datetime2|DateTime|timestamp|TimestampWritable||  
|datetime|DateTime|timestamp|TimestampWritable||  
|time|TimeSpan|timestamp|TimestampWritable||  
|decimal|Decimal|decimal|BigDecimalWritable|이상 Hive0.11에 적용 됩니다.|  
  
 위치 = '*folder_or_filepath*'  
 Hadoop 또는 Azure blob 저장소의 폴더 또는 파일 경로 실제 데이터에 대 한 파일 이름을 지정합니다. 위치에서 루트 폴더에서 시작 됩니다. 루트 폴더에는 외부 데이터 원본에 지정 된 데이터 위치입니다.  
  
 위치를 폴더 수를 지정 하는 경우 외부 테이블에서 선택 하는 PolyBase 쿼리 폴더와 모든 하위 폴더에서 파일을 검색 합니다. Hadoop, 마찬가지로 PolyBase는 숨겨진된 폴더를 반환 하지 않습니다. 파일을 파일 이름은 밑줄 (_) 또는 마침표 (.)로 시작 반환 하지 않습니다.  
  
 이 예에서 경우 위치 ='/ webdata /', PolyBase 쿼리 mydata.txt 및 mydata2.txt에서 행을 반환 합니다.  숨겨진된 폴더의 하위 이므로 mydata3.txt을 반환 하지 않습니다. 숨겨진된 파일 이기 때문에 _hidden.txt을 반환 하지 않습니다.  
  
 ![외부 테이블에 대 한 재귀적 데이터](../../t-sql/statements/media/aps-polybase-folder-traversal.png "외부 테이블에 대 한 재귀적 데이터")  
  
 기본 및 유일한 읽기 루트 폴더에서를 변경 하려면 특성을 설정 \<polybase.recursive.traversal > 코어 site.xml 구성 파일에서 'false'에 있습니다. 이 파일은 아래에 `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`합니다. `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`)을 입력합니다.  
  
 DATA_SOURCE = *external_data_source_name*  
 외부 데이터의 위치를 포함 하는 외부 데이터 원본 이름을 지정 합니다. 이 위치는 Hadoop 또는 Azure blob 저장소입니다. 사용 하 여 외부 데이터 원본을 만들려면 [외부 데이터 원본 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 외부 데이터에 대 한 파일 형식 및 압축 방법을 저장 하는 외부 파일 형식 개체의 이름을 지정 합니다. 외부 파일 형식을 만들려면 사용 [CREATE EXTERNAL FILE FORMAT &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 거부 옵션  
 PolyBase에서 처리 하는 방법을 결정 하는 거부 매개 변수를 지정할 수 *더티* 외부 데이터 원본에서 검색을 기록 합니다. 데이터 레코드 '불량' 경우 것으로 간주 됩니다 것 실제 데이터 형식 또는 열 수가 외부 테이블의 열 정의 일치 하지 않습니다.  
  
 지정 하지 않거나 거부 값을 변경할 때 PolyBase 기본값을 사용 합니다. 거부 매개 변수에 대 한이 정보는 CREATE EXTERNAL TABLE 문을 사용 하 여 외부 테이블을 만들 때 추가 메타 데이터로 저장 됩니다.   이후 SELECT 문 또는 선택 INTO SELECT 문의 외부 테이블에서 데이터를 선택, PolyBase 수 또는 실제 쿼리 실패 하기 전에 거부 될 수 있는 행의 비율을 확인 하려면 거부 옵션을 사용 합니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다. 거부 임계값이 초과 되 면; 쿼리 (부분) 결과 반환 합니다. 그런 다음 적절 한 오류 메시지와 함께 실패합니다.  
  
 REJECT_TYPE = **값** | 백분율  
 REJECT_VALUE 옵션이 리터럴 값 또는 백분율 지정 되어 있는지 여부를 명확히 보여 줍니다.  
  
 value  
 REJECT_VALUE가 백분율이 아닌 리터럴 값입니다. 거부 된 행 수를 초과 하는 경우 PolyBase 쿼리가 실패할 *reject_value*합니다.  
  
 예를 들어 경우 REJECT_VALUE 5와 REJECT_TYPE = = value, SELECT 쿼리는 5 개 행이 거부 된 후 실패 한 PolyBase입니다.  
  
 백분율  
 REJECT_VALUE은 리터럴 값이 아닌 백분율로 표시 됩니다. 시기는 PolyBase 쿼리가 실패 합니다는 *백분율* 가 실패 한 행 개수를 초과 *reject_value*합니다. 실패 한 행의 백분율 간격으로 계산 됩니다.  
  
 REJECT_VALUE = *reject_value*  
 쿼리가 실패 하기 전에 거부 될 수 있는 행의 비율 또는 값을 지정 합니다.  
  
 REJECT_TYPE에 대해 = value, *reject_value* 0에서 2,147,483,647 사이의 정수 여야 합니다.  
  
 REJECT_TYPE = 백분율 *reject_value* 은 float 0에서 100 사이 여야 합니다.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 이 특성은 REJECT_TYPE을 지정 하는 경우 필요 = 백분율입니다. PolyBase는 다시 거부 된 행의 비율을 계산 하기 전에 검색을 시도 하는 행 수를 결정 합니다.  
  
 *reject_sample_value* 매개 변수는 0에서 2,147,483,647 사이의 정수 여야 합니다.  
  
 예를 들어 경우 REJECT_SAMPLE_VALUE = 1000, 외부 데이터 파일에서 1000 개의 행을 가져오려면 시도한 후 PolyBase가 실패 한 행의 비율을 계산 합니다. 실패 한 행의 비율이 하는 경우 보다 작은 *reject_value*, PolyBase를 다른 1000 개의 행을 검색 하려고 합니다. 각 추가 행이 1000 개를 가져오려는 시도가 실패 한 행의 비율을 다시 계산을 계속 합니다.  
  
> [!NOTE]  
>  실패 한 행의 실제 비율을 초과할 수 있습니다 PolyBase 간격으로 실패 한 행의 비율을 계산, 이후 *reject_value*합니다.  
  
 예:  
  
 이 예제는 세 가지 거부 옵션이 서로 상호 작용 하는 방법을 보여 줍니다. 예를 들어 경우 REJECT_TYPE = 백분율, REJECT_VALUE = 30 및 REJECT_SAMPLE_VALUE = 100, 다음 시나리오는 발생할 수 있습니다.  
  
-   PolyBase를; 처음 100 개의 행을 검색 하려고 합니다. 25 실패 및 75 성공 합니다.  
  
-   실패 한 행의 백분율은 30%의 거부 값 보다 작으면 25%로 계산 됩니다. 따라서 PolyBase는 외부 데이터 원본에서 데이터 검색을 계속 합니다.  
  
-   PolyBase를; 다음 100 개의 행을 로드 하려고 합니다. 이 시간 25에 성공 하 고 75 실패 합니다.  
  
-   실패 한 행의 %50 %로 다시 계산 됩니다. 실패 한 행의 비율 30% 거부 값을 초과 했습니다.  
  
-   PolyBase 쿼리가 처음 200 개 행을 반환 하려고 시도한 후 50% 거부 행과 함께 실패 합니다. PolyBase 쿼리 전에 반환 된 행이 일치 하는 참고 거부 임계값이 초과 되 감지 합니다.  
  
 분할 된 외부 테이블 옵션  
 외부 데이터 원본 (SQL Server 이외 데이터 원본) 및 배포 방법에 대 한 지정 된 [탄력적 데이터베이스 쿼리](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)합니다.  
  
 DATA_SOURCE  
 Hadoop 파일 시스템을 Azure blob 저장소에 저장 된 데이터와 같은 외부 데이터 원본 또는 [shard map manager](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/)합니다.  
  
 SCHEMA_NAME  
 SCHEMA_NAME 절에는 원격 데이터베이스에서 다른 스키마에서 테이블을 외부 테이블 정의 매핑할 수가 있습니다. 이 사용 하 여 로컬 및 원격 데이터베이스에 존재 하는 스키마를 구분 합니다.  
  
 OBJECT_NAME  
 OBJECT_NAME 절에는 원격 데이터베이스에서 다른 이름으로 테이블에 외부 테이블 정의 매핑할 수가 있습니다. 이 사용 하 여 로컬 및 원격 데이터베이스에 존재 하는 개체 이름을 구분 합니다.  
  
 배포  
 (선택 사항) 이만 SHARD_MAP_MANAGER 형식의 데이터베이스에만 필요 합니다. 이 테이블은 분할 된 테이블 또는 복제 된 테이블으로 간주 됩니다 있는지 여부를 제어 합니다. 와 **SHARDED** (*열 이름*) 테이블을 다른 테이블의 데이터를에서 겹치지 않습니다. **복제** 테이블 모든 분할 영역에 동일한 데이터를 포함 하도록 지정 합니다. **ROUND_ROBIN** 데이터 배포 하는 응용 프로그램별 메서드 사용 됨을 나타냅니다.  
  
## <a name="permissions"></a>Permissions  
 이러한 사용자 권한이 필요합니다.  
  
-   **CREATE TABLE**  
  
-   **모든 스키마 변경**  
  
-   **모든 외부 데이터 원본 변경**  
  
-   **외부 파일 형식 변경**  

-   **제어 데이터베이스**
  
 참고, 외부 데이터 원본이 생성 하는 로그인에는 Hadoop 또는 Azure blob 저장소에 있는 외부 데이터 소스를 읽고 쓸 수 있는 권한이 있어야 합니다.  


 > [!IMPORTANT]  

>  ALTER ANY EXTERNAL DATA SOURCE 사용 권한을 부여의 보안 주체를 만들고 모든 외부 데이터 원본 개체를 수정 하는 기능 하 고 따라서 데이터베이스의 모든 데이터베이스 범위 자격 증명에 액세스할 수 있도록도 부여 합니다. 높은 권한이 있지만 고 따라서에서 부여 해야 신뢰할 수 있는 보안 주체에만 시스템에는이 사용 권한을 고려 되어야 합니다.

## <a name="error-handling"></a>오류 처리  
 CREATE EXTERNAL TABLE 문을 실행 하는 동안 PolyBase가 외부 데이터 원본에 연결 하려고 합니다. 연결 시도가 실패 하면 문이 실패 하 고 외부 테이블 생성 되지 않습니다. PolyBase 쿼리 결국 실패 하기 전에 연결을 다시 시도 하므로 실패 명령에 따라 몇 분 정도 걸릴 수 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 즉, 선택에서 외부 테이블, 임시 쿼리 시나리오 PolyBase 임시 테이블에서 외부 데이터 원본에서 검색 한 행을 저장 합니다. 하면 쿼리 완료 후 PolyBase를 제거 하 고 임시 테이블을 삭제 합니다. 영구 데이터가 없는 SQL 테이블에 저장 됩니다.  
  
 반면, 가져오기 시나리오 즉, 선택에 외부 테이블에서에서 PolyBase SQL 테이블의 데이터가 영구적으로 외부 데이터 원본에서 검색 한 행을 저장 합니다. 새 테이블은 외부 데이터를 검색 하는 Polybase 쿼리 실행 중 생성 됩니다.  
  
 PolyBase 쿼리 성능을 향상 시키려면 Hadoop으로 쿼리 계산 중 일부를 푸시할 수 있습니다. 이 조건자 푸시 다운이 호출 됩니다. 이러한 기능을 제공 하려면에서 Hadoop 리소스 관리자 위치 옵션을 지정 [외부 데이터 원본 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 같거나 다른 외부 데이터 원본 참조 하는 다양 한 외부 테이블을 만들 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 C t p 2를 내보내기 기능은 지원 되지 않습니다, 즉, 영구적으로 SQL 데이터를 저장 하는 외부 데이터 원본. 이 기능은 c t p 3에서 사용할 수 있습니다.  
  
 외부 테이블에 대 한 데이터 어플라이언스에 오프 있으므로 것 PolyBase 제어 하지 않는 및 수 변경 하거나 제거할 수 언제 든 지 외부 프로세스에 의해 합니다. 이 때문에 외부 테이블에 대 한 쿼리 결과를 명확 하 게 보장 되지 않습니다. 동일한 쿼리에서 외부 테이블에 대해 실행 될 때마다 다른 결과 반환할 수 있습니다. 마찬가지로, 쿼리는 외부 데이터를 제거 하거나 위치를 변경 하는 경우 실패할 수 있습니다.  
  
 다른 외부 데이터 소스를 참조 각각 여러 외부 테이블을 만들 수 있습니다. 그러나 다른 Hadoop 데이터 원본에 대 한 쿼리를 동시에 실행 하는 경우 다음 각 Hadoop 소스 해야 동일한 'hadoop c 서버 구성 설정을 사용 합니다. 예를 들어 실행할 수 없습니다 동시에 쿼리 Cloudera Hadoop 클러스터 및 Hortonworks Hadoop 클러스터에 대 한 이후 이러한 사용 하 여 다양 한 구성 설정. 구성 설정 및 지원 되는 조합에 대 한 참조 [PolyBase Connectivity configuration&#40; Transact SQL &#41; ](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 외부 테이블에 이러한 데이터 정의 언어 (DDL) 문은 허용 됩니다.  
  
-   CREATE TABLE 및 DROP TABLE  
  
-   CREATE STATISTICS 및 통계 삭제  
  
-   보기 만들기 및 DROP VIEW  
  
 구문 및 작업이 지원 되지 않습니다.  
  
-   외부 테이블 열에 DEFAULT 제약 조건  
  
-   Delete, insert 및 update의 데이터 조작 언어 (DML) 작업  
  
 쿼리 제한 사항:  
  
 PolyBase 32 동시 PolyBase 쿼리를 실행 하는 경우 최대 폴더당 33 k 파일을 사용할 수 있습니다. 이 최대 수에 각 HDFS 폴더에서 파일 및 하위 폴더를 모두 포함 됩니다. 동시성 수준을 32 보다 작은 경우 사용자는 HDFS 33 개 이상의 k 파일이 들어 있는 폴더에 대해 PolyBase 쿼리를 실행할 수 있습니다. 외부 파일 경로 짧게 유지 HDFS 폴더 당 30 개 이하의 k 파일을 사용 하는 것이 좋습니다. 너무 많은 파일 참조 되는 가상 컴퓨터 JVM (Java) 메모리 부족 예외가 발생할 수 있습니다.  

표 너비 제한 사항: SQL Server 2016의 PolyBase는 32KB 테이블 정의 의해 단일 유효한 행의 최대 크기에 따라 행 너비 제한 합니다. 열 스키마의 합 32KB 보다 크면, PolyBase는 데이터를 쿼리할 수 없습니다. 

SQL 데이터 웨어하우스에이 제한 사항은 1MB로 변경 되었습니다.


## <a name="locking"></a>잠금  
 SCHEMARESOLUTION 개체에 대 한 잠금을 공유합니다.  
  
## <a name="security"></a>보안  
 외부 테이블에 대 한 데이터 파일은 Hadoop 또는 Azure blob 저장소에 저장 됩니다. 이러한 데이터 파일 생성 및 사용자 고유의 프로세스에 의해 관리 됩니다. 프로그램 외부 데이터의 보안을 관리 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>1. 구분 된 텍스트 형식에서 데이터가 포함 된 외부 테이블 만들기  
 이 예제에서는 외부 텍스트 구분 파일에서 서식이 지정 된 데이터가 있는 테이블을 만드는 데 필요한 모든 단계를 보여 줍니다. 외부 데이터 원본 정의 *mydatasource* 및 외부 파일 형식 *myfileformat*합니다. 이 데이터베이스 수준 개체는 CREATE EXTERNAL TABLE 문에서 다음 참조 됩니다. 자세한 내용은 참조 [외부 데이터 원본 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) 및 [외부 파일 형식 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>2. RCFile 형식에서 데이터가 포함 된 외부 테이블 만들기  
 이 예에서는 데이터 RCFiles 서식이 포함 된 외부 테이블을 만드는 데 필요한 모든 단계를 보여 줍니다. 외부 데이터 원본 정의 *mydatasource_rc* 및 외부 파일 형식 *myfileformat_rc*합니다. 이 데이터베이스 수준 개체는 CREATE EXTERNAL TABLE 문에서 다음 참조 됩니다. 자세한 내용은 참조 [외부 데이터 원본 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) 및 [외부 파일 형식 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT = RCFILE,  
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
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>3. ORC 형식에서 데이터가 포함 된 외부 테이블 만들기  
 이 예에서는 외부 테이블 형식의 데이터 항목이 자기 ORC 파일을 만드는 데 필요한 모든 단계를 보여 줍니다. 외부 데이터 원본 mydatasource_orc 및 외부 파일 형식 myfileformat_orc를 정의합니다. 이 데이터베이스 수준 개체는 CREATE EXTERNAL TABLE 문에서 다음 참조 됩니다. 자세한 내용은 참조 [외부 데이터 원본 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md) 및 [외부 파일 형식 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
 클릭 동향은 Hadoop 클러스터에서 employee.tbl 구분 기호로 분리 된 텍스트 파일에 연결 된 외부 테이블입니다. 다음 쿼리는 표준 테이블에 대 한 쿼리와 마찬가지로 검색합니다. 그러나이 쿼리는 Hadoop에서 데이터를 검색 하 고 계산 하는 두.  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>5. SQL 데이터를 사용 하 여 Hadoop 데이터를 조인 합니다.  
 이 쿼리는 두 SQL 테이블에서 표준 조인와 동일 하 게 검색합니다. 차이가 PolyBase에서 Hadoop 클릭 동향 데이터를 검색 하 고 다음 UrlDescription 테이블에 조인 합니다. 하나 이상의 테이블이 외부 테이블 이며 다른 하나는 표준 SQL 테이블.  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>6. SQL 테이블에 Hadoop에서 데이터 가져오기  
 이 예제에서는 표준 SQL 테이블 간의 조인의 결과 영구적으로 저장 하는 새 SQL 테이블 ms_user *사용자* 및 외부 테이블 *클릭 동향*합니다.  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>7. 분할 된 데이터 원본에 대 한 외부 테이블 만들기  
 이 예에서는 원격 DMV를 SCHEMA_NAME 및 OBJECT_NAME 절을 사용 하 여 외부 테이블을 다시 매핑합니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>8. Azure에 ADLS에서 데이터 가져오기[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
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
  
### <a name="i-join-external-tables"></a>9. 외부 테이블을 조인  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>10. PDW 데이터로 HDFS 데이터 조인  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>11. HDFS에서 행 데이터를 분산된 PDW 테이블 가져오기  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>12. HDFS에서 복제 된 PDW 테이블 행 데이터 가져오기  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [일반적인 메타 데이터 쿼리 예제 (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [외부 TABLE AS SELECT &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [TABLE AS SELECT &#40; 만들기 Azure SQL 데이터 웨어하우스 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



