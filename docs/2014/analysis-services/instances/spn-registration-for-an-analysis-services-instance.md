---
title: Analysis Services 인스턴스에 대 한 SPN 등록 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 9e78dc37-a3f0-415d-847c-32fec69efa8c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f34ff1942ff742a5040d7fa16fedf31f6d806768
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126853"
---
# <a name="spn-registration-for-an-analysis-services-instance"></a>SPN registration for an Analysis Services instance
  SPN(서비스 사용자 이름)은 Kerberos가 클라이언트 및 서비스 ID를 상호 인증하는 데 사용되는 Active Directory 도메인의 서비스 인스턴스를 고유하게 식별합니다. SPN은 서비스 인스턴스가 실행되는 로그온 계정과 연결되어 있습니다.  
  
 Kerberos  인증을 통해 Analysis  Services에 연결하는 클라이언트 응용 프로그램의 경우 Analysis  Services  클라이언트 라이브러리는 지정된 Analysis  Services  릴리스에서 고정된 잘 알려진 변수(예:  서비스 클래스)  및 연결 문자열의 호스트 이름을 사용하여 SPN을 생성합니다.  
  
 상호 인증이 발생하려면 클라이언트에서 생성된 SPN이 Active  Directory  DC(도메인 컨트롤러)의 해당 SPN  개체와 일치해야 합니다. 즉,  사용자가 연결 문자열에 호스트 이름을 지정할 수 있는 모든 방법을 처리하려면 단일 Analysis  Services  인스턴스에 여러 SPN을 등록해야 할 수 있습니다. 예를 들어 서버의 FQDN(정규화된 도메인 이름)과 짧은 컴퓨터 이름을 둘 다 처리하려면 SPN이 두 개 필요할 수 있습니다. Analysis Services SPN을 올바르게 등록하는 것이 성공적인 연결에 필수적입니다. SPN이 존재하지 않거나 잘못된 형식으로 되어 있거나 중복된 경우에는 연결이 실패합니다.  
  
 SPN 등록은 Analysis Services 관리자가 수행하는 수동 작업입니다. SQL  Server  데이터베이스 엔진과 달리 Analysis  Services는 서비스 시작 시 SPN을 자동으로 등록하지 않습니다. 수동 등록은 Analysis  Services가 서비스별 SID를 비롯한 기본 가상 계정,  도메인 사용자 계정이나 기본 제공 계정에서 실행되는 경우에 필요합니다.  
  
 도메인 관리자가 만든 미리 정의된 관리되는 서비스 계정에서 서비스가 실행되는 경우 SPN 등록은 필요하지 않습니다. 도메인의 기능 수준에 따라 SPN을 등록하려면 도메인 관리자 권한이 필요할 수 있습니다.  
  
