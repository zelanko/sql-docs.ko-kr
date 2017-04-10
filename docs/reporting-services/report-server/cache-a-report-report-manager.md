---
title: "보고서 캐시(보고서 관리자) | Microsoft Docs"
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
  - "보고서 실행 속성 [Reporting Services]"
  - "캐시 [Reporting Services]"
  - "캐시된 보고서 [Reporting Services]"
  - "일정 [Reporting Services], 보고서 만료"
  - "만료 [Reporting Services]"
ms.assetid: 723d1cb0-c2e7-4763-8690-a6a7a8bbbb90
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# 보고서 캐시(보고서 관리자)
  성능을 향상시키는 한 가지 방법은 보고서의 캐싱 속성을 구성하는 것입니다. 보고서가 캐시되면 렌더링된 보고서의 복사본이 짧은 시간 동안 저장됩니다. 보고서를 요청하는 첫 번째 사용자는 모든 처리가 완료될 때까지 기다려야 보고서를 볼 수 있습니다. 캐싱 기간 내에 보고서를 요청하는 이후 사용자는 처리가 이미 발생했기 때문에 보고서를 바로 볼 수 있습니다.  
  
 캐시할 수 있는 보고서 유형은 제한되어 있습니다. 예를 들어 사용자 ID에 따라 보고서 출력이 달라지는 경우 또는 보고서를 요청하는 사용자의 보안 토큰을 사용하여 데이터가 검색되는 경우 보고서를 캐시할 수 없습니다. 자세한 내용은 [보고서 캐시&#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)를 참조하세요.  
  
### 캐시된 보고서의 만료를 예약하려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)를 시작합니다.  
  
2.  보고서 관리자에서 **내용** 페이지로 이동합니다. 캐싱 속성을 설정할 보고서로 이동하고 항목 위로 마우스를 이동한 다음 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다.  
  
4.  왼쪽 프레임에서 **처리 옵션**을 클릭합니다.  
  
5.  해당 페이지에서 **항상 최신 데이터로 이 보고서 실행**을 선택합니다.  
  
6.  다음 두 캐시 옵션 중에서 하나를 선택하고 만료 시간을 구성합니다.  
  
    -   캐시된 복사본이 특정 시간 후에 만료되도록 구성하려면 **보고서의 임시 복사본을 캐시합니다. 보고서 복사본은 다음 분 후에 만료됩니다.**를 클릭합니다. 보고서 만료 시간(분)을 입력합니다.  
  
    -   일정에 따라 캐시된 복사본이 만료되도록 구성하려면 **보고서의 임시 복사본을 캐시합니다. 보고서 복사본은 다음 일정으로 만료됩니다.**를 클릭합니다. **구성**을 클릭하거나 공유 일정을 선택하여 보고서 만료를 제어합니다.  
  
7.  **적용**을 클릭합니다.  
  
## 관련 항목:  
 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)   
 [보고서 캐시&#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
  
  