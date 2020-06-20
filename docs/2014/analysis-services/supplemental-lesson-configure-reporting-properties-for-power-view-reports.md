---
title: 파워 뷰 보고서의 보고 속성 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ffc5f44-17d3-42d4-bc2c-baf3b4485e2d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 03afd5bdafe30a8684165fef5febae49f210f042
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940214"
---
# <a name="configure-reporting-properties-for-power-view-reports"></a>Power View 보고서의 보고 속성 구성
  이 추가 단원에서는 Adventure Works Internet Sales Model 프로젝트에 대한 보고 속성을 설정해 봅니다. 보고 속성을 사용하면 최종 사용자가 Power View에서 모델 데이터를 쉽게 선택하고 표시할 수 있습니다. 또한 특정 열과 테이블을 숨기고 차트에서 사용할 새 데이터를 만드는 속성을 설정합니다.  
  
 이 단원을 마치고 모델을 SharePoint와 통합된 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 및 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에 재배포하면 데이터 원본을 만들고 데이터 연결 정보를 지정하고 Power View를 시작하고 모델에 대한 보고서를 디자인할 수 있습니다.  
  
 이 단원에서는 Power View 보고서를 만들고 사용하는 방법에 대해 설명하지는 않습니다. 이 단원의 목적은 테이블 형식 모델 작성자에게 이러한 속성 및 Power View에서 모델 데이터가 표시되는 방식에 영향을 주는 설정에 대한 소개를 제공하기 위한 것입니다. Power View 보고서 작성에 대한 자세한 내용은 [자습서: Power View에서 예제 보고서 만들기](https://go.microsoft.com/fwlink/?LinkId=221204)를 참조하십시오.  
  
 이 단원을 완료하기 위한 예상 시간: **30분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 추가 단원은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 추가 단원의 작업을 수행하기 전에 이전의 단원을 모두 완료해야 합니다.  
  
 이 특정 추가 단원을 완료하려면 다음이 필요합니다.  
  
-   테이블 형식 모드에서 실행되는 Analysis Services 인스턴스에 배포할 준비가 되었거나 이미 배포한 Adventure Works Internet Sales Model(이 자습서를 통해 완료됨)  
  
-   테이블 형식 모드에서 실행되는 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 및 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]와 통합되고 Power View r보고서를 지원하도록 구성된 SharePoint 사이트  
  
-   Adventure Works Internet Sales Model을 가리키는 SharePoint 사이트에서 데이터 연결을 만들 수 있는 충분한 권한을 갖고 있어야 합니다.  
  
## <a name="model-properties-that-affect-reporting"></a>보고에 영향을 주는 모델 속성  
 테이블 형식 모델을 만들 때 Power View에서 최종 사용자 보고 환경을 향상시키기 위해 개별 열과 테이블에서 설정할 수 있는 특정 속성이 있습니다. 또한 추가 모델 데이터를 만들어 데이터 시각화 및 보고 클라이언트에 대한 다른 기능을 지원할 수 있습니다. 예제 Adventure Works Internet Sales Model의 경우 다음과 같이 일부 내용을 변경할 수 있습니다.  
  
-   **새 데이터 추가** -DAX 수식을 사용 하 여 계산 열에 새 데이터를 추가 하면 차트에서 표시 하기 쉬운 형식으로 날짜 정보가 생성 됩니다.  
  
-   **최종 사용자에게 유용하지 않는 테이블 및 열 숨기기** - **숨김** 속성은 테이블 및 테이블 열을 보고 클라이언트에 표시할지 여부를 제어합니다. 숨겨진 항목은 여전히 모델의 일부이며 쿼리 및 계산에 계속 사용할 수 있습니다.  
  
-   **한 번 클릭 테이블 사용** -기본적으로 최종 사용자가 필드 목록에서 테이블을 클릭 하는 경우 아무 동작도 발생 하지 않습니다. 테이블을 클릭하면 보고서에 테이블을 추가하도록 이 동작을 변경하려면 테이블에 추가하려는 각 열에 기본 필드 집합을 설정합니다. 이 속성은 최종 사용자가 사용하려는 테이블 열에 설정됩니다.  
  
-   **필요한 경우 그룹화 설정** - **고유한 행 유지** 속성은 열의 값을 식별자 필드와 같이 다른 필드의 값으로 그룹화해야 하는지 여부를 결정합니다\. Customer Name(예: John Smith라는 이름을 가진 여러 고객)과 같이 중복 값이 포함된 열의 경우 최종 사용자에게 올바른 결과를 제공하기 위해 **행 식별자** 필드에서 그룹화(고유한 행 유지)해야 합니다.  
  
