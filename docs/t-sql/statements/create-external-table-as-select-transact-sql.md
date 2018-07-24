---
title: CREATE EXTERNAL TABLE AS SELECT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.component: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- CREATE EXTERNAL TABLE AS SELECT
- CREATE_EXTERNAL_TABLE_AS_SELECT
- CREATE EXTERNAL TABLE AS SELECT_TSQL
helpviewer_keywords:
- External, table
- PolyBase, external table
- External, table create as select
- PolyBase, create table as select
ms.assetid: 32dfe254-6df7-4437-bfd6-ca7d37557b0a
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 74dc570a61b33aa6b6a2718bde3c927e6eabb1a7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38017513"
---
# <a name="create-external-table-as-select-transact-sql"></a>CREATE EXTERNAL TABLE AS SELECT(Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  외부 테이블을 만든 다음, [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 문의 결과를 Hadoop 또는 Azure Storage Blob에 병렬로 내보냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE EXTERNAL TABLE [ [database_name  . [ schema_name ] . ] | schema_name . ] table_name   
    WITH (   
        LOCATION = 'hdfs_folder',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
    AS <select_statement>  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
}  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>인수  
 [ [ *database_name* . [ *schema_name* ] . ] | *schema_name* . ] *table_name*  
 데이터베이스에 만들려는 테이블의 한 부분에서 세 부분으로 이루어진 이름입니다. 외부 테이블의 경우 테이블 메타데이터만 관계형 데이터베이스에 저장됩니다.  
  
 LOCATION =  '*hdfs_folder*'  
 SELECT 문의 결과를 외부 데이터 원본에 기록할 위치를 지정합니다. 위치는 폴더 이름이며 선택적으로 Hadoop 클러스터 또는 Azure Storage Blob의 루트 폴더에 대한 상대 경로를 포함합니다.  PolyBase는 아직 존재하지 않는 경우 경로 및 폴더를 만듭니다.  
  
 외부 파일은 *hdfs_folder*에 기록되고 *QueryID_date_time_ID.format*로 명명되며, 여기서 *ID*는 증분 식별자이고 *format*은 내보낸 데이터 형식입니다. 예를 들어 QID776_20160130_182739_0.orc입니다.  
  
 DATA_SOURCE = *external_data_source_name*  
 외부 데이터가 저장된 또는 저장될 위치를 포함하는 외부 데이터 원본 개체의 이름을 지정합니다. 위치는 Hadoop 클러스터 또는 Azure Storage Blob 중 하나입니다. 외부 데이터 원본을 만들려면 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)을 사용합니다.  
  
 FILE_FORMAT = *external_file_format_name*  
 외부 데이터 파일에 대한 형식을 포함하는 외부 파일 형식 개체의 이름을 지정합니다. 외부 파일 형식을 만들려면 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)을 사용합니다.  
  
 거부 옵션  
 거부 옵션은 이 CREATE EXTERNAL TABLE AS SELECT 문이 실행될 때 적용되지 않습니다. 그 대신, 나중에 데이터베이스가 외부 테이블에서 데이터를 가져올 때 사용할 수 있도록 여기에 지정됩니다. 나중에 CREATE TABLE AS SELECT 문이 외부 테이블에서 데이터를 선택할 때 데이터베이스는 거부 옵션을 사용하여 가져오기를 중지하는 기준이 되는 가져오기 실패의 행 수 또는 백분율을 결정합니다.  
  
 REJECT_VALUE = *reject_value*  
 데이터베이스가 가져오기를 중지하는 기준이 되는 가져오기 실패 값 또는 행 수를 지정합니다.  
  
 REJECT_TYPE = **value** | percentage  
 REJECT_VALUE 옵션이 리터럴 값으로 지정되는지 또는 백분율로 지정되는지 구체화합니다.  
  
 value  
 REJECT_VALUE는 백분율이 아닌 리터럴 값입니다.  데이터베이스는 실패한 행 수가 *reject_value*를 초과하면 외부 데이터 파일에서 행 가져오기를 중지합니다.  
  
 예를 들어 REJECT_VALUE = 5이고 REJECT_TYPE = value인 경우, 데이터베이스는 행 가져오기에 5번 실패한 후 행 가져오기를 중지합니다.  
  
 percentage  
 REJECT_VALUE는 리터럴 값이 아닌 백분율입니다. 데이터베이스는 실패한 행의 *백분율*이 *reject_value*를 초과하는 경우 외부 데이터 파일에서 행 가져오기를 중지합니다. 실패한 행의 백분율은 일정 간격으로 계산됩니다.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 이 속성은 REJECT_TYPE = percentage일 때 필요하며 데이터베이스가 실패한 행 백분율의 다시 계산을 시도하는 행 수를 지정합니다.  
  
 예를 들어 REJECT_SAMPLE_VALUE = 1000인 경우, 데이터베이스는 외부 데이터 파일에서 행 1000개 가져오기를 시도한 후 실패한 행의 백분율을 계산합니다. 실패한 행의 백분율이 *reject_value*보다 작은 경우, 데이터베이스는 또 다른 행 1000개의 로드를 시도합니다. 계속해서 데이터베이스는 추가로 행 1000개의 가져오기를 시도한 후마다 실패한 행의 백분율을 다시 계산합니다.  
  
