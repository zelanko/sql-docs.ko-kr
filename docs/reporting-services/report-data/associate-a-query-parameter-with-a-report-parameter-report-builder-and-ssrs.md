---
title: "보고서 매개 변수와 쿼리 매개 변수 연결(보고서 작성기 및 SSRS) | Microsoft Docs"
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
helpviewer_keywords: 
  - "쿼리 [Reporting Services], 매개 변수"
  - "매개 변수 [Reporting Services], 쿼리"
ms.assetid: 6d297e1a-ff71-472a-addc-349e863092b5
caps.latest.revision: 49
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 49
---
# 보고서 매개 변수와 쿼리 매개 변수 연결(보고서 작성기 및 SSRS)
  쿼리 변수가 포함된 데이터 집합 쿼리를 정의할 경우 쿼리 명령이 구문 분석됩니다. 각 쿼리 변수에 대해 해당 데이터 집합 매개 변수 및 보고서 매개 변수가 생성됩니다. 데이터 집합 매개 변수는 보고서 매개 변수를 가리킵니다. 이를 통해 사용자는 쿼리에 직접 전달되는 값을 입력할 수 있습니다. 쿼리 명령을 편집할 때마다 동일한 프로세스가 수행됩니다.  
  
 쿼리 매개 변수에 바인딩된 보고서 매개 변수의 이름을 바꾸는 경우 이 항목의 절차를 사용하여 쿼리 매개 변수를 이름이 바뀐 보고서 매개 변수에 직접 연결해야 합니다.  
  
> **참고:** [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### 쿼리 매개 변수를 보고서 매개 변수와 연결하려면  
  
1.  보고서 데이터 창에서 데이터 집합을 마우스 오른쪽 단추로 클릭하고 **데이터 집합 속성**을 클릭한 다음 **매개 변수**를 클릭합니다.  
  
    > **참고:** 보고서 데이터 창이 표시되지 않는 경우 **보기** 메뉴에서 **보고서 데이터**를 클릭합니다.  
  
2.  열 **매개 변수 이름**에서 쿼리 매개 변수의 이름을 찾습니다. 매개 변수 이름은 쿼리를 기반으로 자동 채워집니다. 쿼리를 변경할 때마다 새 쿼리 매개 변수가 있는지 확인됩니다. 직접 만드는 쿼리 매개 변수는 쿼리가 변경될 때 변경되지 않습니다.  
  
    -   **매개 변수 이름**에서 쿼리에 있는 것과 같은 쿼리 매개 변수 이름을 찾습니다. 직접 새 쿼리 매개 변수를 추가하고 이름을 입력할 수도 있습니다.  
  
    -   **매개 변수 값**에서 쿼리 매개 변수에 전달할 값을 반환하는 식을 선택하거나 입력합니다. 이는 일반적으로 보고서 매개 변수의 이름입니다.  
  
        > **참고:** 쿼리 매개 변수에 대한 값으로 보고서 매개 변수만 사용할 수 있는 것은 아닙니다. 값을 반환하는 식을 매개 변수 값으로 사용할 수 있습니다.  
  
3.  쿼리 매개 변수를 추가하려면 2단계를 반복합니다.  
  
## 관련 항목:  
 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   

  
  