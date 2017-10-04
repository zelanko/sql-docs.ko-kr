---
title: "별칭 (Azure SQL 데이터 웨어하우스, 병렬 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: edc81ce4377f490b482d920871ad361c98f961c5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>별칭 (Azure SQL 데이터 웨어하우스, 병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  별칭에 테이블 또는 열 이름 대신 짧고 기억 하기 쉬운 문자열의 임시 대체를 통해 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 쿼리 합니다. 테이블 별칭은 조인 구문을 열을 참조할 때는 정규화 된 개체 이름이 필요 하기 때문에 조인 쿼리에서 자주 사용 됩니다.  
  
 별칭 단어 개체 명명 규칙을 준수 해야 합니다. 자세한 내용은 "개체 이름 지정 규칙"의 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다. 별칭에 공백이 포함 될 수 없습니다 및 단일 또는 이중 따옴표로 묶을 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>인수  
 *object_source*  
 원본 테이블 또는 열의 이름입니다.  
  
 AS  
 선택적인 별칭 전치사 합니다. 범위 변수 앨리어싱을 작업할 때 AS 키워드는 금지 됩니다.  
  
 *별칭*  
 테이블 또는 열에 대 한 원하는 임시 참조 이름입니다. 올바른 개체 이름을 사용할 수 있습니다. 자세한 내용은 "개체 이름 지정 규칙"의 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 여러 조인 사용 하 여 쿼리를 보여 줍니다. 이 예에서 테이블 및 열 모두 앨리어싱 보여 줍니다.  
  
-   열 별칭이: 두 열 모두 선택 목록에 열이 포함 된 식은이 예에서 별칭을 지정 하는 및입니다. `SalesTerritoryRegion AS SalesTR`단순 열 별칭을 보여 줍니다. `Sum(SalesAmountQuota) AS TotalSales`보여 줍니다.  
  
-   테이블 별칭 지정: `dbo.DimSalesTerritory AS st` 만드는 방법을 보여 줍니다는 `st` 별칭을 `dbo.DimSalesTerritory` 테이블입니다.  
  
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
  
 AS 키워드 아래와 같이 제외할 수 있지만 일반적으로 가독성을 위해 포함 됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
