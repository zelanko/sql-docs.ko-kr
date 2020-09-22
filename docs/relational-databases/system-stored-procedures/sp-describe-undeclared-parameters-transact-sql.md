---
description: sp_describe_undeclared_parameters(Transact-SQL)
title: sp_describe_undeclared_parameters (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_undeclared_parameters
- sp_describe_undeclared_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_undeclared_parameters
ms.assetid: 6f016da6-dfee-4228-8b0d-7cd8e7d5a354
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 5ca659670cb68bafa10f758bc2a7997243f5c1a8
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990130"
---
# <a name="sp_describe_undeclared_parameters-transact-sql"></a>sp_describe_undeclared_parameters(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)] 

  일괄 처리의 선언 되지 않은 매개 변수에 대 한 메타 데이터를 포함 하는 결과 집합을 반환 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . ** \@ Tsql** 일괄 처리에 사용 되지만 ** \@ params**에 선언 되지 않은 각 매개 변수를 고려 합니다. 이러한 각 매개 변수에 대한 추론된 형식의 정보와 함께 해당 매개 변수에 대한 하나의 행이 포함된 결과 집합이 반환됩니다. ** \@ Tsql** 입력 일괄 처리에 ** \@ params**에 선언 된 매개 변수가 없는 경우이 프로시저는 빈 결과 집합을 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql
  
sp_describe_undeclared_parameters   
    [ @tsql = ] 'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' data type ] [, ...n]  
