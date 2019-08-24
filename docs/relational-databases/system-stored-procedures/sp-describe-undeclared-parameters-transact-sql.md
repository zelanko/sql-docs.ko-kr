---
title: sp_describe_undeclared_parameters (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 27d30c4160571274339b5befba8f0b9a8cedb859
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053016"
---
# <a name="sp_describe_undeclared_parameters-transact-sql"></a>sp_describe_undeclared_parameters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  선언 되지 않은 매개 변수에 대 한 메타 데이터가 포함 된 결과 집합 반환을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 합니다. 에 사용 되는 각 매개 변수를 고려 합니다  **\@tsql** 일괄 처리에서 선언 되지 있지만  **\@params**합니다. 이러한 각 매개 변수에 대한 추론된 형식의 정보와 함께 해당 매개 변수에 대한 하나의 행이 포함된 결과 집합이 반환됩니다. 프로시저가 빈 경우 결과 집합을 반환 합니다  **\@tsql** 입력된 일괄 처리 매개 변수가 없는에 선언 된 항목을 제외한  **\@params**합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql
  
sp_describe_undeclared_parameters   
    [ @tsql = ] 'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' data type ] [, ...n]  
```  
  
## <a name="arguments"></a>인수  
`[ \@tsql = ] 'Transact-SQL\_batch'` 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. *Transact SQL_batch* 될 수 있습니다 **nvarchar (** _n_ **)** 하거나 **nvarchar (max)** 합니다.  
  
`[ \@params = ] N'parameters'` \@params 매개 변수에 대 한 선언 문자열을 제공 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 방식으로 sp_executesql과 비슷하게 작동 합니다. *매개 변수* 될 수 있습니다 **nvarchar (** _n_ **)** 하거나 **nvarchar (max)** 합니다.  
  
 에 포함 된 모든 매개 변수의 정의 포함 하는 하나의 문자열인 *Transact SQL_batch*합니다. 문자열은 유니코드 상수 또는 유니코드 변수여야 합니다. 각 매개 변수의 정의는 매개 변수 이름과 데이터 형식으로 구성됩니다. n은 추가 매개 변수 정의를 나타내는 자리 표시자입니다. TRANSACT-SQL 문 또는 문의 일괄 처리에 매개 변수가 없는 경우 \@params가 필요 하지 않습니다. 이 매개 변수의 기본값은 NULL입니다.  
  
 데이터 형식  
 매개 변수의 데이터 형식입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **sp_describe_undeclared_parameters** 항상 반환 상태 성공 시 0 반환 합니다. 절차에서 오류를 throw 하 고 프로시저가 RPC로 호출 된 경우 sys.dm_exec_describe_first_result_set의 error_type 열에 설명 된 대로 오류의 유형별로 반환 상태가 채워집니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 프로시저를 호출한 경우 반환 값은 오류가 발생한 경우에도 항상 0입니다.  
  
## <a name="result-sets"></a>결과 집합  
 **sp_describe_undeclared_parameters** 다음 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int NOT NULL**|결과 집합에서 매개 변수의 서수 위치를 포함합니다. 첫 번째 매개 변수의 위치가 1로 지정됩니다.|  
|**name**|**sysname NOT NULL**|매개 변수의 이름을 포함합니다.|  
|**suggested_system_type_id**|**int NOT NULL**|포함 된 **system_type_id** 로 sys.types에 지정 된 매개 변수의 데이터 형식입니다.<br /><br /> CLR 형식에 대 한도 **system_type_name** 열 NULL을 반환 하므로,이 열은 값 240을 반환 합니다.|  
|**suggested_system_type_name**|**nvarchar (256) NULL**|데이터 형식 이름을 포함합니다. 매개 변수의 데이터 형식에 지정된 인수(length, precision, scale 등)를 포함합니다. 데이터 형식이 사용자 정의 별칭 형식인 경우 기본 시스템 형식이 여기에 지정됩니다. 데이터 형식이 CLR 사용자 정의 데이터 형식인 경우 이 열에 NULL이 반환됩니다. 매개 변수의 형식을 추론할 수 없는 경우 NULL이 반환됩니다.|  
|**suggested_max_length**|**smallint NOT NULL**|Sys.columns를 참조 하세요. 에 대 한 **max_length** 열 설명 합니다.|  
|**suggested_precision**|**tinyint NOT NULL**|Sys.columns를 참조 하세요. 참조하세요.|  
|**suggested_scale**|**tinyint NOT NULL**|Sys.columns를 참조 하세요. 참조하세요.|  
|**suggested_user_type_id**|**int NULL**|CLR 및 별칭 형식의 경우 sys.types에 지정된 대로 열 데이터 형식의 user_type_id를 포함합니다. 그렇지 않으면 NULL입니다.|  
|**suggested_user_type_database**|**sysname NULL**|CLR 및 별칭 형식의 경우 해당 형식이 정의된 데이터베이스의 이름을 포함합니다. 그렇지 않으면 NULL입니다.|  
|**suggested_user_type_schema**|**sysname NULL**|CLR 및 별칭 형식의 경우 해당 형식이 정의된 스키마의 이름을 포함합니다. 그렇지 않으면 NULL입니다.|  
|**suggested_user_type_name**|**sysname NULL**|CLR 및 별칭 형식의 경우 형식 이름입니다. 그렇지 않으면 NULL입니다.|  
|**suggested_assembly_qualified_type_name**|**nvarchar (4000) NULL**|CLR 형식의 경우 형식을 정의하는 어셈블리 및 클래스 이름을 반환합니다. 그렇지 않으면 NULL입니다.|  
|**suggested_xml_collection_id**|**int NULL**|Sys.columns에 지정한 대로 매개 변수 데이터 형식의 xml_collection_id를 포함 합니다. 반환된 형식이 XML 스키마 컬렉션과 연결되지 않은 경우 이 열은 NULL을 반환합니다.|  
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
 **sp_describe_undeclared_parameters** 항상 반환 상태 0 반환 합니다.  
  
 애플리케이션에 매개 변수를 포함할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 지정되고 애플리케이션에서 이러한 문을 어떤 식으로든 처리해야 하는 경우에 가장 일반적으로 사용됩니다. 예로 사용자가 ODBC 매개 변수 구문 사용 하 여 쿼리를 제공 하는 위치 (예: odbctest RowsetViewer) 사용자에 대 한 인터페이스입니다. 애플리케이션은 매개 변수 수를 동적으로 검색하여 해당 정보를 사용자에게 표시해야 합니다.  
  
 다른 예로, 사용자 입력이 없는 경우를 들 수 있습니다. 애플리케이션은 매개 변수를 반복하여 테이블과 같은 다른 위치에서 해당 데이터를 가져와야 합니다. 이 경우 애플리케이션에서 모든 매개 변수 정보를 한 번에 전달할 필요는 없습니다. 대신 모든 매개 변수 정보를 공급자에서 가져오고 데이터 자체는 테이블에서 가져올 수 있습니다. 사용 하 여 코드 **sp_describe_undeclared_parameters** 는 보다 일반적인 이며 나중에 데이터 구조가 변경 하는 경우 수정 해야 할 가능성이 적기입니다.  
  
 **sp_describe_undeclared_parameters** 다음 경우 중 하나에서 오류를 반환 합니다.  
  
-   하는 경우 입력 \@tsql 올바르지 않습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 합니다. 유효성 검사는 구문 분석 하 고 분석 하 여 결정 됩니다는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 합니다. 결정할 때 쿼리 최적화 중 또는 실행 하는 동안 일괄 처리에서 발생 한 오류는 아닙니다 여부는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리가 유효한 합니다.  
  
-   경우 \@문자열로 포함 된 경우 선언 하는 매개 변수가 여러 번 또는 매개 변수는 NULL이 아니고 매개 변수는 구문상 유효한 선언 문자열이 아닌 문자열을 포함 합니다.  
  
-   하는 경우 입력 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리에서 선언 된 매개 변수 이름이 같은 지역 변수를 선언 \@매개 변수입니다.  
  
- 문이 임시 테이블을 참조 하는 경우.

- 쿼리에 다음으로 쿼리되는 영구 테이블 생성이 포함되는 경우
  
 하는 경우 \@tsql 이외의 선언 된 매개 변수가 \@매개 변수, 프로시저 빈 결과 집합을 반환 합니다.  
  
## <a name="parameter-selection-algorithm"></a>매개 변수 선택 알고리즘  
 선언되지 않은 매개 변수가 있는 쿼리의 경우 선언되지 않은 매개 변수에 대한 데이터 형식 추론은 다음 3단계로 진행됩니다.  
  
 **1 단계**  
  
 선언되지 않은 매개 변수가 있는 쿼리에 대한 데이터 형식 추론의 첫 번째 단계는 데이터 형식이 선언되지 않은 매개 변수에 종속되지 않는 모든 하위 식의 데이터 형식을 찾는 것입니다. 다음 식에 대해 형식을 확인할 수 있습니다.  
  
-   열, 상수, 변수 및 선언된 매개 변수  
  
-   UDF(사용자 정의 함수) 호출 결과  
  
-   모든 입력에 대해 선언되지 않은 매개 변수에 종속되지 않는 데이터 형식이 포함된 식  
  
 예를 들어 `SELECT dbo.tbl(@p1) + c1 FROM t1 WHERE c2 = @p2 + 2` 쿼리를 고려할 수 있습니다. 식 dbo.tbl (\@p1) + c1과 c2에 데이터 형식 및 식 \@p1 및 \@p2 + 2 하지 않습니다.  
  
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
  
 **2 단계**  
  
 지정된 된 선언 되지 않은 매개 변수의 \@p, 형식 추론 알고리즘은 가장 안쪽 식 E를 찾습니다 (\@p)이 있는 \@p 이며 다음 중 하나:  
  
-   비교 또는 대입 연산자의 인수  
  
-   사용자 정의 함수(테이블 반환 UDF 포함), 프로시저 또는 메서드의 인수  
  
-   인수에는 **값** 절을 **삽입** 문.  
  
-   인수는 **캐스트** 또는 **변환**합니다.  
  
 형식 추론 알고리즘 대상 데이터 형식 TT를 찾습니다 (\@p) e (\@p). 위 예에 대한 대상 데이터 형식은 다음과 같습니다.  
  
-   비교 또는 대입의 다른 쪽 데이터 형식  
  
-   이 인수가 전달되는 매개 변수의 선언된 데이터 형식  
  
-   이 값이 삽입되는 열의 데이터 형식  
  
-   문이 캐스팅 또는 변환되는 데이터 형식  
  
 예를 들어 `SELECT * FROM t WHERE @p1 = dbo.tbl(@p2 + c1)` 쿼리를 고려할 수 있습니다. 다음 E (\@p1) = \@p1 E (\@p2) = \@p2 + c1 TT (\@p1) TT 및 dbo.tbl의 선언 된 반환 데이터 형식 (\@p2) dbo.tbl의 선언 된 매개 변수 데이터 형식입니다.  
  
 경우 \@p 형식 추론 알고리즘 결정에 2 단계 시작 부분에 나열 된 식에 포함 되지 않은 해당 전자 (\@p)가 포함 된 가장 큰 스칼라 식인 \@p 및 형식 추론 알고리즘 하지 않습니다 계산 대상 데이터 형식 TT (\@p) e (\@p). 예를 들어 쿼리는 SELECT `@p + 2` E 다음 (\@p) = \@p + 2 이며 없습니다 TT (\@p).  
  
 **3 단계**  
  
 이제 해당 전자 (\@p)와 TT (\@p)는 식별, 형식 추론 알고리즘에 대 한 데이터 형식을 추론 \@p는 다음 두 가지 방법 중 하나에서:  
  
-   단순 추론  
  
     경우 E (\@p) = \@p와 TT (\@p) 경우 즉, 존재 \@p가 2 단계 시작 부분에 나열 된 인수 식 중 하나에 직접, 형식 추론 알고리즘의 데이터 형식을 유추 \@TT (p \@p). 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p1 AND @p2 = dbo.tbl(@p3)  
    ```  
  
     데이터 형식에 대 한 \@p1 \@p2 및 \@p3 c1 dbo.tbl의 반환 데이터 형식은 변수의 데이터 형식이 되며 dbo.tbl의 매개 변수 데이터를 각각 입력 합니다.  
  
     특수 사례로 경우 \@p는 인수를 \<, >, \<=, 또는 > = 연산자, 단순 추론 규칙이 적용 되지 않습니다. 이 경우 형식 추론 알고리즘에서는 다음 섹션에 설명된 일반 추론 규칙을 사용합니다. 예를 들어 c1이 데이터 형식 char(30)의 열인 경우 다음 두 가지 쿼리를 고려합니다.  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p  
    SELECT * FROM t WHERE c1 > @p  
    ```  
  
     첫 번째 경우에서 형식 추론 알고리즘 추론 **char(30)** 에 대 한 데이터 형식으로 \@p이이 항목의 앞부분에 규칙에 따라 합니다. 두 번째 경우에서 형식 추론 알고리즘 추론 **varchar(8000)** 다음 섹션의 일반 추론 규칙에 따라 합니다.  
  
-   일반 추론  
  
     단순 추론이 적용되지 않는 경우 선언되지 않은 매개 변수에 대해 다음 데이터 형식이 고려됩니다.  
  
    -   정수 데이터 형식 (**비트**, **tinyint**를 **smallint**, **int**하십시오 **bigint**)  
  
    -   Money 데이터 형식 (**smallmoney**하십시오 **money**)  
  
    -   부동 소수점 데이터 형식 (**부동 소수점**하십시오 **실제**)  
  
    -   **숫자 (38, 19)** -다른 numeric 또는 decimal 데이터 형식 고려 되지 않습니다.  
  
    -   **varchar(8000)** , **varchar (max)** 합니다 **nvarchar(4000)** , 및 **nvarchar (max)** -다른 문자열 데이터 형식 (같은 **텍스트**, **char(8000)** 합니다 **nvarchar(30)** 등)는 고려 되지 않습니다.  
  
    -   **varbinary(8000)** 하 고 **varbinary (max)** -다른 이진 데이터 형식 고려 되지 않습니다 (같은 **이미지**를 **binary(8000)** , **varbinary (30)** 등.).  
  
    -   **날짜**, **time(7)** 를 **smalldatetime**를 **datetime**를 **datetime2(7)** , **datetimeoffset(7)**  -다른 날짜 및 시간 형식, 같은 **time(4)** , 간주 되지 않습니다.  
  
    -   **sql_variant**  
  
    -   **xml**  
  
    -   CLR 시스템 정의 형식 (**hierarchyid**를 **기 하 도형**하십시오 **geography**)  
  
    -   CLR 사용자 정의 형식  
  
### <a name="selection-criteria"></a>선택 조건  
 후보 데이터 형식 중 쿼리를 무효화하는 데이터 형식은 거부됩니다. 형식 추론 알고리즘은 남은 후보 데이터 형식 중에서 다음 규칙에 따라 하나를 선택합니다.  
  
1.  E에 암시적 변환이 가장 작은 수를 생성 하는 데이터 형식 (\@p)을 선택 합니다. 특정 데이터 형식이 E에 대 한 데이터 형식을 생성 하는 경우 (\@p) TT와 다른 (\@p), 형식 추론 알고리즘 E의 데이터 형식에서의 추가 암시적 변환 되도록 것으로 간주 (\@p)를 TT (\@p).  
  
     이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_Int + @p  
    ```  
  
     이 경우 E (\@p)는 Col_Int + \@p와 TT (\@p)는 **int**합니다. **int** 에 대 한 선택은 \@p 생성 되는 암시적 변환이 없으므로 합니다. 다른 데이터 형식은 하나 이상의 암시적 변환을 생성합니다.  
  
