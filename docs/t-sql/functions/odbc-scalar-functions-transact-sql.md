---
title: ODBC 스칼라 함수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CURDATE ODBC function
- DAYOFMONTH ODBC function
- WEEK ODBC function
- functions, ODBC CONCAT
- SECOND ODBC function
- functions, ODBC CURRENT_TIME
- functions, ODBC HOUR
- functions, ODBC QUARTER
- TRUNCATE ODBC function
- functions, ODBC SECOND
- DAYOFWEEK ODBC function
- CURRENT_DATE ODBC function
- DAYNAME ODBC function
- CURTIME ODBC function
- functions, ODBC CURRENT_DATE
- MINUTE ODBC function
- functions, ODBC BIT_LENGTH
- functions, ODBC OCTET_LENGTH
- CONCAT ODBC function
- MONTHNAME ODBC function
- functions, ODBC DAYOFYEAR
- OCTET_LENGTH ODBC function
- functions [SQL Server], ODBC scalar functions
- BIT_LENGTH ODBC function
- functions, ODBC DAYOFMONTH
- CURRENT_TIME ODBC function
- functions, ODBC CURDATE
- functions, ODBC CURTIME
- functions, ODBC TRUNCATE
- functions, ODBC MONTHNAME
- functions, ODBC DAYNAME
- ODBC scalar functions
- functions, ODBC MINUTE
- functions, ODBC DAYOFWEEK
- QUARTER ODBC function
- DAYOFYEAR ODBC function
- functions, ODBC WEEK
- HOUR ODBC function
ms.assetid: a0df1ac2-6699-4ac0-8f79-f362f23496f1
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0a58f211c1a838cb0089cbc2f3e5e156936d1c7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914746"
---
# <a name="odbc-scalar-functions-transact-sql"></a>ODBC 스칼라 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [ 문에서 ](https://go.microsoft.com/fwlink/?LinkID=88579)ODBC 스칼라 함수[!INCLUDE[tsql](../../includes/tsql-md.md)]를 사용할 수 있습니다. 이러한 문은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 해석되고, 저장 프로시저 및 사용자 정의 함수에 사용될 수 있습니다. 여기에는 문자열, 숫자, 시간, 날짜, 간격, 시스템 함수가 포함됩니다.  
  
## <a name="usage"></a>사용  
 `SELECT {fn <function_name> [ (<argument>,....n) ] }`  
  
## <a name="functions"></a>함수  
 다음 표에는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 중복되지 않은 ODBC 스칼라 함수가 나와 있습니다.  
  
### <a name="string-functions"></a>문자열 함수  
  
|함수|설명|  
|--------------|-----------------|  
|BIT_LENGTH( string_exp ) (ODBC 3.0)|문자열 식의 길이(비트)를 반환합니다.<br /><br /> String_exp를 문자열로 변환하지 않고 지정된 데이터 형식의 내부 크기를 반환합니다.|  
|CONCAT( string_exp1,string_exp2) (ODBC 1.0)|string_exp2와 string_exp1의 연결 결과인 문자열을 반환합니다. 결과 문자열은 DBMS에 종속됩니다. 예를 들어 string_exp1로 표시되는 열이 NULL 값을 포함할 경우 DB2는 NULL을 반환하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 NULL이 아닌 문자열을 반환합니다.|  
|OCTET_LENGTH( string_exp ) (ODBC 3.0)|문자열 식의 길이(바이트)를 반환합니다. 결과는 비트 수를 8로 나눈 값보다 큰 수 중 가장 작은 정수입니다.<br /><br /> String_exp를 문자열로 변환하지 않고 지정된 데이터 형식의 내부 크기를 반환합니다.|  
  
### <a name="numeric-function"></a>숫자 함수  
  
|함수|설명|  
|--------------|-----------------|  
|TRUNCATE( numeric_exp, integer_exp) (ODBC 2.0)|소수점 이하 integer_exp 위치로 잘린 numeric_exp를 반환합니다. integer_exp가 음수인 경우 numeric_exp는 소수점 왼쪽의 &#124;integer_exp&#124; 위치로 잘립니다.|  
  
### <a name="time-date-and-interval-functions"></a>시간, 날짜 및 간격 함수  
  
