---
title: 웹 애플리케이션 요구 사항(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f0e371ceef793daea080e3a588f6b87161083a6c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208483"
---
# <a name="web-application-requirements-master-data-services"></a>웹 애플리케이션 요구 사항(MDS(Master Data Services))
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 은 IIS(인터넷 정보 서비스)에서 호스트하는 웹 응용 프로그램입니다. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 만 Internet Explorer (IE) 7 이상을 사용할 수 있습니다. IE 7 이하 버전, Microsoft Edge 및 Chrome은 지원되지 않습니다.  
  
 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 웹 응용 프로그램을 만들고 구성하려면 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 를 사용합니다. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 는 로컬 컴퓨터에서 IIS를 구성하므로 초기 웹 구성 작업을 수행할 때 가장 적합합니다. 예를 들어 단일 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션이 있는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 환경을 구성하거나 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]의 스케일 아웃 배포에서 초기 웹 애플리케이션을 구성할 수 있습니다. IIS 도구는 스케일 아웃 배포에서 여러 웹 서버를 구성하는 등 보다 복잡한 태스크를 수행하는 데 사용됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 의 구성 요소를 설치할 모든 컴퓨터는 사용 허가를 받아야 합니다. 자세한 내용은 EULA(최종 사용자 사용권 계약)를 참조하십시오.  
  
## <a name="requirements"></a>요구 사항  
  
### <a name="operating-system"></a>운영 체제  
 아래 Windows 운영 체제에는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 애플리케이션 및 웹 서비스에 필요한 인터넷 정보 서비스(IIS)가 포함되어 있습니다.  
  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (64 비트) x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (64 비트) x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence(64비트) x64|  
|-------------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows 7 Professional, Enterprise 및 Ultimate<br /><br /> Windows 8.0 Professional, Enterprise 및 Ultimate|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|  
  
 버전의 지원 되는 Windows 운영 체제의 전체 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)합니다.  
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램에서 작업하려면 클라이언트 컴퓨터에 Silverlight 5가 설치되어 있어야 합니다. 필요한 Silverlight 버전이 설치되어 있지 않으면 Silverlight이 필요한 웹 애플리케이션 영역으로 이동할 때 Silverlight를 설치하라는 메시지가 표시됩니다. Silverlight 5는 [여기](http://go.microsoft.com/fwlink/?LinkId=243096)에서 설치할 수 있습니다.  
  
### <a name="role-and-role-services-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>역할 및 역할 서비스(Windows Server 2008 또는 Windows Server 2008 R2, Windows 7 운영 체제)  
 Windows Server 2008 R2의 MMC(Microsoft Management Console)에서 **서버 관리자**를 사용하여 **웹 서버(IIS)** 역할 및 다음 필수 역할 서비스를 설치할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] Windows 7 운영 체제를 사용 하 여 **프로그램 및 기능** 에서 이러한 옵션을 사용 하도록 설정 하려면 제어판에서의 **Windows 기능** 대화 상자.  
  
||  
|-|  
|웹 서버<br /><br /> 일반 HTTP 기능<br /><br /> 정적 콘텐츠<br /><br /> 기본 문서<br /><br /> 디렉터리 검색<br /><br /> HTTP 오류<br /><br /> 애플리케이션 개발<br /><br /> ASP.NET<br /><br /> .NET 확장성<br /><br /> ISAPI 확장<br /><br /> ISAPI 필터<br /><br /> 상태 및 진단<br /><br /> HTTP 로깅<br /><br /> 요청 모니터<br /><br /> 보안<br /><br /> Windows 인증<br /><br /> 요청 필터링<br /><br /> 성능<br /><br /> 정적 콘텐츠 압축<br /><br /> 관리 도구<br /><br /> IIS 관리 콘솔|  
  
### <a name="role-and-role-services-windows-server-2012-or-windows-8-operating-systems"></a>역할 및 역할 서비스(Windows Server 2012 또는 Windows 8 운영 체제)  
 Windows Server 2012의 MMC(Microsoft Management Console)에서 **서버 관리자**를 사용하여 **웹 서버(IIS)** 역할 및 다음 필수 역할 서비스를 설치할 수 있습니다.  
  
> [!NOTE]  
>  Windows 8 운영 체제의 제어판에서 **프로그램 및 기능** 을 사용하여 **Windows 기능** 대화 상자의 이러한 옵션을 사용하도록 설정할 수 있습니다.  
  
