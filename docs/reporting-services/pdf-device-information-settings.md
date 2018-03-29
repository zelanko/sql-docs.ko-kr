---
title: PDF 장치 정보 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
caps.latest.revision: ''
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0bd2635a54003fd663dadcf6d3bc5991c1841988
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="pdf-device-information-settings"></a>PDF 장치 정보 설정
  다음 표는 PDF 형식으로 보고서를 렌더링하기 위한 장치 정보 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
| **AccessiblePDF** | 액세스할 수 있는/태그가 지정된 PDF를 렌더링할지 여부를 나타냅니다. 그러면 크기가 더 크지만 화면 판독기 및 기타 보조 기술에서 쉽게 읽고 탐색할 수 있습니다. 기본 값은 **false**입니다. [Power BI Report Server(2018년 3월) 이상에서 사용 가능] |
|**열**|보고서에 대해 설정할 열 수입니다. 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**ColumnSpacing**|보고서에 대해 설정할 열 간격입니다. 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**DpiX**|X 방향의 출력 장치 해상도입니다.|  
|**DpiY**|Y 방향의 출력 장치 해상도입니다.|  
|**EndPage**|렌더링할 보고서의 마지막 페이지입니다. 기본값은 **StartPage**에 대한 값입니다.|  
|**HumanReadablePDF**|압축되지 않은 PDF 파일을 렌더링할지 여부를 나타냅니다. 그러면 크기는 크지만 일반 텍스트 편집기에서 보다 읽기 쉬워집니다. 기본값은 **false.**입니다.|  
|**MarginBottom**|보고서에 대해 설정할 아래쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 1in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**MarginLeft**|보고서에 대해 설정할 왼쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 1in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**MarginRight**|보고서에 대해 설정할 오른쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 1in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**MarginTop**|보고서에 대해 설정할 위쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 1in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**PageHeight**|보고서에 대해 설정할 페이지 높이(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 11in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**PageWidth**|보고서에 대해 설정할 페이지 너비(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 8.5in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**StartPage**|렌더링할 보고서의 첫 페이지입니다. **0** 값은 모든 페이지가 렌더링됨을 나타냅니다. 기본값은 **1**입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [장치 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
