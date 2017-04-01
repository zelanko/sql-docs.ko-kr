---
title: "14단원: 배포 | Microsoft Docs"
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
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 14단원: 배포
이 단원에서는 테이블 형식 모드로 실행되는 Analysis Services의 배포 서버 인스턴스를 지정하고 배포할 모델의 이름을 지정하여 배포 속성을 구성합니다. 그 다음에는 모델을 해당 인스턴스에 배포합니다. 모델을 배포한 후 사용자는 보고 클라이언트 응용 프로그램을 사용하여 모델에 연결할 수 있습니다. 자세한 내용은 [테이블 형식 모델 솔루션 배포&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)를 참조하세요.  
  
이 단원에 소요되는 예상 시간: **5분**  
  
## 필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [13단원: Excel에서 분석](../analysis-services/lesson-13-analyze-in-excel.md)을 완료해야 합니다.  
  
## 모델 배포  
  
#### 배포 속성을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]의 **솔루션 탐색기**에서 **Adventure Works Internet Sales Tabular Model** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **속성**을 클릭합니다.  
  
2.  **AW Internet Sales Tabular Model 속성 페이지** 대화 상자에서 **배포 서버** 아래의 **서버** 속성에 테이블 형식 모드로 실행 중인 Analysis Services 인스턴스의 이름을 입력합니다. 나중에 이 인스턴스에 모델을 배포하게 됩니다.  
  
    > [!IMPORTANT]  
    > 원격 Analysis Services 인스턴스에 배포하려면 해당 인스턴스에 대한 관리자 권한이 있어야 합니다.  
  
3.  **데이터베이스** 속성에 **Adventure Works Internet Sales Model**을 입력합니다.  
  
4.  **큐브 이름** 속성에 **Adventure Works Internet Sales Model**을 입력합니다.  
  
5.  선택한 내용을 확인하고 **확인**을 클릭합니다.  
  
#### Adventure Works Internet Sales 테이블 형식 모델을 배포하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **빌드** 메뉴를 클릭한 다음 **AW Internet Sales Tabular Model 배포**를 클릭합니다.  
  
    배포 대화 상자가 나타나고 메타데이터 및 모델에 포함된 각 테이블의 배포 상태가 표시됩니다.  
  
2. 배포가 성공적으로 완료되면 **닫기**를 클릭합니다.  
  
## 결론  
축하합니다. 첫 번째 Analysis Services 테이블 형식 모델을 제작하고 배포했습니다. 이 자습서에서는 테이블 형식 모델을 만들기 위해 수행해야 하는 대부분의 일반적인 태스크를 완료하는 과정을 안내했습니다. 이제 Adventure Works Internet Sales Model이 배포되었으므로 SQL Server Management Studio를 사용하여 모델을 관리하고 처리 스크립트와 백업 계획을 만들 수 있습니다. 사용자는 Microsoft Excel이나 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 같은 보고 클라이언트 응용 프로그램을 사용하여 모델에 연결할 수 있습니다.  
  
## 추가 리소스  
[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 보고서를 지원하는 테이블 형식 모델 속성에 대한 자세한 내용은 [파워 뷰 보고 속성&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)을 참조하세요.  
  
## 참고 항목  
[DirectQuery 모드&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)  
[기본 데이터 모델링 및 배포 속성 구성&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[테이블 형식 model 데이터베이스&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  
