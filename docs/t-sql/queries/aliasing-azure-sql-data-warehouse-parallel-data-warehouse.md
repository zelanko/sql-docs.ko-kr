---
title: "별칭 지정(Azure SQL Data Warehouse, 병렬 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65d5799c33afabe8ebbdb212c13661699b9fea9e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>별칭 지정(Azure SQL Data Warehouse, 병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  별칭 지정은 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)][!INCLUDE[DWsql](../../includes/dwsql-md.md)] 쿼리에서 테이블 또는 열 이름 대신 짧고 기억하기 쉬운 문자열의 임시 대체를 허용합니다. 테이블 별칭은 JOIN 구문이 열을 참조할 때 정규화된 개체 이름이 필요하기 때문에 JOIN 쿼리에서 자주 사용됩니다.  
  
 별칭은 개체 명명 규칙을 준수하는 단일 단어여야 합니다. 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 “개체 명명 규칙”을 참조하세요. 별칭은 공백을 포함할 수 없고 단일 또는 이중 따옴표로 묶을 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>인수  
 *object_source*  
 원본 테이블 또는 열의 이름입니다.  
  
 AS  
 선택적인 별칭 전치사입니다. 범위 변수 별칭 지정으로 작업할 때 AS 키워드는 금지됩니다.  
  
 *alias*  
 테이블 또는 열에 대해 원하는 임시 참조 이름입니다. 올바른 개체 이름은 모두 사용할 수 있습니다. 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 “개체 명명 규칙”을 참조하세요.  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 여러 Join을 사용하여 쿼리를 보여 줍니다. 이 예에서는 테이블 및 열 별칭 지정을 모두 보여줍니다.  
  
-   열 별칭 지정: 선택 목록에 열을 포함한 열과 식 모두가 이 예에서 별칭이 지정됩니다. `SalesTerritoryRegion AS SalesTR` 단순 열 별칭을 보여줍니다. `Sum(SalesAmountQuota) AS TotalSales` 데모  
  
-   테이블 별칭 지정: `dbo.DimSalesTerritory AS st`은 `dbo.DimSalesTerritory` 테이블에 대해 `st` 별칭을 만드는 방법을 보여줍니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion AS SalesTR,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
  
```  
  
 AS 키워드는 아래와 같이 제외할 수 있지만 일반적으로 가독성을 위해 포함됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) TotalSales, SalesTerritoryRegion SalesTR,  
RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) RankResult  
FROM dbo.DimEmployee e  
INNER JOIN dbo.FactSalesQuota sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
## <a name="see-also"></a>참고 항목  
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
