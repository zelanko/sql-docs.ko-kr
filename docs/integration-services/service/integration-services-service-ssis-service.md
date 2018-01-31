---
title: "Integration Services 서비스(SSIS 서비스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: service
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssiseditserverregistration.connectionproperties.f1
- sql13.swb.connecttodts.connectionproperties.f1
- sql13.swb.connection.login.dtsserver.f1
- sql13.swb.connecttodts.login.f1
- sql13.swb.connecttodtsserver.login.f1
helpviewer_keywords:
- Integration Services service, about Integration Services service
- SQL Server Integration Services service
- service [Integration Services],about Integration Services service
- service [Integration Services]
- SQL Server Integration Services, service
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 06b632de9ef477e31de110f98a8fca4295144bb9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-service-ssis-service"></a>Integration Services 서비스(SSIS 서비스)
  이 섹션의 항목에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. 이 서비스는 Integration Services 패키지를 생성, 저장 및 실행하는 데 필요하지 않습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 는 이전 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 버전과의 호환성을 위한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]서비스를 지원합니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 프로젝트 배포 모델을 사용하여 **서버에 배포한 프로젝트의** SSISDB [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터베이스에 개체, 설정 및 작업 데이터를 저장합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터베이스 엔진의 인스턴스인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버는 데이터베이스를 호스팅합니다. 데이터베이스에 대한 자세한 내용은 [SSIS 카탈로그](../../integration-services/catalog/ssis-catalog.md)를 참조하세요. 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포하는 방법에 대한 자세한 내용은 [Integration Services(SSIS) 프로젝트 및 패키지 배포](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하세요.  
  
## <a name="management-capabilities"></a>관리 기능  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 관리를 위한 Windows 서비스입니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서만 사용할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 다음 관리 기능을 제공합니다.  
  
-   원격 및 로컬에 저장된 패키지 시작  
  
-   원격 및 로컬로 실행 중인 패키지 중지  
  
-   원격 및 로컬로 실행 중인 패키지 모니터링  
  
-   패키지 가져오기 및 내보내기  
  
-   패키지 저장소 관리  
  
-   저장소 폴더 사용자 지정  
  
-   서비스가 중지될 때 실행 중인 패키지 중지  
  
-   Windows 이벤트 로그 보기  
  
-   여러 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결  
  
## <a name="startup-type"></a>시작 유형
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구성 요소를 설치할 때 함께 설치됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 기본적으로 시작되며 서비스의 시작 유형은 자동으로 설정됩니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소에 저장된 패키지를 모니터링하려면 서비스가 실행되고 있어야 합니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 msdb 데이터베이스 또는 파일 시스템 내의 지정된 폴더일 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 디자인 및 실행만 하려는 경우에는 필요하지 않습니다. 하지만 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 패키지를 나열하고 모니터링하려면 이 서비스가 필요합니다.  

## <a name="manage-the-service"></a>서버 관리
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구성 요소를 설치할 때 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스도 함께 설치됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 기본적으로 시작되며 서비스의 시작 유형은 자동으로 설정됩니다. 그러나 서비스를 사용하여 저장 및 실행 중인 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 패키지를 관리하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 도 설치해야 합니다.  
  
> [!NOTE]
> 레거시 Integration Services 서비스의 인스턴스에 직접 연결하려면 Integration Services 서비스가 실행 중인 SQL Server의 버전에 맞는 SSMS(SQL Server Management Studio) 버전을 사용해야 합니다. 예를 들어 SQL Server 2016의 인스턴스에서 실행 중인 레거시 Integration Services 서비스에 연결하려면 SQL Server 2016용으로 릴리스된 SSMS의 버전을 사용해야 합니다. [SSMS(SQL Server Management Studio) 다운로드합니다](../../ssms/download-sql-server-management-studio-ssms.md).
>
>   SSMS **서버에 연결** 대화 상자에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 이전 버전을 실행 중인 서버의 이름을 입력할 수 없습니다. 그러나 원격 서버에 저장된 패키지를 관리하는 경우 해당 원격 서버에 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 인스턴스에 연결할 필요가 없습니다. 대신 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 원격 서버에 저장된 패키지를 표시하도록 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 서비스에 대한 구성 파일을 편집합니다.   
  
 컴퓨터에는 하나의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 인스턴스만 설치할 수 있습니다. 서비스는 특정 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 국한되지 않습니다. 서비스가 실행 중인 컴퓨터의 이름을 사용하여 서비스에 연결합니다.  
  
 MMC(Microsoft Management Console) 스냅인인 SQL Server 구성 관리자나 SQL Server 서비스 중 하나를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 관리할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 패키지를 관리하려면 먼저 서비스를 시작해야 합니다.  
  
 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]와 동시에 설치되는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인스턴스의 msdb 데이터베이스에 있는 패키지를 관리하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 동시에 설치되지 않는 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 로컬 기본 인스턴스에 있는 msdb 데이터베이스에 저장된 패키지를 관리하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 명명된 인스턴스나 원격 인스턴스 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 여러 인스턴스에 저장된 패키지를 관리하려면 서비스의 구성 파일을 수정해야 합니다.
  
 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 서비스를 중지할 때 패키지 실행을 중지하도록 구성되어 있습니다. 그러나 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 패키지가 중지될 때까지 기다리지 않으며 일부 패키지는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 중지된 후에도 계속 실행될 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 중지한 후에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사, [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너, 패키지 실행 유틸리티 및 **dtexec** 명령 프롬프트 유틸리티(dtexec.exe)를 사용하여 패키지를 계속 실행할 수 있습니다. 그러나 실행 중인 패키지는 모니터링할 수 없습니다.  
  
 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 NETWORK SERVICE 계정의 컨텍스트에서 실행됩니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 이벤트를 Windows 이벤트 로그에 기록합니다. 서비스 이벤트는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 볼 수 있습니다. 또한 Windows 이벤트 뷰어를 사용하여 서비스 이벤트를 볼 수도 있습니다.  
  
## <a name="set-the-properties-of-the-service"></a>서비스 속성 설정
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 패키지를 관리하고 모니터링합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 처음 설치하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 시작되고 서비스의 시작 유형이 자동으로 설정됩니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 설치된 후에는 SQL Server 구성 관리자나 서비스 MMC 스냅인을 사용하여 서비스의 속성을 설정할 수 있습니다.  
  
 서비스가 패키지를 저장하고 관리하는 위치 등 서비스의 다른 중요한 기능을 구성하려면 서비스의 구성 파일을 수정해야 합니다.
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-sql-server-configuration-manager"></a>SQL Server 구성 관리자를 사용하여 Integration Services 서비스의 속성을 설정하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, **Microsoft SQL Server**, **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
2.  **SQL Server 구성 관리자** 스냅인의 서비스 목록에서 **SQL Server Integration Services** 를 찾아 **SQL Server Integration Services**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **SQL Server Integration Services 속성** 대화 상자에서 다음을 수행할 수 있습니다.  
  
    -   **로그온** 탭을 클릭하여 계정 이름과 같은 로그온 정보를 확인합니다.  
  
    -   **서비스** 탭을 클릭하여 호스트 컴퓨터 이름과 같은 서비스에 대한 정보를 확인하고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 시작 모드를 지정합니다.  
  
        > [!NOTE]  
        >  **고급** 탭에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 정보가 들어 있지 않습니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  **파일** 메뉴에서 **끝내기** 를 클릭하여 **SQL Server 구성 관리자** 스냅인을 닫습니다.  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-services"></a>서비스를 사용하여 Integration Services 서비스의 속성을 설정하려면  
  
1.  클래식 보기를 사용할 경우에는 **제어판**에서 **관리 도구**를 클릭하고 종류별 보기를 사용할 경우에는 제어판에서 **성능 및 유지 관리** 를 클릭한 후 **관리 도구**를 클릭합니다.  
  
2.  **서비스**를 클릭합니다.  
  
3.  **서비스** 스냅인에서 서비스 목록의 **SQL Server Integration Services** 를 찾은 다음 **SQL Server Integration Services**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
4.  **SQL Server Integration Services 속성** 대화 상자에서 다음을 수행할 수 있습니다.  
  
    -   **일반** 탭을 클릭합니다. 서비스를 사용하려면 시작 유형에 수동 또는 자동을 선택합니다. 서비스를 사용하지 않으려면 **시작 유형** 상자에서 사용 안 함을 선택합니다. 사용 안 함을 선택해도 현재 실행 중인 서비스가 중지되지는 않습니다.  
  
         서비스를 이미 사용하고 있는 경우 **중지** 를 클릭하여 서비스를 중지하거나 **시작** 을 클릭하여 서비스를 시작합니다.  
  
    -   **로그온** 탭을 클릭하여 로그온 정보를 보거나 편집합니다.  
  
    -   **복구** 탭을 클릭하여 서비스 실패 시 기본 컴퓨터의 응답을 봅니다. 사용자 환경에 맞게 이러한 옵션을 수정할 수 있습니다.  
  
    -   **종속성** 탭을 클릭하여 종속 서비스 목록을 봅니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에는 종속성이 없습니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  시작 유형이 수동이거나 자동인 경우 필요에 따라 **SQL Server Integration Services** 를 마우스 오른쪽 단추로 클릭하고 **시작, 중지 또는 다시 시작**을 클릭합니다.  
  
7.  **파일** 메뉴에서 **끝내기** 를 클릭하여 **서비스** 스냅인을 닫습니다.  

## <a name="grant-permissions-to-the-service"></a>서비스에 사용 권한 부여
  이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하면 기본적으로 Users 그룹의 모든 사용자에게 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 액세스 권한이 부여되었지만 현재 릴리스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하면 사용자에게 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 액세스 권한이 부여되지 않습니다. 이 서비스에는 기본적으로 보안이 적용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치된 후 관리자가 서비스에 대한 액세스 권한을 부여해야 합니다.  
  
### <a name="to-grant-access-to-the-integration-services-service"></a>Integration Services 서비스에 대한 액세스 권한을 부여하려면  
  
1.  Dcomcnfg.exe를 실행합니다. Dcomcnfg.exe는 레지스트리의 특정 설정을 수정하는 사용자 인터페이스를 제공합니다.  
  
2.  **구성 요소 서비스** 대화 상자에서 구성 요소 서비스 > 컴퓨터 > 내 컴퓨터 > DCOM 구성 노드를 확장합니다.  
  
3.  **Microsoft SQL Server Integration Services 13.0**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **보안** 탭의 **시작 및 활성화 권한** 영역에서 **편집** 을 클릭합니다.  
  
5.  사용자를 추가하고 적절한 권한을 할당한 다음 확인을 클릭합니다.  
  
6.  액세스 권한에 대해 4-5단계를 반복합니다.  
  
7.  SQL Server Management Studio를 다시 시작합니다.  
  
8.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 다시 시작합니다.  

## <a name="configure-the-service"></a>서비스 구성
 
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치할 때 설치 프로세스는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대한 구성 파일을 만들고 설치합니다. 이 구성 파일에는 다음과 같은 설정이 들어 있습니다.  
  
-   서비스가 중지되면 패키지에 중지 명령이 전송됩니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 개체 탐색기에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 대해 표시할 루트 폴더는 MSDB와 파일 시스템 폴더입니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 관리하는 파일 시스템의 패키지는 %ProgramFiles%\Microsoft SQL Server\130\DTS\Packages에 있습니다.  
  
 이 구성 파일은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 관리할 패키지가 들어 있는 msdb 데이터베이스도 지정합니다. 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 와 동시에 설치되는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]인스턴스의 msdb 데이터베이스에 있는 패키지를 관리하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 동시에 설치되지 않는 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 로컬 기본 인스턴스에 있는 msdb 데이터베이스에 저장된 패키지를 관리하도록 구성됩니다.  
  
### <a name="default-configuration-file-example"></a>기본 구성 파일 예  
 다음 예에서는 아래의 설정을 지정하는 기본 구성 파일을 보여 줍니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 중지되면 패키지 실행도 중지됩니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 패키지 저장소에 대한 루트 폴더는 MSDB와 파일 시스템입니다.  
  
-   서비스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 기본 인스턴스에 있는 msdb 데이터베이스에 저장된 패키지를 관리합니다.  
  
-   서비스에서 파일 시스템의 패키지 폴더에 저장된 패키지를 관리합니다.  
  
 **기본 구성 파일의 예**  
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
\<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    \<Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    \<Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
### <a name="modify-the-configuration-file"></a>구성 파일 수정  
 구성 파일을 수정하여 서비스가 중지되어도 패키지가 계속 실행되게 하거나 개체 탐색기에 추가 루트 폴더를 표시하거나 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 관리할 파일 시스템의 다른 폴더 또는 추가 폴더를 지정할 수 있습니다. 예를 들어 **SqlServerFolder**유형의 추가 루트 폴더를 만들어 추가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스의 msdb 데이터베이스에 저장된 패키지를 관리할 수 있습니다.  
  
> [!NOTE]  
>  일부 문자는 폴더 이름에 적합하지 않습니다. 폴더 이름에 적합한 문자는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스 **System.IO.Path** 와 **GetInvalidFilenameChars** 필드에 의해 결정됩니다. **GetInvalidFilenameChars** 필드는 **Path** 클래스의 멤버에 전달된 경로 문자열 인수에 지정할 수 없는 플랫폼별 문자 배열을 제공합니다. 잘못된 문자 집합은 파일 시스템에 따라 달라질 수 있습니다. 일반적으로 따옴표("), 보다 작음(<) 문자 및 파이프(|) 문자가 잘못된 문자입니다.  
  
 그러나 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 명명된 인스턴스나 원격 인스턴스에 저장된 패키지를 관리하려면 구성 파일을 수정해야 합니다. 구성 파일을 업데이트하지 않으면 **의** 개체 탐색기 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 명명된 인스턴스나 원격 인스턴스의 msdb 데이터베이스에 저장된 패키지를 볼 수 있습니다. **개체 탐색기** 를 사용하여 이러한 패키지를 보려고 하면 다음과 같은 오류 메시지가 나타납니다.  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 구성 파일을 수정하려면 텍스트 편집기를 사용합니다.  
  
> [!IMPORTANT]  
>  서비스 구성 파일을 수정한 후 업데이트된 서비스 구성을 사용하려면 서비스를 다시 시작해야 합니다.  
  
### <a name="modified-configuration-file-example"></a>수정된 구성 파일 예  
 다음 예에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 수정된 구성 파일을 보여 줍니다. 이 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버의 `InstanceName` 이라는 `ServerName`의 명명된 인스턴스에 사용됩니다.  
  
 **SQL Server의 명명된 인스턴스에 대한 수정된 구성 파일 예**  
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
\<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    \<Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    \<Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
### <a name="modify-the-configuration-file-location"></a>구성 파일 위치 수정  
 레지스트리 키 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\ServiceConfigFile**은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서 사용하는 구성 파일의 위치와 이름을 지정합니다. 레지스트리 키의 기본값은 **C:\Program Files\Microsoft SQL Server\130\DTS\Binn\MsDtsSrvr.ini.xml**입니다. 이 레지스트리의 값을 업데이트하여 구성 파일의 이름과 위치를 변경할 수 있습니다. 경로의 버전 번호(SQL Server [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)]의 경우 120, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 경우 130 등)는 SQL Server 버전에 따라 달라집니다.
  
> [!CAUTION]  
>  레지스트리 키를 잘못 편집하면 운영 체제를 다시 설치해야 하는 심각한 문제가 발생할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 는 레지스트리를 잘못 편집하여 발생하는 문제에 대한 해결을 보증하지 않습니다. 레지스트리를 편집하기 전에 중요한 데이터를 백업하십시오. 레지스트리를 백업, 복원 및 편집하는 방법은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 자료 문서 [Microsoft Windows 레지스트리 설명](http://support.microsoft.com/kb/256986)을 참조하십시오.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 시작될 때 구성 파일을 로드하므로 레지스트리 항목의 변경 내용을 적용하려면 서비스를 다시 시작해야 합니다.  

## <a name="connect-to-the-local-service"></a>로컬 서비스에 연결
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 연결하려면 먼저 관리자가 해당 서비스에 대한 액세스 권한을 부여해야 합니다. 
  
### <a name="to-connect-to-the-integration-services-service"></a>Integration Services 서버에 연결하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
2.  **보기** 메뉴에서 **개체 탐색기** 를 클릭합니다.  
  
3.  개체 탐색기 도구 상자에서 **연결**을 클릭하고 **Integration Services**를 클릭합니다.  
  
4.  **서버에 연결** 대화 상자에 서버 이름을 입력합니다. 마침표(.), (local) 또는 **localhost** 를 사용하여 로컬 서버를 지정할 수 있습니다.  
  
5.  **연결**을 클릭합니다.  

## <a name="connect-to-a-remote-ssis-server"></a>원격 SSIS 서버에 연결
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 나 다른 관리 응용 프로그램에서 원격 서버의 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 인스턴스에 연결하려면 응용 프로그램 사용자에게 서버에 대한 특정 권한 집합이 필요합니다.  
  
> [!IMPORTANT]
> 레거시 Integration Services 서비스의 인스턴스에 직접 연결하려면 Integration Services 서비스가 실행 중인 SQL Server의 버전에 맞는 SSMS(SQL Server Management Studio) 버전을 사용해야 합니다. 예를 들어 SQL Server 2016의 인스턴스에서 실행 중인 레거시 Integration Services 서비스에 연결하려면 SQL Server 2016용으로 릴리스된 SSMS의 버전을 사용해야 합니다. [SSMS(SQL Server Management Studio) 다운로드합니다](../../ssms/download-sql-server-management-studio-ssms.md).
>
>  원격 서버에 저장된 패키지를 관리하는 경우 해당 원격 서버에 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 인스턴스에 연결할 필요가 없습니다. 대신 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 원격 서버에 저장된 패키지를 표시하도록 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 서비스에 대한 구성 파일을 편집합니다.
  
### <a name="connecting-to-integration-services-on-a-remote-server"></a>원격 서버의 Integration Services에 연결  
  
#### <a name="to-connect-to-integration-services-on-a-remote-server"></a>원격 서버의 Integration Services에 연결하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
2.  **파일**, **개체 탐색기 연결** 을 차례로 선택하여 **서버에 연결** 대화 상자를 표시합니다.  
  
3.  **서버 유형** 목록에서 **Integration Services** 를 선택합니다.  
  
4.  **서버 이름** 입력란에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버의 이름을 입력합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 인스턴스에 국한되지 않습니다. Integration Services 서버가 실행 중인 컴퓨터의 이름을 사용하여 서비스에 연결합니다.  
  
5.  **연결**을 클릭합니다.  
  
> [!NOTE]  
>  **서버 찾아보기** 대화 상자에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 원격 인스턴스가 표시되지 않습니다. 또한 **옵션** 단추를 클릭하면 표시되는 **서버에 연결** 대화 상자의 **연결 옵션** 탭에서 사용할 수 있는 옵션은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결에는 적용되지 않습니다.  
  
### <a name="eliminating-the-access-is-denied-error"></a>"액세스가 거부되었습니다." 오류 제거  
 충분한 권한이 없는 사용자가 원격 서버의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인스턴스에 연결하려고 하면 "액세스가 거부되었습니다."라는 오류 메시지가 나타납니다. 사용자에게 필요한 DCOM 권한을 부여하면 이 오류 메시지를 방지할 수 있습니다.  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-server-2003-or-windows-xp"></a>Windows Server 2003 또는 Windows XP에서 원격 사용자의 권한을 구성하려면  
  
1.  사용자가 로컬 Administrators 그룹의 멤버가 아니면 분산 COM 사용자 그룹에 해당 사용자를 추가합니다. 이 작업은 **관리 도구** 메뉴에서 액세스할 수 있는 컴퓨터 관리 MMC 스냅인에서 수행할 수 있습니다.  
  
2.  제어판을 열고 **관리 도구** 를 두 번 클릭한 다음 **구성 요소 서비스** 를 두 번 클릭하여 구성 요소 서비스 MMC 스냅인을 시작합니다.  
  
3.  콘솔의 왼쪽 창에서 **구성 요소 서비스** 노드를 확장합니다. **컴퓨터** 노드를 확장하고 **내 컴퓨터**를 확장한 다음 **DCOM 구성** 노드를 클릭합니다.  
  
4.  **DCOM 구성** 노드를 선택하고 구성할 수 있는 응용 프로그램 목록에서 SQL Server Integration Services 11.0을 선택합니다.  
  
5.  SQL Server Integration Services 11.0을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  **SQL Server Integration Services 11.0 속성** 대화 상자에서 **보안** 탭을 선택합니다.  
  
7.  **시작 및 활성화 권한**에서 **사용자 지정**을 선택하고 **편집** 을 클릭하여 **시작 권한** 대화 상자를 엽니다.  
  
8.  **시작 권한** 대화 상자에서 사용자를 추가하거나 삭제하고 적절한 사용자 및 그룹에 적절한 권한을 할당합니다. 로컬 시작, 원격 시작, 로컬 활성화 및 원격 활성화 권한을 할당할 수 있습니다. 시작 권한은 서비스를 시작 및 중지할 수 있는 권한을 부여하거나 거부하고, 활성화 권한은 서비스에 연결할 수 있는 권한을 부여하거나 거부합니다.  
  
9. 확인을 클릭하여 대화 상자를 닫습니다.  
  
10. **액세스 권한**에서 7-8단계를 반복하여 적절한 사용자 및 그룹에 적절한 권한을 할당합니다.  
  
11. MMC 스냅인을 닫습니다.  
  
12. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 다시 시작합니다.  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-2000-with-the-latest-service-packs"></a>Windows 2000 최신 서비스 팩에서 원격 사용자의 권한을 구성하려면  
  
1.  명령 프롬프트에서 **dcomcnfg.exe** 를 실행합니다.  
  
2.  **DCOM 구성 속성** 대화 상자의 **응용 프로그램** 페이지에서 SQL Server Integration Services 11.0을 선택하고 **속성**을 클릭합니다.  
  
3.  **보안** 페이지를 선택합니다.  
  
4.  두 개의 개별 대화 상자를 사용하여 **액세스 권한** 과 **시작 권한**을 구성합니다. 원격 액세스와 로컬 액세스는 구별할 수 없습니다. 액세스 권한에는 로컬 및 원격 액세스가 포함되고 시작 권한에는 로컬 및 원격 시작이 포함됩니다.  
  
5.  대화 상자 및 **dcomcnfg.exe**를 닫습니다.  
  
6.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 다시 시작합니다.  
  
### <a name="connecting-by-using-a-local-account"></a>로컬 계정을 사용하여 연결  
 클라이언트 컴퓨터에서 로컬 Windows 계정으로 작업하는 경우 동일한 이름 및 암호와 적절한 권한이 있는 로컬 계정이 원격 컴퓨터에 있는 경우에만 원격 컴퓨터의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 연결할 수 있습니다.  
  
### <a name="by-default-the-ssis-service-does-not-support-delegation"></a>기본적으로 위임이 지원되지 않는 SSIS 서비스  
기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에서는 자격 증명의 위임(이중 홉이라고도 함)이 지원되지 않습니다. 이 시나리오에서는 클라이언트 컴퓨터에서 작업 중이고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 두 번째 컴퓨터에서 실행 중이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 세 번째 컴퓨터에서 실행 중이라고 가정합니다. 먼저 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 가 클라이언트 컴퓨터에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 실행 중인 두 번째 컴퓨터로 자격 증명을 성공적으로 전달합니다. 그러나 그런 다음 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 두 번째 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 세 번째 컴퓨터에 자격 증명을 위임할 수 없습니다.

SQL Server 서비스 계정에 **모든 서비스에 대한 위임용으로 이 사용자 트러스트(Kerberos만)** 권한을 부여하여 자격 증명을 위임할 수 있으며 하위 프로세스로 Integration Services 서비스(ISServerExec.exe)가 시작됩니다. 이 권한을 부여하기 전에 조직의 보안 요구 사항을 충족하는지 여부를 고려해야 합니다.

자세한 내용은 [Getting Cross Domain Kerberos and Delegation working with SSIS Package](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/)(SSIS 패키지로 도메인 간 Kerberos 및 위임 가져오기)를 참조하세요.
 
## <a name="configure-the-firewall"></a>방화벽 구성
  
 Windows 방화벽 시스템을 사용하면 네트워크 연결을 통해 이루어지는 컴퓨터 리소스에 대한 무단 액세스를 차단할 수 있습니다. 이 방화벽을 통해 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 액세스하려면 액세스 가능하도록 방화벽을 구성해야 합니다.  
  
> [!IMPORTANT]  
>  원격 서버에 저장된 패키지를 관리하는 경우 해당 원격 서버에 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 인스턴스에 연결할 필요가 없습니다. 대신 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 원격 서버에 저장된 패키지를 표시하도록 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 서비스에 대한 구성 파일을 편집합니다.
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에는 DCOM 프로토콜이 사용됩니다. 방화벽을 통한 DCOM 프로토콜 작동 방법은 MSDN Library에서 "[방화벽과 함께 분산 COM 사용(Using Distributed COM with Firewalls)](http://go.microsoft.com/fwlink/?LinkId=12490)" 문서를 참조하십시오.  
  
 사용할 수 있는 방화벽 시스템은 여러 가지가 있습니다. Windows 방화벽 이외의 다른 방화벽을 사용하는 경우 사용 중인 시스템별 정보를 보려면 해당 방화벽 설명서를 참조하십시오.  
  
 방화벽에서 응용 프로그램 수준의 필터링이 지원되는 경우 Windows에서 제공하는 사용자 인터페이스를 사용하여 프로그램 및 서비스와 같이 방화벽을 통해 허용되는 예외를 지정할 수 있습니다. 그렇지 않으면 제한된 TCP 포트 집합을 사용하도록 DCOM을 구성해야 합니다. 이전에 제공된 Microsoft 웹 사이트 링크에는 사용할 TCP 포트 지정 방법에 대한 정보가 포함됩니다.  
  
 Integration Services 서비스에는 포트 135가 사용되며 이 포트는 변경할 수 없습니다. SCM(서비스 제어 관리자)에 액세스하려면 TCP 포트 135를 열어야 합니다. SCM은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 시작 및 중지와 실행 중인 서비스에 대한 제어 요청 전송과 같은 태스크를 수행합니다.  
  
 다음 섹션의 정보는 Windows 방화벽에만 해당됩니다. 명령 프롬프트에서 명령을 실행하거나 Windows 방화벽 대화 상자에서 속성을 설정하여 Windows 방화벽 시스템을 구성할 수 있습니다.  
  
 기본 Windows 방화벽 설정 방법과 데이터베이스 엔진, Analysis Services, Reporting Services 및 Integration Services에 영향을 주는 TCP 포트에 대한 설명은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
### <a name="configuring-a-windows-firewall"></a>Windows 방화벽 구성  
 다음 명령을 사용하면 TCP 포트 135를 열고, 예외 목록에 MsDtsSrvr.exe를 추가하고, 방화벽에 대한 차단 해제 범위를 지정할 수 있습니다.  
  
#### <a name="to-configure-a-windows-firewall-using-the-command-prompt-window"></a>명령 프롬프트 창을 사용하여 Windows 방화벽을 구성하려면  
  
1.  다음 명령을 실행합니다.

    ```dos
    netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET
    ```
  
2.  다음 명령을 실행합니다.

    ```dos
    netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET
    ```
  
    > [!NOTE]  
    >  모든 컴퓨터와 인터넷상의 컴퓨터에 대해서도 방화벽을 열려면 scope=SUBNET을 scope=ALL로 바꿉니다.  
  
 다음 절차에서는 Windows 사용자 인터페이스를 사용하여 TCP 포트 135를 열고, 예외 목록에 MsDtsSrvr.exe를 추가하고, 방화벽에 대한 차단 해제 범위를 지정할 수 있습니다.  
  
#### <a name="to-configure-a-firewall-using-the-windows-firewall-dialog-box"></a>Windows 방화벽 대화 상자를 사용하여 방화벽을 구성하려면  
  
1.  제어판에서 **Windows 방화벽**을 두 번 클릭합니다.  
  
2.  **Windows 방화벽** 대화 상자에서 **예외** 탭을 클릭한 다음 **프로그램 추가**를 클릭합니다.  
  
3.  **프로그램 추가** 대화 상자에서 **찾아보기**를 클릭하고 Program Files\Microsoft SQL Server\100\DTS\Binn 폴더로 이동한 다음 MsDtsSrvr.exe를 클릭하고 **열기**를 클릭합니다. **확인** 을 클릭하여 **프로그램 추가** 대화 상자를 닫습니다.  
  
4.  **예외** 탭에서 **포트 추가**를 클릭합니다.  
  
5.  **포트 추가** 대화 상자의 **이름** 상자에 **RPC(TCP/135)**나 다른 설명이 포함된 이름을 입력하고 **포트 번호** 상자에 **135** 를 입력한 다음 **TCP**를 선택합니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 항상 포트 135를 사용합니다. 다른 포트를 지정할 수 없습니다.  
  
6.  **포트 추가** 대화 상자에서는 선택적으로 **범위 변경** 을 클릭하여 기본 범위를 수정할 수 있습니다.  
  
7.  **범위 변경** 대화 상자에서 **내 네트워크(서브넷 전용)** 을 선택하거나 사용자 지정 목록을 입력한 다음 **확인**을 클릭합니다.  
  
8.  **확인** 을 클릭하여 **포트 추가**대화 상자를 닫습니다.  
  
9. **Windows 방화벽** 대화 상자를 닫으려면 **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  Windows 방화벽을 구성하려면 이 절차에서 제어판의 **Windows 방화벽** 항목을 사용합니다. **Windows 방화벽** 항목은 현재 네트워크 위치 프로필에 대한 방화벽만 구성합니다. 그러나 **netsh** 명령줄 도구 또는 고급 보안이 설정된 Windows 방화벽 MMC([!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console) 스냅인을 사용하여 Windows 방화벽을 구성할 수도 있습니다. 이러한 도구에 대한 자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
