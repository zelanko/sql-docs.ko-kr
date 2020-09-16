---
description: 데이터 정렬 선행 규칙
title: 데이터 정렬 선행 규칙 | Microsoft Docs
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
- coercible-default collation label
- precedence [SQL Server], collations
- collation sensitive
- collations [SQL Server], precedence
- explicit collation label [SQL Server]
- implicit collation label
- no-collation label
- collation insensitive
- operators [Transact-SQL], collations
- collation labels
- collation coercion rules
- rules [SQL Server], collations
ms.assetid: 58c4e64b-5634-4c29-aa22-33193282dd27
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 13a960ed74fe9947d82e6dee3701ce1ba6af7648
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547623"
---
# <a name="collation-precedence"></a>데이터 정렬 선행 규칙
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  데이터 정렬 선행 규칙은 데이터 정렬 강제 규칙이라고도 하며 다음 사항을 결정합니다.  
  
-   문자열로 계산되는 식의 최종 결과에 대한 데이터 정렬  
  
-   문자열 입력을 사용하지만 문자열을 반환하지는 않는 LIKE 및 IN과 같은 데이터 정렬 구분 연산자에서 사용하는 데이터 정렬  
  
데이터 정렬 선행 규칙은 다음과 같은 문자열 데이터 유형에만 적용됩니다. **char**, **varchar**, **text**, **nchar**, **nvarchar** 및 **ntext**. 그 외 다른 데이터 형식의 개체는 데이터 정렬 평가에 적용되지 않습니다.  
  
## <a name="collation-labels"></a>데이터 정렬 레이블  
다음 표에서는 모든 개체의 데이터 정렬이 식별되는 4개의 범주를 나열하고 설명합니다. 각 범주의 이름은 데이터 정렬 레이블이라고 합니다.  
  
|데이터 정렬 레이블|개체의 유형|  
|---------------------|----------------------|  
|기본값 강제 변환|모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문자열 변수, 매개 변수, 리터럴, 또는 카탈로그 기본 제공 함수의 출력이나 문자열 입력을 사용하지 않지만 문자열 출력을 만드는 기본 제공 함수<br /><br /> 개체가 사용자 정의 함수, 저장 프로시저 또는 트리거에서 선언된 경우에는 함수, 저장 프로시저 또는 트리거가 만들어진 데이터베이스의 기본 데이터 정렬이 할당됩니다. 개체가 일괄 처리로 선언된 경우에는 연결에 사용하고 있는 현재 데이터베이스의 기본 데이터 정렬이 할당됩니다.|  
|암시적 X|열 참조. 식(X)의 데이터 정렬은 테이블이나 뷰의 열에 대해 정의된 데이터 정렬을 사용합니다.<br /><br /> CREATE TABLE이나 CREATE VIEW 문의 COLLATE 절을 사용하여 열에 데이터 정렬을 명시적으로 할당한 경우에도 열 참조는 암시적으로 분류됩니다.|  
|명시적 X|식의 COLLATE 절을 사용하여 특정 데이터 정렬(X)로 명시적으로 캐스팅된 식|  
|데이터 정렬 없음|식의 값이 암시적 데이터 정렬 레이블의 서로 충돌하는 데이터 정렬을 가진 두 문자열 사이의 작업 결과임을 표시합니다. 식 결과는 데이터 정렬이 없는 것으로 정의됩니다.|  
  
## <a name="collation-rules"></a>데이터 정렬 규칙  
단 하나의 문자열 개체를 참조하는 단순 식의 데이터 정렬 레이블은 참조되는 개체의 데이터 정렬 레이블입니다.  
  
데이터 정렬 레이블이 같은 두 피연산자 식을 참조하는 복합 식의 데이터 정렬 레이블은 피연산자 식의 데이터 정렬 레이블입니다.  
  
데이터 정렬 레이블이 다른 두 피연산자 식을 참조하는 복합 식의 최종 결과의 데이터 정렬 레이블은 다음 규칙에 따라 결정됩니다.  
  
-   암시적에 비해 명시적이 선행 규칙입니다. 기본값 강제 변환에 비해 암시적이 선형 규칙입니다.  
  
     명시적 > 암시적 > 기본값 강제 변환  
  
-   데이터 정렬이 다르게 할당된 두 명시적 식을 결합하면 오류가 발생합니다.  
  
     명시적 X + 명시적 Y = 오류  
  
-   데이터 정렬이 다르게 할당된 두 암시적 식을 결합하면 데이터 정렬이 없는 식이 됩니다.  
  
     암시적 X + 암시적 Y = 데이터 정렬 없음  
  
-   데이터 정렬이 없는 식과 다른 레이블의 데이터 정렬을 가진 식(명시적 데이터 정렬 제외, 다음 규칙 참조)을 결합하면 데이터 정렬이 없는 식이 됩니다.  
  
     데이터 정렬 없음 + 임의의 레이블 = 데이터 정렬 없음  
  
