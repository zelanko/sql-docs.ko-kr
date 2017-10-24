---
title: "CREATE 함수 (SQL 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cad1b2c-5ea0-4001-9060-2f6832ccd057
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 55f1b7e612a1c7d120e06078b0fdba45d6409d36
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-function-sql-data-warehouse"></a>함수 (SQL 데이터 웨어하우스) 만들기
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]에서 사용자 정의 함수를 만듭니다. 사용자 정의 함수는 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 루틴 매개 변수를 허용 하는 복잡 한 계산과 같은 동작을 수행 하 고 값으로 해당 작업의 결과 반환 합니다. 반환 값에는 스칼라 (단일) 값 이어야 합니다. 이 문을 사용하여 다음과 같은 상황에서 다시 사용할 수 있는 루틴을 만들 수 있습니다.  
  
-   SELECT 등의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문  
  
-   함수를 호출하는 응용 프로그램  
  
-   다른 사용자 정의 함수의 정의  
  
-   열에 CHECK 제약 조건 정의  
  
-   저장 프로시저 바꾸기  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
--Transact-SQL Scalar Function Syntax  
CREATE FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
  
<function_option>::=   
{  
    [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
}  
  
```  
  
## <a name="arguments"></a>인수  
 *schema_name*  
 사용자 정의 함수가 속한 스키마의 이름입니다.  
  
 *function_name*  
 사용자 정의 함수의 이름입니다. 함수 이름은 식별자 규칙을 준수 해야 하며 하며 데이터베이스 내에서 고유 해야 합니다.  
  
> [!NOTE]  
>  매개 변수를 지정하지 않은 경우에도 함수 이름 뒤에 괄호를 사용해야 합니다.  
  
 @*p a r a*  
 사용자 정의 함수의 매개 변수입니다. 하나 이상의 매개 변수를 선언할 수 있습니다.  
  
 하나의 함수에 최대 2,100개의 매개 변수를 지정할 수 있습니다. 매개 변수에 기본값이 정의되지 않은 경우 함수를 실행할 때 사용자가 선언된 각 매개 변수의 값을 지정해야 합니다.  
  
 at 기호(@)를 첫 번째 문자로 사용하여 매개 변수 이름을 지정합니다. 매개 변수 이름은 식별자에 대한 규칙을 따라야 합니다. 매개 변수는 함수에서 로컬로 사용되므로 다른 함수에서 동일한 매개 변수 이름을 사용할 수 있습니다. 매개 변수는 상수 대신 사용할 수 있지만 테이블 이름, 열 이름 또는 다른 데이터베이스 개체의 이름 대신 사용할 수는 없습니다.  
  
> [!NOTE]  
>  저장 프로시저나 사용자 정의 함수에 매개 변수를 전달할 때 또는 일괄 처리 문에서 변수를 선언하고 설정할 때 ANSI_WARNINGS는 인식되지 않습니다. 예를 들어, 변수로 정의 되 면 **char (3)**를 하 고 다음 값으로 설정 된 3 자 보다 큰 데이터 잘리고 정의 된 크기는 INSERT 또는 UPDATE 문이 성공 합니다.  
  
 *parameter_data_type*  
 매개 변수 데이터 형식이입니다. 에 대 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수에서 지원 되는 모든 스칼라 데이터 형식 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 허용 됩니다. 타임 스탬프 (rowversion) 데이터 형식이 지원 되는 형식이 아닙니다.  
  
 [=*기본* ]  
 매개 변수의 기본값입니다. 경우는 *기본* 값이 정의 해당 매개 변수에 대해 값을 지정 하지 않고 함수를 실행할 수 있습니다.  
  
 함수의 매개 변수에 기본값을 지정한 경우 기본값을 가져오는 함수를 호출할 때 DEFAULT 키워드를 지정해야 합니다. 이 동작은 매개 변수를 생략할 경우 자동으로 기본값이 사용되는 저장 프로시저에서 기본값이 있는 매개 변수를 사용하는 것과는 다릅니다.  
  
 *return_data_type*  
 스칼라 사용자 정의 함수의 반환 값입니다. 에 대 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수에서 지원 되는 모든 스칼라 데이터 형식 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 허용 됩니다. 타임 스탬프 (rowversion) 데이터 형식이 지원 되는 형식이 아닙니다. 커서, 테이블 스칼라가 아닌 형식은 허용 되지 않습니다.  
  
 *function_body*  
 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.  function_body SELECT 문을 포함할 수 없습니다 및 데이터베이스 데이터를 참조할 수 없습니다.  function_body 테이블이 나 뷰를 참조할 수 없습니다. 함수 본문 결정적인 다른 함수를 호출할 수는 있지만 비결 정적 함수를 호출할 수 없습니다. 
  
 스칼라 함수에서 *function_body* 는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함께 스칼라 값으로 계산 하는 문입니다.  
  
 *scalar_expression*  
 스칼라 함수가 반환하는 스칼라 값을 지정합니다.  
  
 **\<function_option >:: =** 
  
 함수에 다음 옵션 중 하나 이상이 포함되도록 지정합니다.  
  
 SCHEMABINDING  
 함수를 함수가 참조하는 데이터베이스 개체에 바인딩되도록 지정합니다. SCHEMABINDING을 지정하면 함수 정의에 영향을 미치는 방식으로 기본 개체를 수정할 수 없습니다. 함수 정의 자체를 먼저 수정하거나 삭제하여 수정할 개체에 대한 종속성을 제거해야 합니다.  
  
 다음 동작 중 하나만 발생해도 참조하는 개체에 대한 함수 바인딩이 제거됩니다.  
  
-   함수가 삭제된 경우  
  
-   SCHEMABINDING 옵션을 지정하지 않은 상태에서 ALTER 문을 사용하여 함수를 수정한 경우  
  
 다음 조건을 만족하는 경우에만 함수가 스키마에 바인딩될 수 있습니다.  
  
-   함수에서 참조 하는 사용자 정의 함수는 스키마에 바인딩되어야 합니다.  
  
-   함수 및 다른 Udf 함수에서 참조 한 부분 또는 두 부분으로 이루어진 이름을 사용 하 여 참조 됩니다.  
  
-   만 기본 제공 함수 및 동일한 데이터베이스에서 다른 Udf Udf의 본문 내에서 참조할 수 있습니다.  
  
-   CREATE FUNCTION 문을 실행한 사용자는 해당 함수가 참조하는 데이터베이스 개체에 대한 REFERENCES 권한이 있어야 합니다.  
  
 사용 하 여 ALTER SCHEMABINDING을 제거 하려면  
  
 NULL 입력 시 NULL 반환 | **NULL 입력에 대해 호출**  
 지정 된 **OnNULLCall** 특성 스칼라 반환 함수입니다. 이 특성을 지정하지 않으면 기본적으로 CALLED ON NULL INPUT이 적용됩니다. 즉, 인수로 NULL이 전달되는 경우에도 함수 본문이 실행됩니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 SCHEMABINDING 절을 사용하여 사용자 정의 함수를 만들지 않은 경우 기본 개체에 대한 변경 내용이 함수의 정의에 영향을 주어 함수가 호출될 대 예기치 않은 결과를 초래할 수 있습니다. 기본 개체에 대한 변경으로 인해 함수가 최신 상태를 유지하지 못하게 되는 일이 발생하지 않도록 다음 메서드 중 하나를 구현하는 것이 좋습니다.  
  
-   함수를 만들 때 WITH SCHEMABINDING 절을 지정합니다. 이렇게 하면 함수도 수정되지 않는 한 함수 정의에서 참조된 개체를 수정할 수 없습니다.  
  
## <a name="interoperability"></a>상호 운용성  
 함수에서 유효한 문은 다음과 같습니다.  
  
-   대입 문  
  
-   TRY...CATCH 문을 제외한 흐름 제어 문  
  
-   로컬 데이터 변수를 정의 하는 문을 선언 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 사용자 정의 함수는 데이터베이스 상태 수정 동작을 수행하는 데 사용할 수 없습니다.  
  
 사용자 정의 함수는 중첩될 수 있습니다. 즉, 하나의 사용자 정의 함수가 다른 사용자 정의 함수를 호출할 수 있습니다. 중첩 수준은 호출된 함수의 실행이 시작되면 늘어나고 호출된 함수의 실행이 끝나면 줄어듭니다. 사용자 정의 함수는 최대 32 수준까지 중첩될 수 있습니다. 최대 중첩 수준을 초과하면 전체 함수 호출 체인이 실패합니다.   
  
## <a name="metadata"></a>메타데이터  
 이 섹션에는 사용자 정의 함수에 대 한 메타 데이터를 반환 하는 데 사용할 수 있는 시스템 카탈로그 뷰에 나열 됩니다.  
  
 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) :의 정의 표시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수입니다. 예를 들어  
  
```  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o   
    ON m.object_id = o.object_id   
    AND type = ('FN');  
GO  
  
```  
  
 [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) : 사용자 정의 함수에 정의 된 매개 변수에 대 한 정보를 표시 합니다.  
  
 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) : 함수에서 참조 하는 기본 개체를 표시 합니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CREATE FUNCTION 권한과 함수가 생성되는 스키마에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-a-scalar-valued-user-defined-function-to-change-a-data-type"></a>1. 스칼라 반환 사용자 정의 함수를 사용 하 여 데이터 형식을 변경 하려면  
 이 간단한 함수는 **int** 데이터를 입력 및 반환 형식는 **decimal(10,2)** 데이터 형식으로 출력 합니다.  
  
```  
CREATE FUNCTION dbo.ConvertInput (@MyValueIn int)  
RETURNS decimal(10,2)  
AS  
BEGIN  
    DECLARE @MyValueOut int;  
    SET @MyValueOut= CAST( @MyValueIn AS decimal(10,2));  
    RETURN(@MyValueOut);  
END;  
GO  
  
SELECT dbo.ConvertInput(15) AS 'ConvertedValue';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER FUNCTION (SQL Server PDW)](http://msdn.microsoft.com/en-us/25ff3798-eb54-4516-9973-d8f707a13f6c)   
 [DROP FUNCTION (SQL Server PDW)](http://msdn.microsoft.com/en-us/1792a90d-0d06-4852-9dec-6de1b9cd229e)  
  
  



