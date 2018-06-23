---
title: MHTML 장치 정보 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
caps.latest.revision: 39
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 7eb07733e9db0a1002658cd1e29de02d95d8ad08
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078384"
---
# <a name="mhtml-device-information-settings"></a>MHTML 장치 정보 설정
  다음 표는 웹 보관 파일(MHTML) 형식으로 보고서를 렌더링하기 위한 장치 정보 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
|**JavaScript**|렌더링된 보고서에서 JavaScript가 지원되는지 여부를 나타냅니다.|  
|**OutlookCompat**|Outlook에서 보고서를 보기 좋게 만들어 주는 메타데이터와 함께 렌더링할지 여부를 나타냅니다. 기본값은 `true`입니다.|  
|**MHTML 조각**|전체 MHTML 문서 대신 MHTML 조각이 만들어지는지 여부를 나타냅니다. MHTML 조각은 TABLE 요소에 보고서 내용을 포함하고 HTML 및 BODY 요소를 생략합니다. 기본값은 `false`입니다.|  
|**DataVisualizationFitSizing**|테이블릭스 안에 있을 경우 데이터 시각화 맞춤 동작을 나타냅니다. 여기에는 차트, 계기 및 지도가 포함됩니다.<br /><br /> 가능한 값은 **근사치** 및 **정확한 수치**입니다.<br /><br /> 기본값은 **근사치**입니다. **rsreportserver.config** 파일에서 설정이 제거될 경우 기본 동작은 **정확한 수치**입니다.<br /><br /> 정확한 크기를 결정하기 위한 처리는 더 오래 걸릴 수 있기 때문에 **정확한 수치** 를 설정하면 성능에 영향을 줄 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [장치 정보 설정을 렌더링 확장 프로그램에 전달](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  