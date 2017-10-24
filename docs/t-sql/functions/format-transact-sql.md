---
title: "형식 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 75f944ad28bc56300db7ca9dd7220036faaea711
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="format-transact-sql"></a>FORMAT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지정된 형식 및 선택적 culture로 서식이 지정된 값을 반환합니다. 날짜/시간 및 숫자 값을 문자열로 지정하는 로캘 인식 서식 지정에 FORMAT 함수를 사용합니다. 일반 데이터 형식 변환의 경우 CAST나 CONVERT를 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>인수  
 *value*  
 서식을 지정할 지원되는 데이터 형식의 식입니다. 유효한 형식 목록은 다음 설명 섹션의 표를 참조하세요.  
  
 *형식*  
 **nvarchar** 형식 패턴입니다.  
  
 *형식* 인수 있어야 유효한.NET Framework 형식 문자열을 표준 형식 문자열 (예를 들어, "C" 또는 "D") 또는 사용자 지정 문자 패턴으로 날짜 및 숫자 값 (예를 들어 "MMMM DD, yyyy (dddd)")에 대 한 . 복합 서식 지정은 지원되지 않습니다. 이러한 서식 지정 패턴의 전체 내용은 일반 형식 지정에 문자열, 사용자 지정 날짜 및 시간 형식 및 사용자 지정 숫자 형식에.NET Framework 설명서를 참조 하십시오. 좋은 출발점 항목은 "[형식](http://go.microsoft.com/fwlink/?LinkId=211776)."  
  
 *문화권*  
 선택적 **nvarchar** 문화권을 지정 하는 인수입니다.  
  
 경우는 *문화권* 인수 제공 하지 않으면, 현재 세션의 언어가 사용 됩니다. 이 언어는 SET LANGUAGE 문을 사용하여 명시적으로 또는 암시적으로 설정됩니다. *문화권* ; 인수로 서.NET Framework에서 지 원하는 모든 culture를 허용 하 여 명시적으로 지 원하는 언어로 제한 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 경우는 *문화권* 인수가 유효 하지 않을, 형식에서 오류가 발생 합니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar** 또는 null  
  
 반환 값의 길이에 의해 결정 됩니다는 *형식*합니다.  
  
