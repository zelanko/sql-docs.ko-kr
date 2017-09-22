---
title: "SharePoint 사이트에서 보고서 뷰어 웹 파트 배포 | Microsoft Docs"
ms.custom: 
ms.date: 09/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: ed93b0fd5161686becb4cca05c005fd281f2c176
ms.contentlocale: ko-kr
ms.lasthandoff: 09/15/2017

---

# <a name="deploy-the-report-viewer-web-part-on-a-sharepoint-site"></a>SharePoint 사이트에서 보고서 뷰어 웹 파트를 배포 합니다.

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

보고서 뷰어 웹 파트는 SharePoint 사이트 내에서 SQL Server Reporting Services (기본 모드) 보고서를 보는 데 사용할 수 있는 사용자 지정 웹 파트입니다. 웹 파트를 사용 하 여 탐색 하며 인쇄를 보고서 서버에서 보고서를 내보낼 수 있습니다. 보고서 뷰어 웹 파트는 보고서 정의 파일 (.rdl)에서 SQL Server Reporting Services 보고서 서버 또는 Power BI 보고서 서버 처리와 관련이 있습니다. 이 보고서 뷰어 웹 파트는 Power BI 보고서 서버에서 호스트 되는 Power BI 보고서와 함께 사용할 수 없습니다.

SharePoint Server 2013 또는 SharePoint Server 2016 환경에는 보고서 뷰어 웹 파트를 추가 하는 솔루션 패키지를 수동으로 배포 하려면 다음 지침을 사용 합니다. 솔루션을 배포 하는 것은 웹 파트를 구성 하기 위한 필수 단계입니다.

**보고서 뷰어 웹 파트는 독립 실행형 솔루션 패키지 및 SQL Server Reporting Services에 대 한 SharePoint 통합된 모드로 연결 되어 있지 않습니다.**

## <a name="requirements"></a>요구 사항

**지원 되는 운영 체제:**  
* Windows Server 2008 R2 SP1 이상

**SharePoint Server 버전을 지원 합니다.**  
* SharePoint Server 2016
* SharePoint Server 2013

**Reporting Services 버전을 지원 합니다.**  
* SQL Server 2008 Reporting Services (기본 모드) 및 이후 버전입니다.
* Power BI 보고서 서버

## <a name="download-the-report-viewer-web-part-solution-package"></a>보고서 뷰어 웹 파트 솔루션 패키지를 다운로드 합니다.

보고서 뷰어 웹 파트를 Microsoft 다운로드 센터에서 사용할 수 있습니다.

[보고서 뷰어 웹 파트 솔루션 패키지를 다운로드 합니다.](https://www.microsoft.com/en-us/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>팜 솔루션 배포

이 섹션을 SharePoint 팜에 솔루션 패키지를 배포 하는 방법을 보여 줍니다. 이 태스크는 한 번만 수행해야 합니다.

1. SharePoint 서버에서 사용 하 여 SharePoint 관리 셸을 열고는 **관리자 권한으로 실행** 옵션입니다.

2. 실행 [Add-spsolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx) 팜 솔루션을 추가 합니다.

    ```
    Add-SPSolution –LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    이 cmdlet을 실행하면 솔루션의 이름,  솔루션 ID  및 Deployed=False가 반환됩니다. 다음 단계에서는 솔루션을 배포합니다.

3. 실행 된 [설치 SPSolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx) cmdlet 팜 솔루션을 배포 합니다.

    **SharePoint 2013**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint 2016**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>기능 활성화

1. SharePoint 사이트에서 선택 된 **기어** 왼쪽 위에 하 고 선택 아이콘 **사이트 설정*합니다.

    ![사이트 설정 기어 아이콘에서입니다.](media/sharepoint-site-settings.png)

    기본적으로 SharePoint 웹 응용 프로그램은 포트 80을 통해 액세스됩니다. 즉, 입력 하 여 SharePoint 사이트 자주 액세스할 수 *http://<computer name> * 를 루트 사이트 모음을 엽니다.

3. **사이트 모음 관리**선택, **사이트 모음 기능**합니다.

4. 페이지를 찾을 때까지 아래로 스크롤하여는 **보고서 뷰어 웹 파트** 기능입니다.

5. **활성화**를 선택합니다.

    ![보고서 뷰어 웹 파트 기능 활성화](media/web-part-activiate-feature.png)

6. 각 사이트를 열고 사이트 작업을 클릭 하 여 추가 사이트 모음에 대해 반복 합니다.

필요에 따라 수 또한 PowerShell을 사용 하면 사용 하 여 모든 사이트에서이 기능을 사용 하도록 설정 된 [Enable SPFeature](https://technet.microsoft.com/library/ff607803.aspx) cmdlet.

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>솔루션 제거

SharePoint 중앙 관리에서 솔루션 취소를 제공 하지만 불필요를 취소 하려면는 **ReportViewerWebPart.wsp** 는 설치 또는 패치 배포 문제를 체계적으로 해결 하는 경우가 아니면 파일입니다.

1. SharePoint 중앙 관리에서에서 **시스템 설정**선택, **팜 솔루션 관리**합니다.

2. 선택 **ReportViewerWebPart.wsp**합니다.

3. 선택 솔루션을 취소 합니다.

### <a name="remove-the-web-part-from-site-settings"></a>사이트 설정에서 웹 파트를 제거 합니다.

솔루션을 제거 하면 SharePoint 사이트 내에서 웹 파트 목록에서 보고서 뷰어 웹 파트는 제거 되지 않습니다. 보고서 뷰어 웹 파트를 제거 하려면 다음을 수행 합니다.

1. SharePoint 사이트에서 선택 된 **기어** 왼쪽 위에 하 고 선택 아이콘 **사이트 설정*합니다.

    ![사이트 설정 기어 아이콘에서입니다.](media/sharepoint-site-settings.png)

    기본적으로 SharePoint 웹 응용 프로그램은 포트 80을 통해 액세스됩니다. 즉, 입력 하 여 SharePoint 사이트 자주 액세스할 수 *http://<computer name> * 를 루트 사이트 모음을 엽니다.

2. 아래 **웹 디자이너 갤러리**선택, **웹 파트**합니다.

3. 선택 된 **편집 아이콘** 옆에 **ReportViewerNativeMode.dwp**합니다. 결과의 첫 페이지에 표시 되지 않을 수 있습니다.

4. 선택 **항목 삭제**합니다.

    ![편집 하 고 보고서 뷰어 기본 모드 웹 파트를 삭제 합니다.](media/report-viewer-native-mode-edit-delete.png)

PowerShell을 사용 하 여 웹 파트의 삭제를 시도해 볼 수 있지만 그에 대 한 직접 명령이 아닙니다. 스크립트 예제를 보려면 [웹 파트 갤러리에서 웹 파트를 삭제 하는 방법](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f)합니다.

## <a name="next-steps"></a>다음 단계

보고서 뷰어 웹 파트를 배포한 후 activiated SharePoint 페이지에 웹 파트를 추가할 수 있습니다. 자세한 내용은 참조 [SharePoint 페이지에 추가 하는 보고서 뷰어 웹 파트](add-report-viewer-web-part-to-page.md)합니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