```  

> [!Note] 
> Azure Synapse Analytics (이전의 SQL DW)에서이 저장 프로시저를 사용 하려면 데이터베이스 호환성 수준을 20 이상으로 설정 합니다.   옵트아웃 하려면 데이터베이스 호환성 수준을 10으로 변경 합니다.

## <a name="arguments"></a>인수  
`[ \@tsql = ] 'Transact-SQL\_batch'` 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. *SQL_batch* 는 **nvarchar (**_n_**)** 또는 **nvarchar (max)** 일 수 있습니다.  
  
`[ \@params = ] N'parameters'`\@params는 [!INCLUDE[tsql](../../includes/tsql-md.md)] sp_executesql 작동 방식과 비슷하게 일괄 처리에 대 한 매개 변수에 대 한 선언 문자열을 제공 합니다. *매개 변수* 는 **nvarchar (**_n_**)** 또는 **nvarchar (max)** 일 수 있습니다.  
  
 는 *SQL_batch transact-sql*에 포함 된 모든 매개 변수의 정의를 포함 하는 하나의 문자열입니다. 문자열은 유니코드 상수 또는 유니코드 변수여야 합니다. 각 매개 변수의 정의는 매개 변수 이름과 데이터 형식으로 구성됩니다. n은 추가 매개 변수 정의를 나타내는 자리 표시자입니다. 문의 Transact-sql 문 또는 일괄 처리에 매개 변수가 없는 경우 \@ params가 필요 하지 않습니다. 이 매개 변수의 기본값은 NULL입니다.  
  
 데이터 형식  
 매개 변수의 데이터 형식입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 성공 시 **sp_describe_undeclared_parameters** 항상 반환 상태 0을 반환 합니다. 프로시저에서 오류가 발생 하 고 프로시저가 RPC로 호출 된 경우에는 dm_exec_describe_first_result_set의 error_type 열에 설명 된 대로 오류 유형에 의해 반환 상태가 채워집니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 프로시저를 호출한 경우 반환 값은 오류가 발생한 경우에도 항상 0입니다.  
  
## <a name="result-sets"></a>결과 집합  
 **sp_describe_undeclared_parameters** 는 다음 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int NOT NULL**|결과 집합에서 매개 변수의 서수 위치를 포함합니다. 첫 번째 매개 변수의 위치가 1로 지정됩니다.|  
|**name**|**sysname NULL이 아님**|매개 변수의 이름을 포함합니다.|  
|**suggested_system_type_id**|**int NOT NULL**|에 지정 된 매개 변수의 데이터 형식에 대 한 **system_type_id** 를 포함 하는 형식입니다.<br /><br /> CLR 형식의 경우 **system_type_name** 열이 NULL을 반환 하는 경우에도이 열은 240 값을 반환 합니다.|  
|**suggested_system_type_name**|**nvarchar (256) NULL**|데이터 형식 이름을 포함합니다. 매개 변수의 데이터 형식에 지정된 인수(length, precision, scale 등)를 포함합니다. 데이터 형식이 사용자 정의 별칭 형식인 경우 기본 시스템 형식이 여기에 지정됩니다. 데이터 형식이 CLR 사용자 정의 데이터 형식인 경우 이 열에 NULL이 반환됩니다. 매개 변수의 형식을 추론할 수 없는 경우 NULL이 반환됩니다.|  
|**suggested_max_length**|**NULL이 아닌 smallint**|Sys. columns를 참조 하세요. **max_length** 열 설명입니다.|  
|**suggested_precision**|**tinyint NOT NULL**|Sys. columns를 참조 하세요. 참조하세요.|  
|**suggested_scale**|**tinyint NOT NULL**|Sys. columns를 참조 하세요. 참조하세요.|  
|**suggested_user_type_id**|**int NULL**|CLR 및 별칭 형식의 경우 sys.types에 지정된 대로 열 데이터 형식의 user_type_id를 포함합니다. 그렇지 않으면 NULL입니다.|  
|**suggested_user_type_database**|**sysname NULL**|CLR 및 별칭 형식의 경우 해당 형식이 정의된 데이터베이스의 이름을 포함합니다. 그렇지 않으면 NULL입니다.|  
|**suggested_user_type_schema**|**sysname NULL**|CLR 및 별칭 형식의 경우 해당 형식이 정의된 스키마의 이름을 포함합니다. 그렇지 않으면 NULL입니다.|  
|**suggested_user_type_name**|**sysname NULL**|CLR 및 별칭 형식의 경우 형식 이름입니다. 그렇지 않으면 NULL입니다.|  
|**suggested_assembly_qualified_type_name**|**nvarchar (4000) NULL**|CLR 형식의 경우 형식을 정의하는 어셈블리 및 클래스 이름을 반환합니다. 그렇지 않으면 NULL입니다.|  
|**suggested_xml_collection_id**|**int NULL**|Sys. columns에 지정 된 매개 변수의 데이터 형식에 대 한 xml_collection_id를 포함 합니다. 반환된 형식이 XML 스키마 컬렉션과 연결되지 않은 경우 이 열은 NULL을 반환합니다.|  
|**suggested_xml_collection_database**|**sysname NULL**|이 형식과 연결된 XML 스키마 컬렉션이 정의된 데이터베이스를 포함합니다. 반환된 형식이 XML 스키마 컬렉션과 연결되지 않은 경우 이 열은 NULL을 반환합니다.|  
|**suggested_xml_collection_schema**|**sysname NULL**|이 형식과 연결된 XML 스키마 컬렉션이 정의된 스키마를 포함합니다. 반환된 형식이 XML 스키마 컬렉션과 연결되지 않은 경우 이 열은 NULL을 반환합니다.|  
|**suggested_xml_collection_name**|**sysname NULL**|이 형식과 연결된 XML 스키마 컬렉션 이름을 포함합니다. 반환된 형식이 XML 스키마 컬렉션과 연결되지 않은 경우 이 열은 NULL을 반환합니다.|  
|**suggested_is_xml_document**|**비트 NOT NULL**|반환할 데이터 형식이 XML이고 해당 형식이 XML 문서임이 보장될 경우 1을 반환합니다. 그렇지 않으면 0을 반환합니다.|  
|**suggested_is_case_sensitive**|**비트 NOT NULL**|열이 대/소문자를 구분하는 문자열 형식인 경우 1을 반환하고 그렇지 않으면 0을 반환합니다.|  
|**suggested_is_fixed_length_clr_type**|**비트 NOT NULL**|열이 고정 길이 CLR 형식인 경우 1을 반환하고 그렇지 않으면 0을 반환합니다.|  
|**suggested_is_input**|**비트 NOT NULL**|매개 변수가 대입의 왼쪽이 아닌 다른 곳에 사용되는 경우 1을 반환합니다. 그렇지 않으면 0을 반환합니다.|  
|**suggested_is_output**|**비트 NOT NULL**|매개 변수가 대입의 왼쪽에 사용되거나 저장 프로시저의 출력 매개 변수로 전달되는 경우 1을 반환합니다. 그렇지 않으면 0을 반환합니다.|  
|**formal_parameter_name**|**sysname NULL**|매개 변수가 저장 프로시저 또는 사용자 정의 함수의 인수인 경우 해당 형식 매개 변수의 이름을 반환합니다. 그렇지 않으면 NULL을 반환합니다.|  
|**suggested_tds_type_id**|**int NOT NULL**|내부적으로만 사용할 수 있습니다.|  
|**suggested_tds_length**|**int NOT NULL**|내부적으로만 사용할 수 있습니다.|  
  
## <a name="remarks"></a>설명  
 **sp_describe_undeclared_parameters** 는 항상 반환 상태 0을 반환 합니다.  
  
 애플리케이션에 매개 변수를 포함할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 지정되고 애플리케이션에서 이러한 문을 어떤 식으로든 처리해야 하는 경우에 가장 일반적으로 사용됩니다. 사용자가 ODBC 매개 변수 구문이 있는 쿼리를 제공하는 사용자 인터페이스(예: ODBCTest 도는 RowsetViewer)를 예로 들 수 있습니다. 애플리케이션은 매개 변수 수를 동적으로 검색하여 해당 정보를 사용자에게 표시해야 합니다.  
  
 다른 예로, 사용자 입력이 없는 경우를 들 수 있습니다. 애플리케이션은 매개 변수를 반복하여 테이블과 같은 다른 위치에서 해당 데이터를 가져와야 합니다. 이 경우 애플리케이션에서 모든 매개 변수 정보를 한 번에 전달할 필요는 없습니다. 대신 모든 매개 변수 정보를 공급자에서 가져오고 데이터 자체는 테이블에서 가져올 수 있습니다. **Sp_describe_undeclared_parameters** 를 사용 하는 코드는 보다 일반적 이며, 나중에 데이터 구조가 변경 되는 경우 수정이 필요할 가능성이 적습니다.  
  
 **sp_describe_undeclared_parameters** 는 다음과 같은 경우에 오류를 반환 합니다.  
  
-   입력 \@ tsql이 유효한 일괄 처리가 아닌 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 유효성은 일괄 처리를 구문 분석 하 고 분석 하 여 결정 됩니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . 일괄 처리가 유효한 지 여부를 확인 하는 경우 쿼리 최적화 중에 또는 실행 중에 일괄 처리로 인해 발생 하는 모든 오류는 고려 되지 않습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   \@Params가 NULL이 아니고, 매개 변수에 대 한 구문상 올바른 선언 문자열이 아닌 문자열을 포함 하거나, 매개 변수를 두 번 이상 선언 하는 문자열을 포함 하는 경우입니다.  
  
-   입력 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리가 params에 선언 된 매개 변수와 같은 이름의 지역 변수를 선언 하는 \@ 경우  
  
- 문이 임시 테이블을 참조 하면입니다.

- 쿼리에 다음으로 쿼리되는 영구 테이블 생성이 포함되는 경우
  
 \@Tsql에 params에 선언 된 매개 변수가 아닌 매개 변수가 있는 경우 \@ 프로시저는 빈 결과 집합을 반환 합니다.  
  
## <a name="parameter-selection-algorithm"></a>매개 변수 선택 알고리즘  
 선언되지 않은 매개 변수가 있는 쿼리의 경우 선언되지 않은 매개 변수에 대한 데이터 형식 추론은 다음 3단계로 진행됩니다.  
  
 **1단계**  
  
 선언되지 않은 매개 변수가 있는 쿼리에 대한 데이터 형식 추론의 첫 번째 단계는 데이터 형식이 선언되지 않은 매개 변수에 종속되지 않는 모든 하위 식의 데이터 형식을 찾는 것입니다. 다음 식에 대해 형식을 확인할 수 있습니다.  
  
-   열, 상수, 변수 및 선언된 매개 변수  
  
-   UDF(사용자 정의 함수) 호출 결과  
  
-   모든 입력에 대해 선언되지 않은 매개 변수에 종속되지 않는 데이터 형식이 포함된 식  
  
 예를 들어 `SELECT dbo.tbl(@p1) + c1 FROM t1 WHERE c2 = @p2 + 2` 쿼리를 고려할 수 있습니다. Dbo. tbl ( \@ p1) + c1 및 c2 식에는 데이터 형식이 있고 식 \@ p1 및 \@ p2 + 2는 그렇지 않습니다.  
  
 이 단계 후 UDF 호출 이외의 다른 식에 데이터 형식이 없는 인수가 두 개 있으면 형식 추론이 오류와 함께 실패합니다. 예를 들어 다음과 같은 경우에 오류가 발생합니다.  
  
```sql
SELECT * FROM t1 WHERE @p1 = @p2  
SELECT * FROM t1 WHERE c1 = @p1 + @p2  
SELECT * FROM t1 WHERE @p1 = SUBSTRING(@p2, 2, 3)  
```  
  
 다음 예에서는 오류가 발생하지 않습니다.  
  
```sql
SELECT * FROM t1 WHERE @p1 = dbo.tbl(c1, @p2, @p3)  
```
  
 **2단계**  
  
 선언 되지 않은 지정 된 매개 변수 p의 경우 \@ 형식 추론 알고리즘은 p를 포함 하는 가장 안쪽의 E ( \@ p)를 검색 \@ 하며 다음 중 하나입니다.  
  
-   비교 또는 대입 연산자의 인수  
  
-   사용자 정의 함수(테이블 반환 UDF 포함), 프로시저 또는 메서드의 인수  
  
-   **INSERT** 문의 **VALUES** 절에 대 한 인수입니다.  
  
-   **CAST** 또는 **CONVERT**의 인수입니다.  
  
 형식 추론 알고리즘은 \@ E (p)의 대상 데이터 형식 TT (p)를 찾습니다 \@ . 위 예에 대한 대상 데이터 형식은 다음과 같습니다.  
  
-   비교 또는 대입의 다른 쪽 데이터 형식  
  
-   이 인수가 전달되는 매개 변수의 선언된 데이터 형식  
  
-   이 값이 삽입되는 열의 데이터 형식  
  
-   문이 캐스팅 또는 변환되는 데이터 형식  
  
 예를 들어 `SELECT * FROM t WHERE @p1 = dbo.tbl(@p2 + c1)` 쿼리를 고려할 수 있습니다. 그런 다음 E ( \@ p1) = \@ P1, e ( \@ p2) = \@ P2 + c1, tt ( \@ p1)은 dbo. tbl의 선언 된 반환 데이터 형식이 고, tt ( \@ p2)는 dbo. tbl에 대해 선언 된 매개 변수 데이터 형식입니다.  
  
 \@P가 2 단계 시작 부분에 나열 된 식에 포함 되지 않은 경우 형식 추론 알고리즘은 e ( \@ p)가 p를 포함 하는 가장 큰 스칼라 식 임을 확인 하 \@ 고, 형식 추론 알고리즘은 e (p)의 대상 데이터 형식 TT (p)를 계산 하지 않습니다 \@ \@ . 예를 들어 쿼리가 SELECT 이면 `@p + 2` E ( \@ p) = \@ p + 2이 고 TT (p)가 없는 것입니다 \@ .  
  
 **3단계**  
  
 이제 E ( \@ p) 및 TT ( \@ p)가 확인 되었으므로 형식 추론 알고리즘은 \@ 다음 두 가지 방법 중 하나로 p의 데이터 형식을 추론 합니다.  
  
-   단순 추론  
  
     E ( \@ p) = \@ p 및 TT (p)가 있는 경우 (예 \@ : \@ p가 2 단계 시작 부분에 나열 된 식 중 하나에 대 한 인수) 이면 형식 추론 알고리즘에서 p의 데이터 형식을 \@ TT ( \@ p)로 추론 합니다. 다음은 그 예입니다.   
  
    ```sql
    SELECT * FROM t WHERE c1 = @p1 AND @p2 = dbo.tbl(@p3)  
    ```  
  
     \@P1, \@ p2 및 p3의 데이터 형식은 \@ 각각 c1의 데이터 형식, dbo. tbl의 반환 데이터 형식 및 각각 dbo. d a c o. c o d 1의 매개 변수 데이터 형식입니다.  
  
     특수 한 경우 이지만 \@ p가, = 연산자에 대 한 인수 이면 \<, > \<=, or > 단순 추론 규칙이 적용 되지 않습니다. 이 경우 형식 추론 알고리즘에서는 다음 섹션에 설명된 일반 추론 규칙을 사용합니다. 예를 들어 c1이 데이터 형식 char(30)의 열인 경우 다음 두 가지 쿼리를 고려합니다.  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p  
    SELECT * FROM t WHERE c1 > @p  
    ```  
  
     첫 번째 경우 형식 추론 알고리즘은이 항목의 앞부분에 있는 규칙에 따라 추론의 데이터 형식으로 **char (30)을 (를)** 입력 합니다 \@ . 두 번째 경우에는 다음 섹션의 일반 추론 규칙에 따라 형식 추론 알고리즘에서 **varchar (8000)** 를 추론 합니다.  
  
