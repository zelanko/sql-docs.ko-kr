---
title: "XML 출력 파일 형식(ssbdiagnose) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XML 출력 파일 형식 [ssbdiagnose]"
  - "ssbdiagnose"
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# XML 출력 파일 형식(ssbdiagnose)
  **ssbdiagnose** 유틸리티는 **-XML** 스위치를 사용하여 실행하면 해당 출력을 XML 파일로 생성합니다. XML 출력 파일에는 헤더 정보와 분석된 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 구성 또는 대화에서 발견된 오류가 나열됩니다. 응용 프로그램을 작성하여 이 파일에 나열된 오류를 분석하고 보고하거나 XML 메모장과 같은 일반적인 XML 편집기를 사용하여 이 XML 파일을 볼 수 있습니다.  
  
 **ssbdiangose** 출력 파일에는 다음과 같은 두 개의 자식 유형이 있는 DiagnosticInformation 루트 요소가 포함됩니다.  
  
-   헤더 정보가 있는 Banner 요소  
  
-   **ssbdiagnose**가 보고하는 각 문제에 대한 Issue 요소  
  
## DiagnosticInformation 루트 요소  
  
-   [DiagnosticInformation 요소&#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)  
  
## Banner 요소  
  
-   [Banner 요소&#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)  
  
## Issue 요소  
  
-   [Issue 요소&#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)  
  
## 참고 항목  
 [ssbdiagnose 유틸리티&#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  