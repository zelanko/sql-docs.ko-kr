---
title: sp_describe_first_result_set (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_describe_first_result_set
- sp_describe_first_result_set_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_describe_first_result_set
ms.assetid: f2355a75-3a8e-43e6-96ad-4f41038f6d22
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 90caaef639485fd44f9f715935c1eb5f08540fa0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spdescribefirstresultset-transact-sql"></a>sp_describe_first_result_set(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  가능한 첫 번째 결과 집합에 대 한 메타 데이터를 반환 합니다.는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 합니다. 일괄 처리에서 아무 결과도 반환되지 않은 경우 빈 결과 집합을 반환합니다. 오류가 발생 된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 정적 분석을 수행 하 여 실행 될 첫 번째 쿼리에 대 한 메타 데이터를 확인할 수 없습니다. 동적 관리 뷰 [sys.dm_exec_describe_first_result_set&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md) 같은 정보를 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](http://msdn.microsoft.com/library/bb500435.aspx)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_describe_first_result_set [ @tsql = ] N'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' ]   
    [ , [ @browse_information_mode = ] <tinyint> ] ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@tsql =** ] **'***Transact SQL_batch***'**  
 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. *Transact SQL_batch* 수 **nvarchar (***n***)** 또는 **nvarchar (max)**합니다.  
  
 [  **@params =** ] **N'***매개 변수***'**  
 @params에 대 한 매개 변수에 대 한 선언 문자열을 제공 된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리는 sp_executesql과 비슷하게를 합니다. 매개 변수가 필요할 수 **nvarchar (n)** 또는 **nvarchar (max)**합니다.  
  
 하나의 문자열에 포함 된 모든 매개 변수 정의 포함 하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*합니다. 문자열은 유니코드 상수 또는 유니코드 변수여야 합니다. 각 매개 변수의 정의는 매개 변수 이름과 데이터 형식으로 구성됩니다. *n*추가 매개 변수 정의 나타내는 자리 표시자가입니다. 문에 지정 된 모든 매개 변수에서 정의 되어야 합니다 @params합니다. 경우는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 문의 일괄 처리, 매개 변수가 없으면 @params 필요 하지 않습니다. NULL이 이 매개 변수의 기본값입니다.  
  
 [  **@browse_information_mode =** ] *tinyint*  
 추가 키 열과 원본 테이블 정보를 반환할지 여부를 지정합니다. 1로 설정되면 쿼리에 FOR BROWSE 옵션이 포함된 것처럼 각 쿼리가 분석됩니다. 추가 키 열과 원본 테이블 정보가 반환됩니다.  
  
-   0으로 설정되면 정보가 반환되지 않습니다.  
  
-   1로 설정되면 쿼리에 FOR BROWSE 옵션이 포함된 것처럼 각 쿼리가 분석됩니다. 그러면 원본 열 정보로 기본 테이블 이름을 반환합니다.  
  
-   2로 설정되면 쿼리에 커서 준비 또는 실행에 사용되는 것처럼 각 쿼리가 분석됩니다. 그러면 원본 열 정보로 보기 이름을 반환합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **sp_describe_first_result_set** 항상 상태를 성공 하면 0 반환 합니다. 프로시저는 오류가 발생 하는 경우 프로시저가 RPC로 호출 된 sys.dm_exec_describe_first_result_set의 error_type 열에 설명 된 오류 형식으로 반환 상태가 채워집니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 프로시저를 호출한 경우 반환 값은 오류가 발생한 경우에도 항상 0입니다.  
  
## <a name="result-sets"></a>결과 집합  
 이 공통 메타데이터는 결과 메타데이터의 각 열에 대한 하나의 행이 포함된 결과 집합으로 반환됩니다. 각 행은 다음 섹션에 설명된 형식으로 열의 유형과 Null 허용 여부를 설명합니다. 모든 제어 경로에 대해 첫 번째 문이 없을 경우 행이 0개인 결과 집합이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**비트 NOT NULL**|해당 열이 정보 검색을 목적으로 추가되어 실제로 결과 집합에 나타나지 않는 별도의 열임을 나타냅니다.|  