> [!NOTE]  
>  데이터베이스는 실패한 행의 백분율을 일정 간격으로 계산하므로 실패한 행의 실제 백분율은 *reject_value*를 초과할 수 있습니다.  
  
 예:  
  
 이 예제에서는 REJECT 옵션 세 개가 서로 상호 작용하는 방법을 보여 줍니다. 예를 들어 REJECT_TYPE = percentage, REJECT_VALUE = 30 및 REJECT_SAMPLE_VALUE = 100인 경우 다음과 같은 시나리오가 일어날 수 있습니다.  
  
-   데이터베이스가 처음 100개 행의 로드를 시도하며, 25개가 실패하고 75개가 성공합니다.  
  
-   실패한 행의 백분율은 25%로 계산되며, 이는 거부 값 30%보다 작습니다. 따라서 로드를 중지할 필요가 없습니다.  
  
-   데이터베이스는 다음 100개 행의 로드를 시도하며, 이번에는 25개가 성공하고 75개가 실패합니다.  
  
-   실패한 행의 백분율은 50%로 다시 계산됩니다. 실패한 행의 이 백분율은 30% 거부 값을 초과했습니다.  
  
-   행 200개의 로드를 시도한 후 실패한 행이 50%이고, 이는 지정된 30% 한도보다 크므로 로드가 실패합니다.  
  
 WITH *common_table_expression*  
 CTE(공통 테이블 식)라고도 하는 임시로 이름이 지정된 결과 집합을 지정합니다. 자세한 내용은 [WITH common_table_expression&#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)을 참조하세요.  
  
 SELECT \<select_criteria> 새 테이블을 SELECT 문의 결과로 채웁니다. *select_criteria*는 새 테이블에 복사할 데이터를 결정하는 SELECT 문의 본문입니다. SELECT 문에 대한 자세한 내용은 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)을 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 이 명령을 실행하려면 **데이터베이스 사용자**는 다음 권한 또는 멤버 자격이 모두 필요합니다.  
  
-   **db_ddladmin** 고정 데이터베이스 역할에 새 테이블 또는 멤버 자격을 포함할 로컬 스키마에 대한 **ALTER SCHEMA** 권한.  
  
-   **db_ddladmin** 고정 데이터베이스 역할의 **CREATE TABLE** 권한 또는 멤버 자격.  
  
-   *select_criteria*에 참조된 임의의 개체에 대한 **SELECT** 권한.  
  
 로그인하려면 다음 권한이 모두 필요합니다.  
  
-   **ADMINISTER BULK OPERATIONS** 권한  
  
-   **ALTER ANY EXTERNAL DATA SOURCE** 권한  
  
-   **ALTER ANY EXTERNAL FILE FORMAT** 권한  
  
