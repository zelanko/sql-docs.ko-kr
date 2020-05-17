---
title: WHILE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WHILE_TSQL
- WHILE
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], repeated executions
- statement blocks [SQL Server]
- repeated statement executions
- nested WHILE loops
- WHILE keyword
ms.assetid: 52dd29ab-25d7-4fd3-a960-ac55c30c9ea9
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3ee098b61c233bb3012ab1505553873c30edd5d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74095874"
---
# <a name="while-transact-sql"></a>WHILE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]


  SQL 문 또는 문 블록의 반복 실행을 위한 조건을 설정합니다. 문은 지정된 조건이 true인 한 반복적으로 실행됩니다. WHILE 루프 내의 문 실행은 BREAK와 CONTINUE 키워드를 사용하여 루프 내에서 제어할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK | CONTINUE }  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK }  
  
```  
  
## <a name="arguments"></a>인수  
 *Boolean_expression*  
 [TRUE](../../t-sql/language-elements/expressions-transact-sql.md) 또는 **FALSE**를 반환하는 **식**입니다. 부울 식이 SELECT 문을 포함하는 경우에는 SELECT 문을 괄호로 묶어야 합니다.  
  
 {*sql_statement* | *statement_block*}  
 문 블록에 정의된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이나 문 그룹입니다. 문 블록을 정의하려면 흐름 제어 키워드인 BEGIN 및 END를 사용하세요.  
  
 BREAK  
 현재 위치에 해당하는 WHILE 루프를 종료합니다. 루프의 끝을 표시하는 END 키워드 다음에 있는 모든 문은 그대로 실행됩니다.  
  
 CONTINUE  
 CONTINUE 키워드 다음의 모든 문을 무시하고 WHILE 루프가 다시 시작되도록 합니다.  
  
## <a name="remarks"></a>설명  
 둘 이상의 WHILE 루프가 중첩된 경우 내부 루프에 BREAK가 있으면 현재 루프를 종료하고 한 단계 바깥쪽 루프로 이동합니다. 먼저 내부 루프의 끝 이후에 있는 모든 문이 실행된 다음 바깥쪽 루프가 다시 시작됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-break-and-continue-with-nested-ifelse-and-while"></a>A. 중첩된 IF...ELSE 및 WHILE에서 BREAK 및 CONTINUE 사용  
 다음 예에서는 제품의 평균 정가가 `$300` 미만인 경우 `WHILE` 루프가 가격을 두 배로 한 다음 최대 가격을 선택합니다. 최대 가격이 `$500` 이하인 경우 `WHILE` 루프가 다시 시작되어 가격을 다시 두 배로 만듭니다. 이 루프는 최대 가격이 `$500`를 초과할 때까지 가격을 계속 두 배로 만든 다음 `WHILE` 루프를 종료하고 메시지를 출력합니다.  
  
```  
USE AdventureWorks2012;  
GO  
WHILE (SELECT AVG(ListPrice) FROM Production.Product) < $300  
BEGIN  
   UPDATE Production.Product  
      SET ListPrice = ListPrice * 2  
   SELECT MAX(ListPrice) FROM Production.Product  
   IF (SELECT MAX(ListPrice) FROM Production.Product) > $500  
      BREAK  
   ELSE  
      CONTINUE  
END  
PRINT 'Too much for the market to bear';  
```  
  
### <a name="b-using-while-in-a-cursor"></a>B. 커서에 WHILE 사용  
 다음 예에서는 `@@FETCH_STATUS`를 사용하여 `WHILE` 루프에서 커서 작업을 제어합니다.  
  
```  
DECLARE @EmployeeID as nvarchar(256)
DECLARE @Title as nvarchar(50)

DECLARE Employee_Cursor CURSOR FOR  
SELECT LoginID, JobTitle   
FROM AdventureWorks2012.HumanResources.Employee  
WHERE JobTitle = 'Marketing Specialist';  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor INTO @EmployeeID, @Title;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      Print '   ' + @EmployeeID + '      '+  @Title 
      FETCH NEXT FROM Employee_Cursor INTO @EmployeeID, @Title;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO 
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-while-loop"></a>C: 단순 While 루프  
 다음 예에서는 제품의 평균 정가가 `$300` 미만인 경우 `WHILE` 루프가 가격을 두 배로 한 다음 최대 가격을 선택합니다. 최대 가격이 `$500` 이하인 경우 `WHILE` 루프가 다시 시작되어 가격을 다시 두 배로 만듭니다. 최대 가격이 `$500`를 초과할 때까지 이 루프는 가격을 계속 두 배로 늘린 다음, `WHILE` 루프를 종료합니다.  
  
```  
-- Uses AdventureWorks  
  
WHILE ( SELECT AVG(ListPrice) FROM dbo.DimProduct) < $300  
BEGIN  
    UPDATE dbo.DimProduct  
        SET ListPrice = ListPrice * 2;  
    SELECT MAX ( ListPrice) FROM dbo.DimProduct  
    IF ( SELECT MAX (ListPrice) FROM dbo.DimProduct) > $500  
        BREAK;  
END  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [흐름 제어 언어 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [커서&#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  


