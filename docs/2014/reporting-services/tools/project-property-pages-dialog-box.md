---
title: 프로젝트 속성 페이지 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rpt.rptdesigner.projectpropertypages.general.f1
helpviewer_keywords:
- Project Property Pages dialog box
ms.assetid: 209d9e22-37fc-418f-8739-83adcf447d3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a9d66e6e5317bef72be6bba254ccca0cc82aa026
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100035"
---
# <a name="project-property-pages-dialog-box"></a>프로젝트 속성 페이지 대화 상자
  프로젝트 속성 페이지를 사용하여 보고서 서버 프로젝트의 배포 속성을 구성할 수 있습니다. 이 대화 상자를 열려면 **프로젝트** 메뉴에서 _\<Report Project Name>_ **속성**을 클릭합니다.  
  
 구성 속성을 정의한 후 도구 모음의 **솔루션 구성** 드롭다운 목록에서 구성을 선택할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **구성**  
 편집할 구성을 선택합니다. 처음에는 **Debug**, **DebugLocal**및 **Release**의 3가지 구성을 사용할 수 있습니다. 활성 구성이 첫 번째로 표시됩니다(예: **활성(디버그)**).  
  
 두 개 이상의 구성에 대한 속성을 동시에 보려면 **모든 구성** 또는 **여러 구성**을 선택합니다.  
  
 추가 구성을 만들려면 도구 모음의 **구성 관리자** 를 클릭합니다.  
  
 **Configuration Manager**  
 다른 구성을 추가하거나 전체 솔루션의 구성을 관리합니다. 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 설명서를 참조하세요.  
  
 **OutputPath**  
 보고서의 빌드 확인, 배포 및 미리 보기에 사용되는 보고서 정의를 저장할 경로를 입력하거나 붙여 넣습니다. 이 경로는 프로젝트에 사용하는 경로 및 프로젝트 경로 아래의 자식 폴더인 상대 경로와 달라야 합니다.  
  
> [!NOTE]  
>  여러 구성을 사용하여 수행하는 태스크에 따라 경로 간을 전환할 수 있습니다.  
  
 **ErrorLevel**  
 오류로 보고되는 빌드 문제의 심각도를 입력합니다. **ErrorLevel** 값보다 작거나 같은 심각도 수준을 가진 문제는 오류로 보고되고 그렇지 않은 문제는 경고로 보고됩니다. 오류가 발생하면 빌드 태스크가 실패합니다. 유효한 심각도 수준은 0에서 4까지입니다. 기본값은 2입니다.  
  
 **StartItem**  
 프로젝트가 보고서 서버에 게시된 후 웹 브라우저에 표시될 보고서를 선택하거나 프로젝트를 로컬로 실행하는 경우 미리 보기 창에 표시될 보고서를 선택합니다. 시작 항목은 프로젝트를 배포하지 않고 빌드하는 구성과 **디버그** 명령(**F5**)을 사용하는 경우 반드시 지정해야 합니다. 프로젝트를 배포하는 구성에서는 필수입니다.  
  
 **OverwriteDataSources**  
 보고서가 게시될 때 서버의 데이터 원본을 프로젝트의 데이터 원본으로 덮어쓰려면 **True** 를 선택하고, 서버의 기존 데이터 원본을 그대로 두려면 **False** 를 선택합니다.  
  
 **TargetServerVersion**  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 선택 하거나 **버전 검색** 을 선택 하 여 **TargetServer URL** 속성으로 식별 되는 서버에 설치 된 버전을 자동으로 확인 합니다. 기본값은 **SQL Server 2008 R2**입니다.  
  
 **TargetDataSourceFolder**  
 게시된 공유 데이터 원본을 저장할 폴더의 이름입니다. 폴더를 지정하지 않는 경우 데이터 원본은 보고서와 같은 폴더에 게시됩니다. 보고서 서버에 폴더가 없는 경우 보고서가 게시될 때 보고서 디자이너에서 폴더를 만듭니다.  
  
 기본 모드로 실행 중인 보고서 서버에 게시하는 경우 루트로 시작되는 폴더 계층의 전체 경로를 지정합니다. Folder1/Folder2/Folder3).  
  
 SharePoint 통합 모드로 실행 중인 보고서 서버에 게시하는 경우 SharePoint 라이브러리에 대한 URL을 사용합니다(예: 예를 들어 http://*\<servername>/\<site>*/documents/myfolder.  
  
 **TargetReportFolder**  
 게시된 보고서를 저장할 폴더의 이름입니다. 기본적으로 보고서 프로젝트의 이름입니다. 보고서 서버에 폴더가 없는 경우 보고서가 게시될 때 보고서 디자이너에서 폴더를 만듭니다.  
  
 기본 모드로 실행 중인 보고서 서버에 게시하는 경우 루트로 시작되는 폴더 계층의 전체 경로를 지정합니다. 폴더가 다른 폴더 안에 있는 경우 루트로 시작되는 폴더 경로를 입력합니다(예: Folder1/Folder2/Folder3).  
  
 SharePoint 통합 모드로 실행 중인 보고서 서버에 게시하는 경우 SharePoint 라이브러리에 대한 URL을 사용합니다(예: 예를 들어 http://*\<servername>* / * \<site>*/documents/myfolder.  
  
 **TargetServerURL**  
 대상 보고서 서버의 URL입니다. 보고서를 게시하기 전에 이 속성을 유효한 보고서 서버 URL로 설정해야 합니다.  
  
 기본 모드로 실행 중인 보고서 서버에 게시하는 경우 보고서 서버의 가상 디렉터리 URL을 사용합니다(예: 예: http://\<server>/reportserver 이는 보고서 관리자가 아닌 보고서 서버의 가상 디렉터리입니다. 기본적으로 보고서 서버는 "reportserver"라는 가상 디렉터리에 설치되어 있습니다.  
  
 SharePoint 통합 모드로 실행 중인 보고서 서버에 게시하는 경우 SharePoint 최상위 사이트나 하위 사이트에 대한 URL을 사용합니다. 사이트를 지정하지 않으면 기본 최상위 사이트가 사용됩니다. 예를 들어 http://\<*servername>*, http://<*servername*/\<*site>* 또는 http://\<*servername>* / \< *site>* / \< *하위 *사이트>합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 게시](../publish-reports.md)   
 [SharePoint 라이브러리에 보고서 게시](../reports/publish-a-report-to-a-sharepoint-library.md)   
 [배포 속성 &#40;Reporting Services&#41;설정](set-deployment-properties-reporting-services.md)   
 [보고서 디자이너 F1 도움말](report-designer-f1-help.md)  
  
  