-   로그인하려면 Hadoop 클러스터 또는 Azure Storage Blob의 외부 폴더를 읽고 쓰기 위한 쓰기 권한을 가지고 있어야 합니다.  
 
 > [!IMPORTANT]  
 >  ALTER ANY EXTERNAL DATA SOURCE 권한은 보안 주체에 대해 외부 데이터 원본 개체를 만들고 수정하는 권한을 부여하며, 따라서 데이터베이스의 모든 데이터베이스 범위 자격 증명에 액세스하는 권한도 부여합니다. 이 권한은 높은 수준의 권한으로 간주되어야 하므로, 시스템의 신뢰할 수 있는 보안 주체에만 부여되어야 합니다.
  
## <a name="error-handling"></a>오류 처리  
 CREATE EXTERNAL TABLE AS SELECT가 데이터를 텍스트로 분리된 파일로 내보내는 경우 내보내기에 실패한 행에 대한 거부 파일이 없습니다.  
  
 외부 테이블을 만들 때 데이터베이스는 외부 Hadoop 클러스터 또는 Azure Storage Blob에 연결을 시도합니다. 연결이 실패하면 명령이 실패하고 외부 테이블이 만들어지지 않습니다. 데이터베이스는 연결을 최소 3회 다시 시도하므로 이 명령이 실패하려면 1분 이상 걸릴 수 있습니다.  
  
 CREATE EXTERNAL TABLE AS SELECT이 취소되거나 실패하면 데이터베이스는 외부 데이터 원본에 이미 만들어진 새 파일 및 폴더의 제거를 한 번 시도합니다.  
  
 데이터베이스는 데이터 가져오기 중에 외부 데이터 원본에서 발생한 모든 Java 오류를 보고합니다.  
  
##  <a name="GeneralRemarks"></a> 일반적인 주의 사항  
 CETAS 문이 완료된 후 외부 테이블에 대해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행할 수 있습니다. 이러한 작업은 CREATE TABLE AS SELECT 문을 사용하여 가져오지 않는 한 쿼리 기간 동안 데이터를 데이터베이스로 가져옵니다.  
  
 외부 테이블 이름과 정의는 데이터베이스 메타데이터에 저장됩니다. 데이터는 외부 데이터 원본에 저장됩니다.  
  
 외부 파일의 이름은 *QueryID_date_time_ID.format*입니다. 여기서 *ID* 는 증분 식별자이고 *형식* 은 내보낸된 데이터 형식입니다. 예를 들어 QID776_20160130_182739_0.orc입니다.  
  
 CETAS 문은 원본 테이블이 분할되었더라도 언제나 분할되지 않은 테이블을 만듭니다.  
  
 EXPLAIN으로 만든 쿼리 계획의 경우 데이터베이스는 다음 쿼리 계획 작업을 외부 테이블에 사용합니다.  
  
-   외부 무작위 이동  
  
-   외부 브로드캐스트 이동  
  
