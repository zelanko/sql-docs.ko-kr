---
title: Windows 서비스 계정 및 권한 구성 | Microsoft Docs
ms.custom: ''
ms.date: 05/28/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- startup service states [SQL Server]
- Setup [SQL Server], user accounts
- Windows permissions [SQL Server]
- modifying user accounts
- default accounts
- domains [SQL Server], user accounts
- startup accounts [SQL Server]
- system accounts [SQL Server]
- services [SQL Server], permissions
- ACL (access control list)
- local system accounts [SQL Server]
- instance-aware services [SQL Server]
- permissions [SQL Server], services
- SQL Server Agent service, user accounts
- Windows NT permissions [SQL Server]
- user accounts [SQL Server]
- identifying instance-unaware services [SQL Server]
- installing SQL Server, user accounts
- disabled startup state [SQL Server]
- user accounts [SQL Server], users
- Local Service account [SQL Server]
- SQL Server Installation Wizard
- instance-unaware services [SQL Server]
- services [SQL Server], configuring at installation
- Windows accounts [SQL Server]
- SQL Server services, user accounts
- user accounts [SQL Server], services
- MSSQLServer
- identifying instance-aware services [SQL Server]
- services [SQL Server], accounts
- access control lists
- optional accounts [SQL Server]
- service accounts [SQL Server]
- accounts [SQL Server], services
- built-in system accounts [SQL Server]
- automatic startup state
- domains [SQL Server]
- manual startup state [SQL Server]
- accounts [SQL Server], user
ms.assetid: 309b9dac-0b3a-4617-85ef-c4519ce9d014
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e6215199f10eeec216d1a701755b49b12f576a69
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893160"
---
# <a name="configure-windows-service-accounts-and-permissions"></a>Windows 서비스 계정 및 권한 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 각 서비스는 Windows를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업의 인증을 관리하는 프로세스 또는 프로세스 집합을 나타냅니다. 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이 릴리스에서 기본 서비스 구성과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 그리고 설치 후에 설정할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 구성 옵션에 대해 설명합니다. 이 항목에서는 고급 사용자가 서비스 계정의 세부 정보를 파악하는 데 도움이 되는 정보를 제공합니다.  
  
 대부분의 서비스와 해당 속성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 구성할 수 있습니다. Windows가 C 드라이브에 설치되어 있는 경우 최신 4개 버전의 경로는 다음과 같습니다.  
  
|||  
|-|-|  
|SQL Server 2017|C:\Windows\SysWOW64\SQLServerManager14.msc| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  

##  <a name="Service_Details"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 설치되는 서비스  
 사용자가 설치하도록 선택한 구성 요소에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서는 다음 서비스를 설치합니다.  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 서비스** - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 서비스입니다. 실행 파일 경로는 \<MSSQLPATH>\MSSQL\Binn\sqlservr.exe입니다.  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트** - 작업을 실행하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 모니터링하고 경고를 발생시키고 일부 관리 태스크의 자동화를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 제공되지만 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]인스턴스에서 해제됩니다. 실행 파일 경로는 \<MSSQLPATH>\MSSQL\Binn\sqlagent.exe입니다.  
  
-   **[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]**  - 비즈니스 인텔리전스 애플리케이션을 위한 OLAP(온라인 분석 처리) 및 데이터 마이닝 기능을 제공합니다. 실행 파일 경로는 \<MSSQLPATH>\OLAP\Bin\msmdsrv.exe입니다.  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  - 보고서를 관리, 실행, 작성, 예약 및 배달합니다. 실행 파일 경로는 \<MSSQLPATH>\Reporting Services\ReportServer\Bin\ReportingServicesService.exe입니다.  
  
