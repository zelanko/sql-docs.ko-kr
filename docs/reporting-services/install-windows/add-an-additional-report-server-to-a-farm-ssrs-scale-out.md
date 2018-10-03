---
title: 팜에 추가 보고서 서버 추가(SSRS 확장) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b5e42465bd2a0c4661709dd1a17a2b7de8c6b3a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830841"
---
# <a name="add-an-additional-report-server-to-a-farm-ssrs-scale-out"></a>팜에 추가 보고서 서버 추가(SSRS 확장)

  SharePoint 팜에 두 번째 이상의 SharePoint 모드 보고서 서버를 추가하면 보고서 서버 처리 성능 및 응답 시간을 향상시킬 수 있습니다. 보고서 서버에 더 많은 사용자, 보고서 및 기타 응용 프로그램을 추가할수록 성능이 저하되는 경우에는 보고서 서버를 추가하면 성능을 향상시킬 수 있습니다. 또한 하드웨어에 문제가 있거나 사용자 환경의 개별 서버에 대한 전반적인 관리를 수행하는 경우 보고서 서버의 가용성을 늘리기 위해 두 번째 보고서 서버를 추가하는 것이 좋습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 릴리스부터는 SharePoint 모드에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 환경을 확장하는 단계는 표준 SharePoint 팜 배포를 따르며 SharePoint 부하 분산 기능을 이용합니다.  
  
> [!IMPORTANT]  
>  일부 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 버전에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]확장이 지원되지 않습니다. 자세한 내용은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SQL Server 2016 버전에서 지원하는 기능 [의](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)섹션을 참조하세요.  
  
> [!TIP]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터는 서버를 추가하고 보고서 서버를 확장하는 데 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하지 않습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스가 포함된 SharePoint 서버가 팜에 추가되어 SharePoint 제품에서 보고서 서비스의 확장을 관리합니다.  
  
 기본 모드 보고서 서버를 확장하는 방법은 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)을 참조하세요.  
  
##  <a name="bkmk_loadbalancing"></a> 부하 분산  
 사용자 환경에 사용자 지정 또는 타사 부하 분산 솔루션이 없는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램의 부하 분산은 SharePoint에서 자동으로 관리됩니다. 기본 SharePoint 부하 분산 동작은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 시작한 모든 응용 프로그램 서버에서 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램의 부하를 분산하는 것입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스가 설치되고 시작되었는지 확인하려면 SharePoint 중앙 관리에서 **서버의 서비스 관리** 를 클릭합니다.  
  
##  <a name="bkmk_prerequisites"></a> 필수 구성 요소  
  
-   SQL Server 설치 프로그램을 실행하려면 로컬 관리자여야 합니다.  
  
-   컴퓨터가 도메인에 조인되어 있어야 합니다.  
  
-   SharePoint 구성과 콘텐츠 데이터베이스를 호스팅하는 기존 데이터베이스 서버의 이름을 알고 있어야 합니다.  
  
-   원격 데이터베이스 연결을 허용하도록 데이터베이스 서버를 구성해야 합니다.  이렇게 하지 않으면 새 서버는 SharePoint 구성 데이터베이스에 연결할 수 없기 때문에 새 서버를 팜에 조인할 수 없습니다.  
  
-   현재 팜 서버에서 실행하고 있는 것과 같은 버전의 SharePoint가 새 서버에 설치되어 있어야 합니다. 예를 들어 팜에 이미 SharePoint 2013 SP1(서비스 팩 1)이 설치된 경우 팜을 조인하려면 새 서버에도 SP1을 설치해야 합니다.  
  
##  <a name="bkmk_steps"></a> 단계  
 이 항목의 단계에서는 SharePoint 팜 관리자가 서버를 설치하고 구성한다고 가정합니다. 다이어그램은 일반적인 3계층 환경을 보여주고 다이어그램의 번호가 매겨진 항목이 다음 목록에 설명됩니다.  
  
-   (1) 여러 WFE(웹 프런트 엔드) 서버. WFE 서버에는 SharePoint 2016용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능이 필요합니다.  
  
