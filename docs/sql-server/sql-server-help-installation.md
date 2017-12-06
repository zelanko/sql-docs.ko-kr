---
title: "SQL Server용 도움말 뷰어 및 오프라인 콘텐츠 | Microsoft Docs"
ms.custom: 
ms.date: 06/27/2017
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
caps.latest.revision: "8"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 048b1d257287b8f0a4645f57ce88c30b24a9f654
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="help-viewer-and-offline-content-for-sql-server"></a>SQL Server용 도움말 뷰어 및 오프라인 콘텐츠
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
  
  
이 문서에서는 도움말 뷰어를 설치하고 오프라인에서 SQL Server 문서를 보는 방법을 보여 줍니다. 문서에서는 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)], SQL Server 2016 및 SQL Server 2017에 대한 설명서를 다룹니다. 

## <a name="install-help-viewer"></a>도움말 뷰어 설치
다음 표에서는 사용 중인 SQL Server 버전에 따라 도움말 뷰어를 설치하는 도구를 보여 줍니다. 도움말 뷰어를 설치하려면 나열된 도구 중 하나를 설치합니다.


|**SQL Server 버전**|**도움말 뷰어를 설치하는 도구**|**설치된 도움말 뷰어 버전**|
|---------|---------|---------|
|SQL Server 2017<br>SQL Server 2016     |   [최신 버전의 SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)<br><br>[최신 버전의 Visual Studio 2015용 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)<br><br>Visual Studio 2017(*SQL Server 2016만 지원*)  |  v2.x       |
|SQL Server 2014    | SQL Server 2014 Management Studio<br><br>Visual Studio 2012 이전 버전의 Visual Studio        |  v1.x       |


> [!IMPORTANT]
> SQL Server 2016이 설치하는 도움말 뷰어 1.1은 SQL Server 2016 및 2017에 대한 설명서를 보는 데 사용할 수 없습니다.
> <br>
> <br>
> SQL Server 2017은 도움말 뷰어를 설치하지 않습니다.
> <br>
> <br>
> Visual Studio 2017과 함께 도움말 뷰어를 설치하려면 **Visual Studio 설치 관리자** 프로그램에서 **개별 구성 요소** 탭을 클릭하고 **코드 도구** 범주에서 **도움말 뷰어**를 클릭한 다음 **설치**를 클릭합니다. 
> <br>
> <br>
> **디스크에서 콘텐츠를 설치**하는 경우에만 도움말 뷰어 2.x를 사용하여 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]에 대한 로컬 도움말을 볼 수 있습니다. 


## <a name="sql-server-2016-sql-server-2017-offline-content"></a>SQL Server 2016, SQL Server 2017 오프라인 콘텐츠  
 
