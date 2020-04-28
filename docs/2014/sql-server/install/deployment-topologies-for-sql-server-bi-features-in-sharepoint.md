---
title: SharePoint의 SQL Server BI 기능을 위한 배포 토폴로지 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 39f76bc7-94e6-4dbc-bfa5-d56f4430bb26
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2ba357fc3910779573ffa36f3070b55c08ced8ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388721"
---
# <a name="deployment-topologies-for-sql-server-bi-features-in-sharepoint"></a>SharePoint의 SQL Server BI 기능에 대한 배포 토폴로지
  이 항목에서는 SharePoint 2010 및 SharePoint 2013 환경에 SQL Server Business Intelligence 기능 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 을 설치하기 위한 일반적인 토폴로지에 대해 설명합니다. 예를 들어 단일 서버와 3계층 설치에 대해 설명합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Sharepoint 2013 &#124; SharePoint 2010|  
  
 **항목 내용**  
  
-   [SharePoint 2013 예제 배포 토폴로지](#bkmk_example_deployments_2013)  
  
    -   [SharePoint 2013용 PowerPivot 및 Reporting Services 세 서버 배포](#bkmk_bi_Sharepoint2013_3tier)  
  
    -   [SharePoint 2013용 PowerPivot 단일 서버 배포](#bkmk_powerpivot_sharepoint2013_1server)  
  
    -   [SharePoint 2013용 PowerPivot 두 서버 배포](#bkmk_powerpivot_sharepoint2013_2server)  
  
    -   [SharePoint 2013용 PowerPivot 세 서버 배포](#bkmk_powerpivot_sharepoint2013_3server)  
  
    -   [SharePoint 2013용 PowerPivot 및 Reporting Services 단일 서버 배포](#bkmk_powerpivot_ssrs_sharepoint2013_1server)  
  
    -   [SharePoint 2013용 PowerPivot 및 Reporting Services 두 서버 배포](#bkmk_powerpivot_ssrs_sharepoint2013_2server)  
  
-   [SharePoint 2010 예제 배포 토폴로지](#bkmk_example_deployments_2010)  
  
    -   [단일 서버 배포](#bkmk_sharepoint2010_1server)  
  
    -   [2계층 배포](#bkmk_sharepoint2010_2server)  
  
    -   [3계층 배포](#bkmk_sharepoint2010_3server)  
  
    -   [3계층 확장 배포](#bkmk_sharepoint2010_scaleserver)  
  
##  <a name="sharepoint-2013-example-deployment-topologies"></a><a name="bkmk_example_deployments_2013"></a>SharePoint 2013 예제 배포 토폴로지  
 SQL Server 설치 옵션 **SharePoint용 PowerPivot** 은 SharePoint에 대한 종속성이 없으며 SharePoint 개체 모델이나 인터페이스를 사용하여 통합을 지원하지 않습니다. 따라서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 Windows Server 2008 R2 이상 버전을 실행하는 컴퓨터에 설치할 수 있습니다. SharePoint 팜에서 애플리케이션 서버가 될 수 있지만, 애플리케이션 서버일 필요는 없습니다. 구성 단계 중 하나는 Excel Services가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 실행하는 서버를 가리키도록 하는 것입니다. 로드 균형 조정 및 내결함성을 위해 SharePoint 모드로 실행되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버를 여러 대 설치하고 등록하는 것이 좋습니다.  
  
 Sharepoint 모드에는 sharepoint server 2013이 필요 하며 sharepoint 서비스 응용 프로그램 아키텍처를 활용 합니다. ** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **  
  
 다음 섹션에서는 일반적인 배포 토폴로지를 보여 줍니다.  
  
###  <a name="powerpivot-for-sharepoint-2013-and-reporting-services-three-server-deployment"></a><a name="bkmk_bi_Sharepoint2013_3tier"></a>SharePoint용 PowerPivot 2013 및 Reporting Services 세 가지 서버 배포  
 다음 세 서버 배포에서 SQL Server 데이터베이스 엔진, SharePoint 모드로 실행되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 및 SharePoint는 각각 별도의 서버에서 실행됩니다. SharePoint 서버에서 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 2013 설치 관리자 패키지(**spPowerPivot.msi**)를 실행해야 합니다.  
  
 ![SSAS 및 SSRS SharePoint 모드 3 서버 배포](../../../2014/sql-server/install/media/as-and-rs-3server-deployment.gif "SSAS 및 SSRS SharePoint 모드 3 서버 배포")  
  
|||  
|-|-|  
|**(1**|Excel Services 애플리케이션. 서비스 애플리케이션은 SharePoint 설치의 일부로 만들어집니다.|  
|**fs**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]서비스 응용 프로그램. 기본 이름은 **기본 PowerPivot 서비스 애플리케이션**입니다.|  
|**3**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 만드는 등 기존 설치를 업데이트하는 개별 절차에 이 항목을 사용할 수도 있습니다.|  
|**3-4**|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 미디어 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능 팩에서 SharePoint용 보고 서비스 추가 기능을 설치합니다.|  
|**5**|**Sppowerpivot .msi** 를 실행 하 여 데이터 공급자, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리 및 데이터 새로 고침 예약을 설치 합니다.|  
|**6**|SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버. Excel Services 애플리케이션 **데이터 모델 설정** 에서 이 서버를 사용하도록 구성합니다.|  
|**일**|SharePoint 콘텐츠, 구성 및 서비스 애플리케이션 데이터베이스입니다.|  
  
 ![SharePoint 설정은](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 설정") Microsoft SQL Server 연결 ()https://connect.microsoft.com/SQLServer/Feedback) [을 통해 사용자 의견 및 연락처 정보를 제출](https://connect.microsoft.com/SQLServer/Feedback) 합니다.  
  
###  <a name="powerpivot-for-sharepoint-2013-single-server-deployment"></a><a name="bkmk_powerpivot_sharepoint2013_1server"></a>SharePoint용 PowerPivot 2013 단일 서버 배포  
 단일 서버 배포는 테스트용으로는 유용하지만 프로덕션 배포에는 권장되지 않습니다.  
  
 다음 다이어그램에서는 단일 서버 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포의 일부인 구성 요소를 보여 줍니다.  
  
 ![SharePoint용 PowerPivot 단일 서버 배포](../../../2014/sql-server/install/media/as-powerpivot-mode-1server-deployment.gif "SharePoint용 PowerPivot 단일 서버 배포")  
  
|||  
|-|-|  
|**(1**|Excel Services 애플리케이션. 서비스 애플리케이션은 SharePoint 설치의 일부로 만들어집니다.|  
|**fs**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]서비스 응용 프로그램. 기본 이름은 **기본 PowerPivot 서비스 애플리케이션**입니다.|  
|**3**|SharePoint 콘텐츠, 구성 및 서비스 애플리케이션 데이터베이스입니다.|  
|**3-4**|SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버. Excel Services 애플리케이션 **데이터 모델 설정** 에서 이 서버를 사용하도록 구성합니다.|  
  
###  <a name="powerpivot-for-sharepoint-2013-two-server-deployment"></a><a name="bkmk_powerpivot_sharepoint2013_2server"></a>SharePoint용 PowerPivot 2013 2 서버 배포  
 다음 두 서버 배포에서 SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 SQL Server 데이터베이스 엔진은 SharePoint가 아니라 별도의 서버에서 실행됩니다. SharePoint 2013용 [!INCLUDE[ssGeminiLongvnext](../../includes/ssgeminilongvnext-md.md)] 설치 관리자 패키지(**spPowerPivot.msi**)가 SharePoint 서버에 설치됩니다.  
  
 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)]는 SharePoint Server 2013를 확장 하 여 서버 쪽 데이터 새로 고침 처리, 데이터 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 공급자, 갤러리, 통합 문서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 및 고급 데이터 모델을 사용 하는 Excel 통합 문서에 대 한 관리 지원을 추가 합니다.  
  
 설치 관리자 패키지는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 기능 팩의 일부로 사용할 수 있습니다. 기능 팩은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 다운로드 센터의 microsoft [® SQL Server® 2014 PowerPivot® For microsoft® SharePoint®](https://go.microsoft.com/fwlink/?LinkID=296473) (HYPERLINK "<https://go.microsoft.com/fwlink/?LinkID=296473>" \t "_blank" <https://go.microsoft.com/fwlink/?LinkID=296473>)에서 다운로드할 수 있습니다.  
  
 ![SSAS PowerPivot 모드 2 서버 배포](../../analysis-services/media/as-powerpivot-mode-2server-deployment.gif "SSAS PowerPivot 모드 2 서버 배포")  
  
|||  
|-|-|  
|**(1**|Excel Services 애플리케이션. 서비스 애플리케이션은 SharePoint 설치의 일부로 만들어집니다.|  
|**fs**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]서비스 응용 프로그램. 기본 이름은 **기본 PowerPivot 서비스 애플리케이션**입니다.|  
|**3**|**spPowerPivot.msi** 를 실행하여 데이터 공급자, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리 및 데이터 새로 고침 예약 기능을 설치합니다.|  
|**3-4**|SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버. Excel Services 애플리케이션 **데이터 모델 설정** 에서 이 서버를 사용하도록 구성합니다.|  
|**5**|SharePoint 콘텐츠, 구성 및 서비스 애플리케이션 데이터베이스입니다.|  
  
###  <a name="powerpivot-for-sharepoint-2013-three-server-deployment"></a><a name="bkmk_powerpivot_sharepoint2013_3server"></a>SharePoint용 PowerPivot 2013 3 서버 배포  
 다음 세 서버 배포에서 SQL Server 데이터베이스 엔진, SharePoint 모드로 실행되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 및 SharePoint는 각각 별도의 서버에서 실행됩니다. SharePoint 서버에 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 설치 관리자 패키지(spPowerPivot.msi)를 설치해야 합니다.  
  
 ![AS PowerPivot 모드 3 서버 배포](../../../2014/sql-server/install/media/as-powerpivot-mode-3server-deployment.gif "AS PowerPivot 모드 3 서버 배포")  
  
|||  
|-|-|  
|**(1**|Excel Services 애플리케이션. 서비스 애플리케이션은 SharePoint 설치의 일부로 만들어집니다.|  
|**fs**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]서비스 응용 프로그램. 기본 이름은 **기본 PowerPivot 서비스 애플리케이션**입니다.|  
|**3**|spPowerPivot.msi를 실행하여 데이터 공급자, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리 및 데이터 새로 고침 예약 기능을 설치합니다.|  
|**3-4**|SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버. Excel Services 애플리케이션 **데이터 모델 설정** 에서 이 서버를 사용하도록 구성합니다.|  
|**5**|SharePoint 콘텐츠, 구성 및 서비스 애플리케이션 데이터베이스입니다.|  
  
###  <a name="powerpivot-for-sharepoint-2013-and-reporting-services-single-server-deployment"></a><a name="bkmk_powerpivot_ssrs_sharepoint2013_1server"></a>SharePoint용 PowerPivot 2013 및 Reporting Services 단일 서버 배포  
 단일 서버 배포는 테스트용으로는 유용하지만 프로덕션 배포에는 권장되지 않습니다.  
  
 ![SSAS 및 SSRS SharePoint 모드 1 서버 배포](../../../2014/sql-server/install/media/as-and-rs-1server-deployment.gif "SSAS 및 SSRS SharePoint 모드 1 서버 배포")  
  
|||  
|-|-|  
|**(1**|Excel Services 애플리케이션. 서비스 애플리케이션은 SharePoint 설치의 일부로 만들어집니다.|  
|**fs**|PowerPivot 서비스 애플리케이션입니다. 기본 이름은 **기본 PowerPivot 서비스 애플리케이션**입니다.|  
|**3**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 만드는 등 기존 설치를 업데이트하는 개별 절차에 이 항목을 사용할 수도 있습니다.|  
|**3-4**|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 미디어 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능 팩에서 SharePoint용 보고 서비스 추가 기능을 설치합니다.|  
|**5**|SharePoint 콘텐츠, 구성 및 서비스 애플리케이션 데이터베이스입니다.|  
|**6**|SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버. Excel Services 애플리케이션 **데이터 모델 설정** 에서 이 서버를 사용하도록 구성합니다.|  
  
###  <a name="powerpivot-for-sharepoint-2013-and-reporting-services-two-server-deployment"></a><a name="bkmk_powerpivot_ssrs_sharepoint2013_2server"></a>SharePoint용 PowerPivot 2013 및 Reporting Services 두 서버 배포  
 다음 두 서버 배포에서 SQL Server 데이터베이스 엔진 및 SharePoint 모드로 실행되는 Analysis Services 서버는 SharePoint와 별도의 서버에서 실행됩니다. SharePoint용 PowerPivot 2013 설치 관리자 패키지 **(spPowerPivot.msi)** 를 SharePoint 서버에서 실행해야 합니다.  
  
 ![SSAS 및 SSRS SharePoint 모드 2 서버 배포](../../../2014/sql-server/install/media/as-and-rs-2server-deployment.gif "SSAS 및 SSRS SharePoint 모드 2 서버 배포")  
  
|||  
|-|-|  
|**(1**|Excel Services 애플리케이션. 서비스 애플리케이션은 SharePoint 설치의 일부로 만들어집니다.|  
|**fs**|PowerPivot 서비스 애플리케이션입니다. 기본 이름은 **기본 PowerPivot 서비스 애플리케이션**입니다.|  
|**3**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 만드는 등 기존 설치를 업데이트하는 개별 절차에 이 항목을 사용할 수도 있습니다.|  
|**3-4**|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 미디어 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능 팩에서 SharePoint용 보고 서비스 추가 기능을 설치합니다.|  
|**5**|**spPowerPivot.msi** 를 실행하여 데이터 공급자, PowerPivot 구성 도구, PowerPivot 갤러리 및 일정 데이터 새로 고침을 설치합니다.|  
|**6**|SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버. Excel Services 애플리케이션 **데이터 모델 설정** 에서 이 서버를 사용하도록 구성합니다.|  
|**일**|SharePoint 콘텐츠, 구성 및 서비스 애플리케이션 데이터베이스입니다.|  
  
##  <a name="sharepoint-2010-example-deployment-topologies"></a><a name="bkmk_example_deployments_2010"></a>SharePoint 2010 예제 배포 토폴로지  
 다음 다이어그램에서는 각 계층에서 실행되는 서비스 및 공급자를 보여 줍니다. 다이어그램에는 여러 기본 제공 서비스가 포함되어 있는데 이러한 서비스는 일부 SQL Server BI 시나리오에서 필요합니다. Excel 서비스, Secure Store Services 및 Windows 토큰 서비스에 대한 클레임은 PowerPivot for SharePoint 또는 SharePoint의 Reporting Services 배포를 위해 필요하거나 권장됩니다. 또한 일부 PowerPivot 데이터 액세스 시나리오의 경우 MSOLAP OLE DB 공급자 및 ADO.NET 서비스가 필요합니다. 선택적으로, SharePoint 외부에서 호스팅되는 테이블 형식 모델 데이터베이스를 기준으로 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 보고서를 작성하려는 경우 Analysis Services를 데이터 계층에 설치할 수 있습니다.  
  
 ![논리 아키텍처 다이어그램](../../../2014/sql-server/install/media/sql11bisetup.gif "논리 아키텍처 다이어그램")  
  
##  <a name="single-server-deployments"></a><a name="bkmk_sharepoint2010_1server"></a>단일 서버 배포  
 데이터 계층을 포함하여 모든 서버 구성 요소를 단일 컴퓨터에 설치할 수 있습니다. 이 배포 구성은 SharePoint 모드에서 Reporting Services를 포함하는 사용자 지정 애플리케이션을 개발하거나 소프트웨어를 평가하는 경우 유용합니다. 이 배포는 구성이 가장 간단합니다. 모든 구성 요소가 같은 컴퓨터에 설치되므로 사용하는 라이선스도 가장 적습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 사용이 허가된 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 설치됩니다.  
  
 단일 서버에 모든 기능을 설치하기 위해 동일한 물리적 서버에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 를 순서대로 설치합니다. 독립 실행형 서버 구성에 대 한 지침은 [배포 검사 목록: Reporting Services, 파워 뷰 및 SharePoint용 PowerPivot](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)를 참조 하세요.  
  
##  <a name="two-tier-deployment"></a><a name="bkmk_sharepoint2010_2server"></a>2 계층 배포  
 2계층 배포는 일반적으로 특정 컴퓨터에 SharePoint Server 2010을 배포하고 두 번째 컴퓨터에 SQL Server 데이터베이스 엔진을 배포하는 것입니다. 데이터 계층을 전용 서버로 이동하는 것이 2개 컴퓨터 팜에 대한 가장 일반적인 구성입니다. 2계층 팜에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 를 모두 SharePoint 서버에 설치합니다. 프런트 엔드의 모든 웹 서비스와 애플리케이션 계층의 공유 서비스를 동일한 물리적 서버에서 실행합니다. 2계층 배포의 설치 단계는 독립 실행형 배포와 매우 유사하며 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 를 동일한 물리적 서버에 순서대로 설치합니다.  
  
##  <a name="three-tier-deployment"></a><a name="bkmk_sharepoint2010_3server"></a>3 계층 배포  
 3계층 배포는 일반적으로 웹 프런트 엔드 서비스를 처리 또는 메모리 집중 애플리케이션과 구분합니다. 이 토폴로지의 경우 애플리케이션 서버에만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 를 설치합니다. 웹 프런트 엔드에서 실행되는 웹 서비스는 서버 구성 동안 팜에서 애플리케이션에 배포되는 솔루션을 통해 사후 설치 태스크로 설치됩니다. 다음 다이어그램에서는 3계층 배포를 보여 줍니다.  
  
 ![3 서버 토폴로지](../../../2014/sql-server/install/media/sql11bisetup-3server.gif "3 서버 토폴로지")  
  
##  <a name="three-tier-scale-out-deployment"></a><a name="bkmk_sharepoint2010_scaleserver"></a>3 계층 스케일 아웃 배포  
 이 토폴로지에서는 여러 서버에서 동일한 공유 서비스를 실행하는 스케일 아웃 배포에 대해 설명하며, 대용량 요청을 처리하고 PowerPivot 데이터 또는 Reporting Services 보고서를 위한 뛰어난 처리 성능을 제공합니다. 아래 다이어그램에는 세 개의 애플리케이션 서버 클러스터가 있으며 각 클러스터마다 다른 공유 서비스 조합을 실행합니다. SharePoint 환경에서, 서비스 검색 및 가용성이 팜에 내장됩니다. 동일한 공유 서비스 애플리케이션을 실행하는 여러 물리적 서버에 걸쳐 부하 분산은 공유 서비스 아키텍처의 일부입니다.  
  
 여러 서버 팜을 배포하는 경우 다음 SharePoint 문서의 지침을 준수해야 합니다. [3계층 팜을 위한 다중 서버(SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834)  
  
 ![5-서버 토폴로지](../../../2014/sql-server/install/media/sql11bisetup-5server.gif "5-서버 토폴로지")  
  
## <a name="see-also"></a>참고 항목  
 [Sharepoint 2010 및 sharepoint 2013 &#40;SharePoint 모드 설치 Reporting Services&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [SharePoint용 PowerPivot 2013 설치](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)   
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
