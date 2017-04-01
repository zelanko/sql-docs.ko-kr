---
title: "9단원: 큐브 뷰 만들기 | Microsoft Docs"
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
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 9단원: 큐브 뷰 만들기
이 단원에서는 Internet Sales 큐브 뷰를 만듭니다. 큐브 뷰는 비즈니스 또는 응용 프로그램 중심의 관점에서 파악할 수 있게 해 주는 보기 가능한 모델 하위 집합을 정의합니다. 사용자가 큐브 뷰를 사용하여 모델에 연결하는 경우 해당 모델 개체(테이블, 열, 측정값, 계층 및 KPI)만 해당 큐브 뷰에 정의되어 있는 필드로 볼 수 있습니다.  
  
이 단원에서 만드는 Internet Sales 큐브 뷰에는 Customer 테이블 개체가 제외됩니다. 뷰에서 특정 개체를 제외하는 큐브 뷰를 만들면 해당 개체가 모델에는 그대로 있지만 보고 클라이언트 필드 목록에서는 보이지 않습니다. 큐브 뷰에 포함되어 있거나 포함되어 있지 않은 계산 열 및 측정값을 계속해서 제외된 개체 데이터에서 계산할 수 있습니다.  
  
이 단원의 목표는 큐브 뷰를 만드는 방법을 설명하고 테이블 형식 모델 제작 도구를 파악하도록 돕는 데 있습니다. 나중에 추가 테이블을 포함하도록 이 모델을 확장할 경우 큐브 뷰를 추가로 만들어 모델에 대한 다양한 뷰포인트(예: Inventory 및 Sales Force)를 정의할 수 있습니다.  
  
자세한 내용은 [큐브 뷰&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/perspectives-ssas-tabular.md)를 참조하세요.  
  
이 단원에 소요되는 예상 시간: **5분**  
  
## 필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [8단원: 핵심 성과 지표 만들기](../analysis-services/lesson-8-create-key-performance-indicators.md)를 완료해야 합니다.  
  
## 큐브 뷰 만들기  
  
#### Internet Sales 큐브 뷰를 만들려면  
  
1.  모델 디자이너에서 **모델** 메뉴를 클릭한 다음 **큐브 뷰**, **만들기 및 관리**를 차례로 클릭합니다.  
  
2.  **큐브 뷰** 대화 상자에서 **새 큐브 뷰**를 클릭합니다.  
  
3.  큐브 뷰의 이름을 바꾸려면 **새 큐브 뷰 1** 열 제목을 두 번 클릭한 다음 **Internet Sales**를 입력합니다.  
  
4.  **필드**에서 **Date**, **Geography**, **Product**, **Product Category**, **Product Subcategory** 및 **Internet Sales** 테이블을 선택합니다.  
  
    이 큐브 뷰에서 Customer 테이블과 이 테이블의 모든 열을 제외했습니다. 나중에 12단원에서 Excel에서 분석 기능을 사용하여 이 큐브 뷰를 테스트합니다. Excel 피벗 테이블 필드 목록에는 Customer 테이블을 제외한 각 테이블이 포함됩니다.  
  
5.  선택 항목을 확인하여 **Customer** 테이블이 선택되어 있지 않은지 확인한 다음 **확인**을 클릭합니다.  
  
## 다음 단계  
이 자습서를 계속하려면 다음 단원인 [10단원: 계층 만들기](../analysis-services/lesson-10-create-hierarchies.md)로 이동하세요.  
  
  
  
