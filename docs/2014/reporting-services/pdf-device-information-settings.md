---
title: PDF 디바이스 정보 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 36def4705f6b2be9d5e1828f920ae41a51477272
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108092"
---
# <a name="pdf-device-information-settings"></a>PDF 디바이스 정보 설정
  다음 표는 PDF 형식으로 보고서를 렌더링하기 위한 디바이스 정보 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
|**열**|보고서에 대해 설정할 열 수입니다. 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**ColumnSpacing**|보고서에 대해 설정할 열 간격입니다. 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**DpiX**|X 방향의 출력 디바이스 해상도입니다.|  
|**DpiY**|Y 방향의 출력 디바이스 해상도입니다.|  
|**EndPage**|렌더링할 보고서의 마지막 페이지입니다. 기본값은 `StartPage`에 대한 값입니다.|  
|`HumanReadablePDF`|원본 가독성을 높이도록 PDF를 압축해야 하는지 여부를 나타냅니다. 기본값은 `false.`|  
|**MarginBottom**|보고서에 대해 설정할 아래쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 1in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**MarginLeft**|보고서에 대해 설정할 왼쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 1in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**MarginRight**|보고서에 대해 설정할 오른쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 1in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**MarginTop**|보고서에 대해 설정할 위쪽 여백 값(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 1in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**PageHeight**|보고서에 대해 설정할 페이지 높이(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 11in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|**PageWidth**|보고서에 대해 설정할 페이지 너비(인치)입니다. 정수 또는 10진수 값과 그 뒤의 "in"을 포함해야 합니다(예: 8.5in). 이 값은 보고서의 원래 설정을 재정의합니다.|  
|`StartPage`|렌더링할 보고서의 첫 페이지입니다. `0` 값은 모든 페이지가 렌더링됨을 나타냅니다. 기본값은 `1`입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [디바이스 정보 설정을 렌더링 확장 프로그램에 전달](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