|**column_ordinal**|**int NOT NULL**|결과 집합에서 열의 서수 위치를 포함합니다. 첫째 열의 위치가 1로 지정됩니다.|  
|**name**|**sysname NULL**|이름을 확인할 수 있으면 열 이름을 포함하고 그렇지 않으면 NULL을 포함합니다.|  
|**is_nullable**|**비트 NOT NULL**|열이 NULL을 허용하는 경우 1, 열이 NULL을 허용하지 않는 경우 0, 열이 NULL을 허용하는지 확인할 수 없는 경우 1을 포함합니다.|  
|**system_type_id**|**int NOT NULL**|Sys.types에 지정 된 대로 열 데이터 형식의 system_type_id를 포함합니다. CLR 형식의 경우 system_type_name 열에서 NULL을 반환해도 이 열은 값 240을 반환합니다.|  
|**system_type_name**|**nvarchar (256) NULL**|열의 데이터 형식에 지정한 이름 및 인수(length, precision, scale 등)를 포함합니다. 데이터 형식이 사용자 정의 별칭 형식인 경우 기본 시스템 형식이 여기에 지정됩니다. 데이터 형식이 CLR 사용자 정의 형식인 경우 이 열에 NULL이 반환됩니다.|  
|**max_length**|**smallint NOT NULL**|열의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, 또는 **xml**합니다.<br /><br /> 에 대 한 **텍스트** 열은 **max_length** 값은 16 또는 값 설정 됩니다 **sp_tableoption 'text in row'**합니다.|  
|**전체 자릿수**|**tinyint NOT NULL**|숫자 기반일 경우 열의 전체 자릿수이고 그렇지 않으면 0을 반환합니다.|  
|**크기 조정**|**tinyint NOT NULL**|숫자 기반일 경우 열의 소수 자릿수이고 그렇지 않으면 0을 반환합니다.|  
|**데이터 정렬 이름**|**sysname NULL**|문자 기반일 경우 열의 데이터 정렬 이름이고 그렇지 않으면 NULL을 반환합니다.|  
|**user_type_id**|**int NULL**|CLR 및 별칭 형식의 경우 sys.types에 지정된 대로 열 데이터 형식의 user_type_id를 포함합니다. 그렇지 않으면 NULL입니다.|  
|**user_type_database**|**sysname NULL**|CLR 및 별칭 형식의 경우 해당 형식이 정의된 데이터베이스의 이름을 포함합니다. 그렇지 않으면 NULL입니다.|  
|**user_type_schema**|**sysname NULL**|CLR 및 별칭 형식의 경우 해당 형식이 정의된 스키마의 이름을 포함합니다. 그렇지 않으면 NULL입니다.|  
|**user_type_name**|**sysname NULL**|CLR 및 별칭 형식의 경우 형식 이름입니다. 그렇지 않으면 NULL입니다.|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|CLR 형식의 경우 형식을 정의하는 어셈블리 및 클래스 이름을 반환합니다. 그렇지 않으면 NULL입니다.|  
|**xml_collection_id**|**int NULL**|sys.columns에 지정한 대로 열 데이터 형식의 xml_collection_id를 포함합니다. 반환된 형식이 XML 스키마 컬렉션과 연결되지 않은 경우 이 열은 NULL을 반환합니다.|  
|**xml_collection_database**|**sysname NULL**|이 형식과 연결된 XML 스키마 컬렉션이 정의된 데이터베이스를 포함합니다. 반환된 형식이 XML 스키마 컬렉션과 연결되지 않은 경우 이 열은 NULL을 반환합니다.|  
|**xml_collection_schema**|**sysname NULL**|이 형식과 연결된 XML 스키마 컬렉션이 정의된 스키마를 포함합니다. 반환된 형식이 XML 스키마 컬렉션과 연결되지 않은 경우 이 열은 NULL을 반환합니다.|  
|**xml_collection_name**|**sysname NULL**|이 형식과 연결된 XML 스키마 컬렉션 이름을 포함합니다. 반환된 형식이 XML 스키마 컬렉션과 연결되지 않은 경우 이 열은 NULL을 반환합니다.|  
|**is_xml_document**|**비트 NOT NULL**|반환된 데이터 형식이 XML이고 해당 형식이 XML 조각이 아닌 완전한 XML 문서(루트 노드 포함)라고 보장될 경우 1을 반환합니다. 그렇지 않으면 0을 반환합니다.|  
|**is_case_sensitive**|**비트 NOT NULL**|열이 대/소문자를 구분하는 문자열 형식인 경우 1을 반환하고 그렇지 않으면 0을 반환합니다.|  
|**is_fixed_length_clr_type**|**비트 NOT NULL**|열이 고정 길이 CLR 형식인 경우 1을 반환하고 그렇지 않으면 0을 반환합니다.|  
|**source_server**|**sysname**|이 결과에서 열이 반환한 원본 서버의 이름입니다(원본이 원격 서버인 경우). Sys.servers에 표시 된 대로 이름이 지정 됩니다. 열의 원본이 로컬 서버이거나 원본 서버를 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**source_database**|**sysname**|이 결과에서 열이 반환한 원본 데이터베이스 이름입니다. 데이터베이스를 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**source_schema**|**sysname**|이 결과에서 열이 반환한 원본 스키마 이름입니다. 스키마를 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**source_table**|**sysname**|이 결과에서 열이 반환한 원본 테이블 이름입니다. 테이블을 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**source_column**|**sysname**|결과 열에서 반환한 원본 열의 이름입니다. 열을 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**is_identity_column**|**NULL 비트**|열이 ID 열일 경우 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 ID 열인지 확인할 수 없으면 NULL을 반환합니다.|  
|**is_part_of_unique_key**|**NULL 비트**|열이 고유 인덱스의 일부일 경우(unique 및 primary 제약 조건 포함) 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 고유 인덱스의 일부인지 확인할 수 없으면 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**is_updateable**|**NULL 비트**|열이 업데이트 가능할 경우 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 업데이트 가능한지 확인할 수 없으면 NULL을 반환합니다.|  
|**is_computed_column**|**NULL 비트**|열이 계산 열일 경우 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 계산 열인지 확인할 수 없으면 NULL을 반환합니다.|  
|**is_sparse_column_set**|**NULL 비트**|열이 스파스 열일 경우 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 스파스 열 집합의 일부인지 확인할 수 없으면 NULL을 반환합니다.|  
|**ordinal_in_order_by_list**|**smallint NULL**|ORDER BY 목록에서 이 열의 위치입니다. 열이 ORDER BY 목록에 없거나 ORDER BY 목록을 고유하게 확인할 수 없을 경우 NULL을 반환합니다.|  
|**order_by_list_length**|**smallint NULL**|ORDER BY 목록의 길이입니다. ORDER BY 목록이 없거나 ORDER BY 목록을 고유하게 확인할 수 없는 경우 NULL을 반환합니다. 이 값은 동일 하 게 반환 하는 모든 행에 대 한 참고 **sp_describe_first_result_set 합니다.**|  
|**order_by_is_descending**|**smallint NULL**|Ordinal_in_order_by_list가 NULL이 아닐 경우는 **order_by_is_descending** 열이이 열에 대 한 ORDER BY 절의 방향을 보고 합니다. 그렇지 않으면 NULL을 보고합니다.|  
|**tds_type_id**|**int NOT NULL**|내부적으로만 사용할 수 있습니다.|  
|**tds_length**|**int NOT NULL**|내부적으로만 사용할 수 있습니다.|  
|**tds_collation_id**|**int NULL**|내부적으로만 사용할 수 있습니다.|  
|**tds_collation_sort_id**|**tinyint NULL**|내부적으로만 사용할 수 있습니다.|  
  
