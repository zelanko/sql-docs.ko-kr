---
title: "Word 장치 정보 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 491940329df26ba67f447aacb6a32f5d6578c4a5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="word-device-information-settings"></a>Word 장치 정보 설정
  다음 표는 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 형식으로 렌더링하기 위한 장치 정보 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
|**AutoFit**|**False** 자동 맞춤이 임의의 Word 테이블에서 **false** 로 설정됩니다.<br /><br /> **True**입니다. 자동 맞춤이 모든 Word 테이블에서 **true** 로 설정됩니다.<br /><br /> **Never**입니다. 자동 맞춤 값이 Word 테이블에서 설정되지 않으며 Word 기본값으로 되돌아갑니다.<br /><br /> **Default**입니다. 자동 맞춤이 논리 페이지당 실제 그리기 영역(여백을 제외한 실제 페이지 너비)보다 좁은 테이블에서 설정됩니다.|  
|**ExpandToggles**|표시하거나 숨길 수 있는 모든 항목이 전체 확장 상태로 렌더링되어야 하는지 여부를 나타냅니다. 기본값은 **false**입니다.|  
|**FixedPageWidth**|DOC 파일에 적용되는 페이지 너비가 보고서 본문의 가장 큰 페이지 너비에 맞게 늘어나는지 여부를 나타냅니다. 기본값은 **false**입니다.|  
|**OmitHyperlinks**|하이퍼링크 동작이 설정된 모든 항목에 대한 하이퍼링크 동작을 생략할지 여부를 나타냅니다. 기본값은 **false**입니다.|  
|**OmitDrillthroughs**|드릴스루 동작이 설정된 모든 항목에 대한 드릴스루 동작을 생략할지 여부를 나타냅니다. 기본값은 **false**입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [장치 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조 &#40; Ssrs&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  

