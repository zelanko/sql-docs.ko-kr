---
title: "보고서에 계기 추가(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 45da4fef-2b02-40e1-977c-f8f80d87155e
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# 보고서에 계기 추가(보고서 작성기 및 SSRS)
  페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]시각적 형식으로 데이터를 요약하려는 경우 계기 데이터 영역을 사용할 수 있습니다. 디자인 화면에 계기 데이터 영역을 추가한 후에는 보고서 데이터 집합 필드를 계기의 데이터 창으로 끌 수 있습니다.  
  
## 보고서에 계기를 추가하려면  
  
1.  보고서를 만들거나 기존 보고서를 엽니다.  
  
2.  삽입 탭에서 계기를 두 번 클릭합니다. **계기 유형 선택** 대화 상자가 열립니다.  
  
3.  추가할 계기 유형을 선택합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  차트와 달리 계기에는 선형과 방사형이라는 두 가지 유형만 있습니다. **계기 유형 선택** 대화 상자의 사용 가능한 계기는 이 두 유형의 계기에 대한 템플릿입니다. 따라서 보고서에 계기를 추가한 후에는 계기 유형을 변경할 수 없습니다. 계기 유형을 변경하려면 계기를 삭제한 다음 다시 추가해야 합니다.  
  
     보고서에 데이터 원본 및 데이터 집합이 없으면 **데이터 원본 속성** 대화 상자가 열려 데이터 원본과 데이터 집합을 만드는 단계를 안내합니다. 자세한 내용은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)을 참조하세요.  
  
     보고서에 데이터 원본은 있지만 데이터 집합이 없는 경우에는 **데이터 집합 속성** 대화 상자가 열려 데이터 집합을 만드는 단계를 안내합니다. 자세한 내용은 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)를 참조하세요.  
  
4.  계기를 클릭하여 데이터 창을 표시합니다. 기본적으로 계기에는 하나의 값에 해당하는 하나의 포인터가 있습니다. 하지만 포인터를 추가할 수도 있습니다.  
  
5.  데이터 집합의 필드 하나를 데이터 필드 끌어 놓기 영역에 추가합니다. 필드를 하나만 추가할 수 있습니다. 여러 필드를 표시하려면 각 필드에 하나씩 추가 포인터를 추가해야 합니다.  
  
     계기 눈금을 마우스 오른쪽 단추로 클릭하고 **눈금 속성**을 선택합니다. 눈금의 **최소값** 및 **최대값** 에 값을 입력합니다. 자세한 내용은 [계기의 최소값 또는 최대값 설정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)을 참조하세요.  
  
## 관련 항목:  
 [중첩된 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [계기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  