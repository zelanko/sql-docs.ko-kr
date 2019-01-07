---
title: '2단원: 보고서 데이터 원본 속성 수정 | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7da1fa318ac1bab2310cb8708215db3456d84d66
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399916"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lesson 2: Modifying the Report Data Source Properties
이 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 자습서 단원에서는 웹 포털을 사용하여 받는 사람에게 배달될 보고서를 선택합니다. 사용자가 정의하는 데이터 기반 구독은 **기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;** 자습서에서 만든 [기본 테이블 보고서 만들기 &#40;SSRS 자습서 &#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)보고서를 배포합니다.  다음 단계에서는 보고서에서 데이터를 가져오는 데 사용되는 데이터 원본 연결 정보를 수정합니다. **저장된 자격 증명** 을 사용하여 보고서 데이터 원본에 액세스하는 보고서만 데이터 기반 구독을 통해 배포할 수 있습니다. 저장된 자격 증명은 무인 보고서 처리에 필요합니다.  
  
또한 구독이 특정 주문 및 렌더링 형식에 대해 보고서의 서로 다른 인스턴스를 출력할 수 있도록 `[Order]` 에 대해 보고서를 필터링하는 매개 변수를 사용하기 위해 데이터 세트 및 보고서를 수정합니다.  
  
## <a name="bkmk_modify_datasource"></a>저장된 자격 증명을 사용하도록 데이터 원본을 수정하려면  
  
1.  관리자 권한으로 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 웹 포털로 이동합니다. 예를 들어 Internet Explorer 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  
 
2.    웹 포털 URL로 이동합니다.  예를 들어 다음과 같이 사용할 수 있습니다.   
    `https://<server name>/reports`보고서를 배포합니다.  
    `https://localhost/reports`
 **참고:** 웹 *포털* URL은 Report *Server* URL인 "Reportserver"가 아니라 "Reports"입니다.  
3.  **Sales Orders** 보고서가 포함된 폴더로 이동하고 보고서의 상황에 맞는 메뉴에서 **관리**를 클릭합니다.  
 
 ![ssrs_tutorial_datadriven_manage_report](../reporting-services/media/ssrs-tutorial-datadriven-manage-report.png)
  
3.  왼쪽 창에서 **데이터 원본** 을 클릭합니다.  
  
4.  **연결 형식** 이 **Microsoft SQL Server**인지 확인합니다.  
  
5.  연결 문자열이 다음과 같고 샘플 데이터베이스가 로컬 데이터베이스 서버에 있다고 가정하는지 확인합니다.  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
6.  **다음 자격 증명 사용**을 클릭합니다.  
  
7. **자격 증명 유형**에서 **Windows 사용자 이름 및 암호**를 선택합니다.
8. 사용자 이름( *domain\user*형식 사용)과 암호를 입력합니다. AdventureWorks2014 데이터베이스에 액세스할 권한이 없으면 해당 권한이 있는 로그인을 지정합니다.  
    
9. **연결 테스트** 를 클릭하여 데이터 원본에 연결할 수 있는지 확인합니다.  
  
10. **저장**을 클릭합니다.
11. **취소**를 클릭합니다.  
  
11. 보고서를 확인하여 지정한 자격 증명으로 보고서가 실행되는지 확인합니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.  
  
## <a name="bkmk_modify_dataset"></a>AdventureWorksDataset을 수정하려면  
 다음 단계에서는 매개 변수를 사용하여 주문 번호에 따라 데이터 세트를 필터링하도록 데이터 세트를 수정합니다.
1.  에서 **Sales Orders** 보고서를 엽니다.(!!) [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  `AdventureWorksDataset` 데이터 집합을 마우스 오른쪽 단추로 클릭하고 **데이터 집합 속성**을 클릭합니다.  
    ![ssrs_tutorial_datadriven_datasetproperties](../reporting-services/media/ssrs-tutorial-datadriven-datasetproperties.png)  
3.  `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` 문 앞에 `Group By` 문을 추가합니다. 전체 쿼리 구문은 다음과 같습니다.  
  
    ```  
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal  
    FROM Sales.SalesPerson AS sp INNER JOIN  
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN  
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN  
       Production.Product AS pp ON sd.ProductID = pp.ProductID  
    INNER JOIN  
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID   
    INNER JOIN  
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID  
  
    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)  
  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID  
    HAVING (ppc.Name = 'Clothing')  
    ```  
  
4.  **확인**을 클릭합니다.  
 다음 단계에서는 보고서에 매개 변수를 추가합니다.  보고서 매개 변수는 데이터 세트 매개 변수를 피드합니다. 
## <a name="bkmk_add_reportparameter"></a>보고서 매개 변수를 추가하고 보고서를 다시 게시하려면  
  
1.  **보고서 데이터** 창에서 매개 변수 폴더를 확장하고 **Ordernumber** 매개 변수를 두 번 클릭합니다.  이 매개 변수는 이전 단계에서 데이터 세트에 매개 변수를 추가할 때 자동으로 생성되었습니다. **새로 만들기** and then  **매개 변수...** 를 클릭합니다.  
 ![ssrs_tutorial_datadriven_parameter](../reporting-services/media/ssrs-tutorial-datadriven-parameter.png) 
2.  **이름** 이 `OrderNumber`인지 확인합니다.  
  
3.  **프롬프트** 가 `OrderNumber`인지 확인합니다.  
  
4.  **빈 값("") 허용**을 선택합니다.  
  
5.  **Null 값 허용**을 선택합니다.  
  
6.  **확인**을 클릭합니다.  
  
7.  **미리 보기** 탭을 클릭하여 보고서를 실행합니다. 보고서 맨 위에 있는 매개 변수 입력 상자를 확인합니다. 다음 작업 중 하나를 수행할 수 있습니다.  
  
    -   매개 변수를 사용하지 않고 보고서 보기를 클릭하여 전체 보고서를 봅니다.  
  
    -   **Null** 옵션의 선택을 취소하고 주문 번호(예: *so71949*)를 입력한 다음 **보고서 보기** 를 클릭하여 보고서에서 해당 주문 하나만 봅니다.  
    ![ssrs_tutorial_datadriven_reportviewer_parameter](../reporting-services/media/ssrs-tutorial-datadriven-reportviewer-parameter.png) 
 
  
## <a name="bkmk_redeploy"></a>보고서 다시 배포  
  
1.  다음 단원의 구독 구성에서 이 단원에 수행한 변경 내용을 활용할 수 있도록 보고서를 다시 배포합니다. 테이블 자습서에 사용된 프로젝트 속성에 대한 자세한 내용을 보려면 [6단원: 그룹화 및 합계 추가&#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)의 '보고서 서버에 보고서를 게시하려면(옵션)' 섹션을 참조하세요.  
  
2.  도구 모음에서 **빌드** 를 클릭한 후 **자습서 배포**를 클릭합니다.  
  
## <a name="next-steps"></a>Next Steps  
+ 저장된 자격 증명을 사용하여 데이터를 가져오도록 보고서를 구성했으며, 매개 변수를 사용하여 데이터를 필터링할 수 있습니다. 
+ 다음 단원에서는 웹 포털 데이터 기반 구독 페이지를 사용하여 구독을 구성합니다. [3단원: 데이터 기반 구독 정의](../reporting-services/lesson-3-defining-a-data-driven-subscription.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[보고서 데이터 원본 관리](../reporting-services/report-data/manage-report-data-sources.md)  
[보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
[데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
  