> [!TIP]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos 구성 관리자**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]과의 Kerberos 관련 연결 문제를 해결하는 진단 도구입니다. 자세한 내용은 [SQL Server용 Microsoft Kerberos 구성 관리자](http://www.microsoft.com/download/details.aspx?id=39046)를 참조하십시오.  
  
> [!TIP]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos 구성 관리자**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]과의 Kerberos 관련 연결 문제를 해결하는 진단 도구입니다. 자세한 내용은 [SQL Server용 Microsoft Kerberos 구성 관리자](http://www.microsoft.com/download/details.aspx?id=39046)를 참조하십시오.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [SPN  등록이 필요한 경우](#bkmk_scnearios)  
  
 [Analysis  Services에 대한 SPN  형식](#bkmk_SPNSyntax)  
  
 [가상 계정에 대한 SPN  등록](#bkmk_virtual)  
  
 [도메인 계정에 대한 SPN 등록](#bkmk_domain)  
  
 [기본 제공 계정에 대한 SPN 등록](#bkmk_builtin)  
  
 [명명된 인스턴스에 대한 SPN 등록](#bkmk_spnNamed)  
  
 [SSAS  클러스터에 대한 SPN  등록](#bkmk_spnCluster)  
  
 [HTTP  액세스에 대해 구성된 SSAS  인스턴스에 대한 SPN  등록](#bkmk_spnHTTP)  
  
 [고정 포트에서 수신 대기하는 SSAS  인스턴스에 대한 SPN  등록](#bkmk_spnFixedPorts)  
  
##  <a name="bkmk_scnearios"></a> SPN  등록이 필요한 경우  
 연결 문자열에서 “SSPI=Kerberos”를 지정하는 모든 클라이언트 연결에는 Analysis Services 인스턴스에 대한 SPN 등록 요구 사항이 적용됩니다.  
  
 SPN  등록은 다음 상황에서 필요합니다. 자세한 내용은 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md)를 참조하십시오.  
  
-   클라이언트 응용 프로그램 또는 중간 계층 서비스에서 Analysis  Services로 사용자 ID를 이동하려면 ID  위임이 필요합니다. ID  위임은 사용자별 사용 권한 또는 필터가 특정 개체에 대해 정의된 경우에 일반적으로 사용됩니다.  
  
     ID 위임과 관련된 일반적인 시나리오는 Analysis Services에서 데이터를 검색할 때 사용자 ID를 가장하기 위해 제한된 위임에 대해 Excel 서비스 또는 Reporting Services와 같은 중간 계층 서비스를 구성하는 것입니다. 이 동작을 지원하려면 제한된 위임에 대해 Excel 서비스 또는 Reporting Services를 구성할 때 Analysis Services SPN을 대상 서비스로 제공해야 합니다.  
  
-   Analysis  Services는 DirectQuery  모드를 사용하여 테이블 형식 데이터베이스에 대한 데이터를 SQL  Server  관계형 데이터베이스에서 검색할 때 사용자 ID를 위임합니다. Analysis  Services에서 사용자 ID를 다른 서비스로 위임하는 시나리오는 이 경우뿐입니다.  
  
##  <a name="bkmk_SPNSyntax"></a> Analysis  Services에 대한 SPN  형식  
 SPN을 등록하려면 **setspn** 을 사용합니다. 최신 운영 체제에서 **setspn** 은 시스템 유틸리티로 설치됩니다. 자세한 내용은 [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx)을 참조하세요.  
  
 다음 표에서는 Analysis  Services  SPN의 각 부분에 대해 설명합니다.  
  
|요소|Description|  
|-------------|-----------------|  
|서비스 클래스|MSOLAPSvc.3은 서비스를 Analysis Services 인스턴스로 식별합니다. .3은 Analysis Services 전송에서 사용되는 XMLA-over-TCP/IP 프로토콜의 버전에 대한 참조이며 제품 릴리스와는 관련이 없습니다. 따라서 MSOLAPSvc.3은 프로토콜 자체가 수정될 때까지 SQL  Server  2005,  2008,  2008  R2,  2012  및 Analysis  Services의 모든 이후 릴리스에 대한 올바른 서비스 클래스입니다.|  
|Host-name|서비스가 실행 중인 컴퓨터를 식별합니다. 정규화된 도메인 이름이거나 NetBIOS 이름일 수 있으며, 두 가지 경우 모두 SPN을 등록해야 합니다.<br /><br /> 서버의 NetBIOS  이름에 대한 SPN을 등록할 때 `SetupSPN –S` 를 사용하여 중복 등록을 확인하세요. NetBIOS  이름은 포리스트에서 고유한 것으로 보장되지 않으며 SPN  등록이 중복되면 연결이 실패합니다.<br /><br /> Analysis  Services  부하 분산 클러스터의 경우 호스트 이름은 클러스터에 할당된 가상 이름이어야 합니다.<br /><br /> IP  주소를 사용하여 SPN을 만들지 마세요. Kerberos는 도메인의 DNS  확인 기능을 사용합니다. IP 주소를 지정하면 이 기능이 우회됩니다.|  
|Port-number|포트 번호가 SPN  구문의 일부이지만 Analysis  Services  SPN을 등록할 때는 포트 번호를 지정하지 않습니다. 콜론( : ) 문자는 Analysis Services에서 인스턴스 이름을 지정하는 데 사용됩니다. Analysis Services 인스턴스의 경우 포트는 기본 포트(TCP 2383) 또는 SQL Server Browser 서비스에서 할당한 포트(TCP 2382)로 간주됩니다.|  
|Instance-name|Analysis Services는 동일한 컴퓨터에 여러 번 설치될 수 있는 복제 가능한 서비스입니다. 각 인스턴스는 인스턴스 이름을 통해 식별됩니다.<br /><br /> 인스턴스 이름 앞에는 콜론(:) 문자가 붙습니다. 예를 들어 SRV01이라는 호스트 컴퓨터와 명명된 인스턴스 SSAS-Tabular가 주어진 경우 SPN은 SRV01:SSAS-Tabular이어야 합니다.<br /><br /> 명명된 Analysis  Services  인스턴스를 지정하는 구문은 다른 SQL  Server  인스턴스에서 사용하는 구문과 다릅니다. 다른 서비스는 백슬래시(\)를 사용하여 SPN에서 인스턴스 이름을 추가합니다.|  
|서비스 계정|**MSSQLServerOLAPService** Windows  서비스의 시작 계정입니다. Windows  도메인 사용자 계정,  가상 계정,  MSA(관리 서비스 계정)  또는 기본 제공 계정(예:  서비스별 SID,  NetworkService  또는 LocalSystem)일 수 있습니다. Windows 도메인 사용자 계정으로 도메인 \ 사용자 형식을 지정할 수 있습니다 또는 user@domain합니다.|  
  
##  <a name="bkmk_virtual"></a> 가상 계정에 대한 SPN  등록  
 가상 계정은 SQL  Server  서비스의 기본 계정 유형입니다. 가상 계정은 **NT Service\MSOLAPService** 기본 인스턴스 및 **NT Service\MSOLAP$**\<인스턴스 이름 > 명명 된 인스턴스에 대 한 합니다.  
  
 이름에서 알 수 있는 것처럼 해당 계정은 Active  Directory에 존재하지 않습니다. 가상 계정은 로컬 컴퓨터에서만 존재합니다. 외부 서비스,  응용 프로그램 또는 장치에 연결할 때 연결은 로컬 컴퓨터 계정을 통해 만들어집니다. 이러한 이유로 가상 계정에서 실행되는 Analysis  Services에 대한 SPN  등록은 실제로 시스템 계정에 대한 SPN  등록입니다.  
  
 **NT  Service\MSOLAPService로 실행 중인 기본 인스턴스에 대한 구문 예**  
  
 이 예에서는 기본 가상 계정에서 실행되는 Analysis  Services  기본 인스턴스에 대한 **setspn** 구문을 보여 줍니다. 이 예에서 컴퓨터 호스트 이름은 **AW-SRV01**입니다. 앞에서 설명한 것처럼 SPN 등록에는 가상 계정 *NT Service\MSOLAPService* 대신 **컴퓨터 계정**을 지정해야 합니다.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
> [!NOTE]  
>  두 개의 SPN  등록인 NetBIOS  호스트 이름에 대한 SPN  등록과 호스트의 정규화된 도메인 이름에 대한 SPN  등록을 만들어야 합니다. 다양한 클라이언트 응용 프로그램에서는 Analysis Services에 연결할 때 서로 다른 호스트 이름 규칙을 사용합니다. SPN 등록이 두 개면 호스트 이름의 두 버전이 모두 처리됩니다.  
  
 **NT Service\MSOLAP $로 실행 되는 명명 된 인스턴스에 대 한 구문 예\<인스턴스 이름 >**  
  
 이 예에서는 기본 가상 계정에서 실행되는 명명된 인스턴스에 대한 **setspn** 구문을 보여 줍니다. 이 예에서 컴퓨터 호스트 이름은 **AW-SRV02**이고 인스턴스 이름은 **AW-FINANCE**입니다. 다시는 가상 계정이 아니라 SPN에 대해 지정 된 컴퓨터 계정을 **NT Service\MSOLAP$**\<인스턴스 이름 >.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV02.AdventureWorks.com:AW-FINANCE AW-SRV02  
```  
  
##  <a name="bkmk_domain"></a> 도메인 계정에 대한 SPN 등록  
 Analysis  Services  인스턴스를 실행되는 도메인 계정을 사용하는 것이 일반적입니다.  
  
 네트워크 또는 하드웨어 부하 분산 클러스터에서 실행되는 Analysis  Services  인스턴스의 경우,  도메인 계정이 필요하며 각 인스턴스는 동일한 도메인 계정에서 실행 중인 클러스터에 있습니다.  
  
 **도메인 사용자로 실행 중인 기본 인스턴스의 구문 예**  
  
 이 예에서는 AdventureWorks 도메인의 도메인 사용자 계정 **SSAS-Service** 에서 실행 중인 Analysis Services 기본 인스턴스에 대한 **setspn**구문을 보여 줍니다.  
  
```  
Setspn –s msolapsvc.3\AW-SRV01.Adventureworks.com AdventureWorks\SSAS-Service  
```  
  
> [!TIP]  
>  SPN  등록 방법에 따라 `Setspn -L <domain account>` 또는 `Setspn -L <machinename>`을 실행하여 SPN이 Analysis  Services  서버에 대해 만들어졌는지 확인하세요. MSOLAPSVC.3/ 표시\<호스트 이름 > 목록에서.  
  
##  <a name="bkmk_builtin"></a> 기본 제공 계정에 대한 SPN 등록  
 이 방법은 권장되지는 않지만 이전 Analysis Services 설치는 경우에 따라 네트워크 서비스, 로컬 서비스, 로컬 시스템과 같은 기본 제공 계정에서 실행되도록 구성되어 있습니다.  
  
 **기본 제공 계정에서 실행 중인 기본 인스턴스의 구문 예**  
  
 기본 제공 계정 또는 서비스별 SID에서 실행 중인 서비스에 대한 SPN  등록은 가상 계정에 사용된 SPN  구문과 동일합니다. 계정 이름 대신 시스템 계정을 사용하십시오.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnNamed"></a> 명명된 인스턴스에 대한 SPN 등록  
 Analysis  Services의 명명된 인스턴스에서는 SQL  Server  Browser  서비스를 통해 검색되는 동적 포트 할당을 사용합니다. 명명된 인스턴스를 사용하는 경우 SQL  Server  Browser  서비스 및 Analysis  Services  명명된 인스턴스 모두에 대해 SPN을 등록합니다. 자세한 내용은 [SQL  Server  Analysis  Services  또는 SQL  Server의 명명된 인스턴스에 연결할 때 SQL  Server  Browser  서비스에 대한 SPN이 필요합니다.](http://support.microsoft.com/kb/950599)를 참조하세요.  
  
 **LocalService로 실행 중인 SQL  Server  Browser  서비스에 대한 구문 예**  
  
 서비스 클래스는 **MSOLAPDisco.3**입니다. 이 서비스는 기본적으로 NT  AUTHORITY\LocalService로 실행되며 이것은 SPN  등록이 시스템 계정에 대해 설정된 것을 나타냅니다. 이 예에서 시스템 계정은 **AW-SRV01**이며 컴퓨터 이름에 해당합니다.  
  
```  
Setspn -S MSOLAPDisco.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnCluster"></a> SSAS  클러스터에 대한 SPN  등록  
 Analysis  Services  장애 조치(Failover)  클러스터의 경우 호스트 이름은 클러스터에 할당된 가상 이름이어야 합니다. SQL Server 네트워크 이름이며, 기존 WSFC에 Analysis Services를 설치할 때 SQL Server 설치 중에 지정됩니다. Active Directory에서 이 이름을 찾을 수 있습니다. **장애 조치(Failover) 클러스터 관리자** | **역할** | **리소스** 탭에서 찾을 수도 있습니다. 리소스 탭의 서버 이름은 SPN 명령에 '가상 이름'으로 사용해야 하는 것입니다.  
  
 **Analysis Services 클러스터에 대한 SPN 구문**  
  
```  
Setspn –s msolapsvc.3/<virtualname.FQDN > <domain user account>  
```  
  
 Analysis  Services  클러스터의 노드는 기본 포트(TCP  2383)를 사용하고 각 노드가 동일한 SID를 갖도록 동일한 도메인 사용자 계정에서 실행되어야 합니다. 자세한 내용은 [SQL Server Analysis Services를 클러스터링하는 방법](http://msdn.microsoft.com/library/dn736073.aspx) (영문)을 참조하세요.  
  
##  <a name="bkmk_spnHTTP"></a> HTTP  액세스에 대해 구성된 SSAS  인스턴스에 대한 SPN  등록  
 솔루션 요구 사항에 따라 HTTP  액세스에 대해 Analysis  Services를 구성했을 수 있습니다. 솔루션에 중간 계층 구성 요소로 IIS가 포함되어 있고 Kerberos  인증이 솔루션 요구 사항인 경우 IIS에 대한 SPN을 수동으로 등록해야 할 수 있습니다. 자세한 내용은 [Kerberos  인증을 사용하도록 SQL  Server  2008  Analysis  Services  및 SQL  Server  2005  Analysis  Services를 구성하는 방법](http://support.microsoft.com/kb/917409)에서 "IIS를 실행하는 컴퓨터에서 설정 구성"을 참조하세요.  
  
 Analysis  Services  인스턴스에 대한 SPN  등록의 측면에서는 TCP에 대해 구성된 인스턴스나 HTTP에 대해 구성된 인스턴스 사이에 차이가 없습니다. MSMDPUMP  ISAPI  확장을 사용하여 IIS에서 Analysis  Services에 연결하는 경우 항상 TCP  연결입니다.  
  
 따라서 기본 인스턴스나 명명된 인스턴스에 대한 이전 섹션들의 지침을 사용하여 SPN을 등록할 수 있습니다. 호스트 이름을 지정하는 경우 HTTP  액세스에 대해 서비스를 구성했을 때 msmdpump.ini  파일에서 지정한 호스트 이름을 사용해야 합니다.  
  
 HTTP 액세스에 대한 자세한 내용은 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](configure-http-access-to-analysis-services-on-iis-8-0.md)을 참조하세요.  
  
##  <a name="bkmk_spnFixedPorts"></a> 고정 포트에서 수신 대기하는 SSAS  인스턴스에 대한 SPN  등록  
 Analysis Services SPN 등록에서 포트 번호를 지정할 수 없습니다. Analysis  Services를 기본 인스턴스로 설치하고 고정 포트에서 수신 대기하도록 구성한 경우 이제 기본 포트(TCP  2383)에서 수신 대기하도록 구성해야 합니다. 명명된 인스턴스의 경우 SQL Server Browser 서비스와 동적 포트 할당을 사용해야 합니다.  
  
 Analysis  Services  인스턴스는 단일 포트에서만 수신 대기할 수 있습니다. 여러 포트를 사용하는 것은 지원되지 않습니다. 포트 구성에 대한 자세한 내용은 [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft BI 인증 및 Id 위임](http://go.microsoft.com/fwlink/?LinkID=286576)   
 [Kerberos를 사용한 상호 인증](http://go.microsoft.com/fwlink/?LinkId=299283)   
 [Kerberos 인증을 사용 하도록 SQL Server 2008 Analysis Services 및 SQL Server 2005 Analysis Services를 구성 하는 방법](http://support.microsoft.com/kb/917409)   
 [서비스 사용자 이름 (Spn) SetSPN 구문 (Setspn.exe)](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [어떤 SPN을 사용 하 고 어떻게 합니까?](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx)   
 [서비스 계정 단계별 가이드](http://technet.microsoft.com/library/dd548356\(WS.10\).aspx)   
 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [인터넷 정보 서비스에서 호스트 되는 웹 응용 프로그램을 구성한 경우 Spn을 사용 하는 방법](http://support.microsoft.com/kb/929650)   
 [서비스 계정의 새로운 기능](http://technet.microsoft.com/library/dd367859\(WS.10\).aspx)   
 [SharePoint 2010 제품 (백서)에 대 한 Kerberos 인증 구성](http://technet.microsoft.com/library/ff829837.aspx)  
  
  