## <a name="remarks"></a>주의  
 지정 된 형식 오류에 대 한 아닌 NULL을 반환는 *문화권* 없는 *유효한*합니다. 값에 지정 된 경우 NULL이 반환 하는 예를 들어 *형식* 올바르지 않습니다.  
 
 FORMAT 함수는 비결 정적입니다.   
  
 부여의는.NET Framework 런타임 CLR (공용 언어) 형식을 사용 합니다.  
  
 이 함수는 clr에 의존 하므로 원격 일 수 없습니다. 원격 서비스의 CLR을 필요로 하는 함수는 원격 서버에서 오류가 발생할 수 있습니다.  
  
 형식 서식 설정 규칙 사항이 콜론과 마침표를 이스케이프 해야 하는 CLR에 의존 합니다. 따라서는 형식 (두 번째 매개 변수) 문자열에 콜론 또는 마침표, 콜론 또는 기간 때 입력된 값 백슬래시로 이스케이프 되어야 합니다 (첫 번째 매개 변수)는는 **시간** 데이터 형식입니다. 참조 [D. 형식 시간 데이터 형식으로](#ExampleD)합니다.  
  
 다음 표에서 사용할 수 있는 데이터 형식에 대 한는 *값* 해당.NET Framework 매핑 해당 유형과 함께 인수입니다.  
  
|범주|형식|.NET 형식|  
|--------------|----------|---------------|  
|숫자|bigint|Int64|  
|숫자|int|Int32|  
|숫자|smallint|Int16|  
|숫자|tinyint|Byte|  
|숫자|decimal|SqlDecimal|  
|숫자|numeric|SqlDecimal|  
|숫자|float|Double|  
|숫자|real|Single|  
|숫자|smallmoney|Decimal|  
|숫자|money|Decimal|  
|날짜 및 시간|date|DateTime|  
|날짜 및 시간|time|TimeSpan|  
|날짜 및 시간|datetime|DateTime|  
|날짜 및 시간|smalldatetime|DateTime|  
|날짜 및 시간|datetime2|DateTime|  
|날짜 및 시간|datetimeoffset|DateTimeOffset|  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-format-example"></a>1. 간단한 FORMAT 예  
 다음 예에서는 다양한 culture에 따라 형식이 지정된 간단한 날짜를 반환합니다.  
  
```sql  
DECLARE @d DATETIME = '10/01/2011';  
SELECT FORMAT ( @d, 'd', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'd', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'd', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'd', 'zh-cn' ) AS 'Simplified Chinese (PRC) Result';   
  
SELECT FORMAT ( @d, 'D', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'D', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'D', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'D', 'zh-cn' ) AS 'Chinese (Simplified PRC) Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
US English Result Great Britain English Result  German Result Simplified Chinese (PRC) Result  
----------------  ----------------------------- ------------- -------------------------------------  
10/1/2011         01/10/2011                    01.10.2011    2011/10/1  
  
(1 row(s) affected)  
  
US English Result            Great Britain English Result  German Result                    Chinese (Simplified PRC) Result  
---------------------------- ----------------------------- -----------------------------  ---------------------------------------  
Saturday, October 01, 2011   01 October 2011               Samstag, 1. Oktober 2011        2011年10月1日  
  
(1 row(s) affected)  
```  
  
### <a name="b-format-with-custom-formatting-strings"></a>2. 사용자 지정 서식 문자열이 포함된 FORMAT  
 다음 예에서는 사용자 지정 서식을 지정하여 숫자 값의 서식을 지정하는 방법을 보여 줍니다. 이 예제에서는 현재 날짜가 2012 년 9 월 27 일 이라고 가정 합니다. 이러한 오류 코드 및 기타 사용자 지정 형식에 대 한 자세한 내용은 참조 [사용자 지정 숫자 형식 문자열](http://msdn.microsoft.com/library/0c899ak8.aspx)합니다.  
  
```sql  
DECLARE @d DATETIME = GETDATE();  
SELECT FORMAT( @d, 'dd/MM/yyyy', 'en-US' ) AS 'DateTime Result'  
       ,FORMAT(123456789,'###-##-####') AS 'Custom Number Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DateTime Result  Custom Number Result  
--------------   --------------------  
27/09/2012       123-45-6789  
  
(1 row(s) affected)  
```  
  
### <a name="c-format-with-numeric-types"></a>3. 숫자 유형이 있는 FORMAT  
 5 개의 행을 반환 하는 다음 예제는 **Sales.CurrencyRate** 테이블에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스입니다. 열 **EndOfDateRate** 형식으로 저장 되어 **money** 테이블에 있습니다. 이 예에서는 서식이 지정되지 않은 상태로 열이 반환된 다음 .NET 숫자 형식, 일반 형식 및 통화 형식 유형 중 하나로 서식이 지정됩니다. 이러한 오류 코드 및 다른 숫자 형식에 대 한 자세한 내용은 참조 [표준 숫자 형식 문자열](http://msdn.microsoft.com/library/dwhawy9k.aspx)합니다.  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
            ,FORMAT(EndOfDayRate, 'N', 'en-us') AS 'Number Format'  
            ,FORMAT(EndOfDayRate, 'G', 'en-us') AS 'General Format'  
            ,FORMAT(EndOfDayRate, 'C', 'en-us') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1.00            1.0002          $1.00  
2              1.55          1.55            1.5500          $1.55  
3              1.9419        1.94            1.9419          $1.94  
4              1.4683        1.47            1.4683          $1.47  
5              8.2784        8.28            8.2784          $8.28  
  
(5 row(s) affected)  
  
```  
  
 이 예에서는 독일어 culture(de-de)를 지정합니다.  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
      ,FORMAT(EndOfDayRate, 'N', 'de-de') AS 'Numeric Format'  
      ,FORMAT(EndOfDayRate, 'G', 'de-de') AS 'General Format'  
      ,FORMAT(EndOfDayRate, 'C', 'de-de') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1,00            1,0002          1,00 €  
2              1.55          1,55            1,5500          1,55 €  
3              1.9419        1,94            1,9419          1,94 €  
4              1.4683        1,47            1,4683          1,47 €  
5              8.2784        8,28            8,2784          8,28 €  
  
 (5 row(s) affected)  
```  
  
###  <a name="ExampleD"></a> 4. 시간 데이터 유형이 있는 FORMAT  
 지정 된 형식 때문에 이러한 경우에 NULL을 반환 `.` 및 `:` 는 이스케이프 되지 않습니다.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 때문에 지정 된 형식 반환 서식이 지정 된 문자열의 `.` 및 `:` 이스케이프 됩니다.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