## <a name="remarks"></a>주의  
 **sp_describe_first_result_set** 프로시저 (가상)에 대 한 첫 번째 결과 집합 메타 데이터를 반환 하는 경우 일괄 처리 A 한 경우 해당 일괄 처리 (A) 후 해당 호스트가 실행 보장이 다음 일괄 처리 합니다 (1) 최적화 시간 오류, (2)를 발생 시킵니다. 발생 시키는 런타임 오류 (3) 아무 결과도에서 설명 하는 동일한 메타 데이터가 포함 된 첫 번째 결과 집합을 설정 하거나 (4) 반환 **sp_describe_first_result_set**합니다.  
  
 이름, Null 허용 여부 및 데이터 형식이 다를 수 있습니다. 경우 **sp_describe_first_result_set** 반환 보증은 빈 결과 집합은 일괄 처리 실행 아니요 결과 집합을 반환 합니다.  
  
 이 보장은 서버의 관련 스키마 변경 사항이 없는 것으로 가정합니다. 서버의 관련 스키마 변경 내용을 임시 테이블 만들기를 포함 하지 않거나 테이블 변수는 일괄 처리 시간 사이에서는 **sp_describe_first_result_set** 라고 하는 동안 결과 집합이 반환 되는 시간 2. 일괄 처리에서 변경한 스키마를 포함 하 여 실행  
  
 **sp_describe_first_result_set** 다음과 같은 경우에 오류를 반환 합니다.  
  
