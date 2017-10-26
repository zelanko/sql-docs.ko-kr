---
title: "고급 편집(조건) 대화 상자 | Microsoft 문서"
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.condition.advancededit.f1
ms.assetid: a0bbe501-78c5-45ad-9087-965d04855663
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 553e8aece3969407a818d98cf69c20bf922d3601
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="advanced-edit-condition-dialog-box"></a>고급 편집(조건) 대화 상자
  **고급 편집** 대화 상자를 사용하여 정책 기반 관리 조건에 대한 복잡한 식을 만들 수 있습니다.  
  
## <a name="options"></a>옵션  
 **셀 값**  
 셀 값을 지정할 때 셀 값에 사용할 함수나 식을 표시합니다. **확인**을 클릭하면 **일반** 페이지에서 **새 조건 만들기** 또는 **조건 열기** 대화 상자의 조건 식 상자에 있는 **필드** 또는 **값** 셀에 셀 값이 표시됩니다.  
  
 **함수 및 속성**  
 사용할 수 있는 함수 및 속성을 표시합니다.  
  
 **세부 정보**  
 함수 서명, 함수 설명, 반환 값 및 예 형식으로 함수 및 속성 정보를 표시합니다.  
  
## <a name="syntax"></a>구문  
 올바른 식의 형식은 다음과 같아야 합니다.  
  
 `{property | function | constant}`  
  
 `{operator}`  
  
 `{property | function | constant}`  
  
## <a name="examples"></a>예  
 일부 올바른 식의 예는 다음과 같습니다.  
  
-   *Property1*> 5  
  
-   *Property1*=*Property2*  
  
-   Add(5, Multiply(.2,*Property1*))<*Property2*  
  
-   *Sometext* IN *Property1*  
  
-   *Property1*< Fn(*Property2*)  
  
-   BitwiseAnd(*Property1*,*Property2*)= 0  
  
## <a name="additional-function-information"></a>추가 함수 정보  
 다음 섹션에서는 정책 기반 관리 조건의 복잡한 식을 만드는 데 사용할 수 있는 함수에 대한 추가 정보를 제공합니다.  
  
> **중요!** 정책 기반 관리 조건을 만드는 데 사용할 수 있는 함수에 항상 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문이 사용되는 것은 아닙니다. 함수를 사용할 때는 예로 든 구문을 따라야 합니다. 예를 들어 **DateAdd** 또는 **DatePart** 함수를 사용할 때는 *datepart* 인수를 작은따옴표로 묶어야 합니다.  
  