-   외부 파티션 이동  
  
 **적용 대상:**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]외부 테이블을 만들기 위한 필수 구성 요소로서, 어플라이언스 관리자는 Hadoop 연결을 구성해야 합니다. 자세한 내용은 [여기](http://www.microsoft.com/download/details.aspx?id=48241)서 다운로드할 수 있는 APS 설명서의 외부 데이터 연결 구성(분석 플랫폼 시스템)을 참조하세요.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 외부 테이블 데이터는 데이터베이스 외부에 상주하므로 백업 및 복원 작업은 데이터베이스에 저장된 데이터에 대해서만 작동합니다. 즉, 메타데이터만 백업 및 복원됩니다.  
  
 데이터베이스는 외부 테이블이 포함된 데이터베이스 백업을 복원할 때 외부 데이터 원본에 대한 연결을 확인하지 않습니다. 원래 원본에 액세스할 수 없더라도 외부 테이블의 메타데이터 복원은 여전히 성공하지만 외부 테이블에 대한 SELECT 작업은 실패합니다.  
  
 데이터베이스는 데이터베이스와 외부 데이터 간의 데이터 일관성을 보장하지 않습니다. 고객만이 외부 데이터와 데이터베이스 간의 일관성을 유지할 책임이 있습니다.  
  
 DML(데이터 조작 언어) 작업은 외부 테이블에 대해서는 지원되지 않습니다. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 업데이트, 삽입 또는 삭제[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 외부 데이터를 수정할 수 없습니다.  
  
 CREATE TABLE, DROP TABLE, CREATE STATISTICS, DROP STATISTICS, CREATE VIEW 및 DROP VIEW는 외부 테이블에 대해서만 허용되는 DDL(데이터 정의 언어) 작업입니다.  
  
 PolyBase는 32개의 동시 PolyBase 쿼리를 실행할 때 폴더당 최대 3만 3천 개의 파일을 사용할 수 있습니다. 이 최대 개수는 각 HDFS 폴더의 파일과 하위 폴더를 모두 포함합니다. 동시성 수준이 32보다 작은 경우 사용자는 3만 3천 개보다 많은 파일을 포함하는 HDFS의 폴더에 대해 PolyBase 쿼리를 실행할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 Hadoop 및 PolyBase 사용자에 대해 파일 경로를 짧게 유지하고 HDFS 폴더당 3만 개 이하의 파일을 사용할 것을 권장합니다. 너무 많은 파일이 참조되면 JVM 메모리 부족 예외가 발생할 수 있습니다.  
  
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)은 이 CREATE EXTERNAL TABLE AS SELECT에 아무런 영향도 주지 않습니다. 비슷한 동작을 얻으려면 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)를 사용합니다.  
  
 CREATE EXTERNAL TABLE AS SELECT가 RCFile에서 선택하는 경우 RCFile의 열 값은 파이프 문자 '|'를 포함하지 않아야 합니다.  
  
## <a name="locking"></a>잠금  
 SCHEMARESOLUTION 개체에 대한 공유 잠금을 실행합니다.  
  
##  <a name="Examples"></a> 예  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>1. CREATE EXTERNAL TABLE AS SELECT(CETAS)를 사용하여 Hadoop 테이블 만들기  
 다음 예제에서는 원본 테이블 `dimCustomer`의 열 정의 및 데이터를 사용하여 `hdfsCustomer`라는 새 외부 테이블을 만듭니다.  
  
 테이블 정의는 데이터베이스에 저장되며 SELECT 문의 결과를 Hadoop 외부 데이터 원본 *customer_ds*의 '/pdwdata/customer.tbl' 파일로 내보냅니다. 파일은 외부 파일 형식 *customer_ff*에 따라 서식 지정됩니다.  
  
 파일 이름은 데이터베이스에 의해 생성되며 파일을 생성한 쿼리와 파일을 정렬하기 쉽도록 쿼리 ID를 포함합니다.  
  
 Customer 디렉터리 앞의 경로 `hdfs://xxx.xxx.xxx.xxx:5000/files/`는 이미 존재합니다. 그러나 Customer 디렉터리가 존재하지 않는 경우 데이터베이스에서 해당 디렉터리를 생성합니다.  
  
> [!NOTE]  
>  이 예제에서는 5000을 지정합니다. 포트가 지정되지 않은 경우 데이터베이스에서 8020을 기본 포트로 사용합니다.  
  
 결과 Hadoop 위치 및 파일 이름은 `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`입니다.  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>2. CREATE EXTERNAL TABLE AS SELECT(CETAS)와 함께 쿼리 힌트 사용  
 이 쿼리는 CETAS 문에 쿼리 조인 힌트를 사용하는 기본 구문을 보여줍니다. 쿼리가 제출된 후 데이터베이스는 해시 조인 방법을 사용하여 쿼리 계획을 생성합니다. 조인 힌트 및 OPTION 절을 사용하는 방법에 대한 자세한 내용은 [OPTION 절&#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
>  이 예제에서는 5000을 지정합니다. 포트가 지정되지 않은 경우 데이터베이스에서 8020을 기본 포트로 사용합니다.  
  
```  
  
      -- Example is based on AdventureWorks  
CREATE EXTERNAL TABLE dbo.FactInternetSalesNew  
WITH   
    (   
        LOCATION = '/files/Customer',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
    )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE TABLE &#40;Azure SQL Data Warehouse, 병렬 데이터 웨어하우스&#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  


