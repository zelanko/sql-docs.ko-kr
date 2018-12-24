---
title: 보고서 뷰어 웹 파트의 SharePoint 사이트 설정 - SSRS | Microsoft Docs
ms.date: 11/15/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: jt000
ms.author: jasontre
ms.openlocfilehash: 8add27eefcd46769bd8d06c980f10edb8d0739b8
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416170"
---
# <a name="sharepoint-site-settings-for-the-report-viewer-web-part---reporting-services"></a>보고서 뷰어 웹 파트의 SharePoint 사이트 설정 - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2016-2019](../../includes/ssrs-appliesto-sharepoint-2016-2019.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

보고서 뷰어 웹 파트에는 구성할 수 있는 몇 가지 설정이 있습니다. 이러한 설정은 사이트 관리자가 SharePoint 사이트 설정 페이지에서 활성화 및 비활성화할 수 있습니다. 각 사이트에 자체 설정이 있습니다. 또한 이렇나 설정은 보고서 뷰어 웹 파트를 다시 설치한 후에는 다시 설정할 수 없습니다.

## <a name="accessing-the-site-settings-page"></a>사이트 설정 페이지에 액세스

사이트 설정은 다음과 같은 방법으로 액세스할 수 있습니다.

1. SharePoint 사이트의 왼쪽 위에서 **기어** 아이콘을 선택하고 **사이트 설정**을 선택합니다.

    ![기어 아이콘에서 사이트 설정.](media/sharepoint-site-settings.png)

2. **Reporting Services** 사이트 설정 그룹의 **보고서 뷰어 웹 파트 설정**을 클릭합니다.

    > [!NOTE]
    > 사이트 설정은 `<site>/_layouts/15/ReportViewerWebPart/ReportViewerWebPartSettings.aspx`로 직접 이동하여 액세스할 수도 있습니다.

## <a name="report-viewer-web-part-settings"></a>보고서 뷰어 웹 파트 설정

|설정|주석|  
|-------------|--------------|  
|사용 데이터 수집|제품 개선을 돕기 위해 오류 및 사용 정보를 Microsoft로 전송할 수 있습니다. Microsoft 오류 보고 데이터 수집 정책의 경우 [Microsoft SQL Server 개인정보처리방침](https://go.microsoft.com/fwlink/?LinkID=868444)을 참조하세요.|  
|보고서에 내게 필요한 옵션 메타데이터 사용|렌더링된 보고서에 대한 [`AccessibleTablix` 디바이스 정보](../html-device-information-settings.md)를 설정합니다.| 
