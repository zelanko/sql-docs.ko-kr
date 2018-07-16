---
title: 보고서 서버에 보고서 게시 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
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
caps.latest.revision: 45
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 98482f6ad6e2f98120603c28cdc40181e37ef9a5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273959"
---
# <a name="publishing-reports-to-a-report-server"></a>보고서 서버에 보고서 게시
  보고서 또는 보고서 집합을 디자인 및 테스트한 후 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 기본 제공 배포 기능을 사용하여 보고서를 보고서 서버에 게시할 수 있습니다. 개별 보고서 또는 보고서 서버 프로젝트를 게시할 수 있습니다. 보고서 서버 프로젝트를 게시하는 것은 여러 보고서를 게시하는 가장 쉬운 방법입니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 용어를 사용 하 여 *배포할*, 라는 용어 대신 *게시*합니다. 두 용어는 같은 의미로 사용할 수 있습니다.  
  
 보고서를 게시하려면 보고서를 게시할 권한이 있어야 합니다. 사용 권한은 보고서 서버 관리자가 정의하는 역할 기반 보안을 통해 결정됩니다. 게시 작업은 일반적으로 게시자 역할을 통해 허가됩니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 보고서 게시 관리를 위한 프로젝트 구성을 제공합니다. 이 구성은 보고서 서버의 위치, 보고서 서버에 설치된 SQL Server Reporting Services의 버전, 보고서 서버에 게시된 데이터 원본을 덮어쓰는지 여부 등을 지정합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 제공하는 구성을 사용하는 것 외에도 추가 구성을 만들 수 있습니다.  
  
## <a name="project-configurations"></a>프로젝트 구성  
 유효한 보고서 정의만 보고서 서버에 게시되도록 하기 위해 보고서는 게시되기 전에 빌드됩니다. 프로젝트 구성에는 빌드된 보고서를 임시로 저장하는 폴더, 빌드 문제를 처리하는 방법 등과 같은 보고서 빌드를 위한 속성이 포함됩니다. 또한 보고서 서버의 위치 및 버전과 보고서 서버의 폴더를 지정하는 데 사용되는 속성도 포함됩니다.  
  
 기본적으로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 세 가지 프로젝트 구성을 제공: DebugLocal, Debug 및 Release. 기본 구성은 DebugLocal입니다. 일반적으로 DebugLocal 구성을 사용하면 로컬 미리 보기 창으로 보고서를 볼 수 있고 Debug 구성을 사용하면 테스트 서버에 보고서를 게시할 수 있으며 Release 구성을 사용하면 프로덕션 서버에 보고서를 게시할 수 있습니다. 표준 도구 모음의 솔루션 구성 드롭다운 목록에는 활성 구성이 표시됩니다. 다른 구성을 사용하려면 목록에서 해당 구성을 선택합니다.  
  
 보고 환경에는 여러 보고서 서버와 다른 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가 설치되었을 수 있습니다. 여러 구성을 만든 다음 배포 시나리오에 따라 다른 구성을 사용할 수 있습니다. 자세한 내용은 [배포 및 SQL Server Data Tools의 버전 지원 &#40;SSRS&#41; ](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md) 하 고 [배포 속성 설정 &#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md).  
  
## <a name="publishing-reports"></a>보고서 게시  
 단일 보고서를 게시하거나 여러 보고서를 포함하는 보고서 서버 프로젝트를 게시할 수 있습니다. 보고서를 게시 하는 방법에 대 한 지침은 [보고서 게시](../publish-reports.md)합니다.  
  
### <a name="publishing-a-single-report"></a>단일 보고서 게시  
 프로젝트의 보고서를 일부만 게시하려면 단일 보고서만 게시하도록 선택할 수 있습니다. 이렇게 하려면 보고서를 배포하는 구성(예: Release 구성)을 선택하고 마우스 오른쪽 단추로 해당 보고서를 클릭한 다음 **배포**를 클릭합니다.  
  
 보고서에 공유 데이터 원본을 사용하는 경우 공유 데이터 원본도 배포해야 하며 그렇지 않으면 배포된 보고서가 실행되지 않습니다. 공유 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음 **배포**를 클릭합니다.  
  
 보고서 서버의 대상 서버 URL을 지정해야 하며 보고서 및 공유 데이터 원본이 배포되는 기본 폴더를 변경할 수 있습니다.  
  
### <a name="publishing-multiple-reports"></a>여러 보고서 게시  
 보고서 서버 프로젝트를 게시하면 해당 프로젝트의 모든 보고서가 게시됩니다. 모든 보고서는 동일한 프로젝트 구성을 사용하여 동일한 보고서 서버, 서버의 동일한 폴더 등에 배포됩니다. 보고서를 다른 서버에 게시하려면 하나씩 게시하거나 보고서 서버 프로젝트에 원하는 보고서만 포함합니다. 솔루션은 여러 보고서 서버 프로젝트를 포함할 수 있으며 여러 프로젝트를 사용하면 다른 구성을 사용하여 다른 프로젝트를 배포할 수 있으므로 보고서 배포를 더 쉽게 관리할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [프로젝트 속성 페이지 대화 상자](../tools/project-property-pages-dialog-box.md)   
 [보고서 서버 콘텐츠 관리 &#40;SSRS 기본 모드&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [보고서 업그레이드](../install-windows/upgrade-reports.md)  
  
  