|함수|설명|  
|--------------|-----------------|  
|CURRENT_DATE( ) (ODBC 3.0)|현재 날짜를 반환합니다.|  
|CURDATE( ) (ODBC 3.0)|현재 날짜를 반환합니다.|  
|CURRENT_TIME`[( time-precision )]` (ODBC 3.0)|현재 현지 시간을 반환합니다. time-precision 인수는 반환된 값의 초 전체 자릿수를 결정합니다.|  
|CURTIME() (ODBC 3.0)|현재 현지 시간을 반환합니다.|  
|DAYNAME( date_exp ) (ODBC 2.0)|date_exp의 날짜 부분에 대한 요일의 데이터 원본별 이름을 포함하는 문자열을 반환합니다. 예를 들어 이름은 일요일부터 토요일이나 일요일까지입니다. Sunday에서 영어를 사용하는 데이터 원본의 경우 이름은 독일어를 사용하는 데이터 원본의 Samstag를 통한 Sonntag입니다.|
|DAYOFMONTH( date_exp ) (ODBC 1.0)|date_exp의 월 필드를 기준으로 해당 월을 정수로 반환합니다. 반환 값은 1-31 범위에 있습니다.|  
|DAYOFWEEK( date_exp ) (ODBC 1.0)|date_exp의 주 필드를 기준으로 해당 주를 정수로 반환합니다. 반환 값은 1-7 범위에 있으며, 여기서 1은 일요일을 나타냅니다.|  
|HOUR( time_exp ) (ODBC 1.0)|time_exp의 시간 필드를 기준으로 해당 시간을 0에서 23 사이의 정수 값으로 반환합니다.|  
|MINUTE( time_exp ) (ODBC 1.0)|time_exp의 분 필드를 기준으로 해당 분을 0에서 59 사이의 정수 값으로 반환합니다.|  
|SECOND( time_exp ) (ODBC 1.0)|time_exp의 초 필드를 기준으로 해당 초를 0에서 59 사이의 정수 값으로 반환합니다.|  
|MONTHNAME( date_exp ) (ODBC 2.0)|date_exp의 월 부분에 대한 월 데이터 원본별 이름을 포함하는 문자열을 반환합니다. 예를 들어, 영어를 사용하는 데이터 원본의 이름은 1월에서 12월 사이 또는 1월부터 12월까지입니다. 이름은 독일어를 사용하는 데이터 원본의 Dezember를 통한 Januar입니다.|  
|QUARTER( date_exp ) (ODBC 1.0)|date_exp의 분기를 1에서 4 사이의 정수 값으로 반환합니다. 이 경우 1은 1월 1일에서 3월 31일까지를 나타냅니다.|  
|WEEK( date_exp ) (ODBC 1.0)|date_exp의 주 필드를 기준으로 해당 연도의 주를 1에서 53 사이의 정수 값으로 반환합니다.|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-an-odbc-function-in-a-stored-procedure"></a>1\. 저장 프로시저에서 ODBC 함수 사용  
 다음 예에서는 저장 프로시저에 ODBC 함수를 사용합니다.  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn OCTET_LENGTH( @string_exp )};  
```  
  
### <a name="b-using-an-odbc-function-in-a-user-defined-function"></a>2\. 사용자 정의 함수에서 ODBC 함수 사용  
 다음 예에서는 사용자 정의 함수에 ODBC 함수를 사용합니다.  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn OCTET_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length.');  
--Returns 38  
  
```  
  
### <a name="c-using-an-odbc-functions-in-select-statements"></a>C. SELECT 문에서 ODBC 함수 사용  
 다음 SELECT 문에서는 ODBC 함수를 사용합니다.  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
SELECT {fn OCTET_LENGTH( @string_exp )};  
-- Returns 38  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn TRUNCATE( 100.123456, 4)};  
-- Returns 100.123400  
SELECT {fn CURRENT_DATE( )};  
-- Returns 2007-04-20  
SELECT {fn CURRENT_TIME(6)};  
-- Returns 10:27:11.973000  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-an-odbc-function-in-a-stored-procedure"></a>D. 저장 프로시저에서 ODBC 함수 사용  
 다음 예에서는 저장 프로시저에 ODBC 함수를 사용합니다.  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn BIT_LENGTH( @string_exp )};  
```  
  
### <a name="e-using-an-odbc-function-in-a-user-defined-function"></a>E. 사용자 정의 함수에서 ODBC 함수 사용  
 다음 예에서는 사용자 정의 함수에 ODBC 함수를 사용합니다.  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn BIT_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length in bits.');  
--Returns 432  
  
```  
  
### <a name="f-using-an-odbc-functions-in-select-statements"></a>F. SELECT 문에서 ODBC 함수 사용  
 다음 SELECT 문에서는 ODBC 함수를 사용합니다.  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn CURRENT_DATE( )};  
-- Returns todays date  
SELECT {fn CURRENT_TIME(6)};  
-- Returns the time  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="see-also"></a>참고 항목  
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  