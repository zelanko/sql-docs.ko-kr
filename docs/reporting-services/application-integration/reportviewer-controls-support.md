---
title: 보고서 뷰어 컨트롤 버전 지원
description: Microsoft Report Viewer 컨트롤은 최신 지원 수명 주기 정책을 따르는 SQL Server Reporting Services 및 Power BI Report Server와 호환됩니다.
author: maggiesMSFT
ms.custom: seo-lt-2019
ms.author: maggies
ms.reviewer: jonhp
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.date: 12/01/2020
ms.openlocfilehash: f6c713d579042425dc863b7d4f942229a091d0c4
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96502697"
---
# <a name="support-for-report-viewer-current-branch-versions"></a>보고서 뷰어 현재 분기 버전 지원

**_적용 대상: Microsoft Report Viewer 버전 150.900.148 이상_**

**Microsoft Report Viewer 컨트롤** 은 Microsoft 최신 [수명 주기 정책 지원](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy)을 따르는 SQL Server Reporting Services 및 BI Report Server와 호환됩니다. 이 정보는 [NuGet](https://www.nuget.org/)을 통해 배포된 **ASP.NET** 버전과 **WinForms** 버전에 모두 적용됩니다. 릴리스된 모든 버전은 [NuGet](https://www.nuget.org/)을 통해 제공됩니다. 패치, 기능 또는 기타 업데이트는 최신 버전으로 롤포워드됩니다. 변경 내용을 받으려면 최신 버전을 적용해야 합니다. 보고서 뷰어는 지원 정책 변경에 대한 최소 1년 사전 공지와 함께 **보안 및 중요 업데이트** 를 계속 받습니다.

보고서 뷰어 컨트롤의 버전 기록은 다음 링크를 참조하세요.

- [Windows Forms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/)
- [ASP.NET Web Forms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WebForms/)

## <a name="application-server-and-report-server-combinations"></a>애플리케이션 서버와 보고서 서버의 조합

보고서 뷰어 컨트롤의 일부 기능은 운영 체제의 기본 동작을 사용합니다. 따라서 클라이언트(보고서 뷰어 컨트롤을 실행 하는 애플리케이션 서버)와 서버(Reporting Services를 실행)에 동일한 버전을 실행해야 할 수 있습니다. 다음과 같은 애플리케이션 서버와 보고서 서버의 조합이 지원됩니다.

| 애플리케이션 서버 | 보고서 서버 |
| :----------------- | :------ |
| Windows Server 2012 | Windows Server 2012 |
| Windows Server 2012 | Windows Server 2012 R2 |
| Windows Server 2012 R2 | Windows Server 2012 R2 |
| Windows Server 2012 R2 | Windows Server 2012 |
| Windows Server 2016 이상 | Windows Server 2016 이상 |

## <a name="next-steps"></a>다음 단계

보고서 뷰어 컨트롤에 대한 자세한 내용은 [보고서 뷰어 컨트롤을 사용하여 Reporting Services 통합 시작](integrating-reporting-services-using-reportviewer-controls-get-started.md)을 참조하세요.