-   **[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]**  - [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 스토리지 및 실행을 위한 관리를 지원합니다. 실행 파일 경로는 \<MSSQLPATH>\130\DTS\Binn\MsDtsSrvr.exe입니다.  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser** - 클라이언트 컴퓨터에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 정보를 제공하는 이름 확인 서비스입니다. 실행 경로는 c:\Program Files (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe입니다.  
  
-   **전체 텍스트 검색** - 구조화 또는 반구조화된 데이터의 내용 및 속성에 대한 전체 텍스트 인덱스를 생성하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 문서 필터링 및 단어 분리를 제공합니다.  
  
-   **SQL 기록기** - 백업 및 복원 애플리케이션이 VSS(볼륨 섀도 복사본 서비스) 프레임워크에서 작동할 수 있도록 합니다.
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller** - 여러 Distributed Replay Client 컴퓨터 간의 추적 재생 오케스트레이션을 제공합니다.  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client** - [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 대해 동시 작업을 시뮬레이션하기 위해 Distributed Replay Controller와 함께 작동하는 하나 이상의 Distributed Replay Client 컴퓨터입니다.  
  
-   **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]** - R Services 또는 Machine Learning Services의 일부로 설치된 R 또는 Python 런타임과 같이 Microsoft에서 제공하는 외부 실행 파일을 호스트하는 신뢰할 수 있는 서비스입니다. 위성 프로세스는 실행 패드 프로세스를 통해 시작할 수 있지만 해당 리소스는 개별 인스턴스의 구성에 따라 제어됩니다. 실행 패드 서비스는 자체 사용자 계정에서 실행되며 등록된 특정 런타임에 대한 각 위성 프로세스는 실행 패드의 사용자 계정을 상속합니다. 위성 프로세스는 실행 시간 동안 요청 시에 생성되고 소멸됩니다.

    실행 패드는 도메인 컨트롤러로도 사용되는 컴퓨터에 SQL Server를 설치하는 경우 사용하는 계정을 만들 수 없습니다. 따라서 R Services(데이터베이스 내) 또는 Machine Learning Services(데이터베이스 내)의 설치는 도메인 컨트롤러에서 실패합니다.

  
 - **SQL Server PolyBase 엔진** - 외부 데이터 원본에 분산 쿼리 기능을 제공합니다.
 
 - **SQL Server PolyBase 데이터 이동 서비스** - PolyBase 스케일 아웃 그룹의 SQL Server와 외부 데이터 원본 간에 데이터 이동을 가능하게 합니다.
  
##  <a name="Serv_Prop"></a> 서비스 속성 및 구성

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작하고 실행하는 데 사용되는 시작 계정은 [도메인 사용자 계정](#Domain_User), [로컬 사용자 계정](#Local_User), [관리 서비스 계정](#MSA), [가상 계정](#VA_Desc)또는 [기본 제공 시스템 계정](#Local_Service)일 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 각 서비스를 시작하고 실행하려면 설치 중에 구성된 시작 계정이 있어야 합니다.
  
 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 시작하기 위해 구성할 수 있는 계정, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 사용되는 기본값, 서비스별 SID의 개념, 시작 옵션, 방화벽 구성에 대해 설명합니다.  
  
-   [기본 서비스 계정](#Default_Accts)  
  
-   [자동 시작](#Auto_Start)  
  
-   [서비스 시작 유형 구성](#Configure_services)  
  
-   [방화벽 포트](#Firewall)  
  
###  <a name="Default_Accts"></a> 기본 서비스 계정

다음 표에서는 모든 구성 요소를 설치할 때 설치 프로그램에서 사용되는 기본 서비스 계정을 보여 줍니다. 나열된 기본 계정은 특별한 설명이 있는 경우를 제외하고는 권장되는 계정입니다.
  
 **독립 실행형 서버 또는 도메인 컨트롤러**
  
|구성 요소|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|Windows 7 및 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 이상|  
|---------------|------------------------------------|----------------------------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|[네트워크 서비스](#Network_Service)|[가상 계정](#VA_Desc)*|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트|[네트워크 서비스](#Network_Service)|[가상 계정](#VA_Desc)*|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|[네트워크 서비스](#Network_Service)|[가상 계정](#VA_Desc)\* \*\*|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[네트워크 서비스](#Network_Service)|[가상 계정](#VA_Desc)\*|  
|[!INCLUDE[ssRS](../../includes/ssrs.md)]|[네트워크 서비스](#Network_Service)|[가상 계정](#VA_Desc)\*|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|[네트워크 서비스](#Network_Service)|[가상 계정](#VA_Desc)\*|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|[네트워크 서비스](#Network_Service)|[가상 계정](#VA_Desc)\*|  
|전체 텍스트 검색 FD 표시 아이콘|[로컬 서비스](#Local_Service)|[가상 계정](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 브라우저|[로컬 서비스](#Local_Service)|[로컬 서비스](#Local_Service)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer|[로컬 시스템](#Local_System)|[로컬 시스템](#Local_System)|  
|[!INCLUDE[rsql_extensions](../../includes/rsql-extensions-md.md)]|NTSERVICE\MSSQLLaunchpad|NTSERVICE\MSSQLLaunchpad|  
|PolyBase 엔진  |[네트워크 서비스](#Network_Service) |[네트워크 서비스](#Network_Service)  |
|PolyBase 데이터 이동 서비스 |[네트워크 서비스](#Network_Service) |[네트워크 서비스](#Network_Service)  |
  
 \*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 대한 외부 리소스가 필요한 경우에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)]의 권장 사항에 따라 필요한 최소 권한으로 구성된 MSA(관리 서비스 계정)를 사용하는 것이 좋습니다.   
 \*\* 도메인 컨트롤러에 설치하면 가상 계정이 서비스 계정으로 지원되지 않습니다.
  
 **SQL Server 장애 조치(Failover) 클러스터 인스턴스**
  
|구성 요소|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2|  
|---------------|------------------------------------|---------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|없음 [도메인 사용자](#Domain_User) 계정을 제공합니다.|[도메인 사용자](#Domain_User) 계정을 제공합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트|없음 [도메인 사용자](#Domain_User) 계정을 제공합니다.|[도메인 사용자](#Domain_User) 계정을 제공합니다.|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|없음 [도메인 사용자](#Domain_User) 계정을 제공합니다.|[도메인 사용자](#Domain_User) 계정을 제공합니다.|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[네트워크 서비스](#Network_Service)|[가상 계정](#VA_Desc)|  
|[!INCLUDE[ssRS](../../includes/ssrs.md)]|[네트워크 서비스](#Network_Service)|[가상 계정](#VA_Desc)|  
|전체 텍스트 검색 FD 표시 아이콘|[로컬 서비스](#Local_Service)|[가상 계정](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 브라우저|[로컬 서비스](#Local_Service)|[로컬 서비스](#Local_Service)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer|[로컬 시스템](#Local_System)|[로컬 시스템](#Local_System)|  

####  <a name="Changing_Accounts"></a> 계정 속성 변경
  
> [!IMPORTANT]
>  -   항상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 사용되는 계정을 변경하거나 계정의 암호를 변경할 수 있습니다. 계정 이름을 변경하는 것 외에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 서비스 마스터 키를 보호하는 Windows 로컬 보안 저장소 업데이트와 같은 추가 구성을 수행합니다. Windows 서비스 제어 관리자와 같은 다른 도구를 사용하면 계정 이름을 변경할 수 있지만 모든 필수 설정을 변경할 수 없습니다.  
> -   SharePoint 팜에 배포한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 경우 항상 SharePoint 중앙 관리를 사용하여 [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] 애플리케이션 및 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]에 대한 서버 계정을 변경합니다. 관련 설정 및 사용 권한은 중앙 관리를 사용할 때 새로운 계정 정보를 사용할 수 있도록 업데이트됩니다.  
> -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 옵션을 변경하려면 Reporting Services 구성 도구를 사용합니다.  
  
###  <a name="New_Accounts"></a> 관리 서비스 계정, 그룹 관리 서비스 계정 및 가상 계정  
  
관리 서비스 계정, 그룹 관리 서비스 계정 및 가상 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 같은 중요한 애플리케이션에 고유 계정에 대한 격리성을 제공하도록 설계되었습니다. 따라서 관리자는 이러한 계정에 대한 SPN(서비스 사용자 이름)과 자격 증명을 수동으로 관리할 필요가 없습니다. 결국 서비스 계정 사용자, 암호 및 SPN을 보다 쉽게 장기적으로 관리할 수 있습니다.  
  
-   <a name="MSA"></a> **Managed Service Accounts**  
  
     MSA(관리 서비스 계정)는 도메인 컨트롤러에서 만들어지고 관리되는 도메인 유형입니다. 관리 서비스 계정은 단일 멤버 컴퓨터에서 서비스를 실행하는 데 사용할 수 있도록 할당됩니다. 암호는 도메인 컨트롤러에서 자동으로 관리됩니다. 사용자는 MSA를 사용하여 컴퓨터에 로그인할 수 없지만 컴퓨터는 MSA를 사용하여 Windows 서비스를 시작할 수 있습니다. MSA에는 servicePrincipalName 읽기 및 쓰기 권한이 있을 때 Active Directory 안에서 SPN(서비스 사용자 이름)을 등록하는 기능이 있습니다. MSA는 **$** 접미사를 사용하여 이름이 지정됩니다(예: **DOMAIN\ACCOUNTNAME$** ). MSA를 지정할 때는 암호를 비워 둡니다. MSA는 단일 컴퓨터에 할당되기 때문에 Windows 클러스터의 다른 노드에서 사용할 수 없습니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대해 MSA를 사용할 수 있으려면 먼저 도메인 관리자가 Active Directory에서 MSA를 만들어야 합니다.  
  
-  <a name="GMSA"></a> **그룹 관리 서비스 계정**  
  
     그룹 관리 서비스 계정은 여러 서버의 MSA입니다. Windows는 서버 그룹에서 실행되는 서비스에 대한 서비스 계정을 관리합니다. Active Directory는 서비스를 다시 시작하지 않고 그룹 관리 서비스 계정 암호를 자동으로 업데이트합니다. 그룹 관리 서비스 계정 보안 주체를 사용하도록 SQL Server 서비스를 구성할 수 있습니다. SQL Server 2014부터 SQL Server은 독립 실행형 인스턴스의 경우 그룹 관리 서비스 계정을 지원하고, 장애 조치 클러스터 인스턴스 및 가용성 그룹의 경우 SQL Server 2016 이상을 지원합니다.  
  
    SQL Server 2014 이상에 대해 그룹 관리 서비스 계정을 사용하려면 운영 체제가 Windows Server 2012 R2 이상이어야 합니다. Windows Server 2012 R2를 실행하는 서버의 경우 암호 변경 후 중단 없이 즉시 서비스가 로그인할 수 있도록 [KB 2998082](https://support.microsoft.com/kb/2998082) 를 적용해야 합니다.  
  
    자세한 내용은 [그룹 관리 서비스 계정](https://technet.microsoft.com/library/hh831782.aspx)을 참조하세요.  
      
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대해 그룹 관리 서비스 계정을 사용할 수 있으려면 먼저 도메인 관리자가 Active Directory에서 해당 계정을 만들어야 합니다.  
  
-   <a name="VA_Desc"></a>**Virtual Accounts**  
  
    (Windows Server 2008 R2 및 Windows 7부터) 가상 계정은 서비스 관리를 간소화하기 위해 다음과 같은 기능들을 제공하는 *관리 로컬 계정* 입니다. 가상 계정은 자동으로 관리되며 도메인 환경에서 네트워크에 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 동안 서비스 계정에 기본값을 사용하는 경우 인스턴스 이름을 서비스 이름으로 사용하는 가상 계정이 **NT SERVICE\\** _\<SERVICENAME>_ 형식으로 사용됩니다. 가상 계정으로 실행되는 서비스는 *<domain_name>* __\\__ *<computer_name>* __$__ 형식으로 된 컴퓨터 계정의 자격 증명을 사용하여 네트워크 리소스에 액세스합니다.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작하는 가상 계정을 지정할 때는 암호를 비워 둡니다. 가상 계정을 사용하여 SPN(서비스 사용자 이름)을 등록할 수 없는 경우 SPN을 수동으로 등록합니다. SPN을 수동으로 등록하는 방법에 대한 자세한 내용은 [SPN 수동 등록](register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.  
  
    > [!NOTE]  
    >  가상 계정은 클러스터의 각 노드에서 SID가 동일하지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스에 대해 사용할 수 없습니다.  
  
     다음 표에서는 가상 계정 이름 예를 보여 줍니다.  
  
    |서비스|가상 계정 이름|  
    |-------------|--------------------------|  
    |[!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스의 기본 인스턴스|**NT SERVICE\MSSQLSERVER**|  
    |[!INCLUDE[ssDE](../../includes/ssde-md.md)] 로 이름이 지정된 **로 이름이 지정된**서비스의 명명된 인스턴스|**NT SERVICE\MSSQL$PAYROLL**|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스(기본 인스턴스: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|**NT SERVICE\SQLSERVERAGENT**|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PAYROLL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 이름이 지정된 **로 이름이 지정된**|**NT SERVICE\SQLAGENT$PAYROLL**|  
  
 관리 서비스 계정 및 가상 계정에 대한 자세한 내용은 **서비스 계정 단계별 가이드** 의 [관리 서비스 계정 및 가상 계정 개념](https://technet.microsoft.com/library/dd548356\(WS.10\).aspx) 섹션과 [관리 서비스 계정 FAQ(질문과 대답)](https://technet.microsoft.com/library/ff641729\(WS.10\).aspx)를 참조하세요.  
  
 **보안 정보:** [!INCLUDE[ssNoteLowRights](../../includes/ssnotelowrights-md.md)] 가능하다면 [MSA](#MSA) 또는 [가상 계정](#VA_Desc)을 사용하세요. MSA 및 가상 계정을 사용할 수 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대해 공유 계정 대신 권한이 낮은 특정 사용자 계정 또는 도메인 계정을 사용하십시오. 서로 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대해서는 각각 별도의 계정을 사용하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정 또는 서비스 그룹에 추가 권한을 부여하지 마세요. 권한은 그룹 멤버 자격을 통해 부여되거나 서비스 SID에 직접 부여됩니다(서비스 SID가 지원되는 경우).  
  
###  <a name="Auto_Start"></a> 자동 시작

모든 서비스에는 사용자 계정 외에 다음과 같이 사용자가 제어할 수 있는 3가지 시작 상태가 있습니다.
  
-   **사용 안 함** 서비스가 설치되어 있지만 현재 실행되지 않습니다.  
  
-   **수동** 서비스가 설치되어 있지만 다른 서비스 또는 애플리케이션이 해당 기능을 필요로 하는 경우에만 시작됩니다.  
  
-   **자동** 운영 체제에서 서비스를 자동으로 시작합니다.  
  
 설치하는 동안 시작 상태가 선택됩니다. 명명된 인스턴스를 설치할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 자동으로 시작되도록 설정해야 합니다.  
  
###  <a name="Configure_services"></a> 무인 설치 중 서비스 구성

다음 표에서는 설치 중에 구성할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 보여 줍니다. 무인 설치의 경우 구성 파일 또는 명령 프롬프트에서 스위치를 사용할 수 있습니다.  
  
|SQL Server 서비스 이름|무인 설치용 스위치\*|  
|-----------------------------|---------------------------------------------|  
|MSSQLSERVER|SQLSVCACCOUNT, SQLSVCPASSWORD, SQLSVCSTARTUPTYPE|  
|SQLServerAgent\*\*|AGTSVCACCOUNT, AGTSVCPASSWORD, AGTSVCSTARTUPTYPE|  
|MSSQLServerOLAPService|ASSVCACCOUNT, ASSVCPASSWORD, ASSVCSTARTUPTYPE|  
|ReportServer|RSSVCACCOUNT, RSSVCPASSWORD, RSSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|ISSVCACCOUNT, ISSVCPASSWORD, ISSVCSTARTUPTYPE|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|DRU_CTLR, CTLRSVCACCOUNT,CTLRSVCPASSWORD, CTLRSTARTUPTYPE, CTLRUSERS|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|DRU_CLT, CLTSVCACCOUNT, CLTSVCPASSWORD, CLTSTARTUPTYPE, CLTCTLRNAME, CLTWORKINGDIR, CLTRESULTDIR|  
|R Services 또는 Machine Learning Services|EXTSVCACCOUNT, EXTSVCPASSWORD, ADVANCEDANALYTICS\*\*\*|
|PolyBase 엔진| PBENGSVCACCOUNT, PBENGSVCPASSWORD, PBENGSVCSTARTUPTYPE, PBDMSSVCACCOUNT,PBDMSSVCPASSWORD, PBDMSSVCSTARTUPTYPE, PBSCALEOUT, PBPORTRANGE
  
 \*무인 설치에 대한 자세한 내용과 샘플 구문은 [명령 프롬프트에서 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.  
  
 \*\* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 및 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] Advanced Services 인스턴스에서 사용할 수 없습니다.

 \*\*\*스위치를 통한 실행 패드에 대한 계정 설정은 현재 지원되지 않습니다. SQL Server 구성 관리자를 사용하여 계정 및 다른 서비스 설정을 변경합니다.

###  <a name="Firewall"></a> 방화벽 포트

대부분의 경우 처음 설치할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 와 동일한 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 같은 도구를 사용하여 연결할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 Windows 방화벽의 포트를 열지 않습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 TCP 포트에서 수신 대기하도록 구성하고 Windows 방화벽에서 적합한 연결 포트를 열지 않으면 다른 컴퓨터에서 연결할 수 없습니다. 자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
##  <a name="Serv_Perm"></a> 서비스 권한

이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 서비스별 SID에 대해 구성하는 사용 권한에 대해 설명합니다.  
  
-   [서비스 구성 및 액세스 제어](#Serv_SID)  
  
-   [Windows 사용 권한 및 권한](#Windows)  
  
-   [SQL Server 서비스별 SID 또는 SQL Server 로컬 Windows 그룹에 부여된 파일 시스템 권한](#Reviewing_ACLs)  
  
-   [다른 Windows 사용자 계정 또는 그룹에 부여된 파일 시스템 권한](#File_System_Other)  
  
-   [비정상적인 디스크 위치와 관련된 파일 시스템 권한](#Unusual_Locations)  
  
-   [추가 고려 사항 검토](#Review_additional_considerations)  
  
-   [레지스트리 권한](#Registry)  
  
-   [WMI](#WMI)  
  
-   [명명된 파이프](#Pipes)  
  
###  <a name="Serv_SID"></a> 서비스 구성 및 액세스 제어

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 각 서비스에 대해 서비스별 SID로 서비스 격리 및 철저한 방어 기능을 제공하도록 지원합니다. 서비스별 SID는 서비스 이름에서 파생되며 서비스마다 고유합니다. 예를 들어 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스에 대한 서비스 SID는 **NT Service\MSSQL$** _\<InstanceName>_ 일 수 있습니다. 서비스 격리는 높은 권한 수준의 계정에서 실행되거나 개체의 보안을 약화시키지 않고도 특정 개체에 액세스할 수 있도록 해줍니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스는 서비스 SID가 포함된 액세스 제어 항목을 사용하여 해당 리소스에 대한 액세스를 제한할 수 있습니다.
  
> [!NOTE]  
>  Windows 7 및 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2(이후 버전)에서 서비스별 SID는 서비스에서 사용되는 가상 계정일 수 있습니다.
  
 대부분의 구성 요소에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 서비스별 계정에 대한 ACL을 직접 구성하므로 리소스 ACL 프로세스를 반복할 필요 없이 서비스 계정 변경을 수행할 수 있습니다.
  
 [!INCLUDE[ssAS](../../includes/ssas-md.md)]를 설치하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스에 대한 서비스별 SID가 만들어집니다. 로컬 Windows 그룹은 **SQLServerMSASUser$** _computer_name_ **$** _instance_name* 형식의 이름으로 만들어집니다. 서비스별 SID **NT SERVICE\MSSQLServerOLAPService** 에 로컬 Windows 그룹의 멤버 자격이 부여되고 로컬 Windows 그룹에는 ACL의 적합한 권한이 부여됩니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스를 시작하는 데 사용된 계정이 변경된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자가 일부 Windows 사용 권한(예: 서비스로 로그온 권한 등)을 변경해야 하지만 로컬 Windows 그룹에 부여된 사용 권한은 서비스별 SID가 변경되지 않았기 때문에 업데이트 없이도 계속 사용할 수 있습니다. 이 방식에 따라 업그레이드 중에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스의 이름을 바꿀 수 있습니다.
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스에 대한 로컬 Windows 그룹을 만듭니다. 이러한 서비스에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 로컬 Windows 그룹에 대한 ACL을 구성합니다.  
  
 서비스 구성에 따라 설치 또는 업그레이드 중 서비스 또는 서비스 SID에 대한 서비스 계정이 서비스 그룹의 멤버로 추가됩니다.
  
###  <a name="Windows"></a> Windows 사용 권한 및 권한  
 서비스를 시작하도록 할당된 계정은 해당 서비스에 대해 **시작, 중지 및 일시 중지 권한** 이 필요합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 이를 자동으로 할당합니다.  먼저 RSAT(원격 서버 관리 도구)를 설치하세요. [Windows 7 원격 서버 관리 도구](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=7d2f6ad7-656b-4313-a005-4e344e43997d)를 참조하세요.
  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에서 사용된 서비스별 SID 또는 Windows 그룹에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 요청하는 사용 권한을 보여 줍니다.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 부여된 사용 권한|
|---------------------------------------|------------------------------------------------------------|
|**[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]:**<br /><br /> (서비스별 SID에는 모든 권한이 부여됩니다. 기본 인스턴스: **NT SERVICE\MSSQLSERVER**. 명명된 인스턴스: **NT SERVICE\MSSQL$** InstanceName.)|**서비스로 로그온** (SeServiceLogonRight)<br /><br /> **프로세스 수준 토큰 바꾸기** (SeAssignPrimaryTokenPrivilege)<br /><br /> **트래버스 검사 무시** (SeChangeNotifyPrivilege)<br /><br /> **프로세스의 메모리 할당량 조정** (SeIncreaseQuotaPrivilege)<br /><br /> SQL 기록기를 시작할 수 있는 권한<br /><br /> 이벤트 로그 서비스를 읽을 수 있는 권한<br /><br /> 원격 프로시저 호출 서비스를 읽을 수 있는 권한|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트:** \*<br /><br /> (서비스별 SID에는 모든 권한이 부여됩니다. 기본 인스턴스: **NT Service\SQLSERVERAGENT**. 명명된 인스턴스: **NT Service\SQLAGENT$** _InstanceName_ .)|**서비스로 로그온** (SeServiceLogonRight)<br /><br /> **프로세스 수준 토큰 바꾸기** (SeAssignPrimaryTokenPrivilege)<br /><br /> **트래버스 검사 무시** (SeChangeNotifyPrivilege)<br /><br /> **프로세스의 메모리 할당량 조정** (SeIncreaseQuotaPrivilege)|  
|**[!INCLUDE[ssAS](../../includes/ssas-md.md)]:**<br /><br /> (로컬 Windows 그룹에는 모든 권한이 부여됩니다. 기본 인스턴스: **SQLServerMSASUser$** _ComputerName_ **$MSSQLSERVER**. 명명된 인스턴스: **SQLServerMSASUser$** _ComputerName_ **$** _InstanceName_ . [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 인스턴스: **SQLServerMSASUser$** _ComputerName_ **$** _PowerPivot_ .)|**서비스로 로그온** (SeServiceLogonRight)<br /><br /> 테이블 형식에만 해당:<br /><br /> **프로세스 작업 집합 향상** (SeIncreaseWorkingSetPrivilege)<br /><br /> **프로세스의 메모리 할당량 조정** (SeIncreaseQuotaPrivilege)<br /><br /> **메모리의 페이지 잠금**(SeLockMemoryPrivilege) – 페이징이 전체적으로 해제된 경우에만 필요합니다.<br /><br /> 장애 조치(Failover) 클러스터 설치에만 해당:<br /><br /> **예약 우선 순위 증가** (SeIncreaseBasePriorityPrivilege)|  
|**[!INCLUDE[ssRS](../../includes/ssrs.md)]:**<br /><br /> (서비스별 SID에는 모든 권한이 부여됩니다. 기본 인스턴스: **NT SERVICE\ReportServer**. 명명된 인스턴스: **NT SERVICE\\ReportServer$** _InstanceName_ .)|**서비스로 로그온** (SeServiceLogonRight)|  
|**[!INCLUDE[ssIS](../../includes/ssis-md.md)]:**<br /><br /> (서비스별 SID에는 모든 권한이 부여됩니다. 기본 인스턴스 및 명명된 인스턴스: **NT SERVICE\MsDtsServer130**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 명명된 인스턴스에 대한 개별 프로세스가 없습니다.)|**서비스로 로그온** (SeServiceLogonRight)<br /><br /> 애플리케이션 이벤트 로그에 기록할 수 있는 권한<br /><br /> **트래버스 검사 무시** (SeChangeNotifyPrivilege)<br /><br /> **인증 후 클라이언트 가장** (SeImpersonatePrivilege)|  
|**전체 텍스트 검색:**<br /><br /> (서비스별 SID에는 모든 권한이 부여됩니다. 기본 인스턴스: **NT Service\MSSQLFDLauncher**. 명명된 인스턴스: **NT Service\ MSSQLFDLauncher$** _InstanceName_ .)|**서비스로 로그온** (SeServiceLogonRight)<br /><br /> **프로세스의 메모리 할당량 조정** (SeIncreaseQuotaPrivilege)<br /><br /> **트래버스 검사 무시** (SeChangeNotifyPrivilege)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 브라우저:**<br /><br /> (로컬 Windows 그룹에는 모든 권한이 부여됩니다. 기본 또는 명명된 인스턴스: **SQLServer2005SQLBrowserUser** _$ComputerName_ . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser에는 명명된 인스턴스에 대한 개별 프로세스가 없습니다.)|**서비스로 로그온** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS 기록기:**<br /><br /> (서비스별 SID에는 모든 권한이 부여됩니다. 기본 또는 명명된 인스턴스: **NT Service\SQLWriter**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS 기록기에는 명명된 인스턴스에 대한 개별 프로세스가 없습니다.)|SQLWriter 기록기 서비스는 모든 필수 사용 권한이 있는 LOCAL SYSTEM 계정으로 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 이 서비스에 대한 사용 권한을 검사하거나 부여하지 않습니다.| 
  |**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller:**|**서비스로 로그온** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client:**|**서비스로 로그온** (SeServiceLogonRight)|  
|**PolyBase 엔진 및 DMS**| **서비스로 로그온** (SeServiceLogonRight)  |   
|**실행 패드:**|**서비스로 로그온** (SeServiceLogonRight) <br /><br /> **프로세스 수준 토큰 바꾸기** (SeAssignPrimaryTokenPrivilege)<br /><br />**트래버스 검사 무시** (SeChangeNotifyPrivilege)<br /><br />**프로세스의 메모리 할당량 조정** (SeIncreaseQuotaPrivilege)|     
|**R Services/Machine Learning Services:** **SQLRUserGroup**(SQL 2016 및 2017)  |기본적으로 **로컬 로그온 허용** 권한이 없습니다. |   
|**Machine Learning Services** **‘모든 애플리케이션 패키지’ [AppContainer]** (SQL 2019)  |SQL Server 'Binn', R_Services 및 PYTHON_Services 디렉터리에 대한 **읽기 및 실행 권한** |   

 \*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]의 인스턴스에서 사용할 수 없습니다.  
  
###  <a name="Reviewing_ACLs"></a> SQL Server의 서비스별 SID 또는 로컬 Windows 그룹에 부여된 파일 시스템 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 리소스에 대한 액세스 권한이 있어야 합니다. 액세스 제어 목록은 서비스별 SID 또는 로컬 Windows 그룹에 대해 설정됩니다.  
  
> [!IMPORTANT]  
>  장애 조치(Failover) 클러스터 설치의 경우 공유 디스크의 리소스는 로컬 계정에 대한 ACL에 설정해야 합니다.  
  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 설정하는 ACL을 보여 줍니다.  
  
|서비스 계정 대상|파일 및 폴더|액세스 권한|  
|-------------------------|-----------------------|------------|  
|MSSQLServer|Instid\MSSQL\backup|모든 권한|  
||Instid\MSSQL\binn|읽기, 실행|  
||Instid\MSSQL\data|모든 권한|  
||Instid\MSSQL\FTData|모든 권한|  
||Instid\MSSQL\Install|읽기, 실행|  
||Instid\MSSQL\Log|모든 권한|  
||Instid\MSSQL\Repldata|모든 권한|  
||130\shared|읽기, 실행|  
||Instid\MSSQL\Template Data([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 만 해당)|읽기|  
|SQLServerAgent\*|Instid\MSSQL\binn|모든 권한|  
||Instid\MSSQL\binn|모든 권한|  
||Instid\MSSQL\Log|읽기, 쓰기, 삭제, 실행|  
||130\com|읽기, 실행|  
||130\shared|읽기, 실행|  
||130\shared\Errordumps|읽기, 쓰기|  
||ServerName\EventLog|모든 권한|  
|FTS|Instid\MSSQL\FTData|모든 권한|  
||Instid\MSSQL\FTRef|읽기, 실행|  
||130\shared|읽기, 실행|  
||130\shared\Errordumps|읽기, 쓰기|  
||Instid\MSSQL\Install|읽기, 실행|  
||Instid\MSSQL\jobs|읽기, 쓰기|  
|MSSQLServerOLAPService|130\shared\ASConfig|모든 권한|  
||Instid\OLAP|읽기, 실행|  
||Instid\Olap\Data|모든 권한|  
||Instid\Olap\Log|읽기, 쓰기|  
||Instid\OLAP\Backup|읽기, 쓰기|  
||Instid\OLAP\Temp|읽기, 쓰기|  
||130\shared\Errordumps|읽기, 쓰기|  
|SQLServerReportServerUser|Instid\Reporting Services\Log Files|읽기, 쓰기, 삭제|  
||Instid\Reporting Services\ReportServer|읽기, 실행|  
||Instid\Reportingservices\Reportserver\global.asax|모든 권한|  
||Instid\Reportingservices\Reportserver\Reportserver.config|읽기|  
||Instid\Reporting Services\reportManager|읽기, 실행|  
||Instid\Reporting Services\RSTempfiles|읽기, 쓰기, 실행, 삭제|  
||130\shared|읽기, 실행|  
||130\shared\Errordumps|읽기, 쓰기|  
|MSDTSServer100|130\dts\binn\MsDtsSrvr.ini.xml|읽기|  
||130\dts\binn|읽기, 실행|  
||130\shared|읽기, 실행|  
||130\shared\Errordumps|읽기, 쓰기|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 브라우저|130\shared\ASConfig|읽기|  
||130\shared|읽기, 실행|  
||130\shared\Errordumps|읽기, 쓰기|  
|SQLWriter|해당 없음(로컬 시스템으로 실행)||  
|사용자|Instid\MSSQL\binn|읽기, 실행|  
||Instid\Reporting Services\ReportServer|읽기, 실행, 폴더 내용 보기|  
||Instid\Reportingservices\Reportserver\global.asax|읽기|  
||Instid\Reporting Services\reportManager|읽기, 실행|  
||Instid\Reporting Services\ReportManager\pages|읽기|  
||Instid\Reporting Services\ReportManager\Styles|읽기|  
||130\dts|읽기, 실행|  
||130\tools|읽기, 실행|  
||100\tools|읽기, 실행|  
||90\tools|읽기, 실행|  
||80\tools|읽기, 실행|  
||130\sdk|읽기|  
||Microsoft SQL Server\130\Setup Bootstrap|읽기, 실행|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|\<ToolsDir>\DReplayController\Log\(빈 디렉터리)|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayController\DReplayController.exe|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayController\resources\|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayController\\{모든 dll}|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayController\DReplayController.config|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayController\IRTemplate.tdf|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayController\IRDefinition.xml|읽기, 실행, 폴더 내용 보기|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|\<ToolsDir>\DReplayClient\Log\|R읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayClient\DReplayClient.exe|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayClient\resources\|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayClient\(모든 dll)|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayClient\DReplayClient.config|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayClient\IRTemplate.tdf|읽기, 실행, 폴더 내용 보기|  
||\<ToolsDir>\DReplayClient\IRDefinition.xml|읽기, 실행, 폴더 내용 보기|  
|실행 패드|%binn|읽기, 실행|
||ExtensiblilityData|모든 권한|
||Log\ExtensibiltityLog|모든 권한|
  
 \*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트 서비스는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 및 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] Advanced Services에서 사용할 수 없습니다.  
  
 데이터베이스 파일이 사용자 정의 위치에 저장된 경우 해당 위치에 대한 서비스별 SID 액세스 권한을 부여해야 합니다. 서비스별 SID에 파일 시스템 권한 부여에 대한 자세한 내용은 [데이터베이스 엔진 액세스에 대한 파일 시스템 사용 권한 구성](../../database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md)을 참조하세요.  
  
###  <a name="File_System_Other"></a> 다른 Windows 사용자 계정 또는 그룹에 부여된 파일 시스템 권한  

기본 제공 계정 또는 기타 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 일부 액세스 제어 권한을 부여해야 할 수도 있습니다. 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 설정하는 추가 ACL을 보여 줍니다.  
  
|요구 구성 요소|계정|리소스|사용 권한|  
|--------------------------|-------------|--------------|-----------------|  
|MSSQLServer|성능 로그 사용자|Instid\MSSQL\binn|폴더 내용 보기|  
||성능 모니터 사용자|Instid\MSSQL\binn|폴더 내용 보기|  
||성능, 로그 사용자, 성능 모니터 사용자|\WINNT\system32\sqlctr130.dll|읽기, 실행|  
||관리자 전용|\\\\.\root\Microsoft\SqlServer\ServerEvents\\<sql_instance_name>\*|모든 권한|  
||관리자, 시스템|\tools\binn\schemas\sqlserver\2004\07\showplan|모든 권한|  
||사용자|\tools\binn\schemas\sqlserver\2004\07\showplan|읽기, 실행|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|\<보고서 서버 웹 서비스 계정>|*\<설치>* \Reporting Services\LogFiles|Delete<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||보고서 관리자 애플리케이션 풀 ID, [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 계정, 모든 사람|*\<설치>* \Reporting Services\ReportManager, *\<설치>* \Reporting Services\ReportManager\Pages\\\*.\*, *\<설치>* \Reporting Services\ReportManager\Styles\\\*.\*, *\<설치>* \Reporting Services\ReportManager\webctrl_client\1_0\\*.\*|읽기|  
||보고서 관리자 애플리케이션 풀 ID|*\<설치>* \Reporting Services\ReportManager\Pages\\*.\*|읽기|  
||\<보고서 서버 웹 서비스 계정>|*\<설치>* \Reporting Services\ReportServer|읽기|  
||\<보고서 서버 웹 서비스 계정>|*\<설치>* \Reporting Services\ReportServer\global.asax|전체|  
||모든 사람|*\<설치>* \Reporting Services\ReportServer\global.asax|READ_CONTROL<br /><br /> FILE_READ_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_READ_ATTRIBUTES|  
||네트워크 서비스|*\<설치>* \Reporting Services\ReportServer\ReportService.asmx|전체|  
||모든 사람|*\<설치>* \Reporting Services\ReportServer\ReportService.asmx|READ_CONTROL<br /><br /> SYNCHRONIZE FILE_GENERIC_READ<br /><br /> FILE_GENERIC_EXECUTE<br /><br /> FILE_READ_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_EXECUTE<br /><br /> FILE_READ_ATTRIBUTES|  
||ReportServer Windows 서비스 계정|*\<설치>* \Reporting Services\ReportServer\RSReportServer.config|Delete<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||모든 사람|보고서 서버 키(Instid 하이브)|값 쿼리<br /><br /> 하위 키 열거<br /><br /> 알림<br /><br /> 읽기 제어|  
||터미널 서비스 사용자|보고서 서버 키(Instid 하이브)|값 쿼리<br /><br /> 값 설정<br /><br /> 하위 키 만들기<br /><br /> 하위 키 열거<br /><br /> 알림<br /><br /> DELETE<br /><br /> 읽기 제어|  
||고급 사용자|보고서 서버 키(Instid 하이브)|값 쿼리<br /><br /> 값 설정<br /><br /> 하위 키 만들기<br /><br /> 하위 키 열거<br /><br /> 알림<br /><br /> DELETE<br /><br /> 읽기 제어|  
  
 \*WMI 공급자 네임스페이스입니다.  
  
###  <a name="Unusual_Locations"></a> 비정상적인 디스크 위치와 관련된 파일 시스템 권한  

설치 위치에 대한 기본 드라이브는 일반적으로 C 드라이브인 **시스템 드라이브**입니다. 이 섹션은 tempdb 또는 사용자 데이터베이스가 비정상적인 위치에 설치되었을 때 추가 고려 사항을 설명합니다.  
  
 **기본이 아닌 드라이브**  
  
 기본 드라이브가 아닌 로컬 드라이브에 설치된 경우 서비스별 SID는 파일 위치에 대한 액세스 권한이 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 필요한 액세스 권한을 프로비전합니다.  
  
 **네트워크 공유**  
  
 데이터베이스가 네트워크 설치된 경우 서비스 계정은 사용자의 파일 위치 및 tempdb 데이터베이스에 대한 액세스 권한이 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 네트워크 공유에 대한 액세스 권한을 프로비전할 수 없습니다. 설치 프로그램을 실행하려면 먼저 사용자가 서비스 계정의 tempdb 위치에 대한 액세스 권한을 프로비전해야 합니다. 데이터베이스를 만들기 전에 사용자가 먼저 사용자 데이터베이스 위치에 대한 액세스 권한을 프로비전해야 합니다.  
  
> [!NOTE]  
>  가상 계정은 원격 위치에 대해 인증할 수 없습니다. 모든 가상 계정에는 시스템 계정의 사용 권한이 사용됩니다. _<domain_name>_ **\\** _<computer_name>_ **$** 형식으로 시스템 계정을 프로비전합니다.  
  
###  <a name="Review_additional_considerations"></a> 추가 고려 사항 검토  

다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에서 추가 기능을 제공하는 데 필요한 권한을 보여 줍니다.  
  
|서비스/응용 프로그램|기능|필요한 권한|  
|--------------------------|-------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)|xp_sendmail을 사용하여 메일 슬롯에 씁니다.|네트워크 쓰기 권한|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 이외의 사용자를 위해 xp_cmdshell을 실행합니다.|운영 체제의 일부로 작동하며 프로세스 수준의 토큰을 교체합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트(MSSQLSERVER)|자동 재시작 기능을 사용합니다.|Administrators 로컬 그룹의 멤버여야 합니다.|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자|최적의 쿼리 성능을 위해 데이터베이스를 튜닝합니다.|처음 사용하는 경우 시스템 관리 자격 증명이 있는 사용자가 애플리케이션을 초기화해야 합니다. 초기화한 다음에는 dbo 사용자가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자를 사용하여 자신이 소유한 테이블만 튜닝할 수 있습니다. 자세한 내용은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 온라인 설명서의 "처음 사용할 때의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 튜닝 관리자 초기화"를 참조하십시오.|  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 대해 Windows 인증을 활성화하고 필요한 기본 구성, 즉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sysadmin 그룹의 구성원인지 확인합니다.  
  
###  <a name="Registry"></a> 레지스트리 권한  
 인스턴스 인식형 구성 요소인 경우 레지스트리 하이브는 **HKLM\Software\Microsoft\Microsoft SQL Server\\** _<Instance_ID>_ 아래에 생성됩니다. 예를 들면 다음과 같습니다.  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL13.MyInstance**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSASSQL13.MyInstance**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL.130**  
  
 레지스트리는 또한 인스턴스 이름과 인스턴스 ID의 매핑을 유지 관리합니다. 인스턴스 이름과 인스턴스 ID의 매핑은 다음과 같이 유지 관리됩니다.  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\SQL] "InstanceName"="MSSQL13"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\OLAP] "InstanceName"="MSASSQL13"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\RS] "InstanceName"="MSRSSQL13"**  
  
###  <a name="WMI"></a> WMI  

WMI(Windows Management Instrumentation)에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결할 수 있어야 합니다. 이를 지원하기 위해 Windows WMI 공급자의 서비스별 SID(**NT SERVICE\winmgmt**)가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 프로비전됩니다.  
  
 SQL WMI 공급자에는 다음과 같은 사용 권한이 필요합니다.  
  
-   msdb 데이터베이스에 있는 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할의 멤버 자격  
  
-   서버의**CREATE DDL EVENT NOTIFICATION** 권한  
  
-   **의** CREATE TRACE EVENT NOTIFICATION [!INCLUDE[ssDE](../../includes/ssde-md.md)]권한  
  
-   **VIEW ANY DATABASE** 서버 수준 권한  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 SQL WMI 네임스페이스를 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 SID에 읽기 권한을 부여합니다.  
  
###  <a name="Pipes"></a> 명명된 파이프  

모든 설치에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 로컬 명명된 파이프인 공유 메모리 프로토콜을 통해 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에 대한 액세스 권한을 제공합니다.  
  
##  <a name="Provisioning"></a> 프로비전  
 이 섹션에서는 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 내에서 계정이 프로비전되는 방법에 대해 설명합니다.  
  
-   [데이터베이스 엔진 프로비전](#DE_Prov)  
  
    -   [Windows 보안 주체](#Win_Principals)  
  
    -   [sa 계정](#sa)  
  
    -   [SQL Server 서비스별 SID 로그인 및 권한](#Logins)  
  
    -   [SQL Server 에이전트 로그인 및 사용 권한](#Agent)  
  
    -   [HADRON 및 SQL 장애 조치(Failover) 클러스터 인스턴스 및 사용 권한](#Hadron)  
  
    -   [SQL 기록기 및 사용 권한](#Writer)  
  
    -   [SQL WMI 및 사용 권한](#SQLWMI)  
  
-   [SSAS 프로비전](#SSAS)  
  
-   [SSRS 프로비전](#SSRS)  
  
###  <a name="DE_Prov"></a> 데이터베이스 엔진 프로비전  
 다음 계정이 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 로그인으로 추가됩니다.  
  
####  <a name="Win_Principals"></a> Windows 보안 주체  
 설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서는 적어도 하나의 사용자 계정을 **sysadmin** 고정 서버 역할의 멤버로 명명해야 합니다.  
  
####  <a name="sa"></a> sa 계정  
 **sa** 계정은 항상 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 로그인으로 제공되며 **sysadmin** 고정 서버 역할의 멤버입니다. Windows 인증만 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 설치된 경우에도( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 설정되지 않은 경우) **sa** 로그인이 제공되지만 사용할 수 없습니다. **sa** 계정을 사용하도록 설정하는 방법은 [서버 인증 모드 변경](../../database-engine/configure-windows/change-server-authentication-mode.md)을 참조하세요.  
  
####  <a name="Logins"></a> SQL Server 서비스별 SID 로그인 및 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 서비스별 SID는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 로그인으로 프로비전됩니다. 서비스별 SID 로그인은 **sysadmin** 고정 서버 역할의 멤버입니다.  
  
####  <a name="Agent"></a> SQL Server 에이전트 로그인 및 사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스의 서비스별 SID는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 로그인으로 프로비전됩니다. 서비스별 SID 로그인은 **sysadmin** 고정 서버 역할의 멤버입니다.  
  
####  <a name="Hadron"></a> [!INCLUDE[ssHADRc](../../includes/sshadrc-md.md)] 및 SQL 장애 조치(Failover) 클러스터 인스턴스 및 사용 권한  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 또는 SQL 장애 조치(Failover) 클러스터 인스턴스(SQL FCI)로 설치한 경우 **LOCAL SYSTEM** 은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 프로비전됩니다. **LOCAL SYSTEM** 로그인에는 **ALTER ANY AVAILABILITY GROUP** 권한( [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]용) 및 **VIEW SERVER STATE** 권한(SQL FCI용)이 부여됩니다.  
  
####  <a name="Writer"></a> SQL 기록기 및 사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS 기록기 서비스의 서비스별 SID는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 로그인으로 프로비전됩니다. 서비스별 SID 로그인은 **sysadmin** 고정 서버 역할의 멤버입니다.  
  
####  <a name="SQLWMI"></a> SQL WMI 및 사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 **NT SERVICE\Winmgmt** 계정을 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 로그인으로 프로비전하고 이를 **sysadmin** 고정 서버 역할에 추가합니다.  
  
#### <a name="ssrs-provisioning"></a>SSRS 프로비전  
 설치 중에 지정한 계정은 **RSExecRole** 데이터베이스 역할의 멤버로 프로비전됩니다. 자세한 내용은 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)를 참조하세요.  
  
###  <a name="SSAS"></a> SSAS 프로비전  
 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 서비스 계정 요구 사항은 서버 배포 방법에 따라 다릅니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]를 설치하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하려면 도메인 계정으로 실행하도록 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스를 구성해야 합니다. SharePoint에 기본 제공되는 관리 계정 기능을 지원하려면 도메인 계정이 필요합니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치에 대해 가상 계정과 같은 기본 서비스 계정을 제공하지 않습니다. SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 프로비전하는 방법에 대한 자세한 내용은 [파워 피벗 서비스 계정 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)을 참조하세요.  
  
 다른 모든 독립 실행형 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 설치의 경우 도메인 계정, 기본 제공 시스템 계정, 관리 계정 또는 가상 계정으로 실행하도록 서비스를 프로비전할 수 있습니다. 계정 프로비전에 대한 자세한 내용은 [서비스 계정 구성&#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/configure-service-accounts-analysis-services)을 참조하세요.  
  
 클러스터형 설치의 경우 도메인 계정 또는 기본 제공 시스템 계정을 지정해야 합니다. [!INCLUDE[ssAS](../../includes/ssas-md.md)] 장애 조치(Failover) 클러스터에는 관리 계정이나 가상 계정이 없습니다.  
  
 모든 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 설치에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 시스템 관리자를 지정해야 합니다. 관리자 권한은 Analysis Services **서버** 역할로 프로비전됩니다.  
  
###  <a name="SSRS"></a> SSRS 프로비전  
 설치 중에 지정한 계정은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 **RSExecRole** 데이터베이스 역할의 멤버로 프로비전됩니다. 자세한 내용은 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)를 참조하세요.  
  
##  <a name="Upgrade"></a> 이전 버전에서 업그레이드  
 이 섹션에서는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드하는 동안 수행되는 변경 사항에 대해 설명합니다.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에는 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 SP1, Windows Server 2012, Windows 8.0, Windows Server 2012 R2 또는 Windows 8.1이 필요합니다. 더 낮은 운영 체제 버전에서 실행되는 모든 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하기 전에 운영 체제를 업그레이드해야 합니다.  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 다음과 같은 방식으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성합니다.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 서비스별 SID의 보안 컨텍스트로 실행됩니다. 서비스별 SID에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 파일 폴더(예: DATA) 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 레지스트리 키에 대한 액세스 권한이 부여됩니다.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 서비스별 SID는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 **sysadmin** 고정 서버 역할의 멤버로 프로비전됩니다.  
  
    -   서비스별 SID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 장애 조치(Failover) 클러스터 인스턴스가 아닌 한 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 그룹에 추가됩니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스는 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 그룹에 프로비전된 상태로 유지됩니다.  
  
    -   서비스의 로컬 Windows 그룹은 이름이 **SQLServer2005MSSQLUser$** _<computer_name>_ **$** _<instance_name>_ 에서 **SQLServerMSSQLUser$** _<computer_name>_ **$** _<instance_name>_ 으로 바뀝니다. 마이그레이션된 데이터베이스의 파일 위치에는 로컬 Windows 그룹에 대한 ACE(액세스 제어 항목)가 포함됩니다. 새 데이터베이스의 파일 위치에는 서비스별 SID에 대한 ACE가 포함됩니다.  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]로부터 업그레이드하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 서비스별 SID에 대한 ACE를 보존합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스의 경우 서비스에 대해 구성된 도메인 계정의 ACE가 보존됩니다.  
  
##  <a name="Appendix"></a> 부록  
 이 섹션에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 추가 정보가 포함되어 있습니다.  
  
-   [서비스 계정에 대한 설명](#Serv_Accts)  
  
-   [인스턴스 인식형 및 인스턴스 비인식형 서비스 식별](#Identify_instance_aware_and_unaware)  
  
-   [지역화된 버전의 서비스 이름](#Localized_service_names)  
  
###  <a name="Serv_Accts"></a> 서비스 계정에 대한 설명  
 서비스 계정은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]과 같은 Windows 서비스를 시작하는 데 사용되는 계정입니다.  
  
####  <a name="Any_OS"></a> 모든 운영 체제에서 사용할 수 있는 계정  
 앞에서 설명한 새로운 [MSA](#MSA) 및 [가상 계정](#VA_Desc) 외에도 다음과 같은 계정을 사용할 수 있습니다.  
  
 <a name="Domain_User"></a> **도메인 사용자 계정**  
  
 서비스가 네트워크 서비스, 파일 공유와 같은 액세스 도메인 리소스와 상호 작용해야 하는 경우 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 다른 컴퓨터에 대한 연결된 서버 연결을 사용하는 경우 최소 권한이 부여된 도메인 계정을 사용하는 것이 좋습니다. 서버 간 작업은 많은 경우 도메인 사용자 계정으로만 수행할 수 있습니다. 이 계정은 해당 환경에서 도메인 관리자가 미리 만들어 놓아야 합니다.  
  
> [!NOTE]  
>  도메인 계정을 사용하도록 애플리케이션을 구성한 경우 애플리케이션에 대한 사용 권한을 격리시킬 수 있지만 암호를 수동으로 관리하거나 이러한 암호 관리를 위한 사용자 지정 솔루션을 만들어야 합니다. 여러 서버 애플리케이션들에서 보안 향상을 위해 이러한 전략이 사용되고 있지만 이 전략은 추가 관리 수준과 복잡성이 필요합니다. 이러한 배포에서 서비스 관리자는 Kerberos 인증에 필요한 서비스 암호 및 SPN(서비스 사용자 이름) 관리와 같은 유지 관리 태스크에 상당 시간을 소비해야 합니다. 또한 이러한 유지 관리 태스크로 인해 서비스가 중단될 수 있습니다.  
  
 <a name="Local_User"></a> **Local User Accounts**  
  
 컴퓨터가 도메인에 속하지 않은 경우에는 Windows 관리자 권한이 없는 로컬 사용자 계정을 사용하는 것이 좋습니다.  
  
 <a name="Local_Service"></a> **로컬 서비스 계정**  
  
 로컬 서비스 계정은 리소스 및 개체에 대한 액세스 권한 수준이 Users 그룹 멤버와 동일한 기본 제공 계정입니다. 이러한 액세스 제한을 통해 개별 서비스나 프로세스의 보안이 침해될 때 시스템을 보호할 수 있습니다. 로컬 서비스 계정으로 실행되는 서비스는 자격 증명이 없는 Null 세션으로 네트워크 리소스에 액세스합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 대해서는 로컬 서비스 계정이 지원되지 않습니다. 로컬 서비스는 공유 서비스이고 로컬 서비스로 실행되는 다른 모든 서비스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 시스템 관리자 액세스 권한을 갖기 때문에 해당 서비스를 실행하는 계정으로 지원되지 않습니다. 계정의 실제 이름은 **NT AUTHORITY\LOCAL SERVICE**입니다.  
  
 <a name="Network_Service"></a> **네트워크 서비스 계정**  
  
 네트워크 서비스 계정은 리소스 및 개체에 대한 액세스 권한 수준이 Users 그룹 멤버보다 높은 기본 제공 계정입니다. 네트워크 서비스 계정으로 실행되는 서비스는 _<domain_name>_ **\\** _<computer_name>_ **$** 형식으로 컴퓨터 계정의 자격 증명을 사용하여 네트워크 리소스에 액세스합니다. 계정의 실제 이름은 **NT AUTHORITY\NETWORK SERVICE**입니다.  
  
<a name="Local_System"></a> **로컬 시스템 계정**  
  
 로컬 시스템은 매우 높은 권한이 설정된 기본 계정입니다. 이 계정은 로컬 컴퓨터에 대한 확장된 권한을 가지며 네트워크에서 컴퓨터 역할을 합니다. 계정의 실제 이름은 **NT AUTHORITY\SYSTEM**입니다.  
  
###  <a name="Identify_instance_aware_and_unaware"></a> 인스턴스 인식형 및 인스턴스 비인식형 서비스 식별  
 인스턴스 인식형 서비스는 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스와 연결되며 고유한 레지스트리 하이브를 보유합니다. 각 구성 요소 또는 서비스에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 여러 개의 인스턴스 인식형 서비스 복사본을 설치할 수 있습니다. 인스턴스 비인식형 서비스는 설치된 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 사이에서 공유되며 특정 인스턴스와 연결되지 않습니다. 또한 한 번만 설치되며 함께 작동하도록 설치할 수 없습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스 인식형 서비스는 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services 인스턴스에서는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 에이전트 서비스를 사용할 수 없습니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]\*  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   전체 텍스트 검색  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스 비인식형 서비스는 다음과 같습니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 브라우저  
  
-   SQL 기록기  
  
 \*SharePoint 통합 모드의 Analysis Services는 단일 명명된 인스턴스인 '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]'으로 실행됩니다. 인스턴스 이름은 고정되어 있습니다. 다른 이름을 지정할 수 없습니다. '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]'으로 실행되는 Analysis Services 인스턴스는 각 실제 서버에 하나만 설치할 수 있습니다.  
  
###  <a name="Localized_service_names"></a> 지역화된 버전의 서비스 이름  
 다음 표에서는 각 언어 버전의 Windows에서 표시되는 서비스 이름을 보여 줍니다.  
  
|언어|로컬 서비스 이름|네트워크 서비스 이름|로컬 시스템 이름|관리자 그룹 이름|  
|--------------|----------------------------|------------------------------|---------------------------|--------------------------|  
|영어<br /><br /> 중국어(간체)<br /><br /> 중국어(번체)<br /><br /> 한국어<br /><br /> 일본어|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\SYSTEM|BUILTIN\Administrators|  
|독일어|NT-AUTORITÄT\LOKALER DIENST|NT-AUTORITÄT\NETZWERKDIENST|NT-AUTORITÄT\SYSTEM|VORDEFINIERT\Administratoren|  
|프랑스어|AUTORITE NT\SERVICE LOCAL|AUTORITE NT\SERVICE RÉSEAU|AUTORITE NT\SYSTEM|BUILTIN\Administrators|  
|이탈리아어|NT AUTHORITY\SERVIZIO LOCALE|NT AUTHORITY\SERVIZIO DI RETE|NT AUTHORITY\SYSTEM|BUILTIN\Administrators|  
|스페인어|NT AUTHORITY\SERVICIO LOC|NT AUTHORITY\SERVICIO DE RED|NT AUTHORITY\SYSTEM|BUILTIN\Administradores|  
|러시아어|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\СИСТЕМА|BUILTIN\Администраторы|  
  
## <a name="related-content"></a>관련 내용  
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
 [MDS(Master Data Services) 설치](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