-   **데이터 형식 및 데이터 서식 설정** - 기본적으로 파워 뷰는 열 데이터 형식을 기준으로 규칙을 적용하여 필드를 측정값으로 사용할 수 있는지 여부를 결정합니다. 파워 뷰의 각 데이터 시각화에도 측정값 및 비 측정값을 배치할 수 있는지에 관한 규칙이 있기 때문에 최종 사용자에 대해 원하는 동작을 수행하기 위해 모델에서 데이터 형식을 설정하거나 기본값을 재정의하는 것이 중요합니다.  
  
-   열 기준 **정렬 속성 설정** -열 기준 **정렬** 속성은 열의 값을 다른 필드의 값으로 정렬할지 여부를 지정 합니다. 예를 들어 월 이름이 포함된 Month Calendar 열에서 Month Number 열을 기준으로 정렬합니다.  
  
## <a name="hide-tables-from-client-tools"></a>클라이언트 도구에서 테이블 숨기기  
 Product 테이블에 Product Category 계산 열과 Product Subcategory 계산 열이 이미 있으므로 Product Category 및 Product Subcategory 테이블을 클라이언트 애플리케이션에 표시하지 않아도 됩니다.  
  
#### <a name="to-hide-the-product-category-and-product-subcategory-tables"></a>Product Category 및 Product Subcategory 테이블을 숨기려면  
  
1.  모델 디자이너에서 **Product Category** 테이블(탭)을 마우스 오른쪽 단추로 클릭한 다음 **클라이언트 도구에서 숨기기**를 클릭합니다.  
  
2.  **Product Subcategory** 테이블(탭)을 마우스 오른쪽 단추로 클릭한 다음 **클라이언트 도구에서 숨기기**를 클릭합니다.  
  
## <a name="create-new-data-for-charts"></a>차트의 새 데이터 만들기  
 경우에 따라 DAX 수식을 사용하여 모델에서 새 데이터를 만들어야 할 수 있습니다. 이 태스크에서는 Date 테이블에 새 계산 열 두 개를 추가합니다. 이러한 새 열은 차트에서 사용하기 편리한 서식으로 날짜 필드를 제공합니다.  
  
#### <a name="to-create-new-data-for-charts"></a>차트의 새 데이터를 만들려면  
  
1.  **Date** 테이블에서 맨 오른쪽으로 스크롤한 다음 **열 추가**를 클릭합니다.  
  
2.  수식 입력줄에 다음 수식을 사용하여 새 계산 열 두 개를 추가합니다.  
  
    |열 이름|Formula|  
    |-----------------|-------------|  
    |연도 분기|=[Calendar Year] & " Q" & [Calendar Quarter]|  
    |Year Month|=[Calendar Year] & FORMAT([Month],"#00")|  
  
