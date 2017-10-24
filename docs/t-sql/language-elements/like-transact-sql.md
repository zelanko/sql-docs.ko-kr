---
title: "마찬가지로 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ESCAPE
- LIKE
- ESCAPE_TSQL
- LIKE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ESCAPE keyword
- '% (wildcard - character(s) to match)'
- ASCII pattern matching
- pattern searching [SQL Server]
- wildcard characters [SQL Server]
- literals [SQL Server], using wildcards
- character strings [SQL Server], LIKE
- exact matches [SQL Server]
- Boolean functions
- LIKE comparisons
- matching patterns [SQL Server]
- NOT LIKE keyword
ms.assetid: 581fb289-29f9-412b-869c-18d33a9e93d5
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 07a8bb8b08120f08cd54e42dcd332459544c206d
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="like-transact-sql"></a>LIKE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  특정 문자열이 지정된 패턴과 일치하는지를 확인합니다. 패턴은 일반 문자와 와일드카드 문자를 포함할 수 있습니다. 패턴 일치에서 일반 문자는 문자열에 지정된 문자와 정확하게 일치해야 합니다. 그러나 와일드카드 문자는 문자열에서 어느 한 부분만 일치하면 됩니다. LIKE 연산자에 와일드카드 문자를 사용할 경우 = 및 != 문자열 비교 연산자를 사용하는 것보다 훨씬 융통성이 있습니다. 문자열 데이터 형식의 인수가 하나라도 있을 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 가능한 한 이를 문자열 데이터 형식으로 변환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
match_expression [ NOT ] LIKE pattern [ ESCAPE escape_character ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
match_expression [ NOT ] LIKE pattern  
```  
  
## <a name="arguments"></a>인수  
 *match_expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 데이터 형식입니다.  
  
 *패턴*  
 문자에서 검색할 특정 문자열이 며 *match_expression*, 다음과 같은 유효한 와일드 카드 문자를 포함할 수 있습니다. *패턴* 8, 000 바이트의 최대 일 수 있습니다.  
  
|와일드카드 문자|Description|예제|  
|------------------------|-----------------|-------------|  
|%|0개 이상의 문자를 가진 문자열|WHERE title LIKE '%computer%'는 책 제목에 'computer' 단어가 있는 모든 책 제목을 찾습니다.|  
|_ (밑줄)|단일 문자|WHERE au_fname LIKE '_ean'은 ean으로 끝나는 모든 4문자 이름을 찾습니다(Dean, Sean 등).|  
|[ ]|지정된 범위([a-f]) 또는 집합([abcdef])에 있는 단일 문자|WHERE au_lname LIKE '[C-P]arsen'은 arsen으로 끝나고 C와 P 사이의 단일 문자로 시작하는 저자의 성을 찾습니다. 예를 들면 Carsen, Larsen, Karsen 등입니다. 범위 검색에서 범위에 포함되는 문자는 데이터 정렬의 정렬 규칙에 따라 다를 수 있습니다.|  
|[^]|지정된 범위([^a-f]) 또는 집합([^abcdef])에 없는 단일 문자|WHERE au_lname LIKE 'de[^l]%'은 de로 시작하고 이어지는 문자가 l이 아닌 저자의 성을 모두 찾습니다.|  
  
 *escape_character*  
 와일드카드 문자 앞에 입력하여 와일드카드가 일반 문자로 해석되도록 하는 문자입니다. *escape_character* 기본값이 없는 하나의 문자만 반환 해야 하는 문자 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 마찬가지로 TRUE를 반환 합니다는 *match_expression* 지정 된 일치 *패턴*합니다.  
  
## <a name="remarks"></a>주의  
 LIKE를 사용하여 문자열 비교를 수행할 때는 패턴 문자열의 모든 문자가 의미를 가지며 여기에는 선행 및 후행 공백 역시 포함됩니다. 쿼리에서 비교의 결과로 'abc '(abc 다음에 단일 공백이 옴) 문자열이 있는 행을 모두 반환해야 하면 그 열의 값이 abc인 행(공백 없는 abc)은 반환되지 않습니다. 그러나 패턴과 일치되는 식에 있는 후행 공백은 무시됩니다. 쿼리에서 비교의 결과로 'abc'(공백 없는 abc) 문자열이 있는 행을 모두 반환해야 하면 abc로 시작하고 후행 공백이 0개 이상인 행이 모두 반환됩니다.  
  
 포함 하는 패턴을 사용 하 여 문자열 비교 **char** 및 **varchar** 데이터 데이터가 저장 되는 방식 때문에 LIKE 비교가 성공 하지 않을 수 있습니다. 각 데이터 형식의 저장 방식과 LIKE 비교가 실패할 수 있는 상황을 이해하는 것이 중요합니다. 다음 예제에서는 로컬 전달 **char** 변수 저장된 프로시저와 다음 사용 하 여 패턴 일치를 시작 하는 성을 지정 된 문자 집합으로 모든 직원 찾기를 합니다.  
  
```tsql
-- Uses AdventureWorks  
  
CREATE PROCEDURE FindEmployee @EmpLName char(20)  
AS  
SELECT @EmpLName = RTRIM(@EmpLName) + '%';  
SELECT p.FirstName, p.LastName, a.City  
FROM Person.Person p JOIN Person.Address a ON p.BusinessEntityID = a.AddressID  
WHERE p.LastName LIKE @EmpLName;  
GO  
EXEC FindEmployee @EmpLName = 'Barb';  
GO  
```  
  
 에 `FindEmployee` 프로시저 아무 행도 반환 하기 때문에 **char** 변수 (`@EmpLName`) 이름 문자가 20 개 미만인 후행 공백을 포함 합니다. 때문에 `LastName` 열이 **varchar**, 후행 공백을 포함 하지는 합니다. 이 프로시저에서는 후행 공백이 의미를 가지므로 실패합니다.  
  
 그러나 다음 예제에서는 성공에 후행 공백이 추가 되지 않습니다 때문에 **varchar** 변수입니다.  
  
```tsql
-- Uses AdventureWorks  
  
CREATE PROCEDURE FindEmployee @EmpLName varchar(20)  
AS  
SELECT @EmpLName = RTRIM(@EmpLName) + '%';  
SELECT p.FirstName, p.LastName, a.City  
FROM Person.Person p JOIN Person.Address a ON p.BusinessEntityID = a.AddressID  
WHERE p.LastName LIKE @EmpLName;  
GO  
EXEC FindEmployee @EmpLName = 'Barb';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 FirstName      LastName            City
 ----------     -------------------- --------------- 
 Angela         Barbariol            Snohomish
 David          Barber               Snohomish
 (2 row(s) affected)  
 ``` 
 
## <a name="pattern-matching-by-using-like"></a>LIKE를 사용한 패턴 일치  
 LIKE는 ASCII 패턴 일치와 유니코드 패턴 일치를 지원합니다. 경우 모든 인수 (*match_expression*, *패턴*, 및 *escape_character*있을 경우)는 ASCII 문자 데이터 형식 ASCII 패턴 일치가 수행 됩니다. 반면에 인수 중 유니코드 데이터 형식이 있으면 모든 인수를 유니코드로 변환하고 유니코드 패턴 일치를 수행합니다. 유니코드 데이터를 사용 하는 경우 (**nchar** 또는 **nvarchar** 데이터 형식)를 사용 하 여, 후행 공백이 의미를 가지; 하지만 유니코드가 아닌 데이터에 대 한 후행 공백이 중요 하지 않습니다. 유니코드 LIKE는 ISO 표준과 호환되며 ASCII LIKE는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전과 호환됩니다.  
  
 다음 예에서는 ASCII 패턴 일치 및 유니코드 LIKE 패턴 일치가 반환하는 행의 차이를 보여 줍니다.  
  
```tsql  
-- ASCII pattern matching with char column  
CREATE TABLE t (col1 char(30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE col1 LIKE '% King';   -- returns 1 row  
  
-- Unicode pattern matching with nchar column  
CREATE TABLE t (col1 nchar(30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE col1 LIKE '% King';   -- no rows returned  
  
-- Unicode pattern matching with nchar column and RTRIM  
CREATE TABLE t (col1 nchar (30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE RTRIM(col1) LIKE '% King';   -- returns 1 row  
```  
  
> [!NOTE]  
>  LIKE 비교는 데이터 정렬의 영향을 받습니다. 자세한 내용은 [COLLATE&#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)를 참조하세요.  
  
## <a name="using-the--wildcard-character"></a>% 와일드카드 문자 사용  
 LIKE '5%' 기호를 지정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 숫자 5 다음 0개 이상의 문자가 이어지는 문자열을 검색합니다.  
  
 예를 들어 다음 쿼리는 모두 `dm` 문자로 시작하므로 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 모든 동적 관리 뷰를 보여 줍니다.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT Name  
FROM sys.system_views  
WHERE Name LIKE 'dm%';  
GO  
```  
  
 동적 관리 뷰가 아닌 모든 개체를 보려면 `NOT LIKE 'dm%'`를 사용하세요. 총 32개의 개체가 있고 LIKE로 패턴과 일치하는 이름을 13개 찾는다면 NOT LIKE는 LIKE 패턴과 일치하지 않는 19개의 개체를 찾습니다.  
  
 `LIKE '[^d][^m]%'`와 같은 패턴으로는 항상 동일한 이름을 찾지 못할 수 있습니다. 이 패턴에서는 19개의 이름이 아니라 첫 번째 문자가 `d`이거나 두 번째 문자가 `m`인 이름을 제외하고 동적 관리 뷰 이름도 아닌 14개의 이름을 찾게 됩니다. 이것은 부정적인 와일드카드 문자가 있는 일치 문자열은 하나의 와일드카드씩 단계별로 평가되기 때문입니다. 평가 중에 일치되지 않는 항목은 제거됩니다.  
  
## <a name="using-wildcard-characters-as-literals"></a>와일드카드 문자를 리터럴로 사용  
 와일드카드 패턴 일치 문자를 리터럴 문자로 사용할 수 있습니다. 와일드카드 문자를 리터럴 문자로 사용하려면 와일드카드 문자를 대괄호로 묶으세요. 다음 표에서는 LIKE 키워드와 [ ] 와일드카드 문자를 사용하는 여러 가지 예를 보여 줍니다.  
  
|기호|의미|  
|------------|-------------|  
|LIKE '5[%]'|5%|  
|LIKE '[_]n'|_n|  
|LIKE '[a-cdf]'|a, b, c, d 또는 f|  
|LIKE '[-acdf]'|-, a, c, d 또는 f|  
|LIKE '[ [ ]'|[|  
|LIKE ']'|]|  
|LIKE 'abc[_]d%'|abc_d 및 abc_de|  
|LIKE 'abc[def]'|abcd, abce 및 abcf|  
  
## <a name="pattern-matching-with-the-escape-clause"></a>ESCAPE 절을 사용한 패턴 일치  
 하나 이상의 특수 와일드카드 문자를 포함하는 문자열을 검색할 수 있습니다. 예를 들어 customers 데이터베이스의 discounts 테이블은 백분율 기호(%)를 포함하는 할인 값을 저장할 수 있습니다. 백분율 기호를 와일드카드 문자가 아닌 일반 문자로 취급하여 검색하려면 ESCAPE 키워드와 이스케이프 문자를 제공해야 합니다. 예를 들어 예제 데이터베이스에는 30%라는 텍스트를 포함하는 comment 열이 있습니다. comment 열의 어느 위치든 30%라는 문자열이 있는 모든 행을 검색하려면 `WHERE comment LIKE '%30!%%' ESCAPE '!'`와 같은 WHERE 절을 지정합니다. ESCAPE 및 이스케이프 문자를 지정하지 않은 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 30이라는 문자열이 있는 모든 행을 반환합니다.  
  
 LIKE 패턴에서 이스케이프 문자 뒤에 문자가 없는 경우 해당 패턴은 유효하지 않으며 LIKE는 FALSE를 반환합니다. 이스케이프 문자 뒤에 오는 문자가 와일드카드 문자가 아닌 경우 이스케이프 문자는 무시되고 이스케이프 다음에 오는 문자는 패턴 내의 일반 문자로 처리됩니다. 양쪽 대괄호([ ])로 묶여 있는 백분율 기호(%), 밑줄(_) 및 왼쪽 대괄호([) 와일드카드 문자가 여기에 포함됩니다. 또한 양쪽 대괄호 문자([ ]) 안에서 이스케이프 문자를 사용할 수 있으며 캐럿(^), 하이픈(-) 및 오른쪽 대괄호(])를 이스케이프 처리할 수 있습니다.  
  
 0x0000 (**char(0)**)은 Windows 데이터 정렬에서 정의 되지 않은 문자 이며 LIKE에 포함할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-like-with-the--wildcard-character"></a>1. LIKE와 % 와일드카드 문자 사용  
 다음 예에서는 `415` 테이블에서 지역 번호가 `PersonPhone`인 모든 전화 번호를 찾는 방법을 보여 줍니다.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, ph.PhoneNumber  
FROM Person.PersonPhone AS ph  
INNER JOIN Person.Person AS p  
ON ph.BusinessEntityID = p.BusinessEntityID  
WHERE ph.PhoneNumber LIKE '415%'  
ORDER by p.LastName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 
 ```
 FirstName             LastName             Phone
 -----------------     -------------------  ------------
 Ruben                 Alonso               415-555-124  
 Shelby                Cook                 415-555-0121  
 Karen                 Hu                   415-555-0114  
 John                  Long                 415-555-0147  
 David                 Long                 415-555-0123  
 Gilbert               Ma                   415-555-0138  
 Meredith              Moreno               415-555-0131  
 Alexandra             Nelson               415-555-0174  
 Taylor                Patterson            415-555-0170  
 Gabrielle              Russell             415-555-0197  
 Dalton                 Simmons             415-555-0115  
 (11 row(s) affected)  
 ``` 
 
### <a name="b-using-not-like-with-the--wildcard-character"></a>2. NOT LIKE와 % 와일드카드 문자 사용  
 다음 예에서는 `PersonPhone` 테이블에서 `415` 외의 다른 지역 번호를 포함하는 모든 전화 번호를 찾는 방법을 보여 줍니다.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, ph.PhoneNumber  
FROM Person.PersonPhone AS ph  
INNER JOIN Person.Person AS p  
ON ph.BusinessEntityID = p.BusinessEntityID  
WHERE ph.PhoneNumber NOT LIKE '415%' AND p.FirstName = 'Gail'  
ORDER BY p.LastName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 
 ```
FirstName              LastName            Phone
---------------------- -------------------- -------------------
Gail                  Alexander            1 (11) 500 555-0120  
Gail                  Butler               1 (11) 500 555-0191  
Gail                  Erickson             834-555-0132  
Gail                  Erickson             849-555-0139  
Gail                  Griffin              450-555-0171  
Gail                  Moore                155-555-0169  
Gail                  Russell              334-555-0170  
Gail                  Westover             305-555-0100  
(8 row(s) affected)  
```  

### <a name="c-using-the-escape-clause"></a>3. ESCAPE 절 사용  
 다음 예에서는 `ESCAPE` 절과 이스케이프 문자를 사용하여 `10-15%` 테이블의 `c1` 열에서 `mytbl2`와 정확히 일치하는 문자열을 찾는 방법을 보여 줍니다.  
  
```tsql
USE tempdb;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'mytbl2')  
   DROP TABLE mytbl2;  
GO  
USE tempdb;  
GO  
CREATE TABLE mytbl2  
(  
 c1 sysname  
);  
GO  
INSERT mytbl2 VALUES ('Discount is 10-15% off'), ('Discount is .10-.15 off');  
GO  
SELECT c1   
FROM mytbl2  
WHERE c1 LIKE '%10-15!% off%' ESCAPE '!';  
GO  
```  
  
### <a name="d-using-the---wildcard-characters"></a>4. [ ] 와일드카드 문자 사용  
 다음 예제에서 직원을 찾습니다는 `Person` 의 이름이 포함 된 테이블 `Cheryl` 또는 `Sheryl`합니다.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, FirstName, LastName   
FROM Person.Person   
WHERE FirstName LIKE '[CS]heryl';  
GO  
```  
  
 다음 예에서는 `Person` 테이블에서 성이 `Zheng` 또는 `Zhang`인 직원의 행을 찾습니다.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName  
FROM Person.Person  
WHERE LastName LIKE 'Zh[ae]ng'  
ORDER BY LastName ASC, FirstName ASC;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-like-with-the--wildcard-character"></a>5. LIKE와 % 와일드카드 문자 사용  
 다음 예제에서는 검색에 모든 직원의 `DimEmployee` 로 시작 하는 전화 번호를 가진 테이블 `612`합니다.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="f-using-not-like-with-the--wildcard-character"></a>6. NOT LIKE와 % 와일드카드 문자 사용  
 다음 예제에서는에서 모든 전화 번호를 찾습니다는 `DimEmployee` 로 시작 하지 않는 테이블 `612`합니다.  의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone NOT LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="g-using-like-with-the--wildcard-character"></a>7. LIKE와 _ 와일드 카드 문자 사용  
 다음 예제에서는 부터는 지역 번호는 모든 전화 번호를 찾습니다 `6` 와 끝 `2` 에 `DimEmployee` 테이블입니다. Note 지역 번호 전화 번호의 첫 번째 부분 하 고 열 값에 이후에 추가 문자가 존재 하므로 % 와일드 카드 문자 검색 패턴의 끝에도 됩니다.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '6_2%'  
ORDER by LastName;   
```  
  
## <a name="see-also"></a>관련 항목:  
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
 

