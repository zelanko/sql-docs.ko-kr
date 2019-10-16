---
title: SSRS의 보고서 뷰어 컨트롤에 대한 릴리스 정보
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: d6c7130e45e535ad1849bed5713313bf6f89020f
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923808"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>SSRS의 WebForms 및 WinForms에 대 한 보고서 뷰어 컨트롤의 릴리스 정보

@No__t-0 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS)와 관련 된 WebForms 및 WinForms의 보고서 뷰어 컨트롤에 대 한 릴리스 정보입니다.

SSRS에 대 한 릴리스 정보는 [SQL Server Reporting Services (ssrs) 2017 이상에 대 한 릴리스 정보](../release-notes-reporting-services.md)를 참조 하세요.

## <a name="15013580"></a>150.1358.0
| 설명 변경 | 세부 정보 |
| :----------------- | :------ |
| 버그 수정 | 프로젝트 참조에서 Microsoft ReportViewer. Design 어셈블리를 제거한 변경 내용을 되돌렸습니다. |
|           | 다른 변경의 일부로 두 개의 어셈블리가 15.0 버전에서 15.3로 변경 되었습니다. 이는 되돌려집니다. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 설명 변경 | 세부 정보 |
| :----------------- | :------ |
| 버그 수정  | 높은 DPI 모니터에 대 한 적절 한 인쇄 미리 보기 |
|            | 인쇄 대화 상자는 표시 되는 공간 밖에 표시 됩니다. |
|            | 매개 변수 수가 너무 많아 매개 변수 스크롤 막대와 드롭다운 목록이 제대로 작동 하지 않습니다. |
|            | Null 및 날짜 시간 매개 변수와 관련 된 문제 해결 |
|            | JQuery를 버전 3.3.1로 업데이트 함 |
|            | HTML 렌더링에서 테이블 릭 스 셀과 겹치는 문제 해결 |
|            | 프로젝트에 추가 되는 잘못 된 VS 어셈블리를 제거 하기 위해 디자인 타임 프로젝트 참조를 제거 했습니다. |
|            | 활성 항목에 대해서만 내레이션을 표시 하는 도구 모음에 대 한 내게 필요한 옵션 픽스 |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| 설명 변경 | 세부 정보 |
| :----------------- | :------ |
| 매개 변수 없는 보고서가 **Server.LoadReportDefinition**을 통해 로드되지 않도록 하는 버그 수정 | &nbsp; |
| WebForms 보고서 뷰어 컨트롤 | RTL 페이지(*direction: rtl;* css 속성을 사용하여 텍스트 흐름을 변경하는 페이지)에 포함하도록 지원합니다.<br/><br/>*IReportViewerMessages5* 지역화 인터페이스를 통해 인쇄 대화 상자 텍스트를 사용자 지정하도록 지원합니다.<br/><br/>접근성 지원 개선<br/><br/>&bull; @no__t [WebForms의 보고서 뷰어 컨트롤에 대 한 @no__t 2 NuGet 패키지](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms 보고서 뷰어 컨트롤 | 높은 DPI 모드에서 앱을 실행 중인 경우 인쇄 문제 수정<br/><br/>&bull; @no__t [WinForms의 보고서 뷰어 컨트롤에 대 한 @no__t 2 NuGet 패키지](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>다음 단계

보고서 뷰어 컨트롤 [시작](integrating-reporting-services-using-reportviewer-controls-get-started.md)

추가 질문이 있으신가요? [Reporting Services 포럼을 이용해 보세요.](https://go.microsoft.com/fwlink/?LinkId=620231)
