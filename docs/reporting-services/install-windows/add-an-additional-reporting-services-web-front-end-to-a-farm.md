---
title: 팜에 추가 Reporting Services 웹 프런트 엔드 추가 | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: d7a11bda-ae26-49ac-b071-37d83cae5afe
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 603407cd0642a8fb3bb66826d89300ea0d8c7e0d
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050935"
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>팜에 추가 Reporting Services 웹 프런트 엔드 추가
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드에는 응용 프로그램 서버와 WFE(웹 프런트 엔드) 서버에 필요한 구성 요소가 포함됩니다. 이 항목은 구독, 데이터 경고 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 같은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능에서 사용하는 응용 프로그램 페이지를 포함하여 WFE 서버에 필요한 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]구성 요소 설치에 대해 설명합니다. WFE에 필요한 기본 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치는 SharePoint 2016 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치하는 것입니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
-   SQL Server 설치 프로그램을 실행하려면 로컬 관리자여야 합니다.  
  
-   컴퓨터가 도메인에 조인되어 있어야 합니다.  
  
-   SharePoint 구성과 콘텐츠 데이터베이스를 호스팅하는 기존 데이터베이스 서버의 이름을 알고 있어야 합니다.  
  
-   원격 데이터베이스 연결을 허용하도록 데이터베이스 서버를 구성해야 합니다.  이렇게 하지 않으면 새 서버는 SharePoint 구성 데이터베이스에 연결할 수 없기 때문에 새 서버를 팜에 조인할 수 없습니다.  
  
-   현재 팜 서버에서 실행하고 있는 것과 같은 버전의 SharePoint가 새 서버에 설치되어 있어야 합니다. 예를 들어 팜에 이미 SharePoint 2013 SP1(서비스 팩 1)이 설치된 경우 팜을 조인하려면 새 서버에도 SP1을 설치해야 합니다.  
  
## <a name="steps"></a>단계  
 이 항목의 단계에서는 SharePoint 팜 관리자가 서버를 설치하고 구성한다고 가정합니다. 다이어그램은 일반적인 3계층 환경을 보여주고 다이어그램의 번호가 매겨진 항목이 다음 목록에 설명됩니다.  
  
-   (1) 여러 WFE(웹 프런트 엔드) 서버. WFE 서버에는 SharePoint 2010용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능이 필요합니다. 다음 단계에서는 두 번째 응용 프로그램 서버를 이 계층에 추가합니다.  
  
-   (2) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 실행하는 두 응용 프로그램 서버 및 중앙 관리 같은 웹 사이트.  
  
-   (3) 두 SQL Server 데이터베이스 서버.  
  
-   (4) 소프트웨어 또는 하드웨어 네트워크 부하 분산 솔루션(NLB)을 나타냅니다.  
  
 ![새 SharePoint WFE에 SSRS 추가](../../reporting-services/install-windows/media/rs-sharepointscale-wfe.gif "새 SharePoint WFE에 SSRS 추가")  
  
 다음 단계에서는 관리자가 서버를 설치하고 구성한다고 가정합니다.  
  
|단계|설명 및 링크|  
|----------|--------------------------|  
|SharePoint 서버를 팜에 추가합니다.|다른 Reporting Services 응용 프로그램을 배포하려면 SharePoint를 설치해야 합니다.<br/><br/>SharePoint 2013의 경우 [SharePoint Server 2013에서 팜에 SharePoint 서버 추가](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)를 참조하세요.<br/><br/>SharePoint 2016의 경우 [SharePoint Server 2016에서 팜에 SharePoint 서버 추가](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)를 참조하세요.|  
|SharePoint 2016 제품용 SQL Server Reporting Services 추가 기능을 설치합니다.|추가 기능을 설치하는 방법은 여러 가지가 있습니다. 다음 단계는 SQL Server 설치 마법사를 사용합니다. 추가 기능 설치에 대한 자세한 내용은 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)를 참조하세요.<br /><br /> 1) SQL Server 설치를 실행합니다.<br /><br /> 2) **설치 역할** 페이지에서 **SQL Server 기능 설치**를 선택합니다.<br /><br /> 3) **기능 선택** 페이지에서 **SharePoint 제품용 Reporting Services 추가 기능**을 선택합니다.<br /><br /> 4) 다음 여러 페이지에서 **다음** 을 클릭하여 설치 옵션을 완료합니다.<br /><br/>[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치에 대한 자세한 내용은 [SharePoint 모드에서 첫 번째 보고서 서버 설치](install-the-first-report-server-in-sharepoint-mode.md)를 참조하세요.|  
|새 서버가 작동하는지 확인합니다.|1) SharePoint 중앙 관리의 **시스템 설정** 그룹에서 **이 팜의 서버 관리** 를 클릭합니다.<br /><br /> 2) 새 서버가 목록에 있는지 확인합니다.|  
|NLB 솔루션을 업데이트합니다.|해당하는 경우 새 서버를 포함하도록 하드웨어 또는 소프트웨어 NLB 환경을 업데이트합니다.|  

## <a name="next-steps"></a>다음 단계

[SharePoint Server 2016에서 팜에 SharePoint 서버 추가](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)  
[SharePoint Server 2013에서 팜에 SharePoint 서버 추가](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