-   데이터 정렬이 없는 식과 명시적 데이터 정렬의 식을 결합하면 명시적 레이블의 식이 됩니다.  
  
     데이터 정렬 없음 + 명시적 X = 명시적  
  
다음은 규칙에 대한 요약입니다.  
  
|피연산자 강제 변환 수준|명시적 X|암시적 X|기본값 강제 변환|데이터 정렬 없음|  
|----------------------------|----------------|----------------|------------------------|-------------------|  
|**명시적 Y**|오류 발생|결과는 명시적 Y|결과는 명시적 Y|결과는 명시적 Y|  
|**암시적 Y**|결과는 명시적 X|결과는 데이터 정렬 없음|결과는 암시적 Y|결과는 데이터 정렬 없음|  
|**기본값 강제 변환**|결과는 명시적 X|결과는 암시적 X|결과는 기본값 강제 변환|결과는 데이터 정렬 없음|  
|**데이터 정렬 없음**|결과는 명시적 X|결과는 데이터 정렬 없음|결과는 데이터 정렬 없음|결과는 데이터 정렬 없음|  
  
다음은 데이터 정렬 선행 규칙에 적용되는 추가 규칙입니다.  
  
-   이미 명시적인 식에 여러 개의 COLLATE 절을 사용할 수 없습니다. 예를 들어 다음 `WHERE` 절은 이미 명시적인 식에 `COLLATE` 절이 지정되어 있으므로 잘못된 경우입니다.  
  
     `WHERE ColumnA = ( 'abc' COLLATE French_CI_AS) COLLATE French_CS_AS`  
  
-   **텍스트** 데이터 형식의 코드 페이지 변환은 허용되지 않습니다. 서로 다른 코드 페이지를 가진 경우 한 데이터 정렬에서 다른 데이터 정렬로 **텍스트** 식을 캐스팅할 수 없습니다. 오른쪽 텍스트 피연산자의 데이터 정렬에 왼쪽 텍스트 피연산자와 다른 코드 페이지가 있는 경우에는 할당 연산자가 값을 할당할 수 없습니다.  
  
데이터 정렬 선행 규칙은 데이터 형식 변환 후에 결정됩니다. 결과 데이터 정렬이 도출된 피연산자는 최종 결과의 데이터 형식을 제공하는 피연산자와 다를 수 있습니다. 예를 들어 다음 일괄 처리를 참조하십시오.  
  
```sql  
CREATE TABLE TestTab  
   (PrimaryKey int PRIMARY KEY,  
    CharCol char(10) COLLATE French_CI_AS  
   )  
  
SELECT *  
FROM TestTab  
WHERE CharCol LIKE N'abc'  
```  
  
간단한 `N'abc'` 식의 유니코드 데이터 형식은 우선 순위가 높은 데이터 형식입니다. 따라서 결과 식은 `N'abc'`에 할당된 유니코드 데이터 형식을 갖게 됩니다. 그러나 `CharCol` 식은 암시적 데이터 정렬 레이블을 가지며 `N'abc'`는 이보다 낮은 강제 변환 수준인 기본값 강제 변환을 가집니다. 따라서 `French_CI_AS`의 `CharCol` 데이터 정렬이 사용됩니다.  
  
### <a name="examples-of-collation-rules"></a>데이터 정렬 규칙의 예  
 다음 예에서는 데이터 정렬 규칙이 어떻게 작동하는지 보여 줍니다. 예를 실행하려면 다음 테스트 테이블을 작성하십시오.  
  
```sql  
USE tempdb;  
GO  
  
CREATE TABLE TestTab (  
   id int,   
   GreekCol nvarchar(10) collate greek_ci_as,   
   LatinCol nvarchar(10) collate latin1_general_cs_as  
   )  
INSERT TestTab VALUES (1, N'A', N'a');  
GO  
```  
  
#### <a name="collation-conflict-and-error"></a>데이터 정렬 충돌 및 오류  
 다음 쿼리의 조건자에는 데이터 정렬 충돌이 있으며 오류가 발생합니다.  
  
```sql  
SELECT *   
FROM TestTab   
WHERE GreekCol = LatinCol;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 448, Level 16, State 9, Line 2  
Cannot resolve collation conflict between 'Latin1_General_CS_AS' and 'Greek_CI_AS' in equal to operation.  
```  
  
#### <a name="explicit-label-vs-implicit-label"></a>명시적 레이블과 암시적 레이블  
 오른쪽 식이 명시적 레이블을 가지므로 다음 쿼리에 있는 조건자는 `greek_ci_as` 데이터 정렬에서 계산됩니다. 이는 왼쪽 식의 암시적 레이블보다 높은 우선 순위를 갖습니다.  
  
```sql  
SELECT *   
FROM TestTab   
WHERE GreekCol = LatinCol COLLATE greek_ci_as;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
id          GreekCol             LatinCol  
----------- -------------------- --------------------  
          1 A                    a  
  
(1 row affected)  
```  
  