## <a name="default-field-set"></a>기본 필드 집합  
 기본 필드 집합은 보고서 필드 목록에서 테이블을 클릭할 때 Power View 보고서 캔버스에 자동으로 추가되는 테이블에 대한 미리 정의된 열 및 측정값 목록입니다. 기본적으로 이 테이블이 Power View 보고서에서 표시될 때 사용자가 확인할 수 있도록 기본 열, 측정 값 및 필드 순서를 지정할 수 있습니다.  Internet Sales 모델의 경우 Customer, Geography 및 Product 테이블에 대한 기본 필드 집합 및 순서를 정의합니다. 포함된 내용은 Power View 보고서를 사용하여 Adventure Works Internet Sales 데이터를 분석할 때 사용자가 확인하려는 가장 일반적인 열입니다.  
  
 기본 필드 집합에 대한 자세한 내용은 SQL Server 온라인 설명서에서 [파워 뷰 보고서의 기본 필드 집합 구성&#40;SSAS 테이블 형식&#41;](tabular-models/power-view-configure-default-field-set-for-reports.md).  
  
#### <a name="to-set-default-field-set-for-tables"></a>테이블에 대한 기본 필드 집합을 설정하려면  
  
1.  모델 디자이너에서 **Customer** 테이블(탭)을 클릭합니다.  
  
2.  **속성** 창의 **보고 속성**에 있는 **기본 필드 집합** 속성에서 **편집하려면 클릭** 을 클릭하여 **기본 필드 집합** 대화 상자를 엽니다.  
  
3.  **기본 필드 집합** 대화 상자의 **테이블의 필드** 목록 상자에서 Ctrl 키를 누르고 다음 필드를 선택한 다음 **추가**를 클릭합니다.  
  
     **Birth Date**, **Customer Alternate Id**, **First Name**, **Last Name**  
  
4.  **기본 필드 순서** 창에서 위로 이동 및 아래로 이동 단추를 사용하여 다음 순서로 놓습니다.  
  
     **Customer Alternate Id**  
  
     **이름**  
  
     **성**  
  
     **생년월일**.  
  
5.  **확인** 을 클릭하여 **Customer** 테이블에 대한 **기본 필드 집합** 대화 상자를 닫습니다.  
  
6.  **Geography** 테이블에 대해서도 이와 동일한 단계를 수행합니다. 다음 필드를 선택하고 이 순서대로 놓습니다.  
  
     **City**, **State Province Code**, **State Region Code**  
  
7.  마지막으로 **Product** 테이블에 대해서도 이와 동일한 단계를 수행합니다. 다음 필드를 선택하고 이 순서대로 놓습니다.  
  
     **Product Alternate Id**, **Product Name**  
  
## <a name="table-behavior"></a>테이블 동작  
 테이블 동작 속성을 사용하여 다른 시각화 유형에 대한 기본 동작 및 Power View 보고서에 사용된 테이블에 대한 그룹화 동작을 변경할 수 있습니다. 이렇게 하면 이름, 이미지 또는 제목 등 바둑판식 배열, 카드 및 차트 레이아웃의 식별 정보의 기본 배치가 향상됩니다.  
  
 테이블 동작 속성에 대한 자세한 내용은 SQL Server 온라인 설명서의 [파워 뷰 보고서의 테이블 동작 속성 구성&#40;SSAS 테이블 형식&#41;](tabular-models/power-view-configure-table-behavior-properties-for-reports.md)을 참조하세요.  
  
#### <a name="to-set-table-behavior-for-tables"></a>테이블에 대한 테이블 동작을 설정하려면  
  
1.  모델 디자이너에서 **Customer** 테이블(탭)을 클릭합니다.  
  
2.  **속성** 창의 **테이블 동작** 속성에서 **편집하려면 클릭**을 클릭하여 **테이블 동작** 대화 상자를 엽니다.  
  
3.  **테이블 동작** 대화 상자의 **행 식별자** 드롭다운 목록 상자에서 **Customer Id** 열을 선택합니다.  
  
4.  **고유한 행 유지** 목록 상자에서 **First Name** 과 **Last Name**을 선택합니다.  
  
     이 속성 설정은 예를 들어 이름이 같은 직원이 둘 이상 있는 경우와 같이 중복된 경우 고유한 값으로 처리되어야 하는 값을 제공하는 열을 지정합니다.  
  
5.  **기본 레이블** 드롭다운 목록 상자에서 **Last Name** 열을 선택합니다.  
  
     이 속성 설정은 행 데이터를 표시하도록 표시 이름을 제공하는 열을 지정합니다.  
  
6.  **Geography** 테이블에 대해 이 단계를 반복합니다. **Geography Id** 열을 행 식별자로 선택하고 **고유한 행 유지** 목록 상자에서 **City** 열을 선택합니다. 이 테이블에 대해 기본 레이블을 설정하지 않아도 됩니다.  
  
7.  **Product** 테이블에 대해 이 단계를 반복합니다. **Product Id** 열을 행 식별자로 선택하고 **고유한 행 유지** 목록 상자에서 **Product Name** 열을 선택합니다. **기본 레이블**에 대해 **Product Alternate Id**를 선택합니다.  
  
## <a name="reporting-properties-for-columns"></a>열의 보고 속성  
 여러 기본 열 속성과 모델 보고 환경을 향상시키기 위해 설정할 수 있는 열의 특정 보고 속성이 있습니다. 예를 들어 사용자는 모든 테이블의 모든 열을 보지 않아도 됩니다. 이전에는 열의 Hidden 속성을 사용 하 여 Product Category 및 Product 하위 범주 테이블을 숨긴 것 처럼 다른 방법으로 표시 되는 테이블에서 특정 열을 숨길 수 있습니다. 데이터 형식 및 열 기준 정렬 등 다른 속성은 열 데이터가 보고서에서 어떻게 표시될 수 있는지에도 영향을 줄 수 있습니다. 이제 특정 열에서 이러한 일부 속성을 설정합니다. 다른 열에는 어떤 동작도 수행하지 않으며 아래에 표시되지 않습니다.  
  
 여기에서는 다른 열 속성의 일부만 설정하지만 이외에도 많은 속성이 있습니다. 열 보고 속성에 대한 자세한 내용은 SQL Server 온라인 설명서에서 [열 속성&#40;SSAS 테이블 형식&#41;](tabular-models/properties-ssas-tabular.md)을 참조하세요.  
  
#### <a name="to-set-properties-for-columns"></a>열 속성을 설정하려면  
  
1.  모델 디자이너에서 **Customer** 테이블(탭)을 클릭합니다.  
  
2.  **Customer Id** 열을 클릭하여 열 속성을 **속성** 창에 표시합니다.  
  
3.  **속성** 창에서 **숨김** 속성을 True로 설정합니다. 그러면 모델 디자이너에서 **Customer Id** 열이 회색으로 나타납니다.  
  
4.  이러한 단계를 반복합니다. 다음 열과 지정된 각 테이블의 보고 속성을 설정합니다. 다른 속성은 모두 기본 설정으로 둡니다.  
  
     **고객**  
  
    |열|속성|값|  
    |------------|--------------|-----------|  
    |Geography Id|숨김|True|  
    |Birth Date|데이터 형식|간단한 날짜|  
  
     **날짜**  
  
    > [!NOTE]  
    >  7단원: 날짜 테이블로 표시에서 날짜 테이블로 표시 설정을 사용하여 날짜 테이블을 모델 날짜 테이블로 선택하고 날짜 테이블의 날짜 열을 고유 식별자로 사용할 열로 선택했으므로 날짜 열의 행 식별자 속성이 자동으로 True로 설정되며 변경할 수 없습니다. DAX 수식에서 시간 인텔리전스 함수를 사용할 때는 날짜 테이블을 지정해야 합니다. 이 모델에서는 시간 인텔리전스 함수를 사용하여 이전 분기 및 현재 분기 등 다양한 기간에 대해 KPI에서도 사용할 판매 데이터를 측정하는 여러 측정값을 만들었습니다. 날짜 테이블 지정 방법에 대한 자세한 내용은 SQL Server 온라인 설명서에서 [시간 인텔리전스에 사용할 날짜 테이블로 표시 지정&#40;SSAS 테이블 형식&#41;](tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)을 참조하세요.  
  
    |열|속성|값|  
    |------------|--------------|-----------|  
    |날짜|데이터 형식|간단한 날짜|  
    |Day Number of Week|숨김|True|  
    |Day Name|열 기준 정렬|Day Number of Week|  
    |Day Of Week|숨김|True|  
    |Day of Month|숨김|True|  
    |Day of Year|숨김|True|  
    |Month Name|열 기준 정렬|Month|  
    |월|숨김|True|  
    |Month Calendar|숨김|True|  
    |Fiscal Quarter|숨김|True|  
    |Fiscal Year|숨김|True|  
    |Fiscal Semester|숨김|True|  
  
     **지리**  
  
    |열|속성|값|  
    |------------|--------------|-----------|  
    |Geography Id|숨김|True|  
    |Sales Territory Id|숨김|True|  
  
     **제품**  
  
    |열|속성|값|  
    |------------|--------------|-----------|  
    |Product Id|숨김|True|  
    |Product Alternate Id|기본 레이블|True|  
    |Product Subcategory Id|숨김|True|  
    |Product Start Date|데이터 형식|간단한 날짜|  
    |Product End Date|데이터 형식|간단한 날짜|  
    |Large Photo|숨김|True|  
  
     **Internet Sales**  
  
    |열|속성|값|  
    |------------|--------------|-----------|  
    |Product Id|숨김|True|  
    |Customer Id|숨김|True|  
    |Promotion Id|숨김|True|  
    |Currency Id|숨김|True|  
    |Sales Territory Id|숨김|True|  
    |Order Quantity|데이터 형식<br /><br /> 데이터 형식<br /><br /> 소수 자릿수|10진수<br /><br /> 10진수<br /><br /> 0|  
    |Order Date|데이터 형식|간단한 날짜|  
    |Due Date|데이터 형식|간단한 날짜|  
    |Ship Date|데이터 형식|간단한 날짜|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>Adventure Works Internet Sales 테이블 형식 모델 다시 배포  
 모델을 변경했기 때문에 다시 배포해야 합니다. 기본적으로 [14단원: 배포](lesson-13-deploy.md)에서 수행한 동작을 반복합니다.  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>Adventure Works Internet Sales 테이블 형식 모델을 다시 배포하려면  
  
-   [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **빌드** 메뉴를 클릭한 다음 **Adventure Works Internet Sales Model 배포**를 클릭합니다.  
  
     **배포** 대화 상자가 나타나고 메타 데이터 및 모델에 포함 된 각 테이블의 배포 상태를 표시 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 이제 Power View를 사용하여 모델의 데이터를 시각화할 수 있습니다. SharePoint 사이트의 Analysis Services 및 Reporting Services 계정에 모델에 배포한 Analysis Services 인스턴스에 대한 읽기 권한이 있는지 확인하십시오.  
  
 모델을 가리키는 Reporting Services 보고서 데이터 원본을 만들려면 [테이블 모델 연결 형식(SSRS)](https://msdn.microsoft.com/library/hh270317%28v=SQL.110%29.aspx)을 참조하세요.  
  
  