|함수|서명|설명|인수|반환 값|예제|  
|--------------|---------------|-----------------|---------------|------------------|-------------|  
|**Add()**|Numeric Add(Numeric *expression1*, Numeric *expression2*)|두 숫자를 더합니다.|*expression1* 및 *expression2* - **bit** 데이터 형식을 제외한 숫자 범주의 데이터 형식에 대한 올바른 식입니다. 숫자 형식을 반환하는 상수, 속성 또는 함수일 수 있습니다.|우선 순위가 높은 인수의 데이터 형식을 반환합니다.|`Add(Property1, 5)`|  
|**Array()**|Array Array(VarArgs *expression*)|값 목록에서 배열을 만듭니다. Sum() 및 Count() 같은 집계 함수에서 사용할 수 있습니다.|*expression* - 배열로 변환되는 식입니다.|배열|`Array(2,3,4,5,6)`|  
|**Avg()**|Numeric Avg(*VarArgs*)|인수 목록에 있는 값의 평균을 반환합니다.|*VarArgs* - **bit** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 변형 식 목록입니다.|반환 형식은 계산된 식 결과의 형식에 의해 결정됩니다.<br /><br /> 식 결과가 **integer**, **decimal**, **money** 및 **smallmoney**, **float** 및 **real** 범주이면 반환 형식은 각각 **int**, **decimal**, **money**및 **float**입니다.|`Avg(1.0, 2.0, 3.0, 4.0, 5.0)``3.0` 를 반환합니다.|  
|**BitwiseAnd()**|Numeric BitwiseAnd(Numeric *expression 1*, Numeric *expression2*)|두 정수 값 간에 비트 논리 AND 연산을 수행합니다.|*expression1* 및 *expression2* - 정수 데이터 형식 범주의 데이터 형식에 대한 올바른 식입니다.|정수 데이터 형식 범주의 값을 반환합니다.|`BitwiseAnd(Property1, Property2)`|  
|**BitwiseOr()**|Numeric BitwiseOr(Numeric *expression1*, Numeric *expression2*)|지정된 두 정수 값 간에 비트 논리적 AND 연산을 수행합니다.|*expression1* 및 *expression2* - 정수 데이터 형식 범주의 데이터 형식에 대한 올바른 식입니다.|정수 데이터 형식 범주의 값을 반환합니다.|`BitwiseOr(Property1, Property2)`|  
|**Concatenate()**|String Concatenate(String *string1*, String *string2*)|두 문자열을 연결합니다.|*string1* 및 *string2* - 연결할 두 문자열로, null이 아닌 유효한 모든 문자열일 수 있습니다.|*string1* 과 *string2*가 차례로 연결된 문자열|`Concatenate("Hello", " World` `")` "`Hello World`"를 반환합니다.|  
|**Count()**|Numeric Count(*VarArgs*)|인수 목록에 있는 항목의 수를 반환합니다.|*VarArgs* - **text**, **image**및 **ntext**를 제외한 유형의 식입니다.|정수 데이터 형식 범주의 값을 반환합니다.|`Count(1.0, 2.0, 3.0, 4.0, 5.0)``5` 를 반환합니다.|  
|**DateAdd()**|DateTime DateAdd(String *datepart*, Numeric *number*, DateTime *date*)|지정한 날짜에 일정 간격을 더한 값을 더해서 새 **datetime** 값을 반환합니다.|*datepart* - 새 값을 반환할 날짜 부분에 대해 지정할 매개 변수입니다. 연도(yy, yyyy), 월(mm, m) 및 dayofyear(dy, y) 등의 형식이 지원됩니다. 자세한 내용은 [DATEADD&#40;Transact-SQL&#41;](../../t-sql/functions/dateadd-transact-sql.md)를 참조하세요.<br /><br /> *number* - *datepart*를 늘리는 데 사용되는 값입니다.<br /><br /> *date* - **datetime** 값을 반환하거나 날짜 형식의 문자열을 반환하는 식입니다.|지정한 날짜에 일정 간격을 더한 값을 기준으로 한 새 **datetime** 값입니다.|**예제:** `DateAdd('day', 21, DateTime('2007-08-06 14:21:50'))` 는 `'2007-08-27 14:21:50'` 를 반환합니다.<br /><br /> 다음은 이 함수에서 지원하는 *dateparts* 및 약어입니다.<br /><br /> **년**: yy, yyyy<br /><br /> **월**: mm, m<br /><br /> **dayofyear**: dy, y<br /><br /> **일**: dd, d<br /><br /> **주**: wk, ww<br /><br /> **평일**: dw, w<br /><br /> **시간**: hh<br /><br /> **분**: mi, n<br /><br /> **초**: ss, s<br /><br /> **밀리초**: ms|  
|**DatePart()**|Numeric DatePart(String *datepart*, DateTime *date*)|지정한 날짜에서 특정 *datepart* 를 나타내는 정수를 반환합니다.|*datepart* - 반환할 날짜 부분을 지정하는 매개 변수입니다. year(yy, yyyy), month(mm, m) 및 dayofyear(dy, y) 등의 형식이 지원됩니다. 자세한 내용은 [DATEPART&#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md)를 참조하세요.<br /><br /> *date* - **datetime** 값을 반환하거나 날짜 형식의 문자열을 반환하는 식입니다.|지정한 날짜에서 특정 *datepart* 를 나타내는 정수 데이터 형식 범주의 값을 반환합니다.|`DatePart('month', DateTime('2007-08-06 14:21:50.620'))``8` 를 반환합니다.|  
|**DateTime()**|DateTime DateTime(String *dateString*)|문자열에서 날짜/시간 값을 만듭니다.|*dateString* - 날짜/시간의 문자열 값입니다.|입력 문자열에서 만든 날짜/시간 값을 반환합니다.|`DateTime('3/12/2006')`|  
|**Divide()**|Numeric Divide(Numeric *expression_dividend*, Numeric *expression_divisor*)|한 숫자를 다른 숫자로 나눕니다.|*expression_dividend* - 나눌 숫자 식입니다. 피제수는 숫자 데이터 형식 범주에서 **datetime** 데이터 형식을 제외한 모든 데이터 형식 중 하나에 대한 올바른 식일 수 있습니다.<br /><br /> *expression_divisor* - 피제수를 나눌 숫자 식입니다. 제수는 **datetime** 데이터 형식을 제외한 숫자 데이터 형식 범주의 데이터 형식 중 하나에 대한 올바른 식일 수 있습니다.|우선 순위가 높은 인수의 데이터 형식을 반환합니다.|**예제:** `Divide(Property1, 2)`<br /><br /> 참고: double 연산이 됩니다. 정수를 비교하려면 결과를 `Round()`와 결합해야 합니다. 예를 들면 `Round(Divide(10, 3), 0) = 3`과 같습니다.|  
|**Enum()**|Numeric Enum(String *enumTypeName*, String *enumValueName*)|문자열에서 열거형 값을 만듭니다.|*enumTypeName* - 열거형 형식 이름입니다.<br /><br /> *enumValueName* - 열거형의 값입니다.|숫자 값으로 열거형 값을 반환합니다.|`Enum('CompatibilityLevel','Version100')`|  
|**Escape()**|String Escape(String *replaceString*, String *stringToEscape*, String *escapeString*)|입력 문자열의 부분 문자열을 지정된 이스케이프 문자열로 이스케이프합니다.|*replaceString* - 입력 문자열입니다.<br /><br /> *stringToEscape* - *replaceString*의 부분 문자열입니다. 앞에 이스케이프 문자열을 추가할 문자열입니다.<br /><br /> *escapeString* - 각 *stringToEscape*인스턴스 앞에 추가할 이스케이프 문자열입니다.|각 *replaceString* 인스턴스 앞에 *stringToEscape* 이 있는 수정된 *escapeString*을 반환합니다.|`Escape("Hello", "l", "[")` "`He[l[lo`"를 반환합니다.|  
|**ExecuteSQL()**|Variant ExecuteSQL(String *returnType*, String *sqlQuery*)|대상 서버에 대해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행합니다.<br /><br /> ExecuteSql()에 대한 자세한 내용은 [ExecuteSql() 함수](http://blogs.msdn.com/b/sqlpbm/archive/2008/07/03/executesql.aspx)를 참조하세요.|*returnType* - [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 반환된 데이터의 반환 형식을 지정합니다. *returnType* 에 유효한 리터럴은 **Numeric**, **String**, **Bool**, **DateTime**, **Array**및 **Guid**입니다.<br /><br /> *sqlQuery* - 실행할 쿼리가 포함된 문자열입니다.||`ExecuteSQL ('Numeric', 'SELECT COUNT(*) FROM msdb.dbo.sysjobs') <> 0`<br /><br /> 대상 SQL Server 인스턴스에 대해 스칼라 반환 Transact-SQL 쿼리를 실행합니다. `SELECT` 문에는 열을 하나만 지정할 수 있으며 첫째 열을 제외한 추가 열은 무시됩니다. 결과 쿼리는 행을 하나만 반환하며 첫째 행을 제외한 추가 행은 무시됩니다. 쿼리에서 빈 집합을 반환할 경우 `ExecuteSQL` 을 기반으로 작성한 조건 식의 평가 결과가 false입니다. `ExecuteSql` 은 **요청 시** 및 **예약 시** 평가 모드를 지원합니다.<br /><br /> -`@@ObjectName`:<br />                      [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)의 이름 필드에 해당합니다. 변수가 현재 개체의 이름으로 바뀝니다.<br /><br /> -`@@SchemaName`: [sys.schemas](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)의 이름 필드에 해당합니다. 해당 사항이 있을 경우 변수가 현재 개체의 스키마 이름으로 바뀝니다.<br /><br /> 참고: ExecuteSQL 문에 작은 따옴표를 포함하려면 작은 따옴표에 두 번째 작은 따옴표를 붙여 이스케이프 처리합니다. 예를 들어 O'Brian이라는 사용자에 대한 참조를 포함하려면 O''Brian을 입력합니다.|  
|**ExecuteWQL()**|Variant ExecuteWQL(string *returnType* , string *namespace*, string *wql*)|제공된 네임스페이스에 대해 WQL 스크립트를 실행합니다. Select 문에는 단일 반환 열만 포함될 수 있습니다. 열을 두 개 이상 제공하면 오류가 throw됩니다.|*returnType* - WQL에서 반환된 데이터의 반환 형식을 지정합니다. 유효한 리터럴은 **Numeric**, **String**, **Bool**, **DateTime**, **Array**및 **Guid**입니다.<br /><br /> *namespace* - 실행할 WMI 네임스페이스입니다.<br /><br /> *wql* - 실행할 WQL이 포함된 문자열입니다.||`ExecuteWQL('Numeric', 'root\CIMV2', 'select NumberOfProcessors from win32_ComputerSystem') <> 0`|  
|**False()**|Bool False()|부울 값 FALSE를 반환합니다.|없음|부울 값 FALSE를 반환합니다.|`IsDatabaseMailEnabled = False()`|  
|**GetDate()**|DateTime GetDate()|시스템 날짜를 반환합니다.|없음|시스템 날짜를 DateTime으로 반환합니다.|`@DateLastModified = GetDate()`|  
|**Guid()**|Guid Guid(String *guidString*)|문자열에서 GUID를 반환합니다.|*guidString* - 만들 GUID의 문자열 표현입니다.|문자열에서 만든 GUID를 반환합니다.|`Guid('12340000-0000-3455-0000-000000000454')`|  
|**IsNull()**|Variant IsNull(Variant *check_expression*, Variant *replacement_value*)|NULL이 아니면 *check_expression* 값이 반환되고, 그렇지 않으면 *replacement_value* 가 반환됩니다. 형식이 다른 경우 *replacement_value* 는 암시적으로 *check_expression*형식으로 변환됩니다.|*check_expression* - NULL 여부를 검사할 식입니다. *check_expression* 은 정책 기반 관리 지원 형식인 Numeric, String, Bool, DateTime, Array 및 Guid일 수 있습니다.<br /><br /> *replacement_value* - *check_expression* 이 NULL일 경우 반환할 식입니다. *replacement_value* 는 암시적으로 *check_expression*형식으로 변환되는 형식이어야 합니다.|*check_expression* 이 NULL이 아닌 경우 *check_expression* 유형이 반환되고, 그렇지 않으면 *replacement_value* 유형이 반환됩니다.||  
|**Len()**|Numeric Len(*string_expression*)|후행 공백을 제외하고 제공된 문자열 식의 문자 수를 반환합니다.|*string_expression* - 계산할 문자열 식입니다.|정수 데이터 형식 범주의 값을 반환합니다.|`Len('Hello')``5` 를 반환합니다.|  
|**Lower()**|String Lower(String*_expression*)|대문자를 모두 소문자로 변환한 후에 문자열을 반환합니다.|*expression* - 원본 문자열 식입니다.|대문자를 모두 소문자로 변환한 후에 원본 문자열 식을 나타내는 문자열을 반환합니다.|`Len('HeLlO')``'hello'` 를 반환합니다.|  
|**Mod()**|Numeric Mod(Numeric *expression_dividend*, Numeric *expression_divisor*)|첫 번째 숫자 식을 두 번째 숫자 식으로 나눈 다음 정수 나머지를 제공합니다.|*expression_dividend* - 나눌 숫자 식입니다. *expression_dividend* 는 정수 또는 숫자 데이터 형식 범주의 데이터 형식 중 하나에 대한 올바른 식이어야 합니다.<br /><br /> *expression_divisor* - 피제수를 나눌 숫자 식입니다. *expression_divisor* 는 정수 또는 숫자 데이터 형식 범주의 데이터 형식 중 하나에 대한 올바른 식이어야 합니다.|정수 데이터 형식 범주의 값을 반환합니다.|`Mod(Property1, 3)`|  
|**Multiply()**|Numeric Multiply(Numeric *expression1*, Numeric *expression2*)|두 식을 곱합니다.|*expression1* 및 *expression2* - **datetime** 데이터 형식을 제외한 숫자 범주의 데이터 형식에 대한 올바른 식입니다.|우선 순위가 높은 인수의 데이터 형식을 반환합니다.|`Multiply(Property1, .20)`|  
|**Power()**|Numeric Power(Numeric *numeric_expression*, Numeric *expression_power*)|지정된 식을 거듭제곱한 값을 반환합니다.|*numeric_expression* - bit 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 식입니다.<br /><br /> *expression_power* - *numeric_expression*을 구할 거듭제곱입니다. *expression_power* - **bit** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 식입니다.|반환 형식은 *numeric_expression*과 같습니다.|`Power(Property1, 3)`|  
|**Round()**|Numeric Round(Numeric *expression*, Numeric *expression_precision*)|특정 길이나 전체 자릿수로 반올림한 숫자 식을 반환합니다.|*expression* - **bit** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 식입니다.<br /><br /> *expression_precision* - 식을 반올림할 전체 자릿수입니다. *expression_precision* 이 양수이면 *numeric_expression* 은 길이로 지정된 10진수 자리의 숫자로 반올림됩니다. *expression_precision* 이 음수이면 *numeric_expression* 은 *expression_precision*에서 지정한 대로 소수점 왼쪽에서 반올림됩니다.|*numeric_expression*과 같은 유형을 반환합니다.|`Round(5.333, 0)`|  
|**String()**|String String(Variant*_expression*)|변형을 문자열로 변환합니다.|*expression* - 문자열로 변환할 변형 식입니다.|변형 식의 문자열 값을 반환합니다.|`String(4)`|  
|**Sum()**|Numeric Sum(*VarArgs*)|인수 목록에 있는 모든 값의 합계를 반환합니다. Sum은 숫자 값에만 사용할 수 있습니다.|*VarArgs*- **bit** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 변형 식 목록입니다.|가장 정확한 식 데이터 형식에서 모든 식 값의 합계를 반환합니다.<br /><br /> 식 결과가 **integer**, **numeric**, **money** 및 **small money**, **float** 및 **real** 범주이면 반환 형식은 각각 **int**, **numeric**, **money**및 **float**입니다.|`Sum(1.0, 2.0, 3.0, 4.0, 5.0)``15` 를 반환합니다.|  
|**True()**|Bool TRUE()|부울 값 TRUE를 반환합니다.||부울 값 TRUE를 반환합니다.|`IsDatabaseMailEnabled = True()`|  
|**Upper()**|String Upper(String*_expression*)|소문자를 모두 대문자로 변환한 후에 문자열을 반환합니다.|*expression* - 원본 문자열 식입니다.|소문자를 모두 대문자로 변환한 후에 원본 문자열 식을 나타내는 문자열을 반환합니다.|`Upper('HeLlO')``'HELLO'` 를 반환합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [새 조건 만들기 또는 조건 열기 대화 상자, 일반 페이지](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md)   
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  

