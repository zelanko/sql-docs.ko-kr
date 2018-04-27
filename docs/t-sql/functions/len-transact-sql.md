---
title: LEN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/03/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LEN
- LEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- LEN function
- characters [SQL Server], number of
- number of characters
ms.assetid: fa20fee4-884d-4301-891a-c03e901345ae
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0666ae5b4778b3f573bd99508688959cdf5b1de4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="len-transact-sql"></a>LEN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정한 문자열 식의 후행 공백을 제외한 문자 수를 반환합니다.  
  
> [!NOTE]  
>  식을 표시하는 데 사용된 바이트 수를 반환하려면 [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) 함수를 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
LEN ( string_expression )  
```  
  
## <a name="arguments"></a>인수  
 *string_expression*  
 계산할 문자열 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *string_expression*은 문자나 이진 데이터의 상수, 변수 또는 열일 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 *식*의 데이터 형식이 **varchar(max)**, **nvarchar(max)** 또는 **varbinary(max)** 이면 **bigint**, 그렇지 않으면 **int**입니다.  
  
 SC 데이터 정렬을 사용하는 경우 반환되는 정수 값에서는 UTF-16 서로게이트 쌍이 단일 문자로 계산됩니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 LEN은 후행 공백을 제외합니다. 이것이 문제가 될 경우 문자열을 자르지 않는 [DATALENGTH&#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md) 함수를 사용해 보십시오. 유니코드 문자열을 처리할 경우 DATALENGTH는 문자 수의 두 배를 반환합니다. 다음 예는 후행 공백이 포함된 LEN 및 DATALENGTH를 보여줍니다.  
  
```  
DECLARE @v1 varchar(40),  
    @v2 nvarchar(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [varchar LEN] , DATALENGTH(@v1) AS [varchar DATALENGTH];  
SELECT LEN(@v2) AS [nvarchar LEN], DATALENGTH(@v2) AS [nvarchar DATALENGTH];  
  
```  
  
## <a name="examples"></a>예  
 다음 예에서는 `FirstName`에 있는 사람의 `Australia` 데이터 및 문자 수를 선택합니다. 이 예에서는 AdventureWorks 데이터베이스를 사용합니다.  
  
```  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예는 `FirstName`열의 문자 수를 반환하고 `Australia`에 위치한 직원의 이름과 성을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT LEN(FirstName) AS FNameLength, FirstName, LastName   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.DimGeography AS g   
    ON e.SalesTerritoryKey = g.SalesTerritoryKey   
WHERE EnglishCountryRegionName = 'Australia';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FNameLength  FirstName  LastName  
-----------  ---------  ---------------  
4            Lynn       Tsoflias
```  
  
## <a name="see-also"></a>참고 항목  
 [DATALENGTH&#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [CHARINDEX&#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [PATINDEX&#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)  
 [LEFT&#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)   
 [RIGHT&#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  


