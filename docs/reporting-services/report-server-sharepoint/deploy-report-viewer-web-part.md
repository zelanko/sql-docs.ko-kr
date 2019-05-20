---
title: SharePoint 사이트에 SQL Server Reporting Services 보고서 뷰어 웹 파트 배포 | Microsoft Docs
ms.date: 11/15/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3dc42904701ce69e762a203e09cb320cc797c15c
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65579985"
---
# <a name="deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-site"></a>SharePoint 사이트에 SQL Server Reporting Services 보고서 뷰어 웹 파트 배포

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2016-2019](../../includes/ssrs-appliesto-sharepoint-2016-2019.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

보고서 뷰어 웹 파트는 SharePoint 사이트 내에서 SQL Server Reporting Services(기본 모드) 보고서를 보는 데 사용할 수 있는 사용자 지정 웹 파트입니다. 웹 파트를 사용하여 보고서 서버에서 보고서를 보고, 탐색하고, 인쇄하고, 내보낼 수 있습니다. 보고서 뷰어 웹 파트는 SQL Server Reporting Services 보고서 서버 또는 Power BI Report Server에서 처리하는 보고서 정의 파일(.rdl)과 연결됩니다. 이 보고서 뷰어 웹 파트는 Power BI Report Server에서 호스트되는 Power BI 보고서와 함께 사용할 수 없습니다.

다음 지침을 사용하여 SharePoint Server 2013, SharePoint Server 2016 또는 SharePoint Server 2019 환경에 보고서 뷰어 웹 파트를 추가하는 솔루션 패키지를 수동으로 배포할 수 있습니다. 솔루션을 배포하는 것은 웹 파트를 구성하기 위한 필수 단계입니다.

**보고서 뷰어 웹 파트는 독립 실행형 솔루션 패키지이며 SQL Server Reporting Services에 대한 SharePoint 통합 모드로 연결되어 있지 않습니다.**

## <a name="requirements"></a>요구 사항

> [!IMPORTANT]
> 버전 “15.X.X.X”로 시작하면 ReportViewerWebPart를 기존 Reporting Services SharePoint 통합 모드 공유 서비스 애플리케이션과 나란히 설치할 수 있습니다.
> 이 .wsp 솔루션 업데이트를 통해 새 파일과 이전 솔루션은 취소하고 Uninstall-SPSolution 및 Install-SPSolution cmdlet을 각각 사용하여 새 .wsp를 다시 배포해야 합니다.
>

**SharePoint Server 버전 지원:**
* SharePoint Server 2019
* SharePoint Server 2016
* SharePoint Server 2013

**Reporting Services 버전 지원:**  
* SQL Server 2008 Reporting Services(기본 모드) 이상
* Power BI Report Server

## <a name="download-the-report-viewer-web-part-solution-package"></a>보고서 뷰어 웹 파트 솔루션 패키지 다운로드

보고서 뷰어 웹 파트는 Microsoft 다운로드 센터에서 제공됩니다.

[보고서 뷰어 웹 파트 솔루션 패키지 다운로드](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>팜 솔루션 배포

이 섹션은 SharePoint 팜에 솔루션 패키지를 배포하는 방법을 보여 줍니다. 이 태스크는 한 번만 수행해야 합니다.

1. SharePoint 서버에서 **관리자 권한으로 실행** 옵션을 사용하여 SharePoint 관리 셸을 엽니다.

2. [Add-SPSolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx)을 실행하여 팜 솔루션을 추가합니다.

    ```
    Add-SPSolution -LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    이 cmdlet을 실행하면 솔루션의 이름,  솔루션 ID  및 Deployed=False가 반환됩니다. 다음 단계에서는 솔루션을 배포합니다.

3. [Install-SPSolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx) cmdlet을 실행하여 팜 솔루션을 배포합니다.

    **SharePoint 2013**

    ```
    Install-SPSolution -Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint Server 2016 및 2019**

    ```
    Install-SPSolution -Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>기능 활성화

1. SharePoint 사이트의 왼쪽 위에서 **기어** 아이콘을 선택하고 **사이트 설정**을 선택합니다.

    ![기어 아이콘에서 사이트 설정.](media/sharepoint-site-settings.png)

    기본적으로 SharePoint 웹 애플리케이션은 포트 80을 통해 액세스됩니다. 즉, 루트 사이트 모음을 열기 위해 종종 *https://<computer name>* 를 입력하여 SharePoint 사이트에 액세스할 수 있습니다.

3. **사이트 컬렉션 관리**에서 **사이트 컬렉션 기능**을 선택합니다.

4. **보고서 뷰어 웹 파트** 기능을 찾을 때까지 페이지를 아래로 스크롤합니다.

5. **활성화**를 선택합니다.

    ![보고서 뷰어 웹 파트 기능 활성화](media/web-part-activiate-feature.png)

6. 각 사이트를 열고 사이트 작업을 클릭하여 추가 사이트 모음에 대해 위 단계를 반복합니다.

필요에 따라 [Enable-SPFeature](https://technet.microsoft.com/library/ff607803.aspx) cmdlet을 사용하여 모든 사이트에서 이 기능을 활성화하는 데 PowerShell을 사용할 수도 있습니다.

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>솔루션 제거

SharePoint 중앙 관리에서 솔루션 취소 기능을 제공하기는 하지만 설치 또는 패치 배포 문제를 체계적으로 해결하는 경우가 아니면 **ReportViewerWebPart.wsp** 파일을 취소할 필요가 없습니다.

1. SharePoint 중앙 관리의 **시스템 설정**에서 **팜 솔루션 관리**를 선택합니다.

2. **ReportViewerWebPart.wsp**를 선택합니다.

3. 솔루션 취소를 선택합니다.

### <a name="remove-the-web-part-from-site-settings"></a>사이트 설정에서 웹 파트 제거

솔루션을 제거해도 SharePoint 사이트 내의 웹 파트 목록에서 보고서 뷰어 웹 파트는 제거되지 않습니다. 보고서 뷰어 웹 파트를 제거하려면 다음을 수행합니다.

1. SharePoint 사이트의 왼쪽 위에서 **기어** 아이콘을 선택하고 **사이트 설정**을 선택합니다.

    ![기어 아이콘에서 사이트 설정.](media/sharepoint-site-settings.png)

    기본적으로 SharePoint 웹 애플리케이션은 포트 80을 통해 액세스됩니다. 즉, 루트 사이트 모음을 열기 위해 종종 *https://<computer name>* 를 입력하여 SharePoint 사이트에 액세스할 수 있습니다.

2. **웹 디자이너 갤러리** 아래에서 **웹 파트**를 선택합니다.

3. **ReportViewerNativeMode.dwp** 옆의 **편집 아이콘**을 선택합니다. 결과의 첫 페이지에 표시되지 않을 수 있습니다.

4. **항목 삭제**를 선택합니다.

    ![보고서 뷰어 기본 모드 웹 파트 편집 및 삭제](media/report-viewer-native-mode-edit-delete.png)

웹 파트 삭제는 PowerShell을 사용하여 시도될 수 있지만 직접 명령이 없습니다. 스크립트 예제는 [웹 파트 갤러리에서 웹 파트를 삭제하는 방법](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f)을 참조하세요.

## <a name="supported-languages"></a>지원되는 언어

웹 파트에 지원되는 언어는 다음과 같습니다.

* 영어(en)
* 독일어(de)
* 스페인어(sp)
* 프랑스어(fr)
* 이탈리아어(it)
* 일본어(ja)
* 한국어(ko)
* 포르투갈어(pt)
* 러시아어(ru)
* 중국어(간체 - zh-HANS 및 zh-CHS)
* 중국어(번체 - zh-HANT 및 zh-CHT)

## <a name="troubleshoot"></a>문제 해결

* SharePoint 통합 모드가 구성된 경우, SSRS를 제거할 때 오류가 발생합니다.

    Install-SPRSService : [A] Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService는 [B]Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService로 캐스팅할 수 없습니다. A 형식은 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll' 위치의 ‘기본값’ 컨텍스트에 있는 'Microsoft.ReportingServices.SharePoint.SharedService,Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91'에서 발생합니다. B 형식은 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll' 위치의 ‘기본값’ 컨텍스트에 있는 'Microsoft.ReportingServices.SharePoint.SharedService,Version=12.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91'에서 발생합니다.
    
    해결 방법:
    1. 보고서 뷰어 웹 파트 제거
    2. SSRS 제거
    3. 보고서 뷰어 웹 파트 다시 설치

* SharePoint 통합 모드가 구성된 경우, SharePoint를 업그레이드하려고 할 때 오류가 발생합니다.

    파일 또는 어셈블리 'Microsoft.ReportingServices.Alerting.ServiceContract, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' 또는 해당 종속성 중 하나를 로드할 수 없습니다. 시스템에서 지정한 파일을 찾을 수 없습니다. 00000000-0000-0000-0000-000000000000
    
    해결 방법:
    1. 보고서 뷰어 웹 파트 제거
    2. SSRS 제거
    3. 보고서 뷰어 웹 파트 다시 설치

## <a name="next-steps"></a>다음 단계

보고서 뷰어 웹 파트를 배포 및 활성화한 후 SharePoint 페이지에 웹 파트를 추가할 수 있습니다. 자세한 내용은 [SharePoint 페이지에 보고서 뷰어 웹 파트 추가](add-report-viewer-web-part-to-page.md)를 참조하세요.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
