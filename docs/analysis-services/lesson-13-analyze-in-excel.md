---
title: "13단원: Excel에서 분석 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
caps.latest.revision: 22
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 13단원: Excel에서 분석
이 단원에서는 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 Excel에서 분석 기능을 사용하여 Microsoft Excel을 열고, 모델 작업 영역에 자동으로 데이터 원본을 연결하고, 워크시트에 피벗 테이블을 자동으로 추가합니다. Excel에서 분석 기능을 사용하면 모델을 배포하기 전에 모델 디자인의 효율성을 빠르고 손쉽게 테스트해 볼 수 있습니다. 이 단원에서는 데이터 분석을 수행하지 않습니다. 이 단원의 목표는 모델 작성자가 모델 디자인을 테스트하는 데 사용할 수 있는 도구를 익히도록 하는 것입니다. 모델 작성자를 위한 Excel에서 분석 기능을 사용하는 것과 달리 최종 사용자는 Excel 또는 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]와 같은 클라이언트 보고 응용 프로그램을 사용하여 배포된 모델 데이터에 연결하고 해당 데이터를 검색합니다.  
  
이 단원을 완료하려면 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]가 설치되어 있는 컴퓨터에 Excel이 설치되어 있어야 합니다. 자세한 내용은 [Excel에서 분석&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)을 참조하세요.  
  
이 단원에 소요되는 예상 시간: **20분**  
  
## 필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [11단원: 파티션 만들기](../analysis-services/lesson-11-create-partitions.md)를 완료해야 합니다.  
  
## 기본 큐브 뷰 및 Internet Sales 큐브 뷰를 사용하여 검색  
이 첫 번째 태스크에서는 모든 모델 개체가 포함되어 있는 기본 큐브 뷰와 8단원: 큐브 뷰 만들기에서 만든 Internet Sales 큐브 뷰를 사용하여 모델을 검색합니다. Internet Sales 큐브 뷰에는 Customer 테이블 개체가 제외되어 있습니다.  
  
#### 기본 큐브 뷰를 사용하여 찾아보려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **Excel에서 분석**을 클릭합니다.  
  
2.  **Excel에서 분석** 대화 상자에서 **확인**을 클릭합니다.  
  
    새 통합 문서와 함께 Excel이 열립니다. 현재 사용자 계정을 사용하여 데이터 원본이 연결되고 보기 가능한 필드를 정의하는 데 기본 큐브 뷰가 사용됩니다. 피벗 테이블이 자동으로 워크시트에 추가됩니다.  
  
3.  Excel의 **피벗 테이블 필드 목록**에 **Date** 및 **Internet Sales** 측정값 그룹이 나타나고 해당 큐브 뷰 열이 모두 포함된 **Customer**, **Date**, **Geography**, **Product**, **Product Category**, **Product Subcategory** 및 **Internet Sales** 테이블이 나타나는지 확인합니다.  
  
4.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
#### Internet Sales 큐브 뷰를 사용하여 찾아보려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **Excel에서 분석**을 클릭합니다.  
  
2.  **Excel에서 분석** 대화 상자에서 **현재 Windows 사용자**가 선택된 채로 두고 **큐브 뷰** 드롭다운 목록 상자에서 **Internet Sales**를 선택한 다음 **확인**을 클릭합니다. Excel이 열립니다.  
  
3.  Excel의 **피벗 테이블 필드 목록**에서 Customer 테이블이 필드 목록에서 제외되었는지 확인합니다.  
  
4.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
## 역할을 사용하여 찾아보기  
역할은 테이블 형식 모델의 필수적인 부분입니다. 사용자가 멤버로 추가된 하나 이상의 역할이 없는 경우 사용자는 모델을 사용하여 데이터에 액세스하고 분석할 수 없습니다. Excel에서 분석 기능은 정의한 역할을 테스트하는 방법을 제공합니다.  
  
#### Internet Sales Manager 사용자 역할을 사용하여 찾아보려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **Excel에서 분석**을 클릭합니다.  
  
2.  **Excel에서 분석** 대화 상자의 **모델에 연결하는 데 사용할 사용자 이름 또는 역할을 지정하십시오.**에서 **역할**을 선택한 다음 드롭다운 목록 상자에서 **Internet Sales Manager**를 선택하고 **확인**을 클릭합니다.  
  
    새 통합 문서와 함께 Excel이 열립니다. 피벗 테이블은 자동으로 만들어집니다. 피벗 테이블 필드 목록에는 새 모델에서 사용할 수 있는 모든 데이터 필드가 포함되어 있습니다.  
      
3.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
## 다음 단계  
이 자습서를 계속하려면 다음 단원인 [14단원: 배포](../analysis-services/lesson-14-deploy.md)로 이동하세요.  
  
  
  
