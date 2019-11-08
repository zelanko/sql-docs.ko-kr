---
title: 웹 응용 프로그램 요구 사항
ms.custom: ''
ms.date: 02/13/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- master data services
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 851452cd5170abb6328210ecb35bd95b2bb951a3
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728088"
---
# <a name="web-application-requirements-master-data-services"></a>웹 애플리케이션 요구 사항(MDS(Master Data Services))

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 은 IIS(인터넷 정보 서비스)에서 호스트하는 웹 애플리케이션입니다. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]은 IE(Internet Explorer) 9 이상에서만 사용할 수 있습니다. IE 8 이하 버전, Microsoft Edge 및 Chrome은 지원되지 않습니다.  

**IIS를 설치 및 구성하는 방법에 대한 지침은** [IIS 설치 및 구성](../../master-data-services/master-data-services-installation-and-configuration.md#InstallIIS)을 참조하세요.
  
 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 웹 애플리케이션을 만들고 구성하려면 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 를 사용합니다. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 는 로컬 컴퓨터에서 IIS를 구성하므로 초기 웹 구성 작업을 수행할 때 가장 적합합니다. 예를 들어 단일 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 애플리케이션이 있는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 환경을 구성하거나 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]의 스케일 아웃 배포에서 초기 웹 애플리케이션을 구성할 수 있습니다. IIS 도구는 스케일 아웃 배포에서 여러 웹 서버를 구성하는 등 보다 복잡한 태스크를 수행하는 데 사용됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]의 구성 요소를 설치할 모든 컴퓨터는 사용 허가를 받아야 합니다. 자세한 내용은 EULA(최종 사용자 사용권 계약)를 참조하십시오.  
  
## <a name="requirements"></a>요구 사항  
  
### <a name="operating-system"></a>운영 체제  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 설치하기 전에 다음 요구 사항을 검토하세요.    
    
-   [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서 작업하려면 클라이언트 컴퓨터에 Silverlight 5가 설치되어 있어야 합니다. 필요한 Silverlight 버전이 설치되어 있지 않으면 Silverlight이 필요한 웹 애플리케이션 영역으로 이동할 때 Silverlight를 설치하라는 메시지가 표시됩니다. Silverlight 5는 [여기](https://go.microsoft.com/fwlink/?LinkId=243096)에서 설치할 수 있습니다.  
  
### <a name="role-and-role-services"></a>역할 및 역할 서비스  
 Windows Server 2012 또는 Windows Server 2012 R2의 MMC(Microsoft Management Console)에서 **서버 관리자**를 사용하여 **웹 서버(IIS)** 역할 및 다음 필수 역할 서비스를 설치할 수 있습니다.  
 
 
> [!IMPORTANT]  
>**동적 콘텐츠 압축**은 기본적으로 사용하도록 설정됩니다. 이로 인해 CPU 사용량이 증가하지만 xml 응답 크기가 크게 줄어들고 네트워크 I/O가 저장됩니다.  자세한 내용은 **MDS&#40;Master Data Services&#41;의 새로운 기능** in [What's New in Master Data Services &#40;MDS&#41;](../../master-data-services/what-s-new-in-master-data-services-mds.md)를 참조하세요.  
  
||  
|-|  
|인터넷 정보 서비스<br /><br /> 웹 관리 도구<br /><br /> IIS 관리 콘솔<br /><br /> World Wide Web 서비스<br /><br /> 애플리케이션 개발<br /><br /> .NET 확장성 3.5<br /><br /> .NET 확장성 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> ISAPI 확장<br /><br /> ISAPI 필터<br /><br /> 일반 HTTP 기능<br /><br /> 기본 문서<br /><br /> 디렉터리 검색<br /><br /> HTTP 오류<br /><br /> 정적 콘텐츠<br /><br /> [참고: WebDAV 게시를 설치하지 마세요.]<br /><br /> 상태 및 진단<br /><br /> HTTP 로깅<br /><br /> 요청 모니터<br /><br /> 성능<br /><br /> 정적 콘텐츠 압축<br /><br /> 보안<br /><br /> 요청 필터링<br /><br /> Windows 인증|  
  
### <a name="features"></a>기능 
 Windows Server 2012 및 Windows Server 2012 R2에서 **서버 관리자** 를 사용하여 다음 필수 기능을 설치할 수 있습니다.  
  
||  
|-|  
|.NET framework 3.5(.NET 2.0 및 3.0 포함)<br /><br /> .NET Framework 4.5 Advanced Services<br /><br /> ASP.NET 4.5<br /><br /> WCF Services<br /><br /> HTTP 활성화[참고: 필수 항목입니다.]<br /><br /> TCP 포트 공유<br /><br /> Windows Process Activation Service<br /><br /> 프로세스 모델<br /><br /> .NET 환경<br /><br /> 구성 API<br/><br/>동적 콘텐츠 압축|  
  
 다음은 필수 구성 요소 서버 역할 및 기능을 추가하는 예제 PowerShell 스크립트입니다. 필수 구성 요소 서버 역할 및 기능은 환경에 따라 달라집니다.  
  
```powershell  
Install-WindowsFeature Web-Mgmt-Console, AS-NET-Framework, Web-Asp-Net, Web-Asp-Net45, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Http-Logging, Web-Request-Monitor, Web-Stat-Compression, Web-Filtering, Web-Windows-Auth, NET-Framework-Core, WAS-Process-Model, WAS-NET-Environment, WAS-Config-APIs  
  
Install-WindowsFeature Web-App-Dev, NET-Framework-45-Features -IncludeAllSubFeature -Restart  
```  
  
 PowerShell 명령에 대한 자세한 내용은 [Install-WindowsFeature](/powershell/module/servermanager/install-windowsfeature)를 참조하세요.  
  
### <a name="accounts-and-permissions"></a>계정 및 사용 권한  
  
|형식|설명|  
|----------|-----------------|  
|Windows 계정|웹 서버 컴퓨터에 로그온할 때는 Windows 역할, 역할 서비스 및 기능을 구성하고 애플리케이션 풀, 웹 사이트 및 웹 애플리케이션을 로컬 컴퓨터의 IIS에서 작성 및 관리할 수 있는 사용 권한을 가진 Windows 계정을 사용해야 합니다.|  
|서비스 계정|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 에서 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]웹 애플리케이션을 만들 경우 애플리케이션이 실행되는 애플리케이션 풀의 ID를 지정해야 합니다. 이 계정은 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스를 만들 때 지정한 서비스 계정과 다를 수 있습니다.<br /><br /> 이 ID는 도메인 사용자 계정이어야 하며 데이터베이스 액세스를 위해 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스의 mds_exec 데이터베이스 역할에 추가됩니다. 자세한 내용은 [데이터베이스 로그인, 사용자 및 역할](../../master-data-services/database-logins-users-and-roles-master-data-services.md)을 참조하세요. 또한 이 계정은 파일 시스템의 임시 컴파일 디렉터리인 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]MDSTempDir**에 대한 사용 권한이 부여되는**  Windows 그룹인 **MDS_ServiceAccounts**에 추가됩니다. 자세한 내용은 [폴더 및 파일 사용 권한&#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)을 참조하세요.|  
  
## <a name="see-also"></a>관련 항목:  
 [MDS(Master Data Services) 설치](../../master-data-services/install-windows/install-master-data-services.md)   
      
 [마스터 데이터 관리자 웹 애플리케이션 만들기&#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)   
 [웹 구성 페이지&#40;Master Data Services 구성 마법사&#41;](../../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
  
