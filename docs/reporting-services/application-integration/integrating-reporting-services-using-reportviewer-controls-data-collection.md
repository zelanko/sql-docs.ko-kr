---
title: ReportViewer 컨트롤 2016에서 데이터 수집 | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: application-integration
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
caps.latest.revision: 2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: bc1edeb74cced8b18275b57deca6b078c13a56d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>ReportViewer 컨트롤을 사용하여 Reporting Services 통합 - 데이터 수집
기본적으로 ReportViewer 컨트롤은 Microsoft에서 고객이 컨트롤을 사용하는 방식을 더 잘 이해할 수 있도록 익명의 사용 정보를 수집합니다. 고객이 Viewer Control을 배포하고 사용하는 방법을 더 잘 이해하도록 함으로써 향후 개발 시 고객에게 최고의 가치를 제공하는 개선에 초점을 맞출 수 있습니다.

Microsoft SQL Server 2016 릴리스, 기타 제품 및 서비스에 대한 사용자 데이터 수집 및 사용 방법에 대한 설명은 이 [Microsoft 개인 정보 취급 방침](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx)을 참조하세요.

## <a name="opting-out-of-telemetry"></a>원격 분석 옵트아웃

"EnableTelemetry"를 통해 원격 분석을 프로그래밍 방식으로 해제할 수 있습니다. 컨트롤을 호스팅하는 .aspx 페이지를 편집하여 이 작업을 수행할 수 있습니다.

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

또는 호스팅 페이지의 Page_Load 호출과 같이 컨트롤이 렌더링되기 전에 실제로 수행할 수 있습니다.
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>관련 항목:

[WebForms ReportViewer 컨트롤 사용](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[ReportViewer 컨트롤을 사용하여 Reporting Services 통합](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



