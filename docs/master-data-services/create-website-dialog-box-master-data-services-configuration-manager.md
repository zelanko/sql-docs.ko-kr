---
title: 웹 사이트 만들기 대화 상자(Master Data Services 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createsite.f1
ms.assetid: 179c9c1e-3b06-421b-b71b-1cb64d104f5e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ee0a3d6bc4acb276f1915954f0f1b540419993b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906486"
---
# <a name="create-website-dialog-box-master-data-services-configuration-manager"></a>웹 사이트 만들기 대화 상자(Master Data Services 구성 관리자)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  **웹 사이트 만들기** 대화 상자를 사용하여 로컬 컴퓨터에서 새 웹 사이트를 만들 수 있습니다. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]에서 웹 사이트를 만든 경우 해당 사이트는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램으로 구성된 루트 응용 프로그램이 있는 로컬 컴퓨터의 IIS(인터넷 정보 서비스)에 추가됩니다. 또한 새 애플리케이션 풀이 만들어지고 웹 애플리케이션이 해당 애플리케이션 풀에 배치됩니다.  
  
## <a name="web-site"></a>웹 사이트  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|**웹 사이트 이름**|웹 사이트 이름을 입력하거나 기본 이름을 사용합니다. 이 이름은 IIS에서 사이트를 식별하는 데에만 사용되는 이름이며, 웹 브라우저에서 사이트에 액세스하는 데 사용되지 않습니다.<br /><br /> 이름은 로컬 컴퓨터의 IIS에 있는 모든 사이트 간에 고유해야 합니다.|  
|**프로토콜**|**http**를 표시합니다. 클라이언트와 서버 간에 암호화된 채널을 통한 통신이 필요하지 않은 경우 HTTP(Hypertext Transfer Protocol)를 사용합니다.<br /><br /> **참고**: [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]에서는 HTTPS 사이트를 만들 수 없습니다. HTTPS는 SSL(Secure Sockets Layer)을 사용하는 HTTP 프로토콜로서, 기밀한 데이터 또는 개인 데이터를 교환하거나 사용자가 개인 정보를 전송하기 전에 서버의 ID를 확인하도록 하려는 경우에 유용합니다. 서버와 클라이언트 간에 암호화된 채널을 통해 정보를 전송해야 하는 경우 IIS 관리자와 같은 IIS 도구를 사용하여 HTTPS 바인딩으로 사이트를 구성하고 웹 사이트 바인딩을 서버 인증서와 연결해야 합니다. 이러한 작업은 웹 브라우저에서 웹 사이트를 열기 위해 반드시 필요한 작업입니다. 서버 인증서에 대한 자세한 내용은 [TechNet의](https://go.microsoft.com/fwlink/?LinkId=163220) IIS 7에서 서버 인증서 구성 [!INCLUDE[msCoName](../includes/msconame-md.md)] 을 참조하십시오.|  
|**IP 주소**|사용자가 사이트에 액세스하는 데 사용할 수 있는 IP 주소를 선택합니다. 기본적으로 **모두 할당되지 않음** 이 선택되어 있습니다. 특정 IPv4 또는 IPv6 주소를 사용해야 하는 이유가 있는 경우를 제외하고는 기본값을 사용하십시오.<br /><br /> **모두 할당되지 않음**이 선택된 경우에는 이 사이트에서 포트의 모든 IP 주소 및 사용자가 지정한 선택적 호스트 이름에 대한 요청에 응답합니다. 서버의 다른 사이트에 같은 포트의 특정 IP 주소에 대한 바인딩이 있는 경우 이 사이트는 해당 포트와 특정 IP 주소에 대한 HTTP 요청을 받으며, IP 주소가 **모두 할당되지 않음** 으로 설정된 사이트는 해당 포트와 다른 IP 주소에 대한 다른 모든 HTTP 요청을 받습니다.|  
|**포트**|이 웹 사이트에 대해 요청이 수행되는 포트를 입력합니다. HTTP 프로토콜을 선택하는 경우 기본 포트는 80입니다. 기본 포트와 다른 포트를 지정한 경우 웹 사이트에 연결하려면 클라이언트에서 포트 번호를 지정해야 합니다.<br /><br /> **참고**: IIS의 **기본 웹 사이트**는 할당되지 않은 모든 IP 주소에 포트 80의 HTTP 프로토콜을 사용하도록 구성됩니다. 기본 바인딩 정보를 사용하여 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 에서 웹 사이트를 만들려고 하면 중복된 바인딩이 있다는 오류가 나타납니다. 이 경우 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]에서 사이트에 대한 바인딩 정보를 변경하거나 IIS 관리자와 같은 IIS 도구를 사용하여 기본 웹 사이트에 대한 바인딩 정보를 변경해야 합니다. 또는 IIS에서 웹 사이트를 고유하게 식별할 수 있는 호스트 헤더를 지정할 수 있습니다. 방화벽은 지정한 포트를 통한 트래픽을 허용하도록 구성해야 합니다.|  
|**호스트 헤더**|선택 값. 호스트 헤더 이름을 입력합니다. 이 옵션은 단일 IP 주소 또는 포트를 사용하는 컴퓨터에 도메인 이름이라고도 하는 호스트 이름을 할당하려는 경우에 사용합니다. 호스트 이름을 지정하면 클라이언트에서 IP 주소 대신 해당 이름을 사용하여 웹 사이트에 액세스해야 합니다. 호스트 이름을 구성한 경우에는 DNS 서버에 해당 호스트 이름에 대한 항목이 있어야 웹 브라우저에서 사이트를 열 수 있습니다.<br /><br /> 예를 들어 사용자가 `https://www.contoso.com/` 에서 사이트에 액세스하려고 하면 www.contoso.com 을 호스트 이름으로 지정하고 DNS 서버에 이 호스트 이름에 대한 항목이 있어야 합니다.<br /><br /> 인트라넷에서 웹 사이트를 사용할 수 있는 경우에는 호스트 이름을 지정하지 않아도 사용자가 브라우저에서 서버 이름(예: `https://server_name`)을 입력할 수 있습니다. 그러나 해당 환경의 DNS 서버가 이 웹 서버의 다른 이름을 저장하도록 구성된 경우에는 사용자가 DNS 서버에 의해 저장되는 다른 이름을 사용할 수 있도록 각 호스트 이름에 대해 별도의 바인딩을 만들 수 있습니다. 사이트에 대한 호스트 이름을 두 개 이상 구성해야 하는 경우에는 IIS 관리자와 같은 IIS 도구를 사용하여 다른 사이트 바인딩을 추가할 수 있습니다.|  
  
## <a name="application-pool"></a>애플리케이션 풀  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|**이름**|새 애플리케이션 풀의 고유 이름을 입력하거나 제공된 기본 이름을 사용합니다. 이 웹 사이트의 루트 웹 애플리케이션은 이 애플리케이션 풀에서 실행됩니다.<br /><br /> 애플리케이션 풀은 한 애플리케이션 풀의 애플리케이션이 다른 애플리케이션 풀의 애플리케이션에 영향을 주지 못하도록 하는 경계를 제공합니다.|  
|**사용자 이름**|Active Directory의 도메인 및 사용자 이름을 입력합니다. 이 계정은 웹 애플리케이션이 실행되는 애플리케이션 풀의 ID입니다.<br /><br /> 이 계정은 데이터베이스 액세스를 위해 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 mds_exec 데이터베이스 역할에 추가됩니다. 자세한 내용은 [데이터베이스 로그인, 사용자 및 역할&#40;Master Data Services&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md)을 참조하세요. 또한 이 계정은 파일 시스템의 임시 컴파일 디렉터리인 **MDSTempDir**에 대한 사용 권한이 부여되는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Windows 그룹인 **MDS_ServiceAccounts**에 추가됩니다. 자세한 내용은 [폴더 및 파일 사용 권한&#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md)을 참조하세요.|  
|**암호**|지정된 사용자 계정의 암호를 입력합니다.|  
|**암호 확인**|지정된 사용자 계정의 암호를 다시 입력합니다. **암호** 필드와 **암호 확인** 필드에는 같은 암호를 입력해야 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [웹 구성 페이지&#40;Master Data Services 구성 마법사&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Master Data Services 설치 및 구성](../master-data-services/master-data-services-installation-and-configuration.md)[웹 애플리케이션 요구 사항&#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [마스터 데이터 관리자 웹 애플리케이션 만들기&#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
