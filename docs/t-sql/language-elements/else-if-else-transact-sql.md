---
description: ELSE(IF...ELSE)(Transact-SQL)
title: ELSE(IF...ELSE)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ELSE
- ELSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 6f2b4278-0dea-4603-bbd3-7cbad602a645
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 06c47fb4561844cb92e40301b24068a35d573ccd
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128248"
---
# <a name="else-ifelse-transact-sql"></a>ELSE(IF...ELSE)(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하기 위한 조건을 설정합니다. *Boolean_expression* 이 TRUE로 평가되면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문(*sql_statement*) 다음의 *Boolean_expression* 가 실행됩니다. 선택적인 ELSE 키워드는 *Boolean_expression* 이 FALSE 또는 NULL로 평가될 때 실행되는 대체 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *Boolean_expression*  
 TRUE 또는 FALSE를 반환하는 식입니다. *Boolean_expression* 이 SELECT 문을 포함하는 경우에는 SELECT 문을 괄호로 묶어야 합니다.  
  
 { *sql_statement* | *statement_block* }  
 문 블록에 정의된 유효한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이나 문 그룹입니다. 문 블록(일괄 처리)을 정의하려면 흐름 제어 언어 키워드인 BEGIN과 END를 사용합니다. BEGIN...END 블록 내의 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 유효해도 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 동일한 일괄 처리(문 블록) 내에서 그룹화할 수 없습니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-a-simple-boolean-expression"></a>A. 간단한 부울 식 사용  
 다음 예에 포함된 간단한 부울 식(`1=1`)의 결과는 true이므로 첫째 문이 출력됩니다.  
  
```sql
IF 1 = 1 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
```  
  
 다음 예에 포함된 간단한 부울 식(`1=2`)의 결과는 false이므로 둘째 문이 출력됩니다.  
  
```sql
IF 1 = 2 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
GO  
```  
  
### <a name="b-using-a-query-as-part-of-a-boolean-expression"></a>B. 쿼리를 부울 식의 일부로 사용  
 다음 예에서는 부울 식의 일부로 쿼리를 실행합니다. `Product` 테이블에는 `WHERE` 절을 충족하는 자전거 10대가 있으므로 첫째 print 문이 실행됩니다. 둘째 문이 실행되도록 하려면 `> 5`를 `> 15`로 변경합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
PRINT 'There are more than 5 Touring-3000 bicycles.'  
ELSE PRINT 'There are 5 or less Touring-3000 bicycles.' ;  
GO  
```  
  
### <a name="c-using-a-statement-block"></a>C. 문 블록 사용  
 다음 예에서는 부울 식의 일부로 쿼리를 실행한 후 부울 식의 결과를 기반으로 약간 다른 문 블록을 실행합니다. 각 문 블록은 `BEGIN`으로 시작하여 `END`로 끝납니다.  
  
```sql
USE AdventureWorks2012;  
GO  
DECLARE @AvgWeight DECIMAL(8,2), @BikeCount INT  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
BEGIN  
   SET @BikeCount =   
        (SELECT COUNT(*)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   SET @AvgWeight =   
        (SELECT AVG(Weight)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   PRINT 'There are ' + CAST(@BikeCount AS VARCHAR(3)) + ' Touring-3000 bikes.'  
   PRINT 'The average weight of the top 5 Touring-3000 bikes is ' + CAST(@AvgWeight AS VARCHAR(8)) + '.';  
END  
ELSE   
BEGIN  
SET @AvgWeight =   
        (SELECT AVG(Weight)  
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%' );  
   PRINT 'Average weight of the Touring-3000 bikes is ' + CAST(@AvgWeight AS VARCHAR(8)) + '.' ;  
END ;  
GO  
```  
  
### <a name="d-using-nested-ifelse-statements"></a>D. 중첩된 IF...ELSE 문 사용  
 다음 예제에서는 IF... ELSE 문이 어떻게 다른 문에 중첩될 수 있는지를 보여 줍니다. `@Number` 변수를 `5`, `50` 및 `500`으로 설정하여 각 문을 테스트해 보십시오.  
  
```sql
DECLARE @Number INT;  
SET @Number = 50;  
IF @Number > 100  
   PRINT 'The number is large.';  
ELSE   
   BEGIN  
      IF @Number < 10  
      PRINT 'The number is small.';  
   ELSE  
      PRINT 'The number is medium.';  
   END ;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-query-as-part-of-a-boolean-expression"></a>E. 쿼리를 부울 식의 일부로 사용  
 다음 예에서는 `IF...ELSE`를 사용하여 `DimProduct` 테이블에 있는 항목의 가중치에 따라 두 응답 중 사용자를 표시할 응답을 결정합니다.  
  
```sql
-- Uses AdventureWorks  
  
DECLARE @maxWeight FLOAT, @productKey INTEGER  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight FROM DimProduct WHERE ProductKey=@productKey)   
    (SELECT @productKey, EnglishDescription, Weight, 'This product is too heavy to ship and is only available for pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
ELSE  
    (SELECT @productKey, EnglishDescription, Weight, 'This product is available for shipping or pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [흐름 제어 언어 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [IF...ELSE&#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  


