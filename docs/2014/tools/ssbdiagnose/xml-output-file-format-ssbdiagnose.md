---
title: XML 출력 파일 형식 (ssbdiagnose) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6644b8da77f8ebb6e4e8d6b6fc23ce5d9e356dd6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070833"
---
# <a name="xml-output-file-format-ssbdiagnose"></a>XML 출력 파일 형식(ssbdiagnose)
  **ssbdiagnose** 유틸리티는 **-XML** 스위치를 사용하여 실행하면 해당 출력을 XML 파일로 생성합니다. XML 출력 파일에는 헤더 정보와 분석된 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 구성 또는 대화에서 발견된 오류가 나열됩니다. 애플리케이션을 작성하여 이 파일에 나열된 오류를 분석하고 보고하거나 XML 메모장과 같은 일반적인 XML 편집기를 사용하여 이 XML 파일을 볼 수 있습니다.  
  
 **ssbdiangose** 출력 파일에는 다음과 같은 두 개의 자식 유형이 있는 DiagnosticInformation 루트 요소가 포함됩니다.  
  
-   헤더 정보가 있는 Banner 요소  
  
-   **ssbdiagnose**가 보고하는 각 문제에 대한 Issue 요소  
  
## <a name="diagnosticinformation-root-element"></a>DiagnosticInformation 루트 요소  
  
-   [DiagnosticInformation 요소 &#40;ssbdiagnose&#41;](diagnosticinformation-element-ssbdiagnose.md)  
  
## <a name="banner-element"></a>Banner 요소  
  
-   [Banner 요소 &#40;ssbdiagnose&#41;](banner-element-ssbdiagnose.md)  
  
## <a name="issue-element"></a>Issue 요소  
  
-   [Issue 요소 &#40;ssbdiagnose&#41;](issue-element-ssbdiagnose.md)  
  
## <a name="see-also"></a>관련 항목  
 [ssbdiagnose 유틸리티&#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  
