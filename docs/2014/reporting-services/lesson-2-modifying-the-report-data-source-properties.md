---
title: '2단원: 보고서 데이터 원본 속성 수정 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 41746f2938afd17e59dc4a9f2278179e4ccc1695
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225119"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>2단원: 보고서 데이터 원본 속성 수정
  이 단원에서는 보고서 관리자를 사용하여 받는 사람에게 배달될 보고서를 선택합니다. 사용자가 정의하는 데이터 기반 구독은 **기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;** 자습서에서 만든 [기본 테이블 보고서 만들기&amp;#40;SSRS 자습서&amp;#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)보고서를 배포합니다. 다음 단계에서는 보고서에서 데이터를 가져오는 데 사용되는 데이터 원본 연결 정보를 수정합니다. **저장된 자격 증명** 을 사용하여 보고서 데이터 원본에 액세스하는 보고서만 데이터 기반 구독을 통해 배포할 수 있습니다. 저장된 자격 증명은 무인 보고서 처리에 필요합니다.  
  
 또한 구독이 특정 주문 및 렌더링 형식에 대해 보고서의 서로 다른 인스턴스를 출력할 수 있도록 `[Order]` 에 대해 보고서를 필터링하는 매개 변수를 사용하기 위해 데이터 세트 및 보고서를 수정합니다.  
  
 **항목 내용**  
  
-   [데이터 원본 속성을 수정 하려면](#bkmk_modify_datasource)  
  
-   [AdventureWorksDataset을 수정 하려면](#bkmk_modify_dataset)  
  
-   [보고서 매개 변수를 추가 하 고 보고서를 다시 게시 하려면](#bkmk_add_reportparameter)  
  
-   [보고서 다시 배포 하려면](#bkmk_redeploy)  
  
##  <a name="bkmk_modify_datasource"></a> 데이터 원본 속성을 수정 하려면  
  
1.  시작 [보고서 관리자 &#40;SSRS 기본 모드&#41; ](../../2014/reporting-services/report-manager-ssrs-native-mode.md) 관리자 권한으로 예를 들어, Internet Explorer에 대 한 아이콘을 마우스 오른쪽 단추로 클릭 하 고 클릭 **관리자 권한으로 실행**.  
  
2.  **Sales Orders** 보고서가 포함된 폴더로 이동하고 보고서의 상황에 맞는 메뉴에서 **관리**를 클릭합니다.  
  
     ![보고서 상황에 맞는 메뉴를 열고 관리 선택](../../2014/tutorials/media/ssrs-tutorial-datadriven-manage-report.gif "보고서 상황에 맞는 메뉴를 열고 관리 선택")  
  
3.  **데이터 원본** 탭을 클릭합니다.  
  
4.  **연결 유형**으로 **Microsoft SQL Server**를 선택합니다.  
  
5.  고객 데이터 원본 연결 문자열이 다음과 같고 샘플 데이터베이스가 로컬 데이터베이스 서버에 있다고 가정합니다.  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
6.  **보고서 서버에 안전하게 저장된 자격 증명**을 클릭합니다.  
  
7.  사용자 이름( *domain\user*형식 사용)과 암호를 입력합니다. [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스에 액세스할 권한이 없으면 해당 권한이 있는 로그인을 지정합니다.  
  
8.  **데이터 원본에 연결할 때 Windows 자격 증명으로 사용**을 클릭한 다음 **확인**을 클릭합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인을 사용하는 경우와 같이 도메인 계정을 사용하지 않는 경우에는 이 확인란을 클릭하지 마십시오.  
  
9. **연결 테스트** 를 클릭하여 데이터 원본에 연결할 수 있는지 확인합니다.  
  
10. **적용**을 클릭합니다.  
  
11. 보고서를 확인하여 지정한 자격 증명으로 보고서가 실행되는지 확인합니다. 보고서를 보려면 **보기** 탭을 클릭합니다. 보고서가 열린 다음에는 Employee 이름을 선택하고 **보고서 보기** 단추를 클릭해야 보고서를 볼 수 있습니다.  
  
##  <a name="bkmk_modify_dataset"></a> AdventureWorksDataset을 수정 하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 Sales Orders 보고서를 엽니다.  
  
2.  `AdventureWorksDataset` 데이터 집합을 마우스 오른쪽 단추로 클릭하고 **데이터 집합 속성**을 클릭합니다.  
  
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
  
4.   **확인**을 클릭합니다.  
  
##  <a name="bkmk_add_reportparameter"></a> 보고서 매개 변수를 추가 하 고 보고서를 다시 게시 하려면  
  
1.   **보고서 데이터** 창에서 **새로 만들기** 를 클릭한 후 **매개 변수...** 를 클릭합니다.  
  
2.  **이름**에서 `OrderNumber`을 입력합니다.  
  
3.  **프롬프트**에 `OrderNumber`를 입력합니다.  
  
4.  **빈 값("") 허용**을 선택합니다.  
  
5.  **Null 값 허용**을 선택합니다.  
  
6.  **확인**을 클릭합니다. 매개 변수가 **보고서 데이터 창** 에 추가되고 다음 이미지와 같이 표시됩니다.  
  
     ![새 매개 변수는 보고서 데이터 창에 추가 됩니다](../../2014/tutorials/media/ssrs-tutorial-datadriven-parameter.gif "새 매개 변수는 보고서 데이터 창에 추가")  
  
7.  **미리 보기** 탭을 클릭하여 보고서를 실행합니다. 매개 변수 입력 상자는 보고서 맨 위에 있습니다. 다음을 수행할 수 있습니다.  
  
    -   매개 변수를 사용하지 않고 보고서 보기를 클릭하여 전체 보고서를 봅니다.  
  
    -   Null 옵션의 선택을 취소하고 주문 번호(예: so71949)를 입력하여 보고서에서 해당 주문 하나만 봅니다.  
  
         ![매개 변수 영역이 표시 되는 보고서 뷰어](../../2014/tutorials/media/ssrs-tutorial-datadriven-reportviewer-parameter.gif "매개 변수 영역이 표시 되는 보고서 뷰어")  
  
8.  다음 단원의 구독 구성에서 이 단원에 수행한 변경 내용을 활용할 수 있도록 보고서를 다시 배포합니다. 테이블 자습서에 사용 된 프로젝트 속성에 대 한 자세한 내용은 게시 하려면 보고서를 보고서 서버 (선택 사항)' 섹션을 참조 하세요.의 [단원 6: 그룹화 및 합계 추가&#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)를 참조하세요.  
  
##  <a name="bkmk_redeploy"></a> 보고서 다시 배포 하려면  
  
1.  다음 단원의 구독 구성에서 이 단원에 수행한 변경 내용을 활용할 수 있도록 보고서를 다시 배포합니다. 테이블 자습서에 사용 된 프로젝트 속성에 대 한 자세한 내용은 게시 하려면 보고서를 보고서 서버 (선택 사항)' 섹션을 참조 하세요.의 [단원 6: 그룹화 및 합계 추가&#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)를 참조하세요.  
  
2.  도구 모음에서 **빌드** 를 클릭한 후 **자습서 배포**를 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 저장된 자격 증명을 사용하여 데이터를 가져오도록 보고서를 구성했습니다. 다음 단원에서는 보고서 관리자의 데이터 기반 구독 페이지를 사용하여 구독을 지정합니다. [3단원: 데이터 기반 구독 정의](../reporting-services/lesson-3-defining-a-data-driven-subscription.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 데이터 원본 관리](report-data/manage-report-data-sources.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