||  
|-|  
|인터넷 정보 서비스<br /><br /> 웹 관리 도구<br /><br /> IIS 관리 콘솔<br /><br /> World Wide Web 서비스<br /><br /> 애플리케이션 개발<br /><br /> .NET 확장성 3.5<br /><br /> .NET 확장성 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> ISAPI 확장<br /><br /> ISAPI 필터<br /><br /> 일반 HTTP 기능<br /><br /> 기본 문서<br /><br /> 디렉터리 검색<br /><br /> HTTP 오류<br /><br /> 정적 콘텐츠<br /><br /> [참고: WebDAV 게시를 설치하지 마세요.]<br /><br /> 상태 및 진단<br /><br /> HTTP 로깅<br /><br /> 요청 모니터<br /><br /> 성능<br /><br /> 정적 콘텐츠 압축<br /><br /> 보안<br /><br /> 요청 필터링<br /><br /> Windows 인증|  
  
### <a name="features-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>기능(Windows Server 2008 또는 Windows Server 2008 R2, Windows 7 운영 체제)  
 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 사용할 수 있습니다 Windows Server 2008 R2 **서버 관리자** 다음을 설치 하려면 필수 기능입니다.  
  
> [!NOTE]  
>  [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] Windows 7 운영 체제를 사용 하 여 **프로그램 및 기능** 에서 이러한 옵션을 사용 하도록 설정 하려면 제어판에서의 **Windows 기능** 대화 상자.  
  
||  
|-|  
|.NET Framework 3.0 기능<br /><br /> WCF 활성화<br /><br /> HTTP 활성화<br /><br /> 비 HTTP 활성화<br /><br /> Windows Process Activation Service<br /><br /> 프로세스 모델<br /><br /> .NET 환경<br /><br /> 구성 API|  
  
### <a name="features-windows-server-2012-or-windows-8-operating-systems"></a>기능(Windows Server 2012 또는 Windows 8 운영 체제)  
 Windows Server 2012에서 **서버 관리자** 를 사용하여 다음 필수 기능을 설치할 수 있습니다.  
  
> [!NOTE]  
>  Windows 8 운영 체제의 제어판에서 **프로그램 및 기능** 을 사용하여 **Windows 기능** 대화 상자의 이러한 옵션을 사용하도록 설정할 수 있습니다.  
  
||  
|-|  
|.NET framework 3.5(.NET 2.0 및 3.0 포함)<br /><br /> .NET Framework 4.5 Advanced Services<br /><br /> ASP.NET 4.5<br /><br /> WCF Services<br /><br /> HTTP 활성화[참고: 필수 항목입니다.]<br /><br /> TCP 포트 공유<br /><br /> Windows Process Activation Service<br /><br /> 프로세스 모델<br /><br /> .NET 환경<br /><br /> 구성 API|  
  
### <a name="accounts-and-permissions"></a>계정 및 사용 권한  
  
|형식|Description|  
|----------|-----------------|  
|Windows 계정|웹 서버 컴퓨터에 로그온할 때는 Windows 역할, 역할 서비스 및 기능을 구성하고 애플리케이션 풀, 웹 사이트 및 웹 애플리케이션을 로컬 컴퓨터의 IIS에서 작성 및 관리할 수 있는 사용 권한을 가진 Windows 계정을 사용해야 합니다.|  
|서비스 계정|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 에서 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]웹 응용 프로그램을 만들 경우 응용 프로그램이 실행되는 응용 프로그램 풀의 ID를 지정해야 합니다. 이 계정은 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스를 만들 때 지정한 서비스 계정과 다를 수 있습니다.<br /><br /> 이 ID는 도메인 사용자 계정이어야 하며 데이터베이스 액세스를 위해 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스의 mds_exec 데이터베이스 역할에 추가됩니다. 자세한 내용은 [데이터베이스 로그인, 사용자 및 역할&#40;Master Data Services&#41;](../database-logins-users-and-roles-master-data-services.md)을 참조하세요. 또한 이 계정은 파일 시스템의 임시 컴파일 디렉터리인 **MDSTempDir**에 대한 사용 권한이 부여되는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Windows 그룹인 **MDS_ServiceAccounts**에 추가됩니다. 자세한 내용은 [폴더 및 파일 사용 권한&#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)을 참조하세요.<br /><br /> 서버 오류가 발생하지 않도록 하기 위해 애플리케이션 풀 계정에 VIEW SERVER STATE 권한이 필요합니다. 예를 들어 서버 오류와 함께 MDS 버전 유효성 검사 명령이 실패합니다. 자세한 내용은 [SQL Server 2012 및 SQL Server 2014에서 서버 오류와 함께 MDS 버전 유효성 검사 명령 실패](http://go.microsoft.com/fwlink/p/?LinkId=526304)를 참조하세요.|  
  
## <a name="see-also"></a>관련 항목  
 [Master Data Services 설치](install-master-data-services.md)   
 [마스터 데이터 관리자 웹 응용 프로그램 만들기 &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)   
 [웹 구성 페이지&#40;Master Data Services 구성 마법사&#41;](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  
