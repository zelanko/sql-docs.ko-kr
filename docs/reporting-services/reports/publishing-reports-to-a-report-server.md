---
title: 보고서 서버에 보고서 게시 | Microsoft Docs
ms.custom: ''
ms.date: 06/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- production environments [Reporting Services]
- report projects [Reporting Services]
- Debug configuration [Reporting Services]
- report publishing [Reporting Services]
- publishing reports [Reporting Services]
- report properties [Reporting Services]
- Report Designer [Reporting Services], deploying reports
- Production configuration [Reporting Services]
- publishing reports [Reporting Services], production environments
- DebugLocal configuration [Reporting Services]
- deploying [Reporting Services], reports
- Report Designer [Reporting Services], publishing reports
ms.assetid: bd7aa5e0-61ce-43fd-8f74-5d1aeed078bb
caps.latest.revision: 47
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9a69b67fcbc9d047526ff0c30883731543a826a7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33026670"
---
# <a name="publishing-reports-to-a-report-server"></a>보고서 서버에 보고서 게시
  보고서 또는 보고서 집합을 디자인 및 테스트한 후에 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 기본 제공 배포 기능을 사용하여 보고서를 보고서 서버에 게시할 수 있습니다. 개별 보고서뿐만 아니라 여러 보고서와 데이터 원본을 포함할 수 있는 보고서 서버 프로젝트를 게시할 수 있습니다. 보고서 서버 프로젝트를 게시하는 것은 여러 보고서를 게시하는 가장 쉬운 방법입니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서는 *게시*라는 용어 대신에 *배포*라는 용어를 사용합니다. 두 용어는 같은 의미로 사용할 수 있습니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 보고서 게시 관리를 위한 프로젝트 구성을 제공합니다. 이 구성은 보고서 서버의 위치, 보고서 서버에 설치된 SQL Server Reporting Services의 버전, 보고서 서버에 게시된 데이터 원본을 덮어쓰는지 여부 등을 지정합니다. 예를 들어 "디버그" 구성을 "릴리스" 구성과 다른 서버에 게시할 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 제공하는 구성을 사용하는 것 외에도 추가 구성을 만들 수 있습니다.  
 
## <a name="requirements-to-publish"></a>게시 요구 사항
사용 권한은 보고서 서버 관리자가 정의하는 역할 기반 보안을 통해 결정됩니다. 게시 작업은 일반적으로 **게시자 역할**을 통해 허가됩니다.  
  
## <a name="project-configurations"></a>프로젝트 구성  
 보고 환경에는 여러 보고서 서버와 다른 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가 설치되었을 수 있습니다. 여러 구성을 만든 다음 배포 시나리오에 따라 다른 구성을 사용할 수 있습니다. 프로젝트 구성에는 빌드된 보고서를 임시로 저장하는 폴더, 빌드 문제를 처리하는 방법 등과 같은 보고서 빌드를 위한 속성이 포함됩니다. 또한 보고서 서버의 위치 및 버전과 보고서 서버의 폴더를 지정하는 데 사용되는 속성도 포함됩니다.  
  
 기본적으로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 은 **DebugLocal**, **Debug**및 **Release**라는 세 가지 프로젝트 구성을 제공합니다. 기본 구성은 DebugLocal입니다. 일반적으로 DebugLocal 구성을 사용하면 로컬 미리 보기 창으로 보고서를 볼 수 있고 Debug 구성을 사용하면 테스트 서버에 보고서를 게시할 수 있으며 Release 구성을 사용하면 프로덕션 서버에 보고서를 게시할 수 있습니다. 표준 도구 모음의 솔루션 구성 드롭다운 목록에는 활성 구성이 표시됩니다. 다른 구성을 사용하려면 목록에서 해당 구성을 선택합니다.  
  
 ![ssrs_project_properties](../../reporting-services/reports/media/ssrs-project-properties.png) 
  
 자세한 내용은 다음 항목을 참조하세요.
 + [프로젝트 속성 페이지 대화 상자](../../reporting-services/tools/project-property-pages-dialog-box.md)
 + [SQL Server Data Tools의 배포 및 버전 지원](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)
 + [SSDT에서 Reporting Services 프로젝트에 대한 배포 속성 설정](../../reporting-services/tools/set-deployment-properties-reporting-services.md)
  
## <a name="to-publish-all-reports-in-a-project"></a>프로젝트의 모든 보고서를 게시하려면  
  
**빌드** 메뉴에서 **보고서 프로젝트 이름>\< 배포**를 클릭합니다. 또는 솔루션 탐색기에서 보고서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **배포**를 클릭합니다. 출력 창에서 게시 프로세스의 상태를 볼 수 있습니다.  
  
보고서 서버 프로젝트를 배포할 경우 보고서 프로젝트의 공유 데이터 원본도 배포됩니다. 모든 보고서는 동일한 프로젝트 구성을 사용하여 동일한 보고서 서버, 서버의 동일한 폴더 등에 배포됩니다. 보고서를 다른 서버에 게시하려면 하나씩 게시하거나 보고서 서버 프로젝트에 원하는 보고서만 포함합니다. 솔루션은 여러 보고서 서버 프로젝트를 포함할 수 있으며 여러 프로젝트를 사용하면 다른 구성을 사용하여 다른 프로젝트를 배포할 수 있으므로 보고서 배포를 더 쉽게 관리할 수 있습니다. 
  
## <a name="to-publish-a-single-report"></a>단일 보고서를 게시하려면  
  
솔루션 탐색기에서 보고서를 마우스 오른쪽 단추로 클릭한 다음 **배포**를 클릭합니다. 출력 창에서 게시 프로세스의 상태를 볼 수 있습니다.  
  
 보고서를 게시할 경우 보고서가 사용하는 공유 데이터 원본도 배포해야 합니다.   
 프로젝트의 보고서를 일부만 게시하려면 단일 보고서만 게시하도록 선택할 수 있습니다. 이렇게 하려면 보고서를 배포하는 구성(예: Release 구성)을 선택하고 마우스 오른쪽 단추로 해당 보고서를 클릭한 다음 **배포**를 클릭합니다.  
  
 보고서에 공유 데이터 원본을 사용하는 경우 공유 데이터 원본도 배포해야 하며 그렇지 않으면 배포된 보고서가 실행되지 않습니다. 공유 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음 **배포**를 클릭합니다.  
  
 보고서 서버의 대상 서버 URL을 지정해야 하며 보고서 및 공유 데이터 원본이 배포되는 기본 폴더를 변경할 수 있습니다.  

  
## <a name="see-also"></a>참고 항목  
 [프로젝트 속성 페이지 대화 상자](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [보고서 업그레이드](../../reporting-services/install-windows/upgrade-reports.md)  
  
  
