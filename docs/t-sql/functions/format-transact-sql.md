---
title: FORMAT(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 46c7becb151b1942b411aefe337717172f207bb9
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="format-transact-sql"></a>FORMAT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지정된 형식 및 선택적 culture로 서식이 지정된 값을 반환합니다. 날짜/시간 및 숫자 값을 문자열로 지정하는 로캘 인식 서식 지정에 FORMAT 함수를 사용합니다. 일반 데이터 형식 변환의 경우 CAST나 CONVERT를 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>인수  
 *value*  
 서식을 지정할 지원되는 데이터 형식의 식입니다. 유효한 형식 목록은 다음 설명 섹션의 표를 참조하세요.  
  
 *format*  
 **nvarchar** 형식 패턴  
  
 *format* 인수는 유효한 .NET Framework 형식 문자열을 표준 형식 문자열(예: "C" 또는 "D") 또는 날짜 및 숫자 값에 대한 사용자 지정 문자 패턴(예: "MMMM DD, yyyy (dddd)")으로 포함해야 합니다. 복합 서식 지정은 지원되지 않습니다. 이러한 형식 지정 패턴에 대한 자세한 설명은 .NET Framework 설명서에서 일반적인 문자열 서식 지정, 사용자 지정 날짜 및 시간 형식 및 사용자 지정 숫자 형식을 참조하세요. 시작할 때 유용한 항목은 "[형식 지정](http://go.microsoft.com/fwlink/?LinkId=211776)"입니다.  
  
 *culture*  
 culture를 지정하는 선택적 **nvarchar** 인수입니다.  
  
 *culture* 인수를 지정하지 않으면 현재 세션의 언어가 사용됩니다. 이 언어는 SET LANGUAGE 문을 사용하여 명시적으로 또는 암시적으로 설정됩니다. *culture*에 지정할 수 있는 culture는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 명시적으로 지원하는 언어로만 국한되지 않으며 .NET Framework에서 인수로 지원하는 모든 culture를 지정할 수 있습니다. *culture* 인수가 유효하지 않을 경우 FORMAT은 오류를 발생시킵니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar** 또는 null  
  
 반환 값의 길이는 *format*에 의해 결정됩니다.  
  
## <a name="remarks"></a>Remarks  
 FORMAT은 *valid*가 아닌 *culture* 이외의 다른 오류에 대해 NULL을 반환합니다. 예를 들어 *format*에 지정된 값이 유효하지 않으면 NULL이 반환됩니다.  
 
 FORMAT 함수는 비결정적입니다.   
  
 FORMAT은 .NET Framework CLR(공용 언어 런타임)이 설치되어 있어야 사용할 수 있습니다.  
  
 이 함수는 CLR이 있어야 실행되므로 원격에서 실행할 수 없습니다. CLR이 설치되어 있어야만 실행되는 함수를 원격에서 호출할 경우 원격 서버에서 오류가 발생합니다.  
  
 FORMAT은 콜론과 마침표를 이스케이프해야 하는 CLR 서식 지정 규칙이 있어야 실행됩니다. 따라서 형식 문자열(두 번째 매개 변수)에 콜론 또는 마침표가 포함된 경우 입력 값(첫 번째 매개 변수)이 **time** 데이터 형식이면 백슬래시로 콜론 또는 마침표를 이스케이프해야 합니다. [4. 시간 데이터 형식이 포함된 FORMAT](#ExampleD)  
  
 다음 표에서는 *value* 인수에 사용할 수 있는 데이터 형식과 함께 .NET Framework 매핑에서 이에 해당하는 데이터 형식을 보여 줍니다.  
  
|범주|형식|.NET 형식|  
|--------------|----------|---------------|  
|숫자|bigint|Int64|  
|숫자|ssNoversion|Int32|  
|숫자|SMALLINT|Int16|  
|숫자|TINYINT|Byte|  
|숫자|decimal|SqlDecimal|  
|숫자|NUMERIC|SqlDecimal|  
|숫자|FLOAT|Double|  
|숫자|REAL|Single|  
|숫자|SMALLMONEY|Decimal|  
|숫자|money|Decimal|  
|날짜 및 시간|날짜|DateTime|  
|날짜 및 시간|Time|TimeSpan|  
|날짜 및 시간|DATETIME|DateTime|  
|날짜 및 시간|smalldatetime|DateTime|  
|날짜 및 시간|Datetime2|DateTime|  
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
 다음 예에서는 사용자 지정 서식을 지정하여 숫자 값의 서식을 지정하는 방법을 보여 줍니다. 이 예는 현재 날짜가 2012년 9월 27일인 경우를 가정합니다. 이러한 서식과 다른 사용자 지정 서식에 대한 자세한 내용은 [사용자 지정 숫자 형식 문자열](http://msdn.microsoft.com/library/0c899ak8.aspx)을 참조하세요.  
  
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
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 **Sales.CurrencyRate** 테이블에서 5개의 행을 반환합니다. **EndOfDateRate** 열은 테이블에 **money** 유형으로 저장됩니다. 이 예에서는 서식이 지정되지 않은 상태로 열이 반환된 다음 .NET 숫자 형식, 일반 형식 및 통화 형식 유형 중 하나로 서식이 지정됩니다. 이러한 형식과 다른 숫자 형식에 대한 자세한 내용은 [표준 숫자 형식 문자열](http://msdn.microsoft.com/library/dwhawy9k.aspx)을 참조하세요.  
  
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
  
###  <a name="ExampleD"></a> 4. 시간 데이터 형식이 포함된 FORMAT  
 이러한 경우 `.` 및 `:`가 이스케이프되지 않으므로 FORMAT에서 NULL을 반환합니다.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 `.` 및 `:`가 이스케이프되지 않으므로 Format에서 서식이 지정된 문자열을 반환합니다.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  
  
## <a name="see-also"></a>참고 항목  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR&#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