-   하는 경우 입력 @tsql 유효 하지 않거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 합니다. 유효성을 구문 분석 하 고 분석 하 여 확인할는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 합니다. 쿼리 최적화 중 또는 실행 하는 동안 일괄 처리에 의해 발생 한 오류를 결정할 때 고려 되지 않습니다 여부는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리는 유효 합니다.  
  
-   경우 @params NULL이 아닌 문자열을 포함 하는 문자열을 포함 하는 경우 선언 하는 매개 변수가 여러 번 또는 매개 변수에 대해 구문상 유효한 선언 문자열이 아닙니다.  
  
-   하는 경우 입력 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리에서 선언 된 매개 변수 이름이 같은 지역 변수를 선언 @params합니다.  
  
-   해당 문에서 임시 테이블을 사용하는 경우  
  
-   쿼리에 다음으로 쿼리되는 영구 테이블 생성이 포함되는 경우  
  
 다른 모든 확인이 성공한 경우에는 입력 일괄 처리 내에서 가능한 모든 제어 흐름 경로가 고려됩니다. 이 고려 모든 제어 흐름 문 (GOTO, IF/ELSE, WHILE 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] TRY/CATCH 블록) 동적 모든 절차 뿐만 아니라 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 또는 트리거를 발생 시키는 DDL 문에 EXEC 문에 의해 입력된 일괄 처리에서 호출 DDL 트리거를 발생 또는 발생으로 인해 대상 테이블에서 또는 외래 키 제약 조건에서 연계 동작으로 인해 수정 하는 테이블에서 발생 하는 DML 문입니다. 가능한 대부분의 제어 경로에서 특정 시점에 알고리즘이 중지됩니다.  
  
 각 제어 흐름 경로 대 한 첫 번째 문 (있는 경우)를 반환 하는 결과 집합을 따라 사용자가 **sp_describe_first_result_set**합니다.  
  
 일괄 처리에서 가능한 첫 번째 문이 여러 개 발견된 경우 해당 결과는 열 수, 열 이름, Null 허용 여부 및 데이터 형식이 다를 수 있습니다. 이러한 차이점이 처리되는 방식은 다음과 같습니다.  
  
