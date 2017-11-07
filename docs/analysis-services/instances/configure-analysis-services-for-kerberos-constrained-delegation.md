---
title: "Kerberos 제한 위임에 대해 Analysis Services 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6d751477-6bf1-48b4-8833-5a631bbe7650
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a6158c7263fcd620f1ac577522b09f8ac4b9e08d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="configure-analysis-services-for-kerberos-constrained-delegation"></a>Kerberos 제한 위임에 대해 Analysis Services 구성
  Kerberos 인증에 대해 Analysis Services를 구성하는 경우 데이터를 쿼리할 때 Analysis Services에서 사용자 ID를 가장하도록 하거나 Analysis Services에서 하위 서비스에 사용자 ID를 위임하도록 하는 데 관심을 갖고 있을 가능성이 높습니다. 각 시나리오에는 약간 다른 구성 요구 사항이 필요합니다. 두 시나리오에 공통적으로 필요한 것은 구성이 제대로 수행되었는지 확인하는 작업입니다.  
  
> [!TIP]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos 구성 관리자**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]과의 Kerberos 관련 연결 문제를 해결하는 진단 도구입니다. 자세한 내용은 [SQL Server용 Microsoft Kerberos 구성 관리자](http://www.microsoft.com/download/details.aspx?id=39046)를 참조하십시오.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [Analysis  Services에서 사용자 ID를 가장할 수 있도록 허용](#bkmk_impersonate)  
  
-   [트러스트된 위임에 대해 Analysis  Services  구성](#bkmk_delegate)  
  
-   [가장된 ID  또는 위임된 ID에 대한 테스트](#bkmk_test)  
  
> [!NOTE]  
>  위임은 Analysis  Services에 대한 연결이 단일 홉이거나 솔루션에서 SharePoint  Secure  Store  Service  또는 Reporting  Services가 제공하는 저장된 자격 증명을 사용하는 경우 필요하지 않습니다. 모든 연결이 Excel에서 Analysis Services 데이터베이스로의 직접 연결이거나 저장된 자격 증명을 기반으로 하는 경우, 제한된 위임을 구성할 필요 없이 Kerberos(또는 NTLM)를 사용할 수 있습니다.  
>   
>  사용자 ID가 여러 컴퓨터 연결을 통해 이동해야 하는 경우("이중 홉")에는 Kerberos 제한 위임이 필요합니다. Analysis  Services  데이터 액세스가 사용자 ID를 조건으로 하고 연결 요청이 위임하는 서비스에서 발생한 경우 다음 섹션의 검사 목록을 사용하여 Analysis  Services에서 원래 호출자를 가장할 수 있는지 확인하십시오. Analysis  Services  인증 흐름에 대한 자세한 내용은 [Microsoft  BI  인증 및 ID  위임](http://go.microsoft.com/fwlink/?LinkID=286576)을 참조하십시오.  
>   
>  보안을 극대화하려면 비제한 위임보다 제한된 위임을 적용하는 것이 좋습니다. 제한된 위임을 통해 분명하게 정의된 서비스와 반대로, 비제한 위임은 서비스 ID가 *모든* 다운스트림 컴퓨터, 서비스 또는 응용 프로그램에서 다른 사용자를 가장할 수 있기 때문에 중대한 보안 위험이 됩니다.  
  
##  <a name="bkmk_impersonate"></a> Analysis  Services에서 사용자 ID를 가장할 수 있도록 허용  
 Reporting  Services,  IIS  또는 SharePoint와 같은 상위 서비스가 Analysis  Services에서 사용자 ID를 가장할 수 있도록 허용하려면 해당 서비스에 대한 Kerberos  제한 위임을 구성해야 합니다. 이 시나리오에서 Analysis  Services는 위임하는 서비스에서 제공하는 ID를 사용하여 현재 사용자를 가장하고 사용자 ID의 역할 멤버 자격을 기반으로 결과를 반환합니다.  
  
|태스크|Description|  
|----------|-----------------|  
|1단계: 계정이 위임에 적합한지 확인|서비스를 실행하는 데 사용되는 계정이 Active  Directory에서 올바른 속성을 갖고 있는지 확인합니다. Active  Directory의 서비스 계정은 중요한 계정으로 표시되지 않거나 위임 시나리오에서 특정하게 제외되어야 합니다. 자세한 내용은 [사용자 계정 이해](http://go.microsoft.com/fwlink/?LinkId=235818)를 참조하십시오.<br /><br /> 참고: 일반적으로 모든 계정 및 서버는 동일한 Active Directory 도메인에 속하거나 동일한 포리스트의 트러스트된 도메인에 속해야 합니다. 그러나 Windows Server 2012에서는 도메인 경계를 넘어 위임을 지원하므로 도메인 기능 수준이 Windows Server 2012인 경우 도메인 경계를 넘어 Kerberos 제한 위임을 구성할 수 있습니다. 또는 HTTP 액세스를 위해 Analysis Services를 구성하고 클라이언트 연결에서 IIS 인증 방법을 사용할 수도 있습니다. 자세한 내용은 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)을 참조하세요.|  
|2단계: SPN  등록|제한된 위임을 설정하기 전에 Analysis  Services  인스턴스에 대한 SPN(서비스 사용자 이름)을 등록해야 합니다. 중간 계층 서비스에 대한 Kerberos  제한 위임을 구성할 때 Analysis  Services  SPN이 필요합니다. 방법을 보려면 [SPN registration for an Analysis Services instance](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md) 을 참조하세요.<br /><br /> SPN(서비스 사용자 이름)은 Kerberos  인증에 대해 구성된 도메인의 서비스에 대한 고유 ID를 지정합니다. 통합 보안을 사용하는 클라이언트 연결은 일반적으로 SPN을 SSPI  인증의 일부로 요청합니다. 요청은 Active  Directory  DC(도메인 컨트롤러)로 전달되고 KDC는 클라이언트가 제공하는 SPN이 Active  Directory의 SPN  등록과 일치하는 경우 티켓을 부여합니다.|  
|3단계: 제한된 위임 구성|사용하려는 계정의 유효성을 검사하고 해당 계정에 대한 SPN을 등록한 후에는 IIS,  Reporting  Services  또는 SharePoint  웹 서비스와 같은 상위 서비스를 제한된 위임에 대해 구성하고 Analysis  Services  SPN을 위임이 허용되는 특정 서비스로 지정합니다.<br /><br /> SharePoint  모드의 Reporting  Services  또는 Excel  Services와 같이 SharePoint에서 실행되는 서비스는 Analysis  Services  다차원 또는 표 형식 데이터를 소비하는 통합 문서와 보고서를 호스팅하는 경우가 많습니다. 이러한 서비스에 대한 제한된 위임 구성은 일반적인 구성 태스크이며 Excel  Services에서 데이터 새로 고침을 지원하는 데 필요합니다. 다음 링크에서는 SharePoint  서비스는 물론,  Analysis  Services  데이터에 대한 다운스트림 데이터 연결을 요청할 가능성이 있는 다른 서비스에 대한 지침을 제공합니다.<br /><br /> [Excel Services용 ID 위임(SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=299826) 또는 [SharePoint Server 2010에서 Kerberos 인증에 대해 Excel Services를 구성하는 방법](http://support.microsoft.com/kb/2466519)<br /><br /> [PerformancePoint  Services용 ID  위임(SharePoint  Server  2010)](http://go.microsoft.com/fwlink/?LinkId=299827)<br /><br /> [SQL  Server  Reporting  Services용 ID  위임(SharePoint  Server  2010)](http://go.microsoft.com/fwlink/?LinkId=299828)<br /><br /> IIS 7.0에 대한 자세한 내용은 [Windows 인증 구성(IIS 7.0)](http://technet.microsoft.com/library/cc754628\(v=ws.10\).aspx) 또는 [Kerberos 인증을 사용하도록 SQL Server 2008 Analysis Services 및 SQL Server 2005 Analysis Services를 구성하는 방법](http://support.microsoft.com/kb/917409)을 참조하세요.|  
|4단계: 연결 테스트|테스트할 때 서로 다른 ID로 원격 컴퓨터에서 연결하고 업무용 사용자와 동일한 응용 프로그램을 사용하여 Analysis  Services를 쿼리하십시오. SQL Server Profiler를 사용하여 연결을 모니터링할 수 있습니다. 요청에 대한 사용자 ID가 표시되어야 합니다. 자세한 내용은 이 섹션의 [가장된 ID  또는 위임된 ID에 대한 테스트](#bkmk_test) 를 참조하세요.|  
  
##  <a name="bkmk_delegate"></a> 트러스트된 위임에 대해 Analysis  Services  구성  
 Kerberos  제한 위임에 대해 Analysis  Services를 구성하면 Analysis  Services에서 관계형 데이터베이스 엔진과 같은 하위 서비스에 대해 클라이언트 ID를 가장할 수 있으므로 클라이언트가 직접 연결된 것처럼 데이터를 쿼리할 수 있습니다.  
  
 Analysis  Services에 대한 위임 시나리오는 **DirectQuery** 모드에 대해 구성된 테이블 형식 모델로 제한됩니다. Analysis  Services에서 다른 서비스로 위임된 자격 증명을 전달할 수 있는 시나리오는 이 경우뿐입니다. 이전 섹션에서 언급한 SharePoint 시나리오처럼, 다른 모든 시나리오에서 Analysis Services는 위임 체인의 수신측에 있습니다. DirectQuery에 대한 자세한 내용은 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)를 참조하세요.  
  
> [!NOTE]  
>  ROLAP 저장소, 처리 작업 또는 원격 파티션에 대한 액세스는 제한된 위임이 필요하다고 잘못 생각하는 경우가 흔하지만 그렇지 않습니다. 이러한 작업은 모두 서비스 계정(처리 계정)에서 직접 실행됩니다. 이러한 작업에 대한 권한을 서비스 계정으로 직접 제공하는 경우(예: 서비스에서 데이터를 처리할 수 있도록 관계형 데이터베이스의 granting db_datareader 권한 부여), Analysis Services에서 이러한 작업에 대해 위임이 필요하지 않습니다. 서버 작업 및 사용 권한에 대한 자세한 내용은 [서비스 계정 구성&#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)을 참조하세요.  
  
 이 섹션에서는 트러스트된 위임에 대해 Analysis  Services를 설정하는 방법에 대해 설명합니다. 이 작업을 완료한 후 테이블 형식 솔루션에서 사용되는 DirectQuery 모드를 지원하여, Analysis Services는 위임된 자격 증명을 SQL Server로 전달할 수 있습니다.  
  
 시작하기 전 주의 사항:  
  
-   Analysis  Services가 시작되었는지 확인합니다.  
  
-   Analysis  Services에 대해 등록된 SPN이 올바른지 확인합니다. 자세한 내용은 [SPN registration for an Analysis Services instance](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)을 참조하십시오.  
  
 두 전제 조건이 충족되었으면 다음 단계를 계속 수행합니다. 제한된 위임을 설정하려면 도메인 관리자여야 합니다.  
  
1.  Active  Directory  사용자 및 컴퓨터에서 Analysis  Services가 실행되는 서비스 계정을 찾습니다. 서비스 계정을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     설명을 위해 다음 스크린샷에서는 OlapSvc와 SQLSvc를 사용하여 Analysis  Services와 SQL  Server를 각각 나타냅니다.  
  
     OlapSvc는 SQLSvc로의 제한된 위임에 대해 구성될 계정입니다. 이 작업을 완료하면 OlapSvc가 서비스 티켓의 위임된 자격 증명을 SQLSvc로 전달할 수 있는 권한을 갖게 되며 데이터를 요청할 때 원래 호출자를 가장합니다.  
  
2.  위임 탭에서 **지정한 서비스에 대한 위임용으로만 이 사용자 트러스트**를 선택하고 **Kerberos만 사용**을 선택합니다. **추가** 를 클릭하여 Analysis  Services에서 자격 증명을 위임할 수 있는 서비스를 지정합니다.  
  
     위임 탭은 사용자 계정(OlapSvc)이 서비스(Analysis  Services)에 할당되고 서비스에 대한 SPN이 등록된 경우에만 나타납니다. SPN을 등록하려면 서비스가 실행 중이어야 합니다.  
  
     ![SSAS_Kerberos_1_AccountProperties](../../analysis-services/instances/media/ssas-kerberos-1-accountproperties.gif "SSAS_Kerberos_1_AccountProperties")  
  
3.  서비스 추가 페이지에서 **사용자 또는 컴퓨터**를 클릭합니다.  
  
     ![SSAS_Kerberos_2_](../../analysis-services/instances/media/ssas-kerberos-2.gif "SSAS_Kerberos_2_")  
  
4.  사용자 또는 컴퓨터 선택 페이지에서 Analysis  Services  테이블 형식 model 데이터베이스에 데이터를 제공하는 SQL  Server  인스턴스를 실행하는 데 사용되는 계정을 입력합니다. **확인** 을 클릭하여 서비스 계정을 적용합니다.  
  
     원하는 계정을 선택할 수 없는 경우 SQL  Server가 실행 중이고 해당 계정에 대한 SPN이 등록되어 있는지 확인합니다. 데이터베이스 엔진의 SPN에 대한 자세한 내용은 [Register a Service Principal Name for Kerberos Connections](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하십시오.  
  
     ![SSAS_Kerberos_3_SelectUsers](../../analysis-services/instances/media/ssas-kerberos-3-selectusers.gif "SSAS_Kerberos_3_SelectUsers")  
  
5.  이제 SQL  Server  인스턴스가 서비스 추가에 나타납니다. 해당 계정을 사용하는 모든 서비스도 목록에 나타납니다. 사용할 SQL  Server  인스턴스를 선택합니다. **확인** 을 클릭하여 인스턴스를 적용합니다.  
  
     ![SSAS_Kerberos_4_](../../analysis-services/instances/media/ssas-kerberos-4.gif "SSAS_Kerberos_4_")  
  
6.  이제 Analysis  Services  서비스 계정의 속성 페이지는 다음 스크린샷과 유사합니다. **확인** 을 클릭하여 변경 내용을 저장합니다.  
  
     ![SSAS_Kerberos_5_Finished](../../analysis-services/instances/media/ssas-kerberos-5-finished.gif "SSAS_Kerberos_5_Finished")  
  
7.  다른 ID로 원격 클라이언트 컴퓨터에서 연결하여 성공적인 위임에 대해 테스트하고 테이블 형식 모델을 쿼리합니다. SQL  Server  Profiler에서 요청에 대한 사용자 ID가 표시됩니다.  
  
##  <a name="bkmk_test"></a> 가장된 ID  또는 위임된 ID에 대한 테스트  
 SQL  Server  Profiler를 사용하여 데이터를 쿼리하는 사용자의 ID를 모니터링할 수 있습니다.  
  
1.  Analysis  Services  인스턴스에서 **SQL  Server  Profiler** 를 시작한 다음 새 추적을 시작합니다.  
  
2.  이벤트 선택에서 **Audit Login** 및 **Audit Logout** 이 보안 감사 섹션에서 선택되었는지 확인합니다.  
  
3.  원격 클라이언트 컴퓨터에서 응용 프로그램 서비스(예:  SharePoint  또는 Reporting  Services)를 통해 Analysis  Services에 연결합니다. Audit Login 이벤트는 Analysis Services에 연결하는 사용자의 ID를 보여 줍니다.  
  
 철저하게 테스트하려면 네트워크에서 Kerberos  요청 및 응답을 캡처할 수 있는 네트워크 모니터링 도구를 사용해야 합니다. Kerberos에 대해 필터링된 네트워크 모니터 유틸리티(netmon.exe)가 이 작업에 사용될 수 있습니다. Netmon 3.4 및 기타 도구를 사용하여 Kerberos 인증을 테스트하는 방법에 대한 자세한 내용은 [Kerberos 인증 구성: 핵심 구성(SharePoint Server 2010)](http://technet.microsoft.com/library/gg502602\(v=office.14\).aspx)을 참조하세요.  
  
 그리고 Active Directory 개체 속성 대화 상자에서 위임 탭의 각 옵션에 대한 자세한 설명은 [Active Directory에서 가장 많이 혼동하는 대화 상자](http://windowsitpro.com/windows/most-confusing-dialog-box-active-directory) (영문)를 참조하세요. 이 문서에는 LDP를 사용하여 테스트하고 테스트 결과를 해석하는 방법도 설명되어 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft BI 인증 및 Id 위임](http://go.microsoft.com/fwlink/?LinkID=286576)   
 [Kerberos를 사용한 상호 인증](http://go.microsoft.com/fwlink/?LinkId=299283)   
 [Analysis Services에 연결](../../analysis-services/instances/connect-to-analysis-services.md)   
 [Analysis Services 인스턴스에 대 한 SPN 등록](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)   
 [연결 문자열 속성&#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)  
  
  