-   일반 추론  
  
     단순 추론이 적용되지 않는 경우 선언되지 않은 매개 변수에 대해 다음 데이터 형식이 고려됩니다.  
  
    -   Integer 데이터 형식 (**bit**, **tinyint**, **smallint**, **int**, **bigint**)  
  
    -   Money 데이터 형식 (**smallmoney**, **money**)  
  
    -   부동 소수점 데이터 형식 (**float**, **real**)  
  
    -   **numeric (38, 19)** -다른 숫자 또는 10 진수 데이터 형식을 고려 하지 않습니다.  
  
    -   **varchar (8000)**, **varchar (max)**, **nvarchar (4000)** 및 **nvarchar (max)** -다른 문자열 데이터 형식 (예: **text**, **char (8000)**, **nvarchar (30)** 등)은 고려 되지 않습니다.  
  
    -   **varbinary (8000)** 및 **varbinary (max)** -다른 이진 데이터 형식 (예: **image**, **binary (8000)**, **varbinary (30)** 등)은 고려 되지 않습니다.  
  
    -   **date**, **time (7)**, **smalldatetime**, **datetime**, **datetime2 (7)**, **datetimeoffset (7)** -기타 날짜 및 시간 형식 (예: **시간 (4))** 은 고려 되지 않습니다.  
  
    -   **sql_variant**  
  
    -   **xml**  
  
    -   CLR 시스템 정의 형식 (**hierarchyid**, **geometry**, **geography**)  
  
    -   CLR 사용자 정의 형식  
  
