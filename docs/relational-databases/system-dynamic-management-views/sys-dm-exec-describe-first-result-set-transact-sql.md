---
title: sys.dm_exec_describe_first_result_set(Transact-SQL)
description: sys.dm_exec_describe_first_result_set(Transact-SQL)
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_describe_first_result_set
- sys.dm_exec_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_describe_first_result_set catalog view
ms.assetid: 6ea88346-0bdb-4f0e-9f1f-4d85e3487d23
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 06/10/2016
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 21b823aeaa319263a3e90a3ddd917e9605506c0c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472864"
---
# <a name="sysdm_exec_describe_first_result_set-transact-sql"></a>sys.dm_exec_describe_first_result_set(Transact-SQL)

[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

이 동적 관리 함수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 매개 변수로 사용 하 고 문의 첫 번째 결과 집합에 대 한 메타 데이터를 설명 합니다.  
  
 **sys.dm_exec_describe_first_result_set** 는 [transact-sql&#41;&#40;sys.dm_exec_describe_first_result_set_for_object](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md) 와 동일한 결과 집합 정의가 있으며 sp_describe_first_result_set [&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)와 비슷합니다.  
  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.dm_exec_describe_first_result_set(@tsql, @params, @include_browse_information)  
```  
  
## <a name="arguments"></a>인수  
 *\@tsql*  
 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. *SQL_batch* 는 **nvarchar (**_n_*_)_* 또는 **nvarchar (max)** 일 수 있습니다.  
  
 *\@params*  
 \@params는 [!INCLUDE[tsql](../../includes/tsql-md.md)] sp_executesql와 유사 하 게 일괄 처리에 대 한 매개 변수에 대 한 선언 문자열을 제공 합니다. 매개 변수는 **nvarchar (n)** 또는 **nvarchar (max)** 일 수 있습니다.  
  
 _Batch에 포함 된 모든 매개 변수의 정의를 포함 하는 하나의 문자열입니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . 문자열은 유니코드 상수 또는 유니코드 변수여야 합니다. 각 매개 변수의 정의는 매개 변수 이름과 데이터 형식으로 구성됩니다. *n* 은 추가 매개 변수 정의를 나타내는 자리 표시자입니다. Stmt에 지정 된 모든 매개 변수는 params에 정의 되어야 합니다 \@ . 문의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리에 매개 변수가 없는 경우 \@ params가 필요 하지 않습니다. NULL이 이 매개 변수의 기본값입니다.  
  
 *\@include_browse_information*  
 1로 설정되면 쿼리에 FOR BROWSE 옵션이 있는 것처럼 각 쿼리가 분석됩니다. 추가 키 열과 원본 테이블 정보가 반환됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
 이 공통 메타데이터가 결과 집합으로 반환됩니다. 결과 메타데이터에 있는 각 열의 행 하나가 가지는 열의 유형과 Null 허용 여부를 다음 표에 나타난 형식으로 설명합니다. 모든 제어 경로에 대해 첫 번째 문이 없을 경우 행이 0개인 결과 집합이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit**|해당 열이 검색 및 정보 제공 목적으로 추가되어 실제로 결과 집합에 나타나지 않는 별도의 열임을 지정합니다.|  
|**column_ordinal**|**int**|결과 집합에서 열의 서수 위치를 포함합니다. 첫 번째 열의 위치가 1로 지정됩니다.|  
|**name**|**sysname**|이름을 확인할 수 있으면 열 이름을 포함하고 그렇지 않으면 NULL을 포함합니다.|  
|**is_nullable**|**bit**|다음 값을 포함합니다.<br /><br /> 열에서 NULL을 허용하면 값이 1입니다.<br /><br /> 열에서 NULL을 허용하지 않으면 값이 0입니다.<br /><br /> 열에서 NULL을 허용하는지 확인할 수 없으면 값이 1입니다.|  
|**system_type_id**|**int**|Sys. types에 지정 된 열 데이터 형식의 system_type_id를 포함 합니다. CLR 형식의 경우 system_type_name 열에서 NULL을 반환해도 이 열은 값 240을 반환합니다.|  
|**system_type_name**|**nvarchar(256)**|열의 데이터 형식에 지정한 이름 및 인수(length, precision, scale 등)를 포함합니다.<br /><br /> 데이터 형식이 사용자 정의 별칭 형식일 경우 기본 시스템 형식이 여기에 지정됩니다.<br /><br /> 데이터 형식이 CLR 사용자 정의 형식일 경우 이 열에 NULL이 반환됩니다.|  
|**max_length**|**smallint**|열의 최대 길이(바이트)입니다.<br /><br /> -1 = 열 데이터 형식이 **varchar (max)**, **nvarchar (max)**, **varbinary (max)** 또는 **xml** 입니다.<br /><br /> **텍스트** 열의 경우 **max_length** 값은 16 이거나 **' text in row ' sp_tableoption** 값으로 설정 됩니다.|  
|**전체 자릿수**|**tinyint**|숫자 기반일 경우 열의 전체 자릿수이고 그렇지 않으면 0을 반환합니다.|  
|**scale**|**tinyint**|숫자 기반일 경우 열의 소수 자릿수이고 그렇지 않으면 0을 반환합니다.|  
|**collation_name**|**sysname**|문자 기반일 경우 열의 데이터 정렬 이름이고 그렇지 않으면 NULL을 반환합니다.|  
|**user_type_id**|**int**|CLR 및 별칭 형식의 경우 sys.types에 지정된 대로 열 데이터 형식의 user_type_id를 포함합니다. 그렇지 않으면 NULL입니다.|  
|**user_type_database**|**sysname**|CLR 및 별칭 형식의 경우 해당 형식이 정의된 데이터베이스의 이름을 포함합니다. 그렇지 않으면 NULL입니다.|  
|**user_type_schema**|**sysname**|CLR 및 별칭 형식의 경우 해당 형식이 정의된 스키마의 이름을 포함합니다. 그렇지 않으면 NULL입니다.|  
|**user_type_name**|**sysname**|CLR 및 별칭 형식의 경우 형식 이름입니다. 그렇지 않으면 NULL입니다.|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|CLR 형식의 경우 형식을 정의하는 어셈블리 및 클래스 이름을 반환합니다. 그렇지 않으면 NULL입니다.|  
|**xml_collection_id**|**int**|sys.columns에 지정한 대로 열 데이터 형식의 xml_collection_id를 포함합니다. 반환된 형식이 XML 스키마 데이터 컬렉션과 연결되지 않은 경우 이 열이 NULL을 반환합니다.|  
|**xml_collection_database**|**sysname**|이 형식과 연결된 XML 스키마 컬렉션이 정의된 데이터베이스를 포함합니다. 반환된 형식이 XML 스키마 데이터 컬렉션과 연결되지 않은 경우 이 열이 NULL을 반환합니다.|  
|**xml_collection_schema**|**sysname**|이 형식과 연결된 XML 스키마 컬렉션이 정의된 스키마를 포함합니다. 반환된 형식이 XML 스키마 데이터 컬렉션과 연결되지 않은 경우 이 열이 NULL을 반환합니다.|  
|**xml_collection_name**|**sysname**|이 형식과 연결된 XML 스키마 컬렉션 이름을 포함합니다. 반환된 형식이 XML 스키마 데이터 컬렉션과 연결되지 않은 경우 이 열이 NULL을 반환합니다.|  
|**is_xml_document**|**bit**|반환된 데이터 형식이 XML이고 해당 형식이 XML 조각이 아닌 완전한 XML 문서(루트 노드 포함)라고 보장될 경우 1을 반환합니다. 그렇지 않으면 0을 반환합니다.|  
|**is_case_sensitive**|**bit**|열이 대/소문자를 구분하는 문자열 형식일 경우 1을 반환합니다. 그렇지 않으면 0을 반환합니다.|  
|**is_fixed_length_clr_type**|**bit**|열이 고정 길이 CLR 형식일 경우 1을 반환합니다. 그렇지 않으면 0을 반환합니다.|  
|**source_server**|**sysname**|원본 서버의 이름입니다(원본이 원격 서버일 경우). 이름은 sys. servers에 표시 된 대로 제공 됩니다. 열의 원본이 로컬 서버이거나 원본 서버를 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**source_database**|**sysname**|이 결과에서 열이 반환한 원본 데이터베이스 이름입니다. 데이터베이스를 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**source_schema**|**sysname**|이 결과에서 열이 반환한 원본 스키마 이름입니다. 스키마를 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**source_table**|**sysname**|이 결과에서 열이 반환한 원본 테이블 이름입니다. 테이블을 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**source_column**|**sysname**|결과 열에서 반환한 원본 열의 이름입니다. 열을 확인할 수 없는 경우 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**is_identity_column**|**bit**|열이 ID 열일 경우 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 ID 열인지 확인할 수 없으면 NULL을 반환합니다.|  
|**is_part_of_unique_key**|**bit**|열이 고유 인덱스의 일부일 경우(UNIQUE 및 PRIMARY KEY 제약 조건 포함) 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 고유 인덱스의 일부인지 확인할 수 없으면 NULL을 반환합니다. 정보 검색을 요청할 경우에만 채워집니다.|  
|**is_updateable**|**bit**|열이 업데이트 가능할 경우 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 업데이트 가능한지 확인할 수 없으면 NULL을 반환합니다.|  
|**is_computed_column**|**bit**|열이 계산 열일 경우 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 계산 열인지 확인할 수 없으면 NULL을 반환합니다.|  
|**is_sparse_column_set**|**bit**|열이 스파스 열일 경우 1을 반환하고 그렇지 않으면 0을 반환합니다. 열이 스파스 열 집합의 일부인지 확인할 수 없으면 NULL을 반환합니다.|  
|**ordinal_in_order_by_list**|**smallint**|이 열의 위치가 ORDER BY 목록에 있습니다. 열이 ORDER BY 목록에 없거나 ORDER BY 목록을 고유하게 확인할 수 없을 경우 NULL을 반환합니다.|  
|**order_by_list_length**|**smallint**|ORDER BY 목록의 길이입니다. ORDER BY 목록이 없거나 ORDER BY 목록을 고유하게 확인할 수 없을 경우 NULL이 반환됩니다. sp_describe_first_result_set가 반환하는 모든 열에 대해 이 값이 동일합니다.|  
|**order_by_is_descending**|**smallint NULL**|ordinal_in_order_by_list가 NULL이 아닐 경우 **order_by_is_descending** 열에서 이 열에 대한 ORDER BY 절의 방향을 보고합니다. 그렇지 않으면 NULL을 보고합니다.|  
|**error_number**|**int**|함수가 반환한 오류 번호를 포함합니다. 오류가 발생하지 않은 경우 열에 NULL이 포함됩니다.|  
|**error_severity**|**int**|함수가 반환한 심각도를 포함합니다. 오류가 발생하지 않은 경우 열에 NULL이 포함됩니다.|  
|**error_state**|**int**|함수가 반환한 상태 메시지를 포함합니다. 오류가 발생하지 않은 경우 열에 NULL이 포함됩니다.|  
|**error_message**|**nvarchar (4096)**|함수가 반환한 메시지를 포함합니다. 오류가 발생하지 않은 경우 열에 NULL이 포함됩니다.|  
|**error_type**|**int**|반환할 오류를 나타내는 정수를 포함합니다. error_type_desc에 매핑됩니다. 주의 아래의 목록을 참조하세요.|  
|**error_type_desc**|**nvarchar(60)**|반환할 오류를 나타내는 간단한 대문자 문자열을 포함합니다. error_type에 매핑됩니다. 주의 아래의 목록을 참조하세요.|  
  
## <a name="remarks"></a>설명  
 이 함수는 **sp_describe_first_result_set** 와 동일한 알고리즘을 사용합니다. 자세한 내용은 [sp_describe_first_result_set &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)를 참조 하세요.  
  
 다음 표에서는 오류 유형 및 설명을 나열합니다.  
  
|error_type|error_type|설명|  
|-----------------|-----------------|-----------------|  
|1|MISC|설명하지 않은 모든 오류입니다.|  
|2|SYNTAX|일괄 처리에 발생한 구문 오류입니다.|  
|3|CONFLICTING_RESULTS|가능한 두 개의 첫 번째 문 사이에 충돌이 발생하여 결과를 확인할 수 없습니다.|  
|4|DYNAMIC_SQL|첫 번째 결과를 반환할 수 있는 동적 SQL로 인해 결과를 확인할 수 없습니다.|  
|5|CLR_PROCEDURE|CLR 저장 프로시저가 첫 번째 결과를 반환할 수 있으므로 결과를 확인할 수 없습니다.|  
|6|CLR_TRIGGER|CLR 트리거가 첫 번째 결과를 반환할 수 있으므로 결과를 확인할 수 없습니다.|  
|7|EXTENDED_PROCEDURE|확장 저장 프로시저가 첫 번째 결과를 반환할 수 있으므로 결과를 확인할 수 없습니다.|  
|8|UNDECLARED_PARAMETER|결과 집합의 열 중 하나 이상의 데이터 형식이 선언 되지 않은 매개 변수에 종속 될 수 있으므로 결과를 확인할 수 없습니다.|  
|9|RECURSION|일괄 처리에 재귀 문이 포함되어 있어 결과를 확인할 수 없습니다.|  
|10|TEMPORARY_TABLE|일괄 처리에 임시 테이블이 포함되고 **sp_describe_first_result_set** 에서 일괄 처리를 지원하지 않으므로 결과를 확인할 수 없습니다.|  
|11|UNSUPPORTED_STATEMENT|**sp_describe_first_result_set** 에서 지원하지 않는 문(예: FETCH, REVERT 등)이 일괄 처리에 포함되어 있어 결과를 확인할 수 없습니다.|  
|12|OBJECT_TYPE_NOT_SUPPORTED|\@함수에 전달 된 object_id은 지원 되지 않습니다 (예: 저장 프로시저가 아님).|  
|13|OBJECT_DOES_NOT_EXIST|\@함수에 전달 된 object_id를 시스템 카탈로그에서 찾을 수 없습니다.|  
  
## <a name="permissions"></a>사용 권한  
 Tsql 인수를 실행할 수 있는 권한이 필요 \@ 합니다.  
  
## <a name="examples"></a>예  
 **Sys.dm_exec_describe_first_result_set** 를 사용 하도록 [transact-sql&#41;&#40;sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 항목의 추가 예를 수정할 수 있습니다.  
  
### <a name="a-returning-information-about-a-single-transact-sql-statement"></a>A. 단일 Transact-SQL 문에 대한 정보 반환  
 다음 코드에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 결과에 대한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_exec_describe_first_result_set  
(N'SELECT object_id, name, type_desc FROM sys.indexes', null, 0) ;  
```  
  
### <a name="b-returning-information-about-a-procedure"></a>B. 프로시저에 대한 정보 반환  
 다음 예에서는 두 개의 결과 집합을 반환 하는 pr_TestProc 라는 저장 프로시저를 만듭니다. 그런 다음 **sys.dm_exec_describe_first_result_set** 가 프로시저의 첫 번째 결과 집합 정보를 반환하는 것을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE PROC Production.TestProc  
AS  
SELECT Name, ProductID, Color FROM Production.Product ;  
SELECT Name, SafetyStockLevel, SellStartDate FROM Production.Product ;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set  
('Production.TestProc', NULL, 0) ;  
```  
  
### <a name="c-returning-metadata-from-a-batch-that-contains-multiple-statements"></a>C. 여러 문이 포함된 일괄 처리에서 메타데이터 반환  
 다음 예에서는 두 개의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 포함된 일괄 처리를 평가합니다. 결과 집합이 반환된 첫 번째 결과 집합을 설명합니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set(  
N'SELECT CustomerID, TerritoryID, AccountNumber FROM Sales.Customer WHERE CustomerID = @CustomerID;  
SELECT * FROM Sales.SalesOrderHeader;',  
N'@CustomerID int', 0) AS a;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_describe_first_result_set &#40;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [Transact-sql&#41;sp_describe_undeclared_parameters &#40;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [Transact-sql&#41;sys.dm_exec_describe_first_result_set_for_object &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
  
  