-   열 수가 다른 경우 오류가 발생하고 아무 결과도 반환되지 않습니다.  
  
-   열 이름이 다른 경우 반환되는 열 이름이 NULL로 설정됩니다.  
  
-   Null 허용 여부가 다른 경우 반환되는 Null 허용 여부가 NULL을 허용합니다.  
  
-   데이터 형식이 다른 경우 다음 조합 외에는 오류가 발생하고 아무 결과도 반환되지 않습니다.  
  
    -   **varchar(a)** 를 **varchar(a')** 위치는 ' >는 합니다.  
  
    -   **varchar(a)** 를 **varchar (max)**  
  
    -   **nvarchar(a)** 를 **nvarchar(a')** 위치는 ' >는 합니다.  
  
    -   **nvarchar(a)** 를 **nvarchar (max)**  
  
    -   **varbinary(a)** 를 **varbinary(a')** 위치는 ' >는 합니다.  
  
    -   **varbinary(a)** 를 **varbinary (max)**  
  
 **sp_describe_first_result_set** 간접 재귀를 지원 하지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 실행할 수 있는 권한이 필요는 @tsql 인수입니다.  
  
## <a name="examples"></a>예  
  
### <a name="typical-examples"></a>일반적인 예  
  
#### <a name="a-simple-example"></a>1. 간단한 예  
 다음 예에서는 단일 쿼리에서 반환되는 결과 집합을 설명합니다.  
  
```  
sp_describe_first_result_set @tsql = N'SELECT object_id, name, type_desc FROM sys.indexes'  
```  
  
 다음 예에서는 매개 변수가 포함된 단일 쿼리에서 반환되는 결과 집합을 보여 줍니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes   
WHERE object_id = @id1'  
, @params = N'@id1 int'  
```  
  
#### <a name="b-browse-mode-examples"></a>2. 찾아보기 모드 예제  
 다음 세 가지 예제는 여러 가지 탐색 정보 모드 간의 주요 차이점을 보여줍니다. 쿼리 결과에는 관련된 열만 포함되었습니다.  
  
 정보가 없음을 나타내는 0을 반환하는 예제가 반환됩니다.  
  
```tsql  
CREATE TABLE dbo.t (a int PRIMARY KEY, b1 int);  
GO  
CREATE VIEW dbo.v AS SELECT b1 AS b2 FROM dbo.t;  
GO  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM dbo.v', null, 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1.|b3|NULL|NULL|NULL|NULL|  
  
 1을 사용하는 예제는 쿼리에 FOR BROWSE 옵션이 포함된 것처럼 정보를 반환합니다.  
  
```tsql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 1  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1.|b3|dbo|t|B1|0|  
|1|2|a|dbo|t|a|1.|  
  
 마치 커서를 준비하는 것처럼 분석됨을 나타내는 2를 사용하는 예제.  
  
```tsql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 2  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1.|B 3|dbo|v|B 2|0|  
|1|2|ROWSTAT|NULL|NULL|NULL|0|  
  
### <a name="examples-of-problems"></a>문제 예  
 다음 예에서는 모두 두 개의 테이블을 사용합니다. 예제 테이블을 만들려면 다음 문을 실행합니다.  
  
```  
CREATE TABLE dbo.t1 (a int NULL, b varchar(10) NULL, c nvarchar(10) NULL);  
CREATE TABLE dbo.t2 (a smallint NOT NULL, d varchar(20) NOT NULL, e int NOT NULL);  
```  
  
#### <a name="error-because-the-number-of-columns-differ"></a>서로 다른 열 수로 인한 오류  
 이 예에서는 가능한 첫 번째 결과 집합의 열 수가 서로 다릅니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a, b FROM t1;  
SELECT * FROM t; -- Ignored, not a possible first result set.'  
  
```  
  
#### <a name="error-because-the-data-types-differ"></a>서로 다른 데이터 형식으로 인한 오류  
 여러 개의 가능한 첫 번째 결과 집합에서 열 형식이 서로 다릅니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a FROM t2;  
```  
  
 결과: 오류, 일치 하지 않는 형식 (**int** 비교 **smallint**).  
  
#### <a name="column-name-cannot-be-determined"></a>열 이름을 확인할 수 없는 경우  
 가능한 첫 번째 결과 집합의 열이 동일한 가변 길이 형식의 길이, Null 허용 여부 및 열 이름이 서로 다릅니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d FROM t2; '  
```  
  
 결과: \<알 수 없는 열 이름 > **varchar (20) NULL**  
  
#### <a name="column-name-forced-to-be-identical-through-aliasing"></a>별칭을 통해 동일해진 열 이름  
 이전 예와 동일하지만, 열 별칭을 통해 열 이름이 같아진 경우입니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d AS b FROM t2;'  
```  
  
 결과: b **varchar (20) NULL**  
  
#### <a name="error-because-column-types-cannot-be-matched"></a>일치하지 않는 열 형식으로 인한 오류  
 여러 개의 가능한 첫 번째 결과 집합에서 열 형식이 서로 다릅니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT c FROM t1;'  
```  
  
 결과: 오류, 일치 하지 않는 형식 (**varchar (10)** 비교 **nvarchar (10)**).  
  
#### <a name="result-set-can-return-an-error"></a>결과 집합이 오류를 반환할 수 있음  
 첫 번째 결과 집합이 오류 또는 결과 집합입니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RAISERROR(''Some Error'', 16, 1);  
  
ELSE  
    SELECT a FROM t1;  
SELECT e FROM t2; -- Ignored, not a possible first result set.;'  
```  
  
 결과:는 **intNULL**  
  
#### <a name="some-code-paths-return-no-results"></a>일부 코드 경로에서 아무 결과도 반환하지 않음  
 첫 번째 결과 집합이 Null 또는 결과 집합입니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RETURN;  
SELECT a FROM t1;'  
```  
  
 결과:는 **intNULL**  
  
#### <a name="result-from-dynamic-sql"></a>동적 SQL의 결과  
 첫 번째 결과 집합이 리터럴 문자열이기 때문에 검색 가능한 동적 SQL입니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'EXEC(N''SELECT a FROM t1'');'  
```  
  
 결과:는 **INT NULL**  
  
#### <a name="result-failure-from-dynamic-sql"></a>동적 SQL로 인한 결과 오류  
 첫 번째 결과 집합이 동적 SQL로 인해 정의되지 않습니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL); '  
```  
  
 결과: 오류입니다. 동적 SQL로 인해 결과를 검색할 수 없습니다.  
  
#### <a name="result-set-specified-by-user"></a>사용자가 지정한 결과 집합  
 첫 번째 결과 집합을 사용자가 수동으로 지정합니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL)  
    WITH RESULT SETS(  
        (Column1 BIGINT NOT NULL)  
    ); '  
```  
  
 결과: Column1 **bigint NOT NULL**  
  
#### <a name="error-caused-by-a-ambiguous-result-set"></a>불확실한 결과 집합으로 인한 오류  
 이 예제에서는 user1 라는 다른 사용자가 열이 있는 기본 스키마 s 1에서 t1 테이블이 있는 가정 (한 **int NOT NULL**).  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT * FROM t1;'  
, @params = N'@p int'  
```  
  
 결과: 오류입니다. 다른 dbo.t1 또는 열 수가 서로 다르므로 각각 s1.t1 t1 수 있습니다.  
  
#### <a name="result-even-with-ambiguous-result-set"></a>불확실한 결과 집합이 포함된 결과  
 이전 예와 동일한 가정을 사용합니다.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT a FROM t1;'  
```  
  
 결과:는 **int NULL** dbo.t1.a와 s1.t1.a 형식을 가지 **int** null 허용 여부가 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_describe_undeclared_parameters &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
  
  