-   (2) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 실행하는 단일 응용 프로그램 서버 및 중앙 관리 같은 웹 사이트. 다음 단계에서는 두 번째 응용 프로그램 서버를 이 계층에 추가합니다.  
  
-   (3) 두 SQL Server 데이터베이스 서버.  
  
-   (4) 소프트웨어 또는 하드웨어 네트워크 부하 분산 솔루션(NLB)을 나타냅니다.  
  
 ![Reporting Services 응용 프로그램 서버 추가](../../reporting-services/install-windows/media/rs-sharepointscale.gif "Reporting Services 응용 프로그램 서버 추가")  
  
 다음 단계에서는 관리자가 서버를 설치하고 구성한다고 가정합니다. 서버는 팜에 새 응용 프로그램 서버로 설치되고 WFE(웹 프런트 엔드)로 사용되지 않습니다.  
  
|단계|설명 및 링크|  
|----------|--------------------------|  
|SharePoint 서버를 팜에 추가합니다.|다른 Reporting Services 응용 프로그램을 배포하려면 SharePoint를 설치해야 합니다.<br/><br/>SharePoint 2013의 경우 [SharePoint Server 2013에서 팜에 SharePoint 서버 추가](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)를 참조하세요.<br/><br/>SharePoint 2016의 경우 [SharePoint Server 2016에서 팜에 SharePoint 서버 추가](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)를 참조하세요.|  
|Reporting Services SharePoint 모드 설치 및 구성|SQL Server 설치를 실행합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 설치에 대한 자세한 내용은 [SharePoint 모드에서 첫 번째 보고서 서버 설치](install-the-first-report-server-in-sharepoint-mode.md)를 참조하세요.<br /><br /> 서버가 응용 프로그램 서버로만 사용되고 WFE로 사용되지 않을 경우 **SharePoint 제품용 Reporting Services 추가 기능**을 선택할 필요가 없습니다.<br /><br /> 1) **설치 역할** 페이지에서 **SQL Server 기능 설치**를 선택합니다.<br /><br /> 2) **기능 선택** 페이지에서 **Reporting Services - SharePoint**를 선택합니다.<br /><br /> 3) **Reporting Services 구성**  페이지에서 **Reporting Services SharePoint 모드** 에 대해 **설치만**옵션이 선택되었는지 확인합니다.|  
|Reporting Services가 작동하는지 확인|1) SharePoint 중앙 관리의 **시스템 설정** 그룹에서 **이 팜의 서버 관리** 를 클릭합니다.<br /><br /> 2) **SQL Server Reporting Services 서비스**를 확인합니다.<br /><br />자세한 내용은 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)를 참조하세요.|  
  
##  <a name="bkmk_additional"></a> 기타 고려 사항  
 확장된 배포에서 백그라운드 처리만 수행하도록 개별 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버를 최적화하여 대화형 보고서 실행과 리소스를 두고 경합하지 않도록 할 수 있습니다. 백그라운드 처리에는 일정, 구독 및 데이터 경고가 포함됩니다.  
  
 개별 보고서 서버의 동작을 변경하려면 **RSreportServer.config** 구성 파일에서 **\<IsWebServiceEnable>** 을 false로 설정합니다.  
  
 기본적으로 \<IsWebServiceEnable>을 TRUE로 설정하여 보고서 서버가 구성됩니다. 모든 서버가 TRUE로 구성된 경우 팜의 모든 노드에서 대화형 및 백그라운드의 로드 균형이 조정됩니다.  
  
 \<IsWebServiceEnable>을 False로 설정하여 모든 보고서 서버를 구성하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 사용하려고 시도할 때 다음과 같은 오류 메시지가 나타납니다.  
  
      The Reporting Services Web Service is not enabled. Configure at least one instance of the Reporting Services SharePoint Service to have <IsWebServiceEnable> set to true. 
 
 자세한 내용은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)을 참조하세요.  

## <a name="next-steps"></a>다음 단계

[SharePoint Server 2016에서 팜에 SharePoint 서버 추가](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)  
[SharePoint Server 2013에서 팜에 SharePoint 서버 추가](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
