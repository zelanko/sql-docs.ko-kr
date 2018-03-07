---
title: "외부 TABLE AS SELECT (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f2ca379cf30fe2e7d359a294a18804f0b5e6faeb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="create-external-table-as-select-transact-sql"></a>외부 TABLE AS SELECT (Transact SQL) 만들기
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  외부 테이블을 만들고 내보내므로, 병렬로 결과 [!INCLUDE[tsql](../../includes/tsql-md.md)] Hadoop 또는 Azure 저장소 Blob을 SELECT 문의 합니다.  
  
 만들기 외부 테이블 AS 선택 (CETAS) 문을 사용 합니다.  
  
-   Hadoop 또는 Azure blob 저장소를 데이터베이스 테이블을 내보냅니다.  
  
-   Hadoop 또는 Azure blob 저장소에서 데이터를 가져와서 데이터베이스에 저장 합니다.  
  
-   Hadoop 또는 Azure blob 저장소에서 데이터를 쿼리하고 관계형 테이블에 데이터베이스를 사용 하 여 조인 Hadoop 또는 Azure blob 저장소에 다시 결과 기록 합니다.  
  
-   Hadoop 또는 Azure blob 저장소에서 데이터를 쿼리하고 데이터베이스의 빠른 처리 기능을 사용 하 여 변환 Hadoop 또는 Azure blob 저장소에 다시 써야 합니다.  
  
 자세한 내용은 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [[ *database_name* 합니다. [ *schema_name* ] . ] | *schema_name* . ] *table_name*  
 데이터베이스에서 만들 테이블의 부분 이름 1 ~ 3 년. 따라서 외부 테이블에 대 한 테이블 메타 데이터는 관계형 데이터베이스에 저장 됩니다.  
  
 LOCATION =  '*hdfs_folder*'  
 외부 데이터 원본에 SELECT 문의 결과 쓸 위치를 지정 합니다. 위치 폴더 이름 인지 그리고 Hadoop 클러스터 또는 Azure 저장소 Blob의 루트 폴더의 상대 경로 포함 될 수 있습니다.  PolyBase 이미 존재 하지 않는 경우 경로 및 폴더 만들어집니다.  
  
 외부 파일에 기록 됩니다 *hdfs_folder* 및 명명 된 *QueryID_date_time_ID.format*여기서 *ID* 는 증분 식별자 및 *형식* 내보낸된 데이터 형식입니다. 예를 들어 QID776_20160130_182739_0.orc입니다.  
  
 DATA_SOURCE = *external_data_source_name*  
 외부 데이터 저장 되거나 저장 될 위치를 포함 하는 외부 데이터 원본 개체의 이름을 지정 합니다. 위치는 Hadoop 클러스터 또는 Azure 저장소 Blob 중 하나입니다. 사용 하 여 외부 데이터 원본을 만들려면 [외부 데이터 원본 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 외부 데이터 파일의 형식을 포함 하는 외부 파일 형식 개체의 이름을 지정 합니다. 외부 파일 형식을 만들려면 사용 [CREATE EXTERNAL FILE FORMAT &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 거부 옵션  
 이 CREATE EXTERNAL TABLE AS SELECT 문이 실행 되는 시간에는 거부 옵션이 적용 되지 않습니다. 대신, 이러한 여기에 지정 된 데이터베이스 외부 테이블의 데이터를 가져올 때 나중에 사용할 수 있도록 합니다. 이상에서는 CREATE TABLE AS SELECT 문이 외부 테이블의 데이터를 선택 데이터베이스는 가져오기 중지 하기 전에 가져오지 못할 수 있는 행의 백분율이 나 수를 확인 하려면 거부 옵션을 사용 합니다.  
  
 REJECT_VALUE = *reject_value*  
 데이터베이스 가져오기 중지 하기 전에 가져오기에 실패할 수 있는 행의 비율 또는 값을 지정 합니다.  
  
 REJECT_TYPE = **값** | 백분율  
 REJECT_VALUE 옵션이 리터럴 값 또는 백분율 지정 되어 있는지 여부를 명확히 보여 줍니다.  
  
 value  
 REJECT_VALUE가 백분율이 아닌 리터럴 값입니다.  실패 한 행의 수를 초과 하는 경우 외부 데이터 파일에서 행을 가져올 데이터베이스는 중지 *reject_value*합니다.  
  
 예를 들어 경우 REJECT_VALUE 5와 REJECT_TYPE = = value, 데이터베이스를 가져오려면 5 개 행 실패 후 행 가져오기 중지 됩니다.  
  
 백분율  
 REJECT_VALUE은 리터럴 값이 아닌 백분율로 표시 됩니다. 데이터베이스 외부에서 행 가져오기 중지 됩니다 때 데이터 파일의 *백분율* 가 실패 한 행 개수를 초과 *reject_value*합니다. 실패 한 행의 백분율 간격으로 계산 됩니다.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 경우에 필수 REJECT_TYPE = 백분율, 데이터베이스 다시 실패 한 행의 비율을 계산 하기 전에 가져오기를 시도할 행 수를 지정 합니다.  
  
 예를 들어 경우 REJECT_SAMPLE_VALUE = 1000, 데이터베이스 외부 데이터 파일에서 1000 개의 행을 가져오려면 시도한 후 실패 한 행의 비율을 계산 합니다. 실패 한 행의 비율이 하는 경우 보다 작은 *reject_value*, 데이터베이스는 다른 1000 개의 행을 로드 하려고 시도 합니다. 데이터베이스는 계속 각 추가 행이 1000 개를 가져오려는 시도가 실패 한 행의 비율을 다시 계산 합니다.  
  
> [!NOTE]  
>  실패 한 행의 실제 비율을 초과할 수 있습니다 간격으로 실패 한 행의 비율을 계산 하는 데이터베이스를 이후 *reject_value*합니다.  
  
 예:  
  
 이 예제는 세 가지 거부 옵션이 서로 상호 작용 하는 방법을 보여 줍니다. 예를 들어 경우 REJECT_TYPE = 백분율, REJECT_VALUE = 30 및 REJECT_SAMPLE_VALUE = 100, 다음 시나리오는 발생할 수 있습니다.  
  
-   데이터베이스를 처음 100 개 행; 로드 하려고 합니다. 25 실패 및 75 성공 합니다.  
  
-   실패 한 행의 백분율은 30%의 거부 값 보다 작으면 25%로 계산 됩니다. 따라서 부하를 중단할 필요가 없습니다.  
  
-   데이터베이스를 다음 100 개의 행;을 로드 하려고 합니다. 이 시간 25에 성공 하 고 75 실패 합니다.  
  
-   실패 한 행의 %50 %로 다시 계산 됩니다. 실패 한 행의 비율 30% 거부 값을 초과 했습니다.  
  
-   로드 실패 하지 못했습니다 50% 행 200 개의 행을 로드 하려고 시도한 후 지정된 된 30% 제한 보다 큰 합니다.  
  
 WITH *common_table_expression*  
 CTE(공통 테이블 식)라고도 하는 임시로 이름이 지정된 결과 집합을 지정합니다. 자세한 내용은 참조 [common_table_expression &AMP;#40; Transact SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 선택 \<select_criteria > SELECT 문에서 결과 함께 새 테이블을 채웁니다. *select_criteria* 데이터를 새 테이블로 복사를 결정 하는 SELECT 문의 본문입니다. SELECT 문에 대 한 정보를 참조 하십시오. [select&#40; Transact SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 이 명령을 실행 하는 **데이터베이스 사용자** 모두 이러한 사용 권한 또는 멤버 자격이 필요 합니다.  
  
-   **ALTER SCHEMA** 새 테이블 또는의 멤버 자격이 포함 될 로컬 스키마에 대 한 권한이 **db_ddladmin** 고정된 데이터베이스 역할입니다.  
  
-   **CREATE TABLE** 권한이 나 멤버 자격에는 **db_ddladmin** 고정된 데이터베이스 역할입니다.  
  
-   **선택** 권한에서 참조 되는 개체에 대해서는 *select_criteria*합니다.  
  
 로그인에는 이러한 모든 권한이 필요합니다.  
  
-   **ADMINISTER BULK OPERATIONS** 사용 권한  
  
-   **ALTER ANY EXTERNAL DATA SOURCE** 사용 권한  
  
-   **ANY EXTERNAL FILE FORMAT ALTER** 사용 권한  
  
-   로그인에 읽기 및 쓰기 외부 폴더에는 Hadoop 클러스터 또는 Azure 저장소 Blob에 쓰기 권한이 있어야 합니다.  
 
 > [!IMPORTANT]  
 >  ALTER ANY EXTERNAL DATA SOURCE 사용 권한을 부여의 보안 주체를 만들고 모든 외부 데이터 원본 개체를 수정 하는 기능 하 고 따라서 데이터베이스의 모든 데이터베이스 범위 자격 증명에 액세스할 수 있도록도 부여 합니다. 높은 권한이 있지만 고 따라서에서 부여 해야 신뢰할 수 있는 보안 주체에만 시스템에는이 사용 권한을 고려 되어야 합니다.
  
## <a name="error-handling"></a>오류 처리  
 텍스트 구분 파일 데이터를 내보내는 CREATE EXTERNAL TABLE AS SELECT, 경우에 내보내기에 실패 하는 행에 대 한 거부 파일이 없습니다.  
  
 외부 테이블을 만들 때 데이터베이스 외부의 Hadoop 클러스터 또는 Azure 저장소 Blob에 연결 하려고 합니다. 연결에 실패 하면 명령이 실패 하 고 외부 테이블 생성 되지 않습니다. 명령이 연결 3 배 이상 이후 데이터베이스 다시 시도가 실패 하는 몇 분 정도 걸릴 수 있습니다.  
  
 CREATE EXTERNAL TABLE AS SELECT 취소 되거나 실패, 모든 새 파일 및 외부 데이터 원본에서 이미 만든 폴더를 제거 하려면 1 회 시도 하는 데이터베이스에 생성 됩니다.  
  
 데이터베이스에서 외부 데이터 원본에서 데이터 내보내기 중 발생 하는 모든 Java 오류를 보고 합니다.  
  
##  <a name="GeneralRemarks"></a>일반적인 주의 사항  
 실행할 수 있습니다 CETAS 문의 끝나면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 외부 테이블에 대 한 쿼리 합니다. 이러한 작업은 데이터를 가져올 데이터베이스 쿼리 기간에 대 한 CREATE TABLE AS SELECT 문을 사용 하 여 가져오지 않은 경우.  
  
 외부 테이블 이름과 정의 데이터베이스 메타 데이터에 저장 됩니다. 데이터는 외부 데이터 원본에 저장 됩니다.  
  
 외부 파일의 이름은 *QueryID_date_time_ID.format*입니다. 여기서 *ID* 는 증분 식별자이고 *형식* 은 내보낸된 데이터 형식입니다. 예를 들어 QID776_20160130_182739_0.orc입니다.  
  
 원본 테이블이 분할 된 경우에 CETAS 문은 항상 분할 되지 않은 테이블을 만듭니다.  
  
 쿼리 계획에 대 한 외부 테이블에 이러한 쿼리 계획 작업 설명는 databaseuses로 만듭니다.  
  
-   외부 순서 섞기 이동  
  
-   외부 브로드캐스트 이동  
  
-   파티션 외부 이동  
  
 **적용 대상:**[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]외부 테이블을 만들기 위한 필수 구성 요소로 기기 관리자 hadoop 연결을 구성 해야 합니다. 자세한 내용은 다운로드할 수 있는 APS 설명서에서 외부 데이터 (분석 플랫폼 시스템)에 대 한 연결을 구성을 참조 [여기](http://www.microsoft.com/download/details.aspx?id=48241)합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 외부 테이블 데이터가 있는 데이터베이스 외부에 백업 및 복원 작업은 데이터베이스에 저장 된 데이터 에서만 작동 이후 합니다. 즉, 메타 데이터를 백업 및 복원 됩니다.  
  
 데이터베이스 외부 테이블을 포함 하는 데이터베이스 백업을 복원 하는 경우 외부 데이터 원본에 대 한 연결을 확인 하지 않습니다. 원본에 액세스할 수 없는 경우 외부 테이블의 메타 데이터 복원에는 계속 성공 하지만 외부 테이블에 대 한 SELECT 작업 실패 합니다.  
  
 데이터베이스는 이름도 만들어야 외부 데이터 간의 데이터 일관성을 보장 하지 않습니다. 고객에는 외부 데이터와 데이터베이스 간의 일관성을 유지 하는 전적으로 부담 합니다.  
  
 데이터 조작 언어 (DML) 작업 외부 테이블에서 지원 되지 않습니다. 예를 들어 사용할 수 없습니다는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 업데이트, 삽입 또는 삭제 [!INCLUDE[tsql](../../includes/tsql-md.md)]외부 데이터를 수정 하는 문을 합니다.  
  
 CREATE TABLE, DROP TABLE, CREATE STATISTICS, DROP STATISTICS, 보기 만들기 및 DROP VIEW는 유일한 데이터 정의 언어 (DDL) 작업 외부 테이블에서 허용 됩니다.  
  
 PolyBase 32 동시 PolyBase 쿼리를 실행 하는 경우 최대 폴더당 33 k 파일을 사용할 수 있습니다. 이 최대 수에 각 HDFS 폴더에서 파일 및 하위 폴더를 모두 포함 됩니다. 동시성 수준을 32 보다 작은 경우 사용자는 HDFS 33 개 이상의 k 파일이 들어 있는 폴더에 대해 PolyBase 쿼리를 실행할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]Hadoop 및 PolyBase의 권장 사용자 짧은 파일 경로 유지 하 고 HDFS 폴더 당 30 개 이하의 k 파일을 사용 합니다. 너무 많은 파일이 참조 하는 경우 JVM 메모리 부족 예외가 발생 합니다.  
  
 [SET ROWCOUNT &#40; Transact SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) 이 CREATE EXTERNAL TABLE AS SELECT에 아무 효과가 없습니다. 비슷한 동작이 얻기 위해 사용 하 여 [top&#40; Transact SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 CREATE EXTERNAL TABLE AS SELECT는 RCFile에서 선택, 열 값에는 RCFile 없어야 파이프 ' |' 문자입니다.  
  
## <a name="locking"></a>잠금  
 SCHEMARESOLUTION 개체에 대 한 공유 잠금을 사용합니다.  
  
##  <a name="Examples"></a> 예  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>1. 만들 외부 테이블 AS 선택 (CETAS)를 사용 하 여 Hadoop 테이블 만들기  
 다음 예에서는 라는 새 외부 테이블을 만들어 `hdfsCustomer`, 열 정 및 원본 테이블에서에서 데이터를 사용 하 여 `dimCustomer`합니다.  
  
 테이블 정의 데이터베이스에 저장 되 고 SELECT 문의 결과를 내보내는 ' / pdwdata/customer.tbl' Hadoop 외부 데이터 원본에 대 한 파일 *customer_ds*합니다. 외부 파일 형식에 따라 파일의 형식이 *customer_ff*합니다.  
  
 파일 이름 데이터베이스에서 생성 및 생성 한 쿼리를 사용 하 여 파일을 정렬 하기 쉽도록 쿼리 ID를 포함 합니다.  
  
 경로 `hdfs://xxx.xxx.xxx.xxx:5000/files/` 고객 디렉터리 앞에 이미 존재 해야 합니다. 그러나 고객 디렉터리가 없는 경우 데이터베이스에서 디렉터리가 만들어집니다.  
  
> [!NOTE]  
>  이 예에서는 5000를 지정합니다. 포트가 지정 되지 않은 경우 데이터베이스를 기본 포트로 8020를 사용 합니다.  
  
 위치 및 파일 이름은 결과 Hadoop `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`합니다.  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>2. 외부 테이블 AS 만들기와 쿼리 힌트를 사용 하 여 선택 (CETAS)  
 이 쿼리에서 CETAS 문을 사용 하 여 쿼리 조인 힌트를 사용 하기 위한 기본 구문을 보여 줍니다. 쿼리를 제출 후 데이터베이스 해시 조인 전략을 사용 하 여 쿼리 계획을 생성 합니다. 조인 힌트와 OPTION 절을 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [OPTION 절 &#40; Transact SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
> [!NOTE]  
>  이 예에서는 5000를 지정합니다. 포트가 지정 되지 않은 경우 데이터베이스를 기본 포트로 8020를 사용 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [테이블 &#40; 만들기 Azure SQL 데이터 웨어하우스, 병렬 데이터 웨어하우스 &#41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [TABLE AS SELECT &#40; 만들기 Azure SQL 데이터 웨어하우스 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP table&#40; Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  


