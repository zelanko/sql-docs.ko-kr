---
title: '3단원: 테이블 보고서에 대한 데이터 세트 정의 | Microsoft Docs'
description: 페이지를 매긴 보고서에 대해 데이터 원본을 정의한 후에는 데이터 세트를 정의해야 합니다. SQL Server Reporting Services에서 보고서에 사용되는 데이터는 데이터 세트에 포함됩니다.
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25c62e0cd615748a764937d6dc2b8e4c952e59a1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75244313"
---
# <a name="lesson-3-define-a-dataset-for-the-table-report---sql-server-reporting-services"></a>3단원: 테이블 보고서에 대한 데이터 세트 정의 - SQL Server Reporting Services

페이지를 매긴 보고서에 대해 데이터 원본을 정의한 후에는 데이터 세트를 정의해야 합니다. [!INCLUDE[ssrsnoversion](../includes/ssrsnoversion-md.md)]에서 보고서에 사용하는 데이터는 *데이터 세트*에 포함됩니다. 데이터 세트에는 데이터 원본에 대한 포인터와 보고서, 계산 필드 및 변수에 사용할 쿼리가 포함됩니다.

보고서 디자이너의 쿼리 디자이너를 사용하여 데이터 세트를 정의합니다. 이 자습서에서는 AdventureWorks2016 데이터베이스에서 판매 주문 정보를 검색하는 쿼리를 만들겠습니다.

## <a name="define-a-transact-sql-query-for-report-data"></a>보고서 데이터에 대한 Transact-SQL 쿼리 정의  

1. **보고서 데이터** 창에서 **새로 만들기** > **데이터 세트...** 를 선택합니다. **데이터 세트 속성** 대화 상자가 열리고 **쿼리** 섹션이 표시됩니다.

    ![vs-data_set_properties_dialog](media/lesson-3-defining-a-dataset-for-the-table-report-reporting-services/vs-dataset-properties-dialog.png)

2. **이름** 텍스트 상자에 “AdventureWorksDataset”를 입력합니다.

3. 그 아래에 있는 **내 보고서에 포함된 데이터 세트 사용** 라디오 단추를 선택합니다.

4. **데이터 원본** 드롭다운 상자에서 AdventureWorks2016을 선택합니다.

5. **쿼리 유형**에서 **텍스트** 라디오 단추를 선택합니다.

6. 다음 Transact-SQL 쿼리를 **쿼리** 텍스트 상자에 입력하거나, 복사하여 붙여넣습니다.

    ```T-SQL
    SELECT
       soh.OrderDate AS [Date],
       soh.SalesOrderNumber AS [Order],
       pps.Name AS [Subcat],
       pp.Name as [Product],
       SUM(sd.OrderQty) AS [Qty],
       SUM(sd.LineTotal) AS [LineTotal]
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
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'
    ```

7. (선택 사항) **쿼리 디자이너** 단추를 선택합니다. 텍스트 기반 ‘쿼리 디자이너’에 쿼리가 표시됩니다.  **Query Designer** 도구 모음에서 ![ssrs_querydesigner_run](media/ssrs-querydesigner-run.png) **실행** 단추를 선택하여 쿼리 결과를 확인합니다. 표시되는 데이터 세트에는 AdventureWorks2016 데이터베이스에 있는 테이블 4개의 필드 6개가 포함됩니다. 쿼리는 Transact-SQL 기능을 별칭으로 사용합니다. 예를 들어 SalesOrderHeader 테이블을 *soh*라고 합니다.

8. **확인**을 선택하여 **쿼리 디자이너**를 종료합니다.

9. **확인**을 선택하여 **데이터 세트 속성** 대화 상자를 종료합니다.

**보고서 데이터** 창에 AdventureWorksDataset 데이터 세트와 필드가 표시됩니다.

   ![ssrs_adventureworksdataset](media/ssrs-adventureworksdataset.png)

## <a name="next-steps"></a>다음 단계

보고서에 대한 데이터를 검색하는 쿼리를 성공적으로 지정했습니다. 다음으로, 보고서 레이아웃을 만들어 보겠습니다. [4단원: 보고서에 테이블 추가&#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

[쿼리 디자인 도구&#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)
[SQL Server 연결 형식&#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)
[자습서: Transact-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)
