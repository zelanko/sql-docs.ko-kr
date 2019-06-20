---
title: Master Data Services 설치 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2645ae5b16ffa4738f06e1439abac977c8e18894
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479329"
---
# <a name="install-master-data-services"></a>MDS(Master Data Services) 설치
  다음 워크플로에서는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]을 설치하고 구성하는 방법에 대한 개요를 제공합니다. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 설치는 3단계로 수행되는 프로세스입니다.  
  
-   [설치 전 태스크](#preinstall): 설치 하기 전에 시스템 요구 사항 확인 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]합니다.  
  
-   [설치 작업](#install): 설치할 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램 또는 명령 프롬프트입니다.  
  
-   [설치 후 태스크](#postinstall): 열기 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 사후 설치 작업을 완료 합니다. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스, [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 및 웹 서비스를 만들고 구성하며, 예제 모델을 배포합니다.  
  
##  <a name="preinstall"></a> 설치 전 태스크  
  
|작업|설명|관련 항목|  
|------------|-------------|--------------------|  
|설치 요구 사항 확인|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행할 컴퓨터는 다음에 대한 최소 요구 사항을 충족해야 합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램<br /><br /> [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 및 웹 서비스<br /><br /> 웹 애플리케이션과 동일한 컴퓨터에서 데이터베이스를 호스팅할 경우 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스<br /><br /> 웹 서버 컴퓨터 에서만 설치 프로그램을 실행 하 고 만들어 웹 서버 컴퓨터와 데이터베이스 서버 컴퓨터를 구분할 수 참고를 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 지원 되는 버전 및 버전을 실행 하는 원격 컴퓨터에서 데이터베이스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|[SQL Server 2014 버전에서 지원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)<br /><br /> [SQL Server 2014 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [웹 애플리케이션 요구 사항&#40;Master Data Services&#41;](web-application-requirements-master-data-services.md)<br /><br /> [데이터베이스 요구 사항&#40;Master Data Services&#41;](database-requirements-master-data-services.md)|  
|필요한 역할, 역할 서비스 및 기능 구성|설치 프로그램을 실행하기 전에 필요한 Windows 역할, 역할 서비스 및 기능으로 컴퓨터를 구성합니다.<br /><br /> 참고: 이후의 워크플로에서이 단계를 수행할 수 있습니다, 있지만 설치 직후에 웹 구성 태스크를 수행할 수 있도록 설치 프로그램이 실행 되기 전에이 구성 하는 것이 유용 합니다.|[웹 애플리케이션 요구 사항&#40;Master Data Services&#41;](web-application-requirements-master-data-services.md)|  
|언어 지원 고려 사항 검토|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 를 설치 및 실행할 언어를 결정합니다.|[다국어 및 글로벌 배포&#40;Master Data Services&#41;](multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="install"></a> 설치 작업  
  
|작업|설명|관련 항목|  
|------------|-------------|--------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램 실행|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 및 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 서비스를 호스팅할 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램 또는 명령 프롬프트를 사용하여 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 설치합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하는 경우 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 공유 기능 **의** 기능 선택 **페이지에서**를 사용할 수 있으며, 명령 프롬프트를 사용하는 경우 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 는 기능 매개 변수로 사용할 수 있습니다. 명령줄 설치 프로세스는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 설치하지만 구성하지는 않습니다. Master Data Services 구성 마법사를 사용하여 구성해야 합니다. 설치 프로세스:<br /><br /> 공유 기능에 대해 지정한 위치에 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 폴더와 파일을 설치하고 이러한 개체에 사용 권한을 할당합니다.<br /><br /> GAC(전역 어셈블리 캐시)에 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 어셈블리를 등록합니다.<br /><br /> [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]를 설치합니다.|[설치 마법사에서 SQL Server 2014를 설치 &#40;설치&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [폴더 및 파일 사용 권한&#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="postinstall"></a> 설치 후 태스크  
  
|작업|설명|관련 항목|  
|------------|-------------|--------------------|  
|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 를 열고 사후 설치 작업 완료|설치가 완료되면 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]를 엽니다. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 은 로컬 컴퓨터에서 다음과 같은 설치 후 작업을 수행합니다.<br /><br /> 애플리케이션 풀에 대한 **서비스 계정을 포함하기 위해 Windows 그룹**MDS_ServiceAccounts [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 를 만듭니다.<br /><br /> [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 설치 경로에 MDSTempDir 폴더를 만들고 **MDS_ServiceAccounts**에 대한 사용 권한을 할당합니다. 이 폴더에서는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션에 대한 임시 컴파일 파일이 컴파일됩니다.<br /><br /> 에 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web.config 파일을 구성 합니다 `tempDirectory` 특성을  **\<컴파일 >** MDSTempDir 폴더의 경로를 사용 하 여 요소.<br /><br /> <br /><br /> 설치 프로세스를 스크립팅할 경우 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]를 열어 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 스냅인을 등록할 수 있지만 구성을 완료하려면 다른 단계를 수동으로 수행해야 합니다. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]에서는 마법사 기반 구성 프로세스를 제공합니다. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]를 구성하기 위한 명령줄 프로세스는 없습니다.|[폴더 및 파일 사용 권한&#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md)<br /><br /> [웹 구성 참조&#40;Master Data Services&#41;](../web-configuration-reference-master-data-services.md)|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스 만들기|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 를 사용하여 마스터 데이터에 대한 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스를 만듭니다.|[Master Data Services 데이터베이스 만들기](create-a-master-data-services-database.md)|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 만들기|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 를 사용하여 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]를 호스팅하기 위한 웹 응용 프로그램을 만들고 구성합니다.|[마스터 데이터 관리자 웹 애플리케이션 만들기&#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스를 웹 응용 프로그램과 연결|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 를 사용하여 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램을 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스와 연결합니다.|[Master Data Services 데이터베이스와 웹 응용 프로그램 연결](associate-a-master-data-services-database-and-web-application.md)|  
|Internet Explorer 보안 강화 구성|Windows Server 2008 또는 Windows Server 2008 R2 컴퓨터에 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 를 설치하는 경우 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 애플리케이션 사이트에 대한 스크립팅을 허용하도록 Internet Explorer 보안 강화를 구성해야 할 수 있습니다. 그렇게 하지 않으면 서버 컴퓨터에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 애플리케이션 사이트로의 이동에 실패합니다.|[Internet Explorer: 보안 강화 구성](https://go.microsoft.com/fwlink/p/?LinkId=223869)|  
|설치 - [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|마스터 데이터로 작업하는 사용자는 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]를 설치할 수 있습니다.|[https://go.microsoft.com/fwlink/?LinkId=219530](https://go.microsoft.com/fwlink/?LinkId=219530)|  
|DQS(Data Quality Services) 통합 사용|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]사용자의 경우 유사 데이터를 일치시키는 데 사용할 수 있는 DQS 기능과의 통합을 사용합니다.|[Master Data Services로 Data Quality Services 통합 설정](enable-data-quality-services-integration-with-master-data-services.md)|  
|예제 모델 배포|예제 모델 패키지는 MDS(Master Data Services)와 함께 설치되며, MDSModelDeploy.exe를 사용하여 배포할 수 있습니다.|[SQL Server에 MDS 예제 배포](https://go.microsoft.com/fwlink/?LinkId=251486&clcid=0x409)|  
  
 설치 프로세스 또는 초기 구성 중에 문제가 발생한 경우 TechNet Wiki에서 [설치 및 구성 문제 해결](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) 을 참조하십시오.  
  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 가 컴퓨터에서 더 이상 필요하지 않은 경우 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 를 제거하고 제거 프로세스의 영향을 받지 않는 항목을 제거할지 여부를 결정할 수 있습니다. 자세한 내용은 [Master Data Services 제거](../../sql-server/install/uninstall-and-remove-master-data-services.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server.md)  
  
  
