---
title: "SQL Server 도움말 콘텐츠 및 도움말 뷰어 | Microsoft Docs"
ms.custom: 
ms.date: 12/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: 
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 679d0fb003a8a59185d860a125cfdd8b5601367c
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="sql-server-offline-help-and-help-viewer"></a>SQL Server 오프라인 도움말 및 도움말 뷰어

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SSMS(SQL Server Management Studio) 또는 VS(Visual Studio)의 도움말 뷰어를 사용하여 온라인 소스 또는 디스크의 SQL Server 도움말 패키지를 다운로드 및 설치하고 오프라인으로 볼 수 있습니다. 이 문서에서는 도움말 뷰어를 설치하는 도구, 오프라인 도움말 콘텐츠를 설치하는 방법 및 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)], SQL Server 2016 및 SQL Server 2017에 대한 도움말을 보는 방법을 설명합니다.

> [!NOTE]
> SQL Server 2016 및 SQL Server 2017 도움말은 결합되었지만 일부 항목은 개별 버전에 적용됩니다(명시된 경우). 대부분의 항목은 두 버전 모두에 적용됩니다.

## <a name="install-the-help-viewer"></a>도움말 뷰어 설치

도움말 뷰어는 두 가지 버전이 있습니다. v2.x는 SQL Server 2016/SQL Server 2017 도움말을 지원하고, v1.x는 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 도움말을 지원합니다. 도움말 뷰어는 프록시 설정을 지원하지 않고 ISO 형식을 지원하지 않습니다. 

다음 도구는 도움말 뷰어를 설치합니다. 

|**도움말 뷰어를 설치하는 도구**|**설치된 도움말 뷰어 버전**|
|---------|---------|
|[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)| v2.2|
|[Visual Studio 2015용 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)| v2.2|
|Visual Studio 2017* | v2.3|
|Visual Studio 2015 | v2.2|
|SQL Server 2014 Management Studio | v1.x|
|이전 버전의 Visual Studio | v1.x|
|SQL Server 2016 | v1.x|

\* Visual Studio 2017과 함께 도움말 뷰어를 설치하려면 Visual Studio 설치 관리자의 개별 구성 요소 탭에서 코드 도구 아래에 있는 **도움말 뷰어**를 선택한 다음 **설치**를 클릭합니다. 

>[!NOTE]
> - SQL Server 2016은 SQL Server 2016 도움말을 지원하지 않는 도움말 뷰어 1.1을 설치합니다. 
> - SQL Server 2017을 설치하면 어떠한 도움말 뷰어도 설치되지 않습니다.
> - 디스크에서 콘텐츠를 설치할 경우 도움말 뷰어 v2.x가 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 도움말도 지원할 수 있습니다.

## <a name="use-help-viewer-v2x"></a>도움말 뷰어 v2.x 사용

SSMS 17.x와 VS 2015 및 2017은 SQL Server 2016/2017 도움말을 지원하는 도움말 뷰어 2.x를 사용합니다. 

**도움말 뷰어 v2.x를 사용하여 오프라인 도움말 콘텐츠를 다운로드하고 설치하려면**

