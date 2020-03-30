---
title: 보고서 뷰어 컨트롤에 대한 릴리스 정보
description: Reporting Services와 관련된 WebForms 및 WinForms 보고서 뷰어 컨트롤에 대한 릴리스 정보입니다.
ms.date: 01/16/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: 5ee9bd80519e9dc9d75bb78a98b548b2a60ef247
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76259381"
---
# <a name="release-notes-for-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>SSRS의 WebForms 및 WinForms 보고서 뷰어 컨트롤의 릴리스 정보

다음은 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)](SSRS)와 관련된 WebForms 및 WinForms용 보고서 뷰어 컨트롤에 대한 릴리스 정보입니다.

SSRS에 대한 릴리스 정보는 [SQL Server Reporting Services(SSRS) 2017 이상 릴리스 정보](../release-notes-reporting-services.md)를 참조하세요.

## <a name="15014000"></a>150.1400.0
| 변경 설명 | 세부 정보 |
| :----------------- | :------ |
| 버그 수정 | 뷰어 컨트롤이 디자인 모드에서 로드되지 않는 문제를 해결했습니다. |
| &nbsp; | &nbsp; |

## <a name="15013580"></a>150.1358.0
| 변경 설명 | 세부 정보 |
| :----------------- | :------ |
| 버그 수정 | 프로젝트 참조에서 Microsoft ReportViewer.Design 어셈블리를 제거한 변경 내용을 되돌렸습니다. |
|           | 다른 변경의 일부로 두 개의 어셈블리가 15.0 버전에서 15.3으로 변경되었습니다. 이제 다시 되돌렸습니다. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| 변경 설명 | 세부 정보 |
| :----------------- | :------ |
| 버그 수정  | 고 DPI 모니터용 적절한 인쇄 미리 보기 |
|            | 인쇄 대화 상자가 표시 공간 밖에 표시됨 |
|            | 매개 변수 수가 너무 많아 매개 변수 스크롤 막대와 드롭다운 목록이 제대로 작동하지 않음 |
|            | Null 및 날짜 시간 매개 변수와 관련된 문제 해결됨 |
|            | JQuery를 버전 3.3.1로 업데이트함 |
|            | HTML 렌더링에서 테이블릭스 셀과 겹치는 문제가 해결됨 |
|            | 프로젝트에 추가되는 잘못된 VS 어셈블리를 제거하기 위해 디자인 타임 프로젝트 참조를 제거함 |
|            | 활성 항목에 대해서만 내레이션을 제공하도록 도구 모음에 대한 접근성 수정 |
| &nbsp; | &nbsp; |

## <a name="150900148"></a>150.900.148

| 변경 설명 | 세부 정보 |
| :----------------- | :------ |
| 매개 변수 없는 보고서가 **Server.LoadReportDefinition**을 통해 로드되지 않도록 하는 버그 수정 | &nbsp; |
| WebForms 보고서 뷰어 컨트롤 | RTL 페이지(*direction: rtl;* css 속성을 사용하여 텍스트 흐름을 변경하는 페이지)에 포함하도록 지원합니다.<br/><br/>*IReportViewerMessages5* 지역화 인터페이스를 통해 인쇄 대화 상자 텍스트를 사용자 지정하도록 지원합니다.<br/><br/>접근성 지원 개선<br/><br/>&bull; &nbsp; &nbsp; [WebForms 보고서 뷰어 컨트롤에 대한 NuGet 패키지](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| WinForms 보고서 뷰어 컨트롤 | 높은 DPI 모드에서 앱을 실행 중인 경우 인쇄 문제 수정<br/><br/>&bull; &nbsp; &nbsp; [WinForms 보고서 뷰어 컨트롤에 대한 NuGet 패키지](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>다음 단계

보고서 뷰어 컨트롤 [시작](integrating-reporting-services-using-reportviewer-controls-get-started.md)

추가 질문이 있으신가요? [Reporting Services 포럼을 이용해 보세요.](https://go.microsoft.com/fwlink/?LinkId=620231)