**오프라인 콘텐츠를 설치하려면**  
1. SQL Server Management Studio 또는 Visual Studio를 시작하고 **도움말** 메뉴에서 **도움말 콘텐츠 추가 및 제거**를 클릭하여 도움말 뷰어를 엽니다.  
2. **콘텐츠 관리** 탭을 클릭합니다.  
3. 온라인 원본에서 도움말을 설치하려면 **설치 원본** 영역에서 **온라인**을 클릭합니다.  
![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/helpviewer2-managecontent-onlinesource.png)  
7. 설치할 설명서 옆의 **추가** 를 클릭하고 **업데이트**를 클릭합니다.  
![HelpViewer2_ManageContent_AddContent](../sql-server/media/helpviewer2-managecontent-addcontent.png)     
  
   >[!IMPORTANT] 
   >SQL Server Management Studio 및 Visual Studio에서 설명서를 추가하는 프로세스 중에 도움말 뷰어 응용 프로그램이 중단(정지)될 수 있습니다. 이 문제를 해결하려면 다음을 수행하세요. 이 문제에 대한 자세한 내용은 [Visual Studio 도움말 뷰어가 중단됨](https://msdn.microsoft.com/library/mt654096.aspx)을 참조하세요.  
   >>메모장에서 %LOCALAPPDATA%\Microsoft\HelpViewer2.3\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio15_en-US.settings 파일을 열고 다음 코드의 날짜를 미래의 날짜로 변경합니다. 이 파일은 Visual Studio를 설치한 경우에만 로컬 컴퓨터에서 사용할 수 있습니다. 
   >>>Cache LastRefreshed="12/31/2017 00:00:00"  
  
    왼쪽 창의 목차가 자동으로 업데이트되어 추가한 설명서가 포함됩니다.  
![HelpViewer2_withContentInstalled](../sql-server/media/helpviewer2-withcontentinstalled.png)

1. (선택 사항) **콘텐츠 관리** 탭의 **로컬 저장소 경로** 상자에 로컬 컴퓨터에서 설명서가 설치된 위치가 표시됩니다. 설명서를 다른 위치로 이동하려면 **이동**을 클릭하고, **콘텐츠 이동** 대화 상자의 **대상** 필드에 폴더 경로를 입력하고, **확인**을 클릭합니다.

   ![HelpViewer2_Move Content Dialog](../sql-server/media/helpviewer2-move-content-dialog.png)

   콘텐츠가 이동된 후 새 위치가 **로컬 저장소 경로**에 표시됩니다.
      
   >[!IMPORTANT]
   > 이동 작업이 실패했음을 나타내는 메시지가 표시되면 메시지 상자를 닫고, 도움말 뷰어를 닫고 나서, 도움말 뷰어를 다시 엽니다. 이제 콘텐츠의 새 위치가 **로컬 저장소 경로**에 표시됩니다.   
 
## <a name="includesssql14mdincludessssql14-mdmd-offline-content"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 오프라인 콘텐츠 
 
  
**오프라인 콘텐츠를 설치하려면**  
1. 도움말 콘텐츠에 대한 [다운로드 사이트](https://www.microsoft.com/en-us/download/details.aspx?id=42557)로 이동하고 **다운로드**를 클릭합니다.  
2. 메시지 상자에서 **저장**을 클릭하여 SQLServer2014Documentation_*.exe 파일을 컴퓨터에 저장합니다.  

 방화벽 및 프록시로 제한된 환경에서는 해당 환경으로 가져올 수 있도록 다운로드한 파일을 USB 드라이브 또는 기타 휴대용 미디어에 저장합니다.   

3. .exe를 두 번 클릭하여 도움말 콘텐츠 파일의 압축을 풀고 파일을 로컬 또는 공유 폴더에 저장합니다.  
4. SQL Server Management Studio 또는 Visual Studio를 시작하고 **도움말** 메뉴에서 **도움말 설정 관리**를 클릭하여 **도움말 라이브러리 관리자**를 엽니다.  
5. **디스크에서 콘텐츠 설치**를 클릭하고 도움말 콘텐츠 파일의 압축을 푼 폴더로 이동합니다.  
  
     디스크에서 설치 콘텐츠 선택  |도움말 콘텐츠 파일로 이동   
     ---------|---------  
     ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
     >[!IMPORTANT]
     > 부분 목차만 포함된 로컬 도움말 콘텐츠를 설치하지 않으려면 **도움말 라이브러리 관리자**에서 **디스크에서 콘텐츠 설치** 옵션을 사용합니다.  
     >>**온라인에서 콘텐츠 설치** 옵션을 사용했고 도움말 뷰어에 부분 목차가 표시되는 경우 문제 해결 단계를 보려면 이 [블로그 게시물](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/)을 참조하세요. 

8. HelpContentSetup.msha 파일을 클릭하고, **열기**, **다음**을 차례로 클릭합니다.  
9. 설치할 설명서 옆의 **추가** 를 클릭하고 **업데이트**를 클릭합니다.  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. **마침**을 클릭한 다음 **끝내기**를 클릭합니다.
11. **도움말 라이브러리 관리자**를 다시 열고 **온라인 또는 로컬 도움말 선택**을 클릭한 다음 **로컬 도움말 사용**을 클릭합니다.
12. **도움말** 메뉴에서 **도움말 보기**를 클릭하여 도움말 뷰어를 열고 콘텐츠를 확인합니다. 직접 설치한 콘텐츠가 왼쪽 창의 목차에 나열되어야 합니다.  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
## <a name="view-online-content-in-help-viewer"></a>도움말 뷰어에서 온라인 콘텐츠 보기

도움말 뷰어 v2.x에서 다음 중 하나를 수행하여 온라인 콘텐츠를 볼 수 있습니다.

- SQL Server Management Studio의 **도움말** 메뉴에서 **도움말 보기**를 클릭합니다. 설명서가 브라우저에 표시됩니다.
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../sql-server/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)

- Visual Studio의**도움말** 메뉴에서 **도움말 기본 설정 지정**을 클릭한 다음 **브라우저에서 시작**을 클릭합니다. **도움말** 메뉴에서 **도움말 보기**를 클릭하면 설명서가 브라우저에 표시됩니다.

![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../sql-server/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)   

도움말 뷰어 v1.x에서 다음을 수행하여 온라인 콘텐츠를 볼 수 있습니다.
1. **Help** 메뉴에서 **도움말 설정 관리**를 클릭하여 **도움말 라이브러리 관리자**를 엽니다.  
2. **도움말 라이브러리 관리자** 대화 상자에서 **온라인 또는 로컬 도움말 선택**을 클릭합니다.  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. **온라인 도움말 사용**, **확인**, **끝내기**를 차례로 클릭합니다.  

   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

## <a name="f1-help-and-other-tips"></a>F1 도움말 및 기타 팁

F1 키를 누르면 해당 항목이 온라인으로 표시됩니다. 이 항목은 로컬 도움말로 표시할 수 없습니다.

또한 도움말 뷰어는 프록시 설정을 지원하지 않고 ISO 형식을 지원하지 않습니다. 

## <a name="additional-information"></a>추가 정보
[Microsoft 도움말 뷰어 - Visual Studio](/visualstudio/ide/microsoft-help-viewer)  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
