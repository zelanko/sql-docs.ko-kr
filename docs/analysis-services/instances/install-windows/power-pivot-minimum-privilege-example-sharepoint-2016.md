---
title: Power Pivot 최소 권한 예제-SharePoint 2016 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eac736994b104ffbce855fa1ad6761d592fccad1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209477"
---
# <a name="power-pivot-minimum-privilege-example---sharepoint-2016"></a>Power Pivot 최소 권한 예제-SharePoint 2016
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  이 항목에서는 최소 권한을 사용하는 SharePoint 2016용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 예제에 대해 설명합니다. 이 구성은 세 가지 구성 요소 각각에 대해 다른 계정을 사용하며 계정마다 취소 수준의 권한이 있습니다.  
  
## <a name="summary-of-accounts"></a>계정 요약  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 다음의 SharePoint 2016용에서는 Analysis Services 서비스 계정에 네트워크 서비스 계정을 사용할 수 있습니다.: 네트워크 서비스 계정은 SharePoint 2010에서 지원하는 시나리오가 아닙니다. 서비스 계정에 대 한 자세한 내용은 참조 하세요. [Windows 서비스 계정 및 권한 구성](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) (http://msdn.microsoft.com/library/ms143504.aspx) 합니다.  
  
 다음 표에는 최소 권한 구성에 대한 이 예에서 사용된 세 계정이 요약되어 있습니다.  
  
|범위|속성|  
|-----------|----------|  
|SharePoint 관리자 계정|**SPAdmin**|  
|SharePoint 팜 계정|**SPFarm**|  
|Analysis Services 서비스 계정|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>SharePoint 관리자 계정(SpAdmin)  
 **SPAdmin** 은 팜을 설치하고 구성하는 데 사용하는 도메인 계정입니다. SharePoint 구성 마법사 및 SharePoint 2016용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구를 실행하는 데 사용되는 계정입니다. 로컬 관리자 권한이 필요한 계정은 **SPAdmin** 계정뿐입니다. [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구를 실행하기 전에 SharePoint에서 콘텐츠 및 구성 데이터베이스를 만드는 SQL Server 데이터베이스 인스턴스에 **SPAdmin** 계정 권한을 부여합니다. 최소 권한 시나리오에서 SPAdmin 계정을 구성하려면 해당 계정이 **securityadmin** 및 **dbcreator**역할의 구성원이어야 합니다.  
  
### <a name="the-farm-account-spfarm"></a>팜 계정(SPFarm)  
 **SPFarm** 은 SharePoint Timer Service 및 중앙 관리용 웹 응용 프로그램에서 SharePoint 콘텐츠 데이터베이스에 액세스할 때 사용하는 도메인 계정입니다. 이 계정은 로컬 관리자가 아니어도 됩니다. SharePoint 구성 마법사는 백 엔드 SQL Server 데이터베이스에 적절한 최소 권한을 부여합니다. 최소 SQL Server 권한 구성은 **securityadmin** 및 **dbcreator**역할의 멤버 자격입니다.  
  
### <a name="the-service-account-for-power-pivot-service-spsvc"></a>파워 피벗 서비스(SPsvc)용 서비스 계정  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구를 실행하기 전에 새 SharePoint 팜을 구성하지 않으면 기본적으로 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구에 의해 다음 응용 프로그램이 만들어집니다.  
  
-   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 서비스 응용 프로그램  
  
-   보안 저장소 애플리케이션  
  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구는 두 개의 서비스 응용 프로그램을 모두 기본 응용 프로그램 풀에서 구성합니다. 해당 애플리케이션 풀은 일반적으로 SPFarm 계정으로 실행되도록 구성됩니다. 이 계정은 서비스 계정에 필요 없는 많은 리소스에 액세스할 수 있습니다. 최소 권한이 지정된 환경을 만들려면 해당 애플리케이션 풀 및 웹 애플리케이션에서 사용할 새 도메인 계정을 구성합니다.  
  
 **SharePoint 서비스 계정으로 사용할 새 도메인 계정을 만들려면**  
  
1.  SharePoint 중앙 관리에서 **보안**을 선택합니다.  
  
2.  **서비스 계정 구성**을 선택합니다.  
  
3.  **새 관리되는 계정을 등록하세요.** 를 선택합니다.  
  
 **SPSvc** 계정에 로컬 관리자 권한이 없으며, Spsvc에는 SharePoint 데이터베이스에 대한 권한이 없습니다. SPsvc에 필요한 권한은 Analysis Services의 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 인스턴스에 대한 관리 권한뿐입니다.  
  
 **SPsvc 계정을 사용할 적절한 응용 프로그램 풀을 구성하려면**  
  
1.  SharePoint 중앙 관리에서 **보안**을 선택합니다.  
  
2.  **서비스 계정 구성**을 선택합니다.  
  
3.  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 서비스 응용 프로그램에서 사용하는 서비스 응용 프로그램 풀을 선택합니다. SPSvc 계정을 선택합니다.  
  
 **PowerShell로 웹 응용 프로그램에 대한 액세스 권한을 부여하려면**  
  
1.  관리자 권한으로 SharePoint 2016 관리 셸을 실행합니다.  
  
2.  다음 PowerShell 코드를 실행합니다.  
  
    ```  
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")  
  
    ```  
  
  
