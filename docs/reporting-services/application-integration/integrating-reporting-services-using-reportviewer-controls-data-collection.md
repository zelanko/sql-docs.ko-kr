---
title: "ReportViewer 컨트롤 2016에서 데이터 수집 | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
caps.latest.revision: 2
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4e8b0226c27380bd2089acf8d2d6c8d7b27c7c5b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>ReportViewer 컨트롤-데이터 수집을 사용 하 여 Reporting Services 통합
ReportViewer 컨트롤을 기본적으로 고객 하는 방법을 더 잘 이해 하려면 microsoft에서 익명 사용 정보 수집 사용 하는 제어 합니다. 고객 배포 하 고 뷰어 컨트롤을 사용 하는 방법을 더 잘 이해 만들어서 이후 개발 고객에 게 가장 많은 가치를 제공 하는 향상 된 기능 집중 될 수 있습니다.

Microsoft SQL Server 2016 릴리스, 기타 제품 및 서비스에 대한 사용자 데이터 수집 및 사용 방법에 대한 설명은 이 [Microsoft 개인 정보 취급 방침](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx)을 참조하세요.

## <a name="opting-out-of-telemetry"></a>원격 분석을 옵트아웃

원격 분석 "EnableTelemetry"를 통해 프로그래밍 방식으로 해제할 수 있습니다. 컨트롤을 호스팅하는.aspx 페이지를 편집 하 여이 작업을 수행할 수 있습니다.

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

또는 실용적인 렌더링 하기 전에 컨트롤 등 호스팅 페이지 Page_Load 호출 처럼 합니다.
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>참고 항목

[WebForms ReportViewer 컨트롤 사용](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[ReportViewer 컨트롤을 사용 하 여 Reporting Services 통합](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 




