---
title: '3단원: 테이블 보고서에 대한 데이터 세트 정의(Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f4c78328e02215520b8d33213e01871f010f62d6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108457"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>3단원: (Reporting Services) 테이블 보고서에 대 한 데이터 집합 정의
  데이터 원본을 정의한 후에는 데이터 세트를 정의해야 합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 보고서에 사용하는 데이터는 *데이터 집합*에 포함됩니다. 데이터 세트에는 데이터 원본에 대한 포인터와 보고서에서 사용하는 쿼리는 물론 계산된 필드 및 변수도 포함됩니다.  
  
 보고서 디자이너에서 쿼리 디자이너를 사용하여 쿼리를 디자인할 수 있습니다. 이 자습서에서는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]**2008** 데이터베이스에서 판매 주문 정보를 검색하는 쿼리를 만듭니다.  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>보고서 데이터에 대한 Transact-SQL 쿼리를 정의하려면  
  
1.  **보고서 데이터** 창에서 **새로 만들기**를 클릭한 다음, **데이터 세트...** 를 클릭합니다. **데이터 집합 속성** 대화 상자가 열립니다.  
  
2.  **이름** 상자에 **AdventureWorksDataset**을 입력합니다.  
  
3.  **내 보고서에 포함된 데이터 집합 사용**을 클릭합니다.  
  
4.  데이터 원본의 이름 AdventureWorks2012가 **데이터 원본** 입력란에 있고 **쿼리 유형** 이 **텍스트**인지 확인합니다.  
  
5.  다음 Transact-SQL 쿼리를 **쿼리** 상자에 입력하거나, 복사하여 붙여 넣습니다.  
  
    ```  
    SELECT   
       soh.OrderDate AS [Date],   
       soh.SalesOrderNumber AS [Order],   
       pps.Name AS Subcat, pp.Name as Product,    
       SUM(sd.OrderQty) AS Qty,  
       SUM(sd.LineTotal) AS LineTotal  
    FROM Sales.SalesPerson sp   
       INNER JOIN Sales.SalesOrderHeader AS soh   
          ON sp.BusinessEntityID = soh.SalesPersonID  
       INNER JOIN Sales.SalesOrderDetail AS sd   
          ON sd.SalesOrderID = soh.SalesOrderID  
       INNER JOIN Production.Product AS pp   
          ON sd.ProductID = pp.ProductID  
       INNER JOIN Production.ProductSubcategory AS pps   
          ON pp.ProductSubcategoryID = pps.ProductSubcategoryID  
       INNER JOIN Production.ProductCategory AS ppc   
          ON ppc.ProductCategoryID = pps.ProductCategoryID  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,   
       soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'  
    ```  
  
6.  (옵션) **쿼리 디자이너** 단추를 클릭합니다. 쿼리가 텍스트 기반 쿼리 디자이너에 표시됩니다. **텍스트로 편집**을 클릭하여 그래픽 쿼리 디자이너로 전환할 수 있습니다. 쿼리 디자이너 도구 모음에서 실행 **(!)** 단추를 클릭하여 쿼리 결과를 봅니다.  
  
     [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스에서 네 가지 테이블의 여섯 필드에 있는 데이터를 봅니다. 쿼리는 Transact-SQL 기능을 별칭으로 사용합니다. 예를 들어 SalesOrderHeader 테이블을 soh라고 부릅니다.  
  
     **확인** 을 클릭하여 쿼리 디자이너를 종료합니다.  
  
7.  **확인** 을 클릭하여 **데이터 집합 속성** 대화 상자를 종료합니다.  
  
     **AdventureWorksDataset** 데이터 집합 및 필드가 보고서 데이터 창에 나타납니다.  
  
## <a name="next-task"></a>다음 태스크  
 보고서에 대한 데이터를 검색하는 쿼리를 지정했습니다. 다음 단원에서는 보고서 레이아웃을 만듭니다. [4단원: 보고서에 테이블 추가&#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리, 보고서 디자이너 SQL Server Data Tools의 디자인 도구 &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)   
 [SQL Server 연결 형식&#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)   
 [자습서: Transact-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