1. SSMS 또는 VS의 도움말 메뉴에서 **도움말 콘텐츠 추가 및 제거**를 클릭합니다. 

   ![HelpViewer2 Add Remove Content](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   도움말 뷰어에서 콘텐츠 관리 탭이 열립니다.  
   
2. 최신 도움말 콘텐츠 패키지를 설치하려면 설치 소스 아래에서 **온라인**을 선택합니다.
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > 디스크(SQL Server 2014 도움말)에서 설치하려면 설치 소스 아래에서 **디스크**를 선택하고 디스크 위치를 지정합니다.
   
   콘텐츠 관리 탭의 로컬 저장소 경로에 콘텐츠가 설치될 로컬 컴퓨터의 위치가 표시됩니다. 위치를 변경하려면 **이동**을 클릭하고 **대상** 필드에 다른 폴더 경로를 입력한 다음 **확인**을 클릭합니다.
   로컬 저장소 경로를 변경한 후 도움말 설치에 실패할 경우 도움말 뷰어를 닫았다가 다시 열고, 로컬 저장소 경로에 새 위치가 표시되는지 확인한 후, 설치를 다시 시도해 보세요.

3. 설치하려는 각 콘텐츠 패키지(책) 옆에 있는 **추가**를 클릭합니다. 
   모든 SQL Server 도움말 콘텐츠를 설치하려면 SQL Server 아래에 있는 13권의 책을 모두 추가합니다. 
   
4. 오른쪽 아래에 있는 **업데이트**를 클릭합니다. 
   왼쪽의 도움말 목차에 추가된 책이 자동으로 업데이트됩니다. 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> SQL Server 목차의 모든 상위 노드 제목이 해당하는 다운로드식 도움말 책의 이름과 정확히 일치하는 것은 아닙니다. 목차 제목은 다음과 같이 책 이름에 매핑됩니다.

| 내용 창 | SQL Server 책 |
|-----|-----|
|Analysis Services 언어 참조 | Analysis Services(MDX) 언어 참조|
|DAX(Data Analysis Expressions) 참조 | DAX(Data Analysis Expressions) 참조|
|DMX(Data Mining Extensions) 참조 | DMX(Data Mining Extensions) 참조|
|SQL Server용 개발자 가이드 | SQL Server 개발자 참조|
|SQL Server Management Studio 다운로드 | SQL Server Management Studio|
|SQL Server에서 기계 학습 시작 | Microsoft Machine Learning Services|
|파워 쿼리 M 참조 | 파워 쿼리 M 참조|
|SQL Server 드라이버 | SQL Server 연결 드라이버|
|Linux의 SQL Server | Linux의 SQL Server|
|SQL Server 기술 설명서 | SQL Server 기술 설명서(SSIS, SSRS, DB 엔진, 설치 프로그램)|
|Azure SQL Database용 도구 및 유틸리티 | SQL Server 도구|
|Transact-SQL 참조(데이터베이스 엔진) | Transact-SQL 참조|
|XQuery 언어 참조(SQL Server) | XQuery 언어 참조(SQL Server)|

> [!NOTE]
> 콘텐츠를 추가하는 동안 도움말 뷰어가 멈추면(중지되면) %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings 또는 HlpViewer_VisualStudiox_en-US.settings 파일의 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 줄을 미래의 날짜로 변경합니다. 이 문제에 대한 자세한 내용은 [Visual Studio 도움말 뷰어가 중단됨](https://msdn.microsoft.com/en-us/library/dd831853.aspx)을 참조하세요.

**도움말 뷰어 v2.x를 사용하여 SSMS에서 오프라인 도움말 콘텐츠를 보려면**

SSMS에서 설치된 도움말을 보려면 CTRL + ALT + F1을 누르거나 도움말 메뉴에서 **콘텐츠 추가 또는 제거**를 선택하여 도움말 뷰어를 시작합니다. 

   ![HelpViewer2 Add Remove Content](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

도움말 뷰어에서 콘텐츠 관리 탭이 열리고, 왼쪽 창에 설치된 도움말 목차가 표시됩니다. 목차에서 항목을 클릭하면 오른쪽 창에 표시됩니다. 
> [!TIP]
> 내용 창이 표시되지 않으면 왼쪽 여백에서 내용을 클릭합니다. 압정 아이콘을 클릭하면 내용 창이 계속 열려 있습니다.  

   ![도움말 뷰어 v2.x와 콘텐츠](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

**도움말 뷰어 v2.x를 사용하여 VS에서 오프라인 도움말 콘텐츠를 보려면**

Visual Studio에서 설치된 도움말을 보려면:
1. 도움말 메뉴에서 **도움말 기본 설정 지정**을 가리키고 **도움말 뷰어에서 시작**을 선택합니다. 

   ![VS Help View Set Preference Help Viewer](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. 도움말 메뉴에서 **도움말 보기**를 클릭하여 도움말 뷰어에 콘텐츠를 표시합니다. 

   ![도움말 보기](../sql-server/media/sql-server-help-installation/viewhelp.png)

   도움말 목차가 왼쪽에 표시되고, 선택한 도움말 항목이 오른쪽에 표시됩니다. 
   
## <a name="use-help-viewer-v1x"></a>도움말 뷰어 v1.x 사용

이전 버전의 SSMS 및 VS에서는 SQL Server 2014 도움말을 지원하는 도움말 뷰어 1.x를 사용합니다. 

**도움말 뷰어 v1.x를 사용하여 오프라인 도움말 콘텐츠를 다운로드하고 설치하려면**

이 프로세스에서는 도움말 뷰어 1.x를 사용하여 Microsoft 다운로드 센터에서 SQL Server 2014 도움말을 다운로드하고 컴퓨터에 설치합니다.

1. [Microsoft SQL Server 2014 제품 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=42557)로 이동하고 사이트를 다운로드한 후 **다운로드**를 클릭합니다.  
2. 메시지 상자에서 **저장**을 클릭하여 *SQLServer2014Documentation\_\*.exe* 파일을 컴퓨터에 저장합니다.  
   
   >[!NOTE]
   >방화벽 및 프록시로 제한된 환경에서는 해당 환경으로 가져올 수 있도록 다운로드한 파일을 USB 드라이브 또는 기타 휴대용 미디어에 저장합니다.   
   
3. .exe를 두 번 클릭하여 도움말 콘텐츠 파일의 압축을 풀고 파일을 로컬 또는 공유 폴더에 저장합니다.  
4. SSMS를 시작하거나 도움말 메뉴에서 **도움말 설정 관리**를 클릭하여 **도움말 라이브러리 관리자**를 엽니다.  
5. **디스크에서 콘텐츠 설치**를 클릭하고 도움말 콘텐츠 파일의 압축을 푼 폴더로 이동합니다.  
   
   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)
   
   > [!IMPORTANT]
   > 부분 목차만 포함된 로컬 도움말 콘텐츠를 설치하지 않으려면 **도움말 라이브러리 관리자**에서 **디스크에서 콘텐츠 설치** 옵션을 사용해야 합니다.  **온라인에서 콘텐츠 설치**를 사용했고 도움말 뷰어에 부분 목차가 표시되는 경우 문제 해결 단계를 보려면 이 [블로그 게시물](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/)을 참조하세요. 
   
8. HelpContentSetup.msha 파일을 클릭하고, **열기**, **다음**을 차례로 클릭합니다.  
9. 설치할 설명서 옆의 **추가** 를 클릭하고 **업데이트**를 클릭합니다.  
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)  
   
10. **마침**을 클릭한 다음 **끝내기**를 클릭합니다.

**도움말 뷰어 v1.x를 사용하여 오프라인 도움말 콘텐츠를 보려면**

11. 설치된 도움말을 보려면 **도움말 라이브러리 관리자**를 열고 **온라인 또는 로컬 도움말 선택**을 클릭한 다음 **로컬 도움말 사용**을 클릭합니다.
12. **도움말** 메뉴에서 **도움말 보기**를 클릭하여 도움말 뷰어를 열고 콘텐츠를 확인합니다. 왼쪽 창에 설치된 콘텐츠가 나열됩니다.  
   
   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  
   
## <a name="view-online-help"></a>온라인 도움말 보기

온라인 도움말에는 항상 가장 최근의 콘텐츠가 표시됩니다. 

**SSMS 17.x에서 SQL Server 온라인 도움말을 보려면**

- **도움말** 메뉴에서 **도움말 보기**를 클릭합니다. 최신 SQL Server 2016/2017 설명서([https://docs.microsoft.com/sql/https://docs.microsoft.com/en-us/sql/sql-server/sql-server-technical-documentation](https://docs.microsoft.com/en-us/sql/sql-server/sql-server-technical-documentation))는 브라우저에서 표시됩니다. 

   ![도움말 보기](../sql-server/media/sql-server-help-installation/viewhelp.png)

**Visual Studio에서 Visual Studio 온라인 도움말을 보려면**

1. 도움말 메뉴에서 **도움말 기본 설정 지정**을 가리키고 **브라우저에서 시작** 또는 **도움말 뷰어에서 시작**을 선택합니다. 
2. 도움말 메뉴에서 **도움말 보기**를 클릭합니다. 선택한 환경에서 최신 Visual Studio 도움말이 표시됩니다. 

**도움말 뷰어 v1.x를 사용하여 온라인 도움말을 보려면**

1. 도움말 메뉴에서 **도움말 설정 관리**를 클릭하여 **도움말 라이브러리 관리자**를 엽니다.  
2. 도움말 라이브러리 관리자 대화 상자에서 **온라인 또는 로컬 도움말 선택**을 클릭합니다.  
   
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
   
3. **온라인 도움말 사용**, **확인**, **끝내기**를 차례로 클릭합니다.  
   
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/sql-server-help-installation/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)
   
4. **도움말** 메뉴에서 **도움말 보기**를 클릭하여 도움말 뷰어를 열고 콘텐츠를 확인합니다. 

## <a name="view-f1-help"></a>F1 도움말 보기

SSMS 또는 VS의 대화 상자에서 F1 키를 누르거나 **도움말** 또는 **?** 아이콘을 클릭하면 브라우저 또는 도움말 뷰어에 상황에 맞는 온라인 도움말 항목이 나타납니다. 

**F1 도움말을 보려면**

1. 도움말 메뉴에서 **도움말 기본 설정 지정**을 가리키고 **브라우저에서 시작** 또는 **도움말 뷰어에서 시작**을 선택합니다. 
2. 표시되는 대화 상자에서 F1 키를 누르거나 **도움말** 또는 **?**를 클릭하여 선택한 환경에서 상황에 맞는 온라인 항목을 봅니다.

>  [!NOTE]
>  F1 도움말은 온라인 상태일 경우에만 작동합니다. F1 도움말에 대한 오프라인 소스는 없습니다. 
   

## <a name="next-steps"></a>다음 단계
[Microsoft 도움말 뷰어 - Visual Studio](/visualstudio/ide/microsoft-help-viewer)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
