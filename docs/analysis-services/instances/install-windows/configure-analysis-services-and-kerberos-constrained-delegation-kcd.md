---
title: "분석 구성 서비스 및 Kerberos 제한 위임 (KCD) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0006e143-d3ba-4d10-a415-e42c45e2bb0a
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ae2cafe597e5540a58cc89e28cee87516942d021
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="configure-analysis-services-and-kerberos-constrained-delegation-kcd"></a>Analysis Services 및 KCD(Kerberos 제한 위임) 구성
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Kerberos 제한 위임 KCD ()는 Windows 인증에서 클라이언트 자격 증명을 위임할 구성할 수는 인증 프로토콜 환경 전체에서 서비스에는 서비스입니다. KCD에는 추가 인프라(예: 도메인 컨트롤러) 및 사용자 환경의 추가 구성이 필요합니다. KCD는 SharePoint 2016에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 데이터와 관련된 일부 시나리오의 요구 사항입니다. SharePoint 2016에서는 Excel Services가 SharePoint 팜에서 별도의 새로운 서버인 **Office Online Server**로 이동되었습니다. Office Online Server는 별도의 서버이므로 두 가지 홉 시나리오에서 클라이언트 자격 증명을 위임할 방법이 필요합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016|  
  
## <a name="overview"></a>개요  
 KCD를 사용하면 리소스에 대한 액세스를 제공하기 위한 목적으로 하나의 계정이 다른 계정을 가장할 수 있습니다. 가장하는 계정은 웹 응용 프로그램에 할당된 서비스 계정 또는 웹 서버의 컴퓨터 계정이고, 가장된 계정은 리소스에 대한 액세스가 필요한 사용자 계정입니다. KCD는 서비스 수준에서 작동하므로 서버의 선택된 서비스에는 가장하는 계정에 의해 액세스 권한이 부여될 수 있지만 동일한 서버의 다른 서비스 또는 다른 서버의 서비스는 액세스가 거부됩니다.  
  
 이 항목의 섹션에서는 KCD가 필요한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 과 관련된 일반적인 시나리오와 예제 서버 배포를 검토하며, 설치 및 구성하는 데 필요한 항목에 대한 개략적인 요약을 제공합니다. 도메인 컨트롤러 및 KCD와 관련된 기술에 대한 자세한 정보를 제공하는 링크는 [추가 정보 및 커뮤니티 콘텐츠](#bkmk_moreinfo) 섹션을 참조하세요.  
  
## <a name="scenario-1-workbook-as-data-source-wds"></a>시나리오 1: WDS(데이터 소스로서의 통합 문서)  
 ![1 참조](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "1 참조") Office Online Server는 Excel 통합 문서를 열고 및 ![2 참조](../../../analysis-services/instances/install-windows/media/ssas-callout2.png "2 참조") 다른 통합 문서에 대 한 데이터 연결을 검색 합니다. Office Online Server는 요청을 보냅니다는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 리디렉터 서비스 ![3 참조](../../../analysis-services/instances/install-windows/media/ssas-callout3.png "3 참조") 두 번째 통합 문서 및 데이터를 열려면 ![4 참조](../../../analysis-services/instances/install-windows/media/ssas-callout4.png "4 참조 ").  
  
 이 시나리오에서는 Office Online Server에서 SharePoint의 SharePoint [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 리디렉터 서비스로 사용자 자격 증명을 위임해야 합니다.  
  
 ![데이터 원본으로 통합 문서](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-wds.png "데이터 원본으로 통합 문서")  
  
## <a name="scenario-2-an-analysis-services-tabular-model-links-to-an-excel-workbook"></a>시나리오 2: Excel 통합 문서에 Analysis Services 테이블 형식 모델 연결  
 Analysis Services 테이블 형식 모델 ![1 참조](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "1 참조") 파워 피벗 모델을 포함 하는 Excel 통합 문서에 연결 합니다. 이 시나리오에서는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에서 테이블 형식 모델을 로드할 때 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에서 통합 문서에 대한 링크를 검색합니다. 모델을 처리할 때 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는 SharePoint에 통합 문서를 로드하는 쿼리 요청을 보냅니다. 이 시나리오에서는 Analysis Services에서 SharePoint로 클라이언트 자격 증명을 위임할 필요가 **없지만** 클라이언트 응용 프로그램이 확장 바인딩에서 데이터 소스 정보를 덮어쓸 수 있습니다. 확장 바인딩 요청이 현재 사용자를 가장하도록 지정하는 경우에는 사용자 자격 증명을 위임해야 하며, 이를 위해 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 와 SharePoint 간에 KCD를 구성해야 합니다.  
  
 ![office online server](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-oos.png "office online server")  
  
## <a name="example-deployment-of-kcd-with-office-online-server-and-analysis-services"></a>Office Online Server와 Analysis Services 간의 KCD 배포 예제  
 이 섹션에서는 4대의 컴퓨터를 사용하는 예제 배포를 설명합니다. 다음 섹션에는 각 컴퓨터에 대한 주요 설치 및 구성 단계가 요약되어 있습니다. 배포를 시작하기 전에 컴퓨터에 최신 운영 체제 패치를 적용하고 컴퓨터 이름을 확인하는 것이 좋습니다. 컴퓨터 이름은 일부 구성 단계에 필요하기 때문입니다.  
  
-   도메인 컨트롤러  
  
-   SQL Server 데이터베이스 엔진 및 PowerPivot 모드의 Analysis Services. 데이터베이스 엔진 인스턴스는 SharePoint 콘텐츠 데이터베이스에 사용됩니다.  
  
-   SharePoint Server 2016  
  
-   Office Online Server  
  
 ![domain controller](../../../analysis-services/instances/install-windows/media/ssas-kcd-domainserver-icon.png "domain controller")  
  
### <a name="domain-controller"></a>도메인 컨트롤러  
 다음은 DC(도메인 컨트롤러)에 대해 설치할 항목에 대한 요약입니다.  
  
-   **역할:** Active Directory 도메인 서비스. 개요는 [Windows Server 2012에서 Active Directory(AD DS) 구성](http://sharepointgeorge.com/2012/configuring-active-directory-ad-ds-in-windows-server-2012/)을 참조하세요.  
  
-   **역할:** DNS 서버  
  
-   **기능:** .NET Framework 3.5 기능/.NET Framework 3.5  
  
-   **기능:** 원격 서버 관리 도구/역할 관리 도구  
  
-   새 포리스트를 만들고 도메인에 컴퓨터를 가입하도록 Active Directory를 구성합니다. 다른 컴퓨터를 개인 도메인에 추가하기 전에 클라이언트 컴퓨터 DNS를 DC의 IP 주소로 구성해야 합니다. DC 컴퓨터에서 `ipconfig /all` 을 실행하여 다음 단계를 위해 IPv4 및 IPv6 주소를 가져옵니다.  
  
-   IPv4 및 IPv6 주소를 둘 다 구성하는 것이 좋습니다. Windows 제어판에서 이 작업을 수행할 수 있습니다.  
  
    1.  **네트워크 및 공유 센터**를 클릭합니다.  
  
    2.  이더넷 연결을 클릭합니다.  
  
    3.  **속성**을 클릭합니다.  
  
    4.  **인터넷 프로토콜 버전 6(TCP/IPv6)**을 클릭합니다.  
  
    5.  **속성**을 클릭합니다.  
  
    6.  **다음 DNS 서버 주소 사용**을 클릭합니다.  
  
    7.  Ipconfig 명령에서 IP 주소를 입력합니다.  
  
    8.  **고급** 단추를 클릭한 다음 **DNS** 탭을 클릭하고 DNS 접미사가 올바른지 확인합니다.  
  
    9. **다음 DNS 접미사 추가**를 클릭합니다.  
  
    10. IPv4에 대해 단계를 반복합니다.  
  
-   **참고:** Windows 제어판의 시스템 설정에서 컴퓨터를 도메인에 가입할 수 있습니다. 자세한 내용은 [Windows Server 2012를 도메인에 가입하는 방법](http://social.technet.microsoft.com/wiki/contents/articles/20260.how-to-join-windows-server-2012-to-a-domain.aspx)을 참조하세요.  
  
 ![powerpivot 모드의 ssas 서버](../../../analysis-services/instances/install-windows/media/ssas-kcd-powerpivotserver-icon.png "powerpivot 모드의 ssas 서버")  
  
### <a name="2016-sql-server-database-engine-and-analysis-services-in-power-pivot-mode"></a>2016 SQL Server 데이터베이스 엔진 및 PowerPivot 모드의 Analysis Services  
 다음은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 컴퓨터에 설치할 항목에 대한 요약입니다.  
  
 ![참고](../../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "참고") 에 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 설치 마법사 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 파워 피벗 모드 기능 선택 워크플로의 일부로 설치 됩니다.  
  
1.  기능 선택 페이지에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 설치 마법사를 실행하고 데이터베이스 엔진, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]및 관리 도구를 클릭합니다. 설치 마법사의 이후 설정에서 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 에 대해 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]모드를 지정할 수 있습니다.  
  
2.  인스턴스 구성의 경우 "POWERPIVOT"의 명명된 된 인스턴스를 구성합니다.  
  
3.  Analysis Services 구성 페이지에서 **파워 피벗** 모드에 대해 Analysis Services 서버를 구성하고 Office Online Server의 **컴퓨터 이름** 을 Analysis Services 서버 관리자 목록에 추가합니다. 자세한 내용은 [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)를 참조하세요.  
  
4.  기본적으로 "컴퓨터" 개체 유형은 검색에 포함되지 않습니다. 클릭 ![개체 컴퓨터 계정을 추가 하려면 클릭](../../../analysis-services/instances/install-windows/media/ss-objects-button.png "추가할 컴퓨터 계정 개체를 클릭 하 여") 컴퓨터 개체를 추가 합니다.  
  
     ![ssas 관리자로 컴퓨터 계정 추가](../../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "ssas 관리자로 컴퓨터 계정 추가")  
  
5.  Analysis Services 인스턴스에 대한 SPN(서비스 사용자 이름)을 만듭니다.  
  
     유용한 SPN 명령은 다음과 같습니다.  
  
    -   관심 서비스를 실행하는 특정 계정 이름에 대한 SPN 나열: `SetSPN -l <account-name>`  
  
    -   관심 서비스를 실행하는 계정 이름에 대한 SPN 설정: `SetSPN -a <SPN> <account-name>`  
  
    -   관심 서비스를 실행하는 특정 계정 이름에 대한 SPN 삭제: `SetSPN -D <SPN> <account-name>`  
  
    -   중복된 SPN 검색: `SetSPN -X`  
  
     PowerPivot 인스턴스에 대한 SPN의 형식은 다음과 같습니다.  
  
    ```  
    MSSQLSvc.3/\<Fully Qualified Domain Name (FQDN)>:POWERPIVOT  
    MSSQLSvc.3/<NetBIOS Name>:POWERPIVOT  
    ```  
  
     여기서 FQDN 및 NetBIOS 이름은 인스턴스가 있는 컴퓨터의 이름입니다. 이러한 SPN은 서비스 계정에 사용되는 도메인 계정에 배치됩니다.  네트워크 서비스, 로컬 시스템 또는 서비스 ID를 사용하는 경우 도메인 컴퓨터 계정에 SPN을 배치할 수 있습니다.  도메인 사용자 계정을 사용하는 경우 해당 계정에 SPN을 배치합니다.  
  
6.  Analysis Services 컴퓨터에 SQL Browser 서비스에 대한 SPN을 만듭니다.  
  
     [자세히 알아보기](https://support.microsoft.com/en-us/kb/950599)  
  
7.  외부 소스에 대한 Analysis Services 서비스 계정의**제한된 위임 구성** 설정은 SQL Server 또는 Excel 파일 등에서 새로 고쳐집니다. Analysis Services 서비스 계정에 대해 다음이 설정되어 있는지 확인할 수 있습니다.  
  
     **참고:** Active Directory 사용자 및 컴퓨터 내에 계정에 대한 위임 탭이 표시되지 않는 경우 이는 해당 계정에 SPN이 없기 때문입니다.  가짜 SPN을 추가하여 `my/spn`과 같이 표시되도록 할 수 있습니다.  
  
     **지정한 서비스에 대한 위임용으로만 이 사용자 트러스트** 및 **모든 인증 프로토콜 사용**  
  
     이를 제한된 위임이라고 하며, Windows 토큰이 프로토콜 전환에 제한된 위임이 필요한 C2WTS(Claims to Windows Token Services)에서 시작되기 때문에 필요합니다.  
  
     ![Analysis Services-제한 된 위임](../../../analysis-services/instances/install-windows/media/analysis-services-constrained-delegation.png "Analysis Services-제한 된 위임")  
  
     또한 위임할 서비스를 추가해야 합니다. 이는 사용자 환경에 따라 다릅니다.  
  
### <a name="office-online-server"></a>Office Online Server  
  
1.  Office Online Server를 설치합니다.  
  
2.  **서버에 연결하도록** Office Online Server를 구성 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 합니다. Office Online Server 컴퓨터 계정은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버의 관리자여야 합니다. 이는 이 항목의 이전 섹션인 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버 설치 섹션에서 완료되었습니다.  
  
    1.  Office Online Server에서 관리자 권한으로 PowerShell 창을 열고 다음 명령을 실행합니다.  
  
    2.  `New-OfficeWebAppsExcelBIServer –ServerId <AS instance name>`  
  
    3.  예제: `New-OfficeWebAppsExcelBIServer –ServerId "MTGQLSERVER-13\POWERPIVOT"`  
  
3.  Office Online Server 컴퓨터 계정이 사용자를 SharePoint 서비스 계정으로 가장하는 것을 허용하도록**Active Directory를 구성** 합니다. 따라서 Office Online Server에서 SharePoint Web Services용 응용 프로그램 풀을 실행하는 보안 주체에 대한 위임 속성을 설정합니다. 이 섹션의 PowerShell 명령에는 AD(Active Directory) PowerShell 개체가 필요합니다.  
  
    1.  Office Online Server의 Active Directory ID 가져오기  
  
        ```  
        $computer1 = Get-ADComputer -Identity [ComputerName]  
        ```  
  
         작업 관리자/세부 정보/w3wp.exe의 사용자 이름에서 이 보안 주체(예: “svcSharePoint”)를 찾을 수 있습니다.  
  
        ```  
        Set-ADUser svcSharePoint -PrincipalsAllowedToDelegateToAccount $computer1  
  
        ```  
  
    2.  속성이 올바르게 설정되었는지 확인하려면  
  
    3.  ```  
        Get-ADUser svcSharePoint –Properties PrincipalsAllowedToDelegateToAccount  
        ```  
  
4.  Office Online Server 계정에서 Analysis Services 파워 피벗 인스턴스로**제한된 위임 설정을 구성** 합니다. 이는 Office Online Server가 실행되는 컴퓨터 계정이어야 합니다. Office Online 서비스 계정에 대해 다음이 설정되어 있는지 확인할 수 있습니다.  
  
     **참고:** Active Directory 사용자 및 컴퓨터 내에 계정에 대한 위임 탭이 표시되지 않는 경우 이는 해당 계정에 SPN이 없기 때문입니다.  가짜 SPN을 추가하여 `my/spn`과 같이 표시되도록 할 수 있습니다.  
  
     **지정한 서비스에 대한 위임용으로만 이 사용자 트러스트** 및 **모든 인증 프로토콜 사용**  
  
     이를 제한된 위임이라고 하며, Windows 토큰이 프로토콜 전환에 제한된 위임이 필요한 C2WTS(Claims to Windows Token Services)에서 시작되기 때문에 필요합니다.  그런 다음 위에서 만든 MSOLAPSvc.3 및 MSOLAPDisco.3 SPN으로의 위임을 허용할 수 있습니다.  
  
5.  C2WTS(Windows 토큰 서비스에 대한 클레임)를 설정합니다. **이는 시나리오 1에 필요합니다**. 자세한 내용은 [C2WTS(Windows 토큰 서비스에 대한 클레임) 개요](https://msdn.microsoft.com/library/ee517278.aspx)를 참조하세요.  
  
6.  C2WTS 서비스 계정에서**제한된 위임 설정을 구성** 합니다.  설정은 4단계에서 수행한 것과 일치해야 합니다.  
  
 ![sharepoint 서버](../../../analysis-services/instances/install-windows/media/ssas-kcd-sharepointserver-icon.png "sharepoint 서버")  
  
### <a name="sharepoint-server-2016"></a>SharePoint Server 2016  
 다음은 SharePoint Server 설치에 대한 요약입니다.  
  
1.  SharePoint 필수 구성 요소 설치 관리자를 실행합니다.  
  
2.  SharePoint 설치를 실행하고 **단일 서버 팜** 설치 역할을 선택합니다.  
  
3.  SharePoint용 PowerPivot 추가 기능(spPowerPivot16.msi)을 실행합니다. 자세한 내용은 참조 [설치 또는 파워 피벗에 대 한 SharePoint 추가 기능 (SharePoint 2016) 제거](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
4.  PowerPivot 구성 마법사를 실행합니다. [파워 피벗 구성 도구](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)를 참조하세요.  
  
5.  Office Online Server에 SharePoint를 연결합니다.    ??Configure_xlwac_on_SPO.ps1 ??  
  
6.  Kerberos에 대해 SharePoint 인증 공급자를 구성합니다. **이는 시나리오 1에 필요합니다**. 자세한 내용은 [SharePoint 2013에서 Kerberos 인증 계획](https://technet.microsoft.com/library/ee806870.aspx)을 참조하세요.  
  
##  <a name="bkmk_moreinfo"></a> 추가 정보 및 커뮤니티 콘텐츠  
 [사용 중인 관리자에 대한 Kerberos](http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx)  
  
 [Kerberos 이중 홉 이해](http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx)  
  
 [.Net 및 SharePoint에 대한 모든 것](http://sbrickey.com/Tech/Blog/Post/Kerberos_Primer)  
  
 [리소스 기반 Kerberos 제한 위임](http://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)  
  
 [KERBEROS 입문 - 비디오](http://blog.martinlund.it/kerberos-primer/)  
  
 [SQL Server®용 Microsoft® Kerberos 구성 관리자](http://www.microsoft.com/en-us/download/details.aspx?id=39046)  
  
  
