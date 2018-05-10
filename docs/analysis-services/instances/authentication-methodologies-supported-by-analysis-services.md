---
title: Analysis Services에서 지 원하는 인증 방법 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d8a3186d07dd0e030038c2a3cb5bebe307dba624
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="authentication-methodologies-supported-by-analysis-services"></a>Analysis Services에서 지원하는 인증 방법
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  클라이언트 응용 프로그램에서 Analysis Services 인스턴스에 연결하려면 Windows 인증(통합)이 필요합니다. 다음 방법 중 하나를 사용하여 Windows 사용자 ID를 제공할 수 있습니다.  
  
-   NTLM  
  
-   자세한 내용은 [Kerberos 제한된 위임에 대해 Analysis Services 구성](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)을 참조하세요.  
  
-   연결 문자열의 EffectiveUserName  
  
-   기본 또는 익명(HTTP 액세스 구성 필요)  
  
-   저장된 자격 증명  
  
 클레임 인증은 지원되지 않습니다. Windows 클레임 토큰을 사용하여 Analysis Services에 액세스할 수 없습니다. Analysis Services 클라이언트 라이브러리는 Windows 보안 주체와만 작동합니다. BI 솔루션에 클레임 ID가 포함된 경우 각 사용자에 대한 Windows ID 섀도 계정이 필요하며 저장된 자격 증명을 사용하여 Analysis Services 데이터에 액세스해야 합니다.  
  
 BI 및 Analysis Services 인증 흐름에 대한 자세한 내용은 [Microsoft BI 인증 및 ID 위임](http://go.microsoft.com/fwlink/?LinkID=286576)을 참조하십시오.  
  
##  <a name="bkmk_auth"></a> 인증 대체 방법 이해  
 Analysis Services 데이터베이스에 연결하려면 Windows 사용자 또는 그룹 ID 및 연결된 사용 권한이 필요합니다. 이 ID는 보고서를 보려는 사용자가 사용하는 일반적인 목적의 로그인이지만, 개별 사용자의 ID를 포함할 가능성이 높습니다.  
  
 테이블 형식 또는 다차원 모델은 대개 요청하는 대상에 따라 개체별로 또는 데이터 자체 내에서 서로 다른 수준의 데이터 액세스 권한을 갖게 됩니다. 이 요구 사항을 충족하기 위해 NTLM, Kerberos, EffectiveUserName 또는 기본 인증을 사용할 수 있습니다. 이러한 모든 기술은 각 연결을 통해 서로 다른 사용자 ID에 전달하기 위한 방법을 제공합니다. 그러나, 이러한 방법에는 대부분 단일 홉 제한이 적용됩니다. 위임이 가능한 Kerberos 인증을 통해서만 기존 사용자 ID로 여러 컴퓨터 연결을 거쳐 원격 서버의 백 엔드 데이터 저장소로 이동할 수 있습니다.  
  
 **NTLM**  
  
 `SSPI=Negotiate`를 지정하는 연결의 경우, NTLM은 Kerberos 도메인 컨트롤러를 사용할 수 없을 때 사용되는 백업 인증 하위 시스템입니다. NTLM을 사용하는 경우 요청이 클라이언트에서 서버로의 직접 연결 요청이고, 연결을 요청하는 사람은 해당 리소스에 대한 권한을 갖고 있으며, 클라이언트와 서버 컴퓨터가 같은 도메인에 있는 한 모든 사용자 또는 클라이언트 응용 프로그램은 서버 리소스에 액세스할 수 있습니다.  
  
 다중 계층 솔루션에서는 NTLM의 단일 홉 제한이 주요 제약 조건일 수 있습니다. 요청을 만드는 사용자 ID는 정확히 하나의 원격 서버에서 가장될 수 있지만 더 이상 이동하지는 않습니다. 현재 작업에 여러 컴퓨터에서 실행 중인 서비스가 필요한 경우, 백 엔드 서버에서 보안 토큰을 다시 사용하여 Kerberos 제한된 위임을 구성해야 합니다. 또는 저장된 자격 증명이나 기본 인증을 사용하여 단일홉 접속에 대한 새 ID 정보에 전달할 수 있습니다.  
  
 **Kerberos 인증 및 Kerberos 제한된 위임**  
  
 Kerberos 인증은 Active Directory 도메인에서 Windows 통합 보안의 기준입니다. NTLM과 마찬가지로, 위임을 사용하도록 설정하지 않는 한 Kerberos를 통한 가장은 단일 홉으로 제한됩니다.  
  
 다중 홉 연결을 지원하는 Kerberos에서는 제한된 위임과 비제한된 위임 모두 가능하지만, 대개의 경우 제한된 위임이 가장 좋은 보안 방식으로 간주됩니다. 제한된 위임을 통해 서비스에서 원격 컴퓨터의 지정된 하위 서비스로 사용자 ID의 보안 토큰을 전달할 수 있습니다. 다중 계층 응용 프로그램의 경우, 중간 계층 응용 프로그램 서버에서 Analysis Services와 같은 백 엔드 데이터베이스로 사용자 ID를 위임하는 것이 일반적인 요구 사항입니다. 예를 들어, 사용자 ID에 따라 서로 다른 데이터를 반환하는 표 형식 또는 다차원 모델에서는 사용자가 자격 증명을 다시 입력하지 않아도 되도록 중간 계층 서비스에서의 ID 위임이 필요합니다. 또는 보안 자격 증명을 기타 다른 방법으로 받습니다.  
  
 요청의 전송 끝점 및 수신 끝점 모두에서 서비스가 위임에 대해 명시적으로 권한이 부여된 Active Directory에서는 제한된 위임에 추가 구성이 필요합니다. 사전에 구성 비용이 들겠지만, 일단 서비스가 구성되면 Active Directory에서 독립적으로 암호 업데이트를 관리합니다. 앞서 설명한 저장된 자격 증명 옵션을 사용하는 경우 응용 프로그램에 저장된 계정 정보를 업데이트할 필요가 없습니다.  
  
 제한된 위임에 대해 Analysis Services를 구성하는 방법에 대한 자세한 내용은 [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)을 참조하십시오.  
  
> [!NOTE]  
>  Windows Server 2012는 도메인 간의 제한된 위임을 지원합니다. 반면 Windows Server 2008 또는 2008 R2와 같이 더 낮은 기능 수준에서 도메인의 Kerberos 제한된 위임을 구성하려면 클라이언트 및 서버 컴퓨터가 모두 같은 도메인의 멤버여야 합니다.  
  
 **EffectiveUserName**  
  
 EffectiveUserName은 ID 정보를 Analysis Services에 전달하는 데 사용되는 연결 문자열 속성입니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 은 이 속성을 사용하여 사용자 작업을 사용 현황 로그에 기록합니다. Excel Services 및 PerformancePoint Services에서는 이 속성을 사용하여 SharePoint의 통합 문서 또는 대시보드에 사용된 데이터를 검색할 수 있습니다. 또한 Analysis Services 인스턴스에서 작업을 수행하는 사용자 지정 응용 프로그램 또는 스크립트에서도 이 속성을 사용할 수 있습니다.  
  
 SharePoint에서 EffectiveUserName을 사용하는 방법에 대한 자세한 내용은 [SharePoint Server 2010에서 Analysis Services EffectiveUserName 사용](http://go.microsoft.com/fwlink/?LinkId=311905)을 참조하십시오.  
  
 **기본 인증 및 익명 사용자**  
  
 기본 인증은 특정 사용자로 백 엔드 서버에 연결하는 네 번째 방법을 제공합니다. 기본 인증을 사용하여 Windows 사용자 이름 및 암호를 연결 문자열에 전달하고, 전송 중 중요한 정보가 보호되도록 연결 암호화 요구 사항을 추가로 적용합니다. 기본 인증의 중요한 장점 중 하나는 이 인증 요청이 도메인 경계를 넘을 수 있다는 점입니다.  
  
 익명 인증의 경우 익명 사용자 ID를 특정 Windows 사용자 계정(기본적으로 IUSR_GUEST) 또는 응용 프로그램 풀 ID로 설정할 수 있습니다. 익명 사용자 계정은 Analysis Services 연결에서 사용되며 Analysis Services 인스턴스에서 데이터 액세스 권한을 갖고 있어야 합니다. 이 방법을 사용할 경우 익명 계정에 연결된 사용자 ID만으로 연결하게 됩니다. 응용 프로그램에서 추가 ID 관리를 요구하는 경우, 다른 인증 방법 중 하나를 선택하거나 사용자의 ID 관리 솔루션으로 보완해야 할 수 있습니다.  
  
 기본 및 익명 인증은 HTTP 액세스에 대해 Analysis Services를 구성해야 사용할 수 있으며, 이때 IIS 및 msmdpump.dll을 사용하여 연결을 설정합니다. 자세한 내용은 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)을 참조하십시오.  
  
 **Stored Credentials**  
  
 대부분의 중간 계층 응용 프로그램 서비스에는 나중에 Analysis Services 또는 SQL Server 관계형 엔진 등 하위 데이터 저장소에서 데이터를 검색하는 데 사용되는 사용자 이름과 암호를 저장하는 기능이 있습니다. 즉, 저장된 자격 증명은 데이터를 가져오는 다섯 번째 방법입니다. 이 방법의 단점은 사용자 이름 및 암호를 최신으로 유지하는 데 필요한 유지 관리 비용, 그리고 연결 시 단일 ID를 사용한다는 점 등입니다. 사용자 솔루션에서 원래 호출자의 ID를 요구하는 경우에는 저장된 자격 증명을 대안으로 이용할 수 없습니다.  
  
 저장된 자격 증명에 대한 자세한 내용은 [공유 데이터 원본 만들기, 수정 및 삭제&#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) 및 [SharePoint Server 2013에서 보안 저장소 서비스와 함께 Excel Services 사용](http://go.microsoft.com/fwlink/?LinkID=309869)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [전송 보안을 통해 가장 사용](http://go.microsoft.com/fwlink/?LinkId=311727)   
 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Kerberos 제한된 위임에 대해 Analysis Services 구성](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Analysis Services 인스턴스에 대 한 SPN 등록](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)   
 [Analysis Services에 연결](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
