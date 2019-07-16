---
title: SSRS의 보고서 뷰어 컨트롤에 대한 릴리스 정보
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maghan
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: 1528358c8aff5d6e99869f0f4f8c1676ee2d5e75
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730911"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>WebForms 및 WinForms의 SSRS에 보고서 뷰어 컨트롤에 대 한 릴리스 정보

WebForms 및 WinForms, 관련 된 보고서 뷰어 컨트롤에 대 한 릴리스 이들은 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS).

SSRS에 대 한 릴리스 정보를 참조 하세요 [릴리스 정보에 대 한 SQL Server Reporting Services (SSRS) 2017 이상](../release-notes-reporting-services.md)합니다.

## <a name="15013580"></a>150.1358.0
| 설명 변경 | 세부 정보 |
| :----------------- | :------ |
| 버그 수정 | 프로젝트 참조에서 Microsoft.ReportViewer.Design 어셈블리를 제거 하는 변경이 되돌려집니다. |
|           | 다른 변경의 일환으로, 15.3 하도록 두 어셈블리는 15.0 버전에서 변경 되었습니다. 이 되돌려 졌습니다. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 설명 변경 | 세부 정보 |
| :----------------- | :------ |
| 버그 수정  | 높은 DPI 모니터에 대 한 적절 한 인쇄 미리 보기 |
|            | 인쇄 대화 상자 표시 공간 밖에 표시 됩니다. |
|            | 매개 변수 스크롤 막대와 제대로 작동 하지 않을 드롭 다운 목록에서 발생 한 많은 수의 매개 변수 |
|            | Null 및 날짜 시간 매개 변수를 사용 하 여 문제 해결된 |
|            | 업데이트 된 JQuery 버전 3.3.1 |
|            | HTML 렌더링에서 테이블 릭 스 셀을 사용 하 여 겹치는 고정 |
|            | 디자인 타임 프로젝트를 프로젝트에 추가 되는 잘못 된 VS 어셈블리가 제거에 대 한 참조를 제거 합니다. |
|            | 현재 항목에 대해서만 설명 도구 모음에 대 한 내게 필요한 옵션 수정 |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| 설명 변경 | 세부 정보 |
| :----------------- | :------ |
| 매개 변수 없는 보고서가 **Server.LoadReportDefinition**을 통해 로드되지 않도록 하는 버그 수정 | &nbsp; |
| WebForms 보고서 뷰어 컨트롤 | RTL 페이지(*direction: rtl;* css 속성을 사용하여 텍스트 흐름을 변경하는 페이지)에 포함하도록 지원합니다.<br/><br/>*IReportViewerMessages5* 지역화 인터페이스를 통해 인쇄 대화 상자 텍스트를 사용자 지정하도록 지원합니다.<br/><br/>접근성 지원 개선<br/><br/>&bull; &nbsp; &nbsp; [WebForms의 보고서 뷰어 컨트롤에 대 한 NuGet 패키지](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms 보고서 뷰어 컨트롤 | 높은 DPI 모드에서 앱을 실행 중인 경우 인쇄 문제 수정<br/><br/>&bull; &nbsp; &nbsp; [WinForms의 보고서 뷰어 컨트롤에 대 한 NuGet 패키지](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>다음 단계

보고서 뷰어 컨트롤 [시작](integrating-reporting-services-using-reportviewer-controls-get-started.md)

추가 질문이 있으신가요? [Reporting Services 포럼을 이용해 보세요.](https://go.microsoft.com/fwlink/?LinkId=620231)