### <a name="selection-criteria"></a>선택 조건  
 후보 데이터 형식 중 쿼리를 무효화하는 데이터 형식은 거부됩니다. 형식 추론 알고리즘은 남은 후보 데이터 형식 중에서 다음 규칙에 따라 하나를 선택합니다.  
  
1.  E (p)에서 가장 적은 수의 암시적 변환을 생성 하는 데이터 형식이 \@ 선택 됩니다. 특정 데이터 형식이 E (p)에 대해 TT (p)와 다른 데이터 형식을 생성 하는 경우 \@ \@ 형식 추론 알고리즘은이를 e (p)의 데이터 형식에서 \@ tt (p)로 추가 암시적 변환으로 간주 합니다 \@ .  
  
     다음은 그 예입니다.   
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_Int + @p  
    ```  
  
     이 경우 E ( \@ p)는 Col_Int + p이 \@ 고 TT ( \@ p)는 **Int**입니다. **int** 는 \@ 암시적 변환을 생성 하지 않으므로 p에 대해 선택 됩니다. 다른 데이터 형식은 하나 이상의 암시적 변환을 생성합니다.  
  
2.  변환 수가 가장 적은 데이터 형식에 여러 데이터 형식이 연결된 경우 우선 순위가 가장 높은 데이터 형식이 사용됩니다. 예  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_smallint + @p  
    ```  
  
     이 경우 **int** 와 **smallint** 는 하나의 변환을 생성 합니다. 다른 모든 데이터 형식은 두 번 이상 변환을 생성합니다. **Int** 는 **smallint**보다 우선적으로 적용 되므로 p에 **int** 가 사용 됩니다 \@ . 데이터 형식 우선 순위에 대 한 자세한 내용은 [transact-sql&#41;&#40;데이터 형식 우선 순위 ](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조 하세요.  
  
     이 규칙은 규칙 1에 따라 연결된 모든 데이터 형식과 우선 순위가 가장 높은 데이터 형식 간에 암시적 변환이 있는 경우에만 적용됩니다. 암시적 변환이 없으면 데이터 형식 추론이 오류와 함께 실패합니다. 예를 들어 쿼리에서 데이터 형식이 `SELECT @p FROM t` 동일 하기 때문에 데이터 형식 추론에 실패 \@ 합니다. 예를 들어 **int** 에서 **xml**로의 암시적 변환은 없습니다.  
  
3.  **Varchar (8000)** 및 **varchar (max)** 와 같이 유사한 두 데이터 형식이 규칙 1에 연결 된 경우 더 작은 데이터 형식 (**varchar (8000)**)이 선택 됩니다. **Nvarchar** 및 **varbinary** 데이터 형식에도 동일한 원칙이 적용 됩니다.  
  
4.  규칙 1의 목적상, 형식 추론 알고리즘에서 선호하는 변환에는 우선 순위가 있습니다. 가장 선호하는 변환부터 순서대로 나열하면 다음과 같습니다.  

    1.  길이가 다른 동일한 기본 데이터 형식 간의 변환  
  
    2.  동일한 데이터 형식 (예: **char** - **varchar**)의 고정 길이 및 가변 길이 버전 간의 변환입니다.  
  
    3.  **NULL** 과 **int**간의 변환입니다.  
  
    4.  기타 변환  
  
 예를 들어 쿼리의 경우 `SELECT * FROM t WHERE [Col_varchar(30)] > @p` 변환 (a)이 가장 적합 하므로 **varchar (8000)** 가 선택 됩니다. 쿼리의 경우 `SELECT * FROM t WHERE [Col_char(30)] > @p` varchar ( **8000)** 는 형식 (b)을 변환 하 고, 다른 선택 (예: **varchar (4000)**)을 통해 형식 (d) 변환이 발생 하기 때문에 계속 선택 됩니다.  
  
 마지막 예로, 쿼리를 지정 하면 `SELECT NULL + @p` **int** \@ 형식 (c) 변환이 발생 하므로 p에 대해 int가 선택 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 Tsql 인수를 실행할 수 있는 권한이 필요 \@ 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 선언되지 않은 `@id` 및 `@name` 매개 변수에 필요한 데이터 형식과 같은 정보를 반환합니다.  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR name = @name'  
  
```  
  
 `@id` 매개 변수가 `@params` 참조로 제공된 경우에는 `@id` 매개 변수가 결과 집합에서 생략되고 `@name` 매개 변수만 설명됩니다.  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR NAME = @name',  
@params = N'@id int'  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_describe_first_result_set &#40;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [dm_exec_describe_first_result_set &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [dm_exec_describe_first_result_set_for_object &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)
