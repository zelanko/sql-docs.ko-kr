---
title: 관리 되는 인스턴스에서 데이터베이스를 호스팅합니다.
description: MDS (MDS(Master Data Services)) 데이터베이스를 만들고 구성 하 고 Azure SQL Managed Instance에 호스트 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 07/01/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19519697-c219-44a8-9339-ee1b02545445
author: v-redu
ms.author: lle
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 671ae0d9578c81d56c3324f73a4240152594dd49
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194435"
---
# <a name="host-an-mds-database-on-a-managed-instance"></a>관리 되는 인스턴스에서 MDS 데이터베이스를 호스팅합니다.

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  이 문서에서는 관리 되는 인스턴스에서 MDS (MDS(Master Data Services)) 데이터베이스를 구성 하는 방법을 설명 합니다.
  
## <a name="preparation"></a>준비

준비 하려면 Azure SQL Managed Instance를 만들고 구성 하 고 웹 응용 프로그램 컴퓨터를 구성 해야 합니다.

### <a name="create-and-configure-the-database"></a>데이터베이스 만들기 및 구성

1. 가상 네트워크를 사용 하 여 관리 되는 인스턴스를 만듭니다. 자세한 내용은 [빠른 시작: SQL Managed Instance 만들기를](/azure/sql-database/sql-database-managed-instance-get-started) 참조 하세요.

1. 지점 및 사이트 간 연결을 구성 합니다. 지침은 [네이티브 Azure 인증서 인증을 사용 하 여 VNet에 지점 및 사이트 간 연결 구성: Azure Portal](/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) 을 참조 하세요.

1. SQL Managed Instance를 사용 하 여 Azure Active Directory 인증을 구성 합니다. 자세한 내용은 [SQL을 사용 하 여 Azure Active Directory 인증 구성 및 관리](/azure/sql-database/sql-database-aad-authentication-configure) 를 참조 하세요.

### <a name="configure-web-application-machine"></a>웹 응용 프로그램 컴퓨터 구성

1. 지점 및 사이트 간 연결 인증서와 VPN을 설치 하 여 컴퓨터가 관리 되는 인스턴스에 액세스할 수 있도록 합니다. 지침은 [네이티브 Azure 인증서 인증을 사용 하 여 VNet에 지점 및 사이트 간 연결 구성: Azure Portal](/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) 을 참조 하세요.

1. 다음 역할 및 기능을 설치 합니다.
   - 역할:
     - 인터넷 정보 서비스
     - 웹 관리 도구
     - IIS 관리 콘솔
     - World Wide Web 서비스
     - 애플리케이션 개발
     - .NET 확장성 3.5
     - .NET 확장성 4.5
     - ASP.NET 3.5
     - ASP.NET 4.5
     - ISAPI 확장
     - ISAPI 필터
     - 일반 HTTP 기능
     - 기본 문서
     - 디렉터리 검색
     - HTTP 오류
     - 정적 콘텐츠
     - 상태 및 진단
     - HTTP 로깅
     - 요청 모니터
     - 성능
     - 정적 콘텐츠 압축
     - 보안
     - 요청 필터링
     - Windows 인증
       > [!NOTE]
       > WebDAV 게시를 설치 하지 않음

   - 기능:
     - .NET framework 3.5(.NET 2.0 및 3.0 포함)
     - .NET Framework 4.5 Advanced Services
     - ASP.NET 4.5
     - WCF Services
     - HTTP 활성화 (필수)
     - TCP 포트 공유
     - Windows Process Activation Service
     - 프로세스 모델
     - .NET 환경
     - 구성 API
     - 동적 콘텐츠 압축

## <a name="install-and-configure-an-mds-web-application"></a>MDS 웹 응용 프로그램 설치 및 구성

다음으로를 설치 하 고 구성 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 합니다.

### <a name="install-sql-server-2019"></a>SQL Server 2019 설치

설치 SQL Server 설치 마법사 또는 명령 프롬프트를 사용 하 여를 설치 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 합니다.

1. `Setup.exe`을 열고 설치 마법사의 단계를 따릅니다.

