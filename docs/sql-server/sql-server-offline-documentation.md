---
title: 이전 버전의 SQL Server 설명서를 오프라인으로 설치
description: SQL Server 2019, 2017, 2016, 2014 및 2012용 오프라인 설명서를 설치하는 방법을 알아봅니다. SSMS(SQL Server Management Studio)를 사용하여 오프라인 콘텐츠를 볼 수 있습니다.
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: markingmyname
ms.author: maghan
ms.date: 04/20/2020
ms.openlocfilehash: 1420e18fbf335e22d44bf78d526ab35c8b1434e5
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087873"
---
# <a name="install-previous-versions-of-sql-server-documentation-to-view-offline-in-ssms"></a>이전 버전의 SQL Server 설명서를 설치하여 오프라인으로 SSMS에서 보기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 오프라인 SQL Server 콘텐츠를 다운로드하고 [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)에서 보는 방법을 설명합니다. 오프라인 콘텐츠를 사용하면 인터넷에 연결되어 있지 않아도 설명서에 액세스할 수 있습니다(처음에 다운로드할 때는 인터넷 연결이 필요함).

오프라인 설명서는 SQL Server의 여러 이전 버전에서 사용할 수 있습니다. [온라인으로 이전 버전의 콘텐츠를 볼](https://docs.microsoft.com/previous-versions/sql/) 수도 있지만 오프라인 옵션을 사용하면 이전 콘텐츠에 편리하게 액세스할 수 있습니다.

## <a name="how-to-download-and-configure-offline-content"></a>오프라인 콘텐츠를 다운로드하고 구성하는 방법

온라인 원본 또는 로컬 디스크에서 SQL Server 도움말 다운로드 및 설치 패키지를 사용할 수 있습니다. 다음 섹션에서는 다양한 SQL Server 버전에 대한 오프라인 콘텐츠를 로드하는 방법을 설명합니다.

- [SQL Server 2019](#sql2019)
- [SQL Server 2017](#sql2017)
- [SQL Server 2016](#sql2016)
- [SQL Server 2014](#sql2014)
- [SQL Server 2012](#sql2012)

## <a name="sql-server-2019"></a><a id="sql2019"></a> SQL Server 2019

SQL Server 2019용 오프라인 설명서를 로드하려면 다음 단계를 따르세요.

1. SSMS의 도움말 메뉴에서 **도움말 콘텐츠 추가 및 제거**를 선택합니다.

   ![도움말 뷰어 콘텐츠 추가 제거](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   도움말 뷰어에서 콘텐츠 관리 탭이 열립니다.

2. SQL Server 2019용 최신 도움말 콘텐츠를 찾으려면 **콘텐츠 관리** 탭에서 설치 원본 아래에 있는 **온라인**을 선택한 다음 검색 창에 *sql server 2019*를 입력합니다.

   ![도움말 뷰어에서 SQL Server 2019 설명서 검색](../sql-server/media/sql-server-help-installation/sql-2019-search.png)

   > [!Note]
   > 콘텐츠 관리 탭의 로컬 저장소 경로는 로컬 컴퓨터에서 콘텐츠가 설치된 위치를 표시합니다. 이 위치를 변경하려면 **이동**을 선택하고 **대상** 필드에 다른 폴더 경로를 입력한 다음, **확인**을 선택합니다. 로컬 저장소 경로를 변경한 후 도움말 설치에 실패하면 도움말 뷰어를 닫았다가 다시 여세요. 로컬 저장소 경로에 새 경로가 보이는지 확인한 후 다시 설치해보세요.

3. SQL Server 2019용 최신 도움말 콘텐츠를 설치하려면 설치하려는 각 콘텐츠 패키지(책) 옆의 **추가**를 선택한 다음 오른쪽 아래에서 **업데이트**를 선택합니다.

   ![도움말 뷰어에서 SQL Server 2019 책 추가 및 업데이트](../sql-server/media/sql-server-help-installation/sql-2019-add-update.png)

   > [!NOTE]
   > 콘텐츠를 추가하는 동안 도움말 뷰어가 멈추면(중지되면) %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings 또는 HlpViewer_VisualStudiox_en-US.settings 파일의 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 줄을 미래의 날짜로 변경합니다. 이 문제에 대한 자세한 내용은 [Visual Studio 도움말 뷰어가 중단됨](/visualstudio/welcome-to-visual-studio)을 참조하세요.

4. 왼쪽에 있는 콘텐츠 창에서 *sql server 2019*를 검색하여 SQL Server 2019 콘텐츠가 로드되었는지 확인할 수 있습니다.

   ![SQL Server 2019 책이 자동으로 업데이트됨](../sql-server/media/sql-server-help-installation/sql-2019-content.png)

## <a name="sql-server-2017"></a><a id="sql2017"></a> SQL Server 2017

SQL Server 2017용 오프라인 설명서를 로드하려면 다음 단계를 따르세요.

1. SSMS의 도움말 메뉴에서 **도움말 콘텐츠 추가 및 제거**를 선택합니다.

   ![도움말 뷰어 콘텐츠 추가 제거](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   도움말 뷰어에서 콘텐츠 관리 탭이 열립니다.

2. SQL Server 2017용 최신 도움말 콘텐츠를 찾으려면 **콘텐츠 관리** 탭에서 설치 원본 아래에 있는 **온라인**을 선택한 다음 검색 창에 *sql server 2017*을 입력합니다.

   ![도움말 뷰어에서 SQL Server 2017 책 검색](../sql-server/media/sql-server-help-installation/sql-2017-search.png)

   > [!Note]
   > 콘텐츠 관리 탭의 로컬 저장소 경로는 로컬 컴퓨터에서 콘텐츠가 설치된 위치를 표시합니다. 이 위치를 변경하려면 **이동**을 선택하고 **대상** 필드에 다른 폴더 경로를 입력한 다음, **확인**을 선택합니다. 로컬 저장소 경로를 변경한 후 도움말 설치에 실패하면 도움말 뷰어를 닫았다가 다시 여세요. 로컬 저장소 경로에 새 경로가 보이는지 확인한 후 다시 설치해보세요.

3. SQL Server 2017용 최신 도움말 콘텐츠를 설치하려면 설치하려는 각 콘텐츠 패키지(책) 옆의 **추가**를 선택한 다음 오른쪽 아래에서 **업데이트**를 선택합니다.

   ![도움말 뷰어에서 SQL Server 2017 책 추가 및 업데이트](../sql-server/media/sql-server-help-installation/sql-2017-add-update.png)

   > [!NOTE]
   > 콘텐츠를 추가하는 동안 도움말 뷰어가 멈추면(중지되면) %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings 또는 HlpViewer_VisualStudiox_en-US.settings 파일의 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 줄을 미래의 날짜로 변경합니다. 이 문제에 대한 자세한 내용은 [Visual Studio 도움말 뷰어가 중단됨](/visualstudio/welcome-to-visual-studio)을 참조하세요.

4. 왼쪽에 있는 콘텐츠 창에서 *sql server 2017*을 검색하여 SQL Server 2017 콘텐츠가 로드되었는지 확인할 수 있습니다.

   ![SQL Server 2017 책이 자동으로 업데이트됨](../sql-server/media/sql-server-help-installation/sql-2017-content.png)

## <a name="sql-server-2016"></a><a id="sql2016"></a> SQL Server 2016

SQL Server 2016용 오프라인 설명서를 로드하려면 다음 단계를 따르세요.

1. SSMS의 도움말 메뉴에서 **도움말 콘텐츠 추가 및 제거**를 선택합니다.

   ![도움말 뷰어 콘텐츠 추가 제거](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   도움말 뷰어에서 콘텐츠 관리 탭이 열립니다.

2. SQL Server 2016용 최신 도움말 콘텐츠를 찾으려면 **콘텐츠 관리** 탭에서 설치 원본 아래에 있는 **온라인**을 선택한 다음 검색 창에 *sql server 2016*을 입력합니다.

   ![도움말 뷰어에서 SQL Server 2016 책 검색](../sql-server/media/sql-server-help-installation/sql-2016-search.png)

   > [!Note]
   > 콘텐츠 관리 탭의 로컬 저장소 경로는 로컬 컴퓨터에서 콘텐츠가 설치된 위치를 표시합니다. 이 위치를 변경하려면 **이동**을 선택하고 **대상** 필드에 다른 폴더 경로를 입력한 다음, **확인**을 선택합니다. 로컬 저장소 경로를 변경한 후 도움말 설치에 실패하면 도움말 뷰어를 닫았다가 다시 여세요. 로컬 저장소 경로에 새 경로가 보이는지 확인한 후 다시 설치해보세요.

3. SQL Server 2016용 최신 도움말 콘텐츠를 설치하려면 설치하려는 각 콘텐츠 패키지(책) 옆의 **추가**를 선택한 다음 오른쪽 아래에서 **업데이트**를 선택합니다.

   ![도움말 뷰어에서 SQL Server 2016 책 추가 및 업데이트](../sql-server/media/sql-server-help-installation/sql-2016-add-update.png)

   > [!NOTE]
   > 콘텐츠를 추가하는 동안 도움말 뷰어가 멈추면(중지되면) %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings 또는 HlpViewer_VisualStudiox_en-US.settings 파일의 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 줄을 미래의 날짜로 변경합니다. 이 문제에 대한 자세한 내용은 [Visual Studio 도움말 뷰어가 중단됨](/visualstudio/welcome-to-visual-studio)을 참조하세요.

4. 왼쪽에 있는 콘텐츠 창에서 *sql server 2016*을 검색하여 SQL Server 2016 콘텐츠가 로드되었는지 확인할 수 있습니다.

   ![SQL Server 2016 책이 자동으로 업데이트됨](../sql-server/media/sql-server-help-installation/sql-2016-content.png)

## <a name="sql-server-2014"></a><a id="sql2014"></a> SQL Server 2014

SQL Server 2014용 오프라인 설명서를 로드하려면 다음 단계를 따르세요.

1. 다운로드 센터에서 [방화벽 및 프록시로 제한된 환경의 Microsoft SQL Server 2014 제품 설명서](https://www.microsoft.com/download/details.aspx?id=42557)를 다운로드하여 폴더에 저장합니다.

2. 파일의 압축을 풀어 .msha 파일을 확인합니다.

   ![SQL Server 2014 도움말 설명서 설치 파일](../sql-server/media/sql-server-help-installation/sql-2014-help-content-setup-msha.png)

3. SSMS의 도움말 메뉴에서 **도움말 콘텐츠 추가 및 제거**를 선택합니다.

   ![도움말 뷰어 콘텐츠 추가 제거](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   도움말 뷰어에서 콘텐츠 관리 탭이 열립니다.

4. 최신 도움말 콘텐츠를 설치하려면 설치 원본에서 **디스크**를 선택한 다음 줄임표(...)를 선택합니다.

   ![도움말 뷰어 콘텐츠 관리 디스크 원본](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > 콘텐츠 관리 탭의 로컬 저장소 경로는 로컬 컴퓨터에서 콘텐츠가 설치된 위치를 표시합니다. 이 위치를 변경하려면 **이동**을 선택하고 **대상** 필드에 다른 폴더 경로를 입력한 다음, **확인**을 선택합니다.
   로컬 저장소 경로를 변경한 후 도움말 설치에 실패하면 도움말 뷰어를 닫았다가 다시 여세요. 로컬 저장소 경로에 새 경로가 보이는지 확인한 후 다시 설치해보세요.

5. 콘텐츠의 압축을 푼 폴더를 찾습니다. 폴더에서 **HelpContentSetup.msha** 파일을 선택한 다음 **열기**를 선택합니다.

   ![SQL Server 2014 Help Content Setup.msha 파일 열기](../sql-server/media/sql-server-help-installation/sql-2014-open-msha.png)

6. 검색 창에 *sql server 2014*를 입력합니다. 2014 콘텐츠가 사용 가능하다고 표시되면 도움말 뷰어에 설치하려는 각 콘텐츠 패키지(책) 옆의 **추가**를 선택한 다음 **업데이트**를 선택합니다.

   ![도움말 뷰어에서 SQL Server 2014 책 검색](../sql-server/media/sql-server-help-installation/sql-2014-search.png)

   ![도움말 뷰어에서 SQL Server 2014 책 추가 및 업데이트](../sql-server/media/sql-server-help-installation/sql-2014-add-update.png)

    > [!NOTE]
    > 콘텐츠를 추가하는 동안 도움말 뷰어가 멈추면(중지되면) %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings 또는 HlpViewer_VisualStudiox_en-US.settings 파일의 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 줄을 미래의 날짜로 변경합니다. 이 문제에 대한 자세한 내용은 [Visual Studio 도움말 뷰어가 중단됨](/visualstudio/welcome-to-visual-studio)을 참조하세요.

7. 왼쪽에 있는 콘텐츠 창에서 *sql server 2014*를 검색하여 SQL Server 2014 콘텐츠가 로드되었는지 확인할 수 있습니다.

   ![SQL Server 2014 책이 자동으로 업데이트됨](../sql-server/media/sql-server-help-installation/sql-2014-content.png)

## <a name="sql-server-2012"></a><a id="sql2012"></a> SQL Server 2012

SQL Server 2012용 오프라인 설명서를 로드하려면 다음 단계를 따르세요.

1. 다운로드 센터에서 [방화벽 및 프록시로 제한된 환경의 Microsoft SQL Server 2012 제품 설명서](https://www.microsoft.com/download/details.aspx?id=35750)를 다운로드하여 폴더에 저장합니다.

2. 파일의 압축을 풀어 .msha 파일을 확인합니다.

   ![SQL Server 2012 도움말 콘텐츠 설치 파일](../sql-server/media/sql-server-help-installation/sql-2012-help-content-setup-msha.png)

3. SSMS의 도움말 메뉴에서 **도움말 콘텐츠 추가 및 제거**를 선택합니다.

   ![도움말 뷰어 콘텐츠 추가 제거](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   도움말 뷰어에서 콘텐츠 관리 탭이 열립니다.

4. 최신 도움말 콘텐츠를 설치하려면 설치 원본에서 **디스크**를 선택한 다음 줄임표(...)를 선택합니다.

   ![도움말 뷰어 콘텐츠 관리 디스크 원본](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > 콘텐츠 관리 탭의 로컬 저장소 경로는 로컬 컴퓨터에서 콘텐츠가 설치된 위치를 표시합니다. 이 위치를 변경하려면 **이동**을 선택하고 **대상** 필드에 다른 폴더 경로를 입력한 다음, **확인**을 선택합니다.
   로컬 저장소 경로를 변경한 후 도움말 설치에 실패하면 도움말 뷰어를 닫았다가 다시 여세요. 로컬 저장소 경로에 새 경로가 보이는지 확인한 후 다시 설치해보세요.

5. 콘텐츠의 압축을 푼 폴더를 찾습니다. 폴더에서 **HelpContentSetup.msha** 파일을 선택한 다음 **열기**를 선택합니다.

   ![SQL Server 2012 Help Content Setup.msha 파일 열기](../sql-server/media/sql-server-help-installation/sql-2012-open-msha.png)

6. 검색 창에 *sql server 2012*를 입력합니다. 2012 콘텐츠가 사용 가능하다고 표시되면 도움말 뷰어에 설치하려는 각 콘텐츠 패키지(책) 옆의 **추가**를 선택한 다음 **업데이트**를 선택합니다.

   ![도움말 뷰어에서 SQL Server 2012 책 검색](../sql-server/media/sql-server-help-installation/sql-2012-search.png)

   ![도움말 뷰어에서 SQL Server 2012 책 추가 및 업데이트](../sql-server/media/sql-server-help-installation/sql-2012-add-update.png)

    > [!NOTE]
    > 콘텐츠를 추가하는 동안 도움말 뷰어가 멈추면(중지되면) %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings 또는 HlpViewer_VisualStudiox_en-US.settings 파일의 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 줄을 미래의 날짜로 변경합니다. 이 문제에 대한 자세한 내용은 [Visual Studio 도움말 뷰어가 중단됨](/visualstudio/welcome-to-visual-studio)을 참조하세요.

7. 왼쪽에 있는 콘텐츠 창에서 *sql server 2012*을 검색하여 SQL Server 2012 콘텐츠가 로드되었는지 확인할 수 있습니다.

   ![SQL Server 2012 설명서가 자동으로 업데이트됨](../sql-server/media/sql-server-help-installation/sql-2012-content.png)

## <a name="view-offline-documentation"></a>오프라인 설명서 보기

최신 버전의 [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)에서 **도움말** 메뉴를 사용하여 SQL Server 도움말 콘텐츠를 볼 수 있습니다.

### <a name="view-offline-help-content-in-ssms"></a>SSMS에서 오프라인 도움말 콘텐츠 보기

SSMS에서 설치된 도움말을 보려면 도움말 메뉴에서 **도움말 뷰어에서 시작**을 선택하여 도움말 뷰어를 시작합니다.

   ![도움말 뷰어에서 시작](../sql-server/media/sql-server-help-installation/helpviewer-view-offline.png)  

도움말 뷰어에서 콘텐츠 관리 탭이 열리고, 왼쪽 창에 설치된 도움말 목차가 표시됩니다. 목차에서 항목을 선택하면 오른쪽 창에 표시됩니다.

> [!TIP]
> 콘텐츠 창이 표시되지 않으면 왼쪽 여백에서 콘텐츠를 선택합니다. 압정 아이콘을 선택하면 콘텐츠 창이 계속 열려 있습니다.  

   ![콘텐츠가 포함된 도움말 뷰어](../sql-server/media/sql-server-help-installation/view-offline-all.png)

## <a name="life-cycle-policy"></a>수명 주기 정책

특정 제품, 서비스 또는 기술이 지원되는 방식에 대한 자세한 내용은 Microsoft 제품 수명 주기를 참조하세요.

- [Microsoft 수명 주기 정책](https://support.microsoft.com/lifecycle/selectindex)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="next-steps"></a>다음 단계

보관된 콘텐츠 및 도움말 뷰어에 대한 자세한 내용을 보려면 아래 링크를 참조하세요.

- [이전 버전 SQL Server 설명서에 대한 직접 링크](https://docs.microsoft.com/previous-versions/sql/)
- [Microsoft 도움말 뷰어 - Visual Studio](https://docs.microsoft.com/visualstudio/help-viewer/overview)
- [SQL Server 설명서, 시작](../sql-server/index.yml?view=sql-server-2016)
- [SQL 버전 관리 시스템 설명서](../sql-server/versioning-system-monikers-ui-sql-server.md?view=sql-server-2016)