#### <a name="no-collation-labels"></a>데이터 정렬 레이블 없음  
다음 쿼리의 `CASE` 식에는 데이터 정렬 레이블이 없으므로 SELECT 목록에 표시할 수 없으며 데이터 정렬 인식 연산자로 연산할 수 없습니다. 그러나 데이터 정렬을 인식하지 않는 연산자로 이 식을 연산하는 것은 가능합니다.  
  
```sql  
SELECT (CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END)   
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 451, Level 16, State 1, Line 1  
Cannot resolve collation conflict for column 1 in SELECT statement.  
```  
  
```sql  
SELECT PATINDEX((CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END), 'a')  
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 446, Level 16, State 9, Server LEIH2, Line 1  
Cannot resolve collation conflict for patindex operation.  
```  
  
```sql  
SELECT (CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END) COLLATE Latin1_General_CI_AS   
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------  
a  
  
(1 row affected)  
```  
  
## <a name="collation-sensitive-and-collation-insensitive"></a>데이터 정렬 인식 및 데이터 정렬 인식 안 함  
연산자와 함수는 데이터 정렬을 인식하거나 또는 인식하지 않습니다.  
  
데이터 정렬 인식  
데이터 정렬 없음 피연산자를 지정하면 컴파일할 때 오류가 발생하는 것을 의미합니다. 식 결과는 데이터 정렬 없음이 될 수 없습니다.  
  
데이터 정렬 인식 안 함  
피연산자와 결과가 데이터 정렬 없음이 될 수 있는 것을 의미합니다.  
  
### <a name="operators-and-collation"></a>연산자 및 데이터 정렬  
비교 연산자와 MAX, MIN, BETWEEN, LIKE, IN 연산자는 데이터 정렬을 인식합니다. 연산자가 사용하는 문자열에는 우선 순위가 높은 피연산자의 데이터 정렬 레이블이 할당됩니다. UNION 문 또한 데이터 정렬을 인식하며 모든 문자열 피연산자와 최종 결과에는 우선 순위가 높은 피연산자의 데이터 정렬이 할당됩니다. UNION 피연산자와 결과의 데이터 정렬 선행 규칙은 열별로 평가됩니다.  
  
할당 연산자는 데이터 정렬을 인식하지 않으며 오른쪽 식이 왼쪽 데이터 정렬로 캐스팅됩니다.  
  
문자열 연결 연산자는 데이터 정렬을 인식하며 두 문자열 피연산자와 결과에는 데이터 정렬 우선 순위가 가장 높은 피연산자의 데이터 정렬 레이블이 할당됩니다. UNION ALL 및 CASE 문은 데이터 정렬을 인식하지 않으며 모든 문자열 피연산자와 최종 결과에는 우선 순위가 가장 높은 피연산자의 데이터 정렬 레이블이 할당됩니다. UNION ALL 피연산자와 결과의 데이터 정렬 선행 규칙은 열별로 평가됩니다.  
  
### <a name="functions-and-collation"></a>함수 및 데이터 정렬  
CAST, CONVERT, COLLATE 함수는 **char**, **varchar** 및 **text** 데이터 형식에 대해 데이터 정렬을 인식합니다. CAST와 CONVERT 함수의 입력과 출력은 문자열이며 출력 문자열에는 입력 문자열의 데이터 정렬 레이블이 적용됩니다. 입력이 문자열이 아닌 경우에는 출력 문자열은 기본값 강제 변환이 되며 연결에 사용하는 현재 데이터베이스의 데이터 정렬이나 CAST 또는 CONVERT를 참조하는 사용자 정의 함수, 저장 프로시저, 트리거를 포함하는 데이터베이스의 데이터 정렬이 할당됩니다.  
  
 문자열을 반환하지만 입력 문자열은 사용하지 않는 기본 제공 함수의 경우 결과 문자열은 기본값 강제 변환이 되며 현재 데이터베이스의 데이터 정렬 또는 함수를 참조하는 사용자 정의 함수, 저장 프로시저, 트리거를 포함하는 데이터베이스의 데이터 정렬이 할당됩니다.  
  
 다음은 함수는 데이터 정렬을 인식하며 입력 문자열의 데이터 정렬 레이블을 출력 문자열에 적용합니다.  

:::row:::
    :::column:::
        CHARINDEX
    :::column-end:::
    :::column:::
        REPLACE
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        DIFFERENCE
    :::column-end:::
    :::column:::
        REVERSE
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        ISNUMERIC
    :::column-end:::
    :::column:::
        RIGHT
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        LEFT
    :::column-end:::
    :::column:::
        SOUNDEX
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        LEN
    :::column-end:::
    :::column:::
        STUFF
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        LOWER
    :::column-end:::
    :::column:::
        SUBSTRING
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        PATINDEX
    :::column-end:::
    :::column:::
        UPPER
    :::column-end:::
:::row-end:::
  
## <a name="see-also"></a>참고 항목  
 [COLLATE&#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [데이터 형식 변환&#40;Database Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