2. [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 기능 선택 **페이지의** 공유 기능 **에서**를 선택합니다.
이 작업은 다음을 설치 합니다.
   - [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]
   - 어셈블리
   - Windows PowerShell 스냅인
   - 웹 응용 프로그램 및 서비스에 대 한 폴더 및 파일입니다.

   ![mds-SQLServer2019-MI-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "SQLServer2019-MI_SQLFeatureSelection")  

### <a name="set-up-the-database-and-website"></a>데이터베이스 및 웹 사이트 설정

1. Azure Virtual Network을 연결 하 여 관리 되는 인스턴스에 연결할 수 있는지 확인 합니다.

   ![SQLServer2019-MI-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "SQLServer2019-MI_P2SVPNConnect")

1. 를 연 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 다음 왼쪽 창에서 **데이터베이스 구성** 을 선택 합니다.

1. 데이터베이스 **만들기** 를 선택 하 여 **데이터베이스 만들기 마법사**를 엽니다. **다음**을 선택합니다.

1. **데이터베이스 서버** 페이지에서 **SQL Server 인스턴스** 필드를 완성 한 다음 **인증 유형을**선택 합니다. **연결 테스트** 를 선택 하 여 선택한 인증 유형을 통해 데이터베이스에 연결 하는 데 자격 증명을 사용할 수 있는지 확인 합니다. **다음**을 선택합니다.

   > [!NOTE]
   > - SQL Server 인스턴스는와 같습니다 `xxxxxxx.xxxxxxx.database.windows.net` .
   > - 관리 되는 인스턴스의 경우 **"SQL Server 계정"** 및 **"현재 사용자-Active Directory 통합"** 인증 유형을 선택 합니다.
   > - **현재 사용자 –** 인증 유형으로 통합 Active Directory 선택 하는 경우 **사용자 이름** 필드는 읽기 전용 이며 현재 로그온 한 Windows 사용자 계정을 표시 합니다. [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]AZURE vm (가상 머신)에서 SQL Server 2019를 실행 하는 경우 **사용자 이름** 필드에 vm의 로컬 관리자 계정에 대 한 vm 이름 및 사용자 이름이 표시 됩니다.

   인증에 관리 되는 인스턴스에 대 한 **"sysadmin"** 규칙이 포함 되어 있어야 합니다.

   ![SQLServer2019-MI-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "SQLServer2019-MI_CreateDBConnect")  

1. **데이터베이스 이름** 필드에 이름을 입력합니다. 필요에 따라 Windows 데이터 정렬을 선택 하려면 **기본 데이터 정렬 SQL Server** 확인란의 선택을 취소 하 고 사용 가능한 옵션 중 하나 이상을 선택 합니다. 예를 들어 대 **/소문자를 구분**합니다. **다음**을 선택합니다.

   ![SQLServer2019-MI-CreatedDBName](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "SQLServer2019-MI_CreatedDBName")

1. **사용자 이름** 필드에서에 대 한 기본 슈퍼 사용자의 Windows 계정을 지정 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 합니다. 슈퍼 사용자는 모든 기능 영역에 액세스할 수 있으며 모든 모델을 추가, 삭제 및 업데이트할 수 있습니다.

   ![SQLServer2019-MI-CreateDBUserName](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "SQLServer2019-MI_createDBUserName")

1. **다음** 을 선택 하 여 데이터베이스의 설정에 대 한 요약을 확인 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 합니다. **다음** 을 다시 선택 하 여 데이터베이스를 만듭니다. **진행률 및 마침** 페이지가 표시 됩니다.

1. 데이터베이스를 만들고 구성한 후 **마침**을 선택 합니다.

   **데이터베이스 만들기 마법사**의 설정에 대 한 자세한 내용은 [데이터베이스 만들기 마법사 &#40;[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)를 참조 하세요.

1. 의 **데이터베이스 구성** 페이지에서 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] **데이터베이스 선택**을 선택 합니다.

1. **연결**을 선택 하 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 고 데이터베이스를 선택한 다음 **확인**을 선택 합니다.

   ![SQLServer2019-MI-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "SQLServer2019-MI_connectDBName")

1. 의 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 왼쪽 창에서 **웹 구성** 을 선택 합니다.

1. **웹 사이트 목록 상자** 에서 **기본 웹 사이트**를 선택한 다음 **만들기** 를 선택 하 여 웹 응용 프로그램을 만듭니다.

   ![SQLServer2019-MI 구성](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "SQLServer2019-MI_WebConfiguration")

   > [!NOTE]
   > **기본 웹 사이트**를 선택 하는 경우 웹 응용 프로그램을 별도로 만들어야 합니다. 목록 상자에서 **새 웹 사이트 만들기** 를 선택 하면 응용 프로그램이 자동으로 만들어집니다.

1. **응용 프로그램 풀** 섹션에서 다른 사용자 이름을 입력 하 고 암호를 입력 한 다음 **확인**을 선택 합니다.

   ![mds-SQLServer2019-MI-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "SQLServer2019-MI_CreateWebApplication")

   > [!NOTE]
   > 사용자가 최근에 만든 Active Directory 통합 인증을 사용 하 여 데이터베이스에 액세스할 수 있는지 확인 합니다. 또는 나중에에서 연결을 변경할 수 있습니다 `web.config` .

   **웹 응용 프로그램 만들기** 대화 상자에 대 한 자세한 내용은 [웹 응용 프로그램 만들기 대화 상자 &#40;[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)를 참조 하세요.

1. 웹 **응용 프로그램** 창의 **웹 구성** 창에서 사용자가 만든 응용 프로그램을 선택 하 고 **데이터베이스에 응용 프로그램 연결** 섹션에서 **선택** 을 선택 합니다.

1. **연결** 을 선택 하 고 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 웹 응용 프로그램과 연결할 데이터베이스를 선택 합니다. **확인**을 선택합니다.

   웹 사이트 설정을 완료 했습니다. 이제 **웹 구성** 페이지에 선택한 웹 사이트, 만든 웹 응용 프로그램 및 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 응용 프로그램과 관련 된 데이터베이스가 표시 됩니다.

   ![SQLServer2019-MI-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "SQLServer2019-MI_WebConfigSelectDB")

1. **적용**을 선택합니다. **구성 완료** 메시지가 표시 됩니다. 메시지 상자에서 **확인** 을 선택 하 여 웹 응용 프로그램을 시작 합니다. 웹 사이트 주소는 `http://server name/web application/` 입니다.

## <a name="configure-authentication"></a>인증 구성

관리 되는 인스턴스 데이터베이스를 웹 응용 프로그램에 연결 하려면 다른 인증 유형을 변경 해야 합니다.

`web.config`에서 파일을 찾습니다 `C:\Program Files\Microsoft SQL Server\150\Master Data Services\WebApplication` . 다른 인증 유형을 변경 하 여 관리 되는 인스턴스 데이터베이스에 연결 하려면 connectionString을 수정 합니다.

기본 인증 형식은 `Active Directory Integrated` 다음 샘플 연결 문자열에 표시 된 것과 같습니다.

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
   ```

MDS는 다음 샘플 연결 문자열에 표시 된 것 처럼 Active Directory 암호 인증 및 SQL Server 인증도 지원 합니다.

- Active Directory 암호 인증

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
   ```

- SQL Server 인증

   ```xml
   <add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
   ```

## <a name="upgrade-ssmdsshort_md-and-sql-database-version"></a>업그레이드 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 및 SQL Database 버전

### <a name="upgrade-ssmdsshort_md"></a>업그레이드할 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]

**SQL Server 2019 누적 업데이트**를 설치 합니다. [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 자동으로 업데이트 됩니다.

### <a name="upgrade-sql-server"></a>SQL Server 업그레이드

`The client version is incompatible with the database version` **SQL Server 2019 누적 업데이트**를 설치한 후 오류가 발생할 수 있습니다.
![SQLServer2019-MI-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "SQLServer2019-MI_UpgradeDBPage")

이 문제를 해결 하려면 데이터베이스 버전을 업그레이드 해야 합니다.

1. 를 연 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 다음 왼쪽 창에서  **데이터베이스 구성** 을 선택 합니다.

1. 의 **데이터베이스 구성** 페이지에서 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] **데이터베이스 선택**을 선택 합니다.

1. [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]웹 응용 프로그램과 연결 된 데이터베이스를 선택 합니다. **연결**을 선택한 다음 **확인**을 선택 합니다.

   ![SQLServer2019-MI-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "SQLServer2019-MI_ConnectDBName")

1. **데이터베이스 업그레이드** ...를 선택 합니다. .

   ![mds-SQLServer2019-MI-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "SQLServer2019-MI_SelectUpgradeDB")

1. 데이터베이스 업그레이드 마법사의 **시작** 페이지에서 **다음** 을 선택 하 고 **업그레이드 검토** 페이지에서 다음을 선택 합니다.

   ![mds-SQLServer2019-MI-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "SQLServer2019-MI_UpgradeDBWizard")

1. 모든 작업이 완료 되 면 **마침** 을 선택 합니다.

## <a name="see-also"></a>참고 항목

- [Master Data Services 데이터베이스](../master-data-services/master-data-services-database.md)
- [마스터 데이터 관리자 웹 애플리케이션](../master-data-services/master-data-manager-web-application.md)
- [데이터베이스 구성 페이지&#40;Master Data Services 구성 관리자&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)
- [MDS&#40;Master Data Services&#41;의 새로운 기능](../master-data-services/what-s-new-in-master-data-services-mds.md)