2.  변환 수가 가장 적은 데이터 형식에 여러 데이터 형식이 연결된 경우 우선 순위가 가장 높은 데이터 형식이 사용됩니다. 예를 들면 다음과 같습니다.  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_smallint + @p  
    ```  
  
     이 예에서 **int** 하 고 **smallint** 하나의 변환을 생성 합니다. 다른 모든 데이터 형식은 두 번 이상 변환을 생성합니다. 때문에 **int** 우선 **smallint**합니다 **int** 는 \@p. 데이터 형식 우선 순위에 대 한 자세한 내용은 참조 하세요. [데이터 형식 우선 순위 &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)합니다.  
  
     이 규칙은 규칙 1에 따라 연결된 모든 데이터 형식과 우선 순위가 가장 높은 데이터 형식 간에 암시적 변환이 있는 경우에만 적용됩니다. 암시적 변환이 없으면 데이터 형식 추론이 오류와 함께 실패합니다. 예를 들어 다음 쿼리에서 `SELECT @p FROM t`, 데이터 형식에 대 한 모든 데이터 형식 추론이 실패 \@p 좋은 동일 하 게 됩니다. 예를 들어 된 암시적 변환이 없는 **int** 하 **xml**합니다.  
  
3.  두 비슷한 데이터 형식이 규칙 1에 따라 예를 들어 연결할 **varchar(8000)** 하 고 **varchar (max)** 보다 작은 데이터 형식 (**varchar(8000)** ) 선택 됩니다. 동일한 원칙이 적용 됩니다 **nvarchar** 하 고 **varbinary** 데이터 형식입니다.  
  
4.  규칙 1의 목적상, 형식 추론 알고리즘에서 선호하는 변환에는 우선 순위가 있습니다. 가장 선호하는 변환부터 순서대로 나열하면 다음과 같습니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    1.  길이가 다른 동일한 기본 데이터 형식 간의 변환  
  
    2.  동일한 데이터 형식의 고정 길이 및 가변 길이 버전 간의 변환 (예를 들어 **char** 하 **varchar**).  
  
    3.  간의 변환을 **NULL** 하 고 **int**합니다.  
  
    4.  기타 변환  
  
 쿼리에 대 한 예를 들어 `SELECT * FROM t WHERE [Col_varchar(30)] > @p`, **varchar(8000)** (a) 변환이 적합 하기 때문에 선택 됩니다. 쿼리에 대 한 `SELECT * FROM t WHERE [Col_char(30)] > @p`, **varchar(8000)** 여전히 선택 하 고 (b) 형식 변환이 발생 하기 때문에 다른 선택 (같은 **varchar(4000)** ) (d) 형식 변환이 발생 합니다.  
  
 마지막 예로, 쿼리를 지정 `SELECT NULL + @p`, **int** 에 대 한 선택은 \@p 형식 (c) 변환이 있기 때문입니다.  
  
## <a name="permissions"></a>사용 권한  
 실행 하기 위한 권한이 필요 합니다 \@tsql 인수입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [sp_describe_first_result_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)
