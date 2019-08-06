---
title: 관리 되는 인스턴스의 호스트 데이터베이스 | Microsoft Docs
description: 관리 되는 인스턴스에서 MDS 데이터베이스를 구성 하는 방법을 설명 합니다.
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
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b4ca791a1a0ce46929f4d409d234f8dbc7efdec3
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794898"
---
# <a name="host-database-on-managed-instance"></a>관리 되는 인스턴스의 호스트 데이터베이스

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 문서에서는 관리 되는 인스턴스에서 MDS 데이터베이스를 구성 하는 방법을 설명 합니다.
  
## <a name="preparation"></a>준비

준비 단계를 완료 하려면 다음 단계를 완료 해야 합니다.
- 관리 되는 인스턴스 만들기 및 구성을 완료 합니다. 가상 네트워크 및 지점 및 사이트 간 VPN을 포함 합니다.
- 웹 응용 프로그램 컴퓨터 구성을 완료 합니다.
  - 지점 및 사이트 간 VPN 설치를 포함 합니다.
  - 역할 및 기능을 설치 합니다.

**데이터베이스 쪽:**

1. 가상 네트워크를 포함 하 Azure SQL Database 관리 되는 인스턴스를 만듭니다. [빠른 시작: Azure SQL Database 관리 되는 인스턴스 만들기](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started)
2. 지점 및 사이트 간 연결을 구성 합니다. [네이티브 Azure 인증서 인증을 사용 하 여 VNet에 지점 및 사이트 간 연결 구성: Azure Portal](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
3. SQL Database 관리 되는 인스턴스를 사용 하 여 Azure Active Directory 인증을 구성 합니다. [SQL을 사용 하 여 Azure Active Directory 인증 구성 및 관리](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)

**웹 응용 프로그램 컴퓨터 쪽:**

1. 컴퓨터에서 관리 되는 인스턴스에 SQL Database 액세스할 수 있도록 지점 및 사이트 간 연결 인증서와 VPN을 설치 합니다. [네이티브 Azure 인증서 인증을 사용 하 여 VNet에 지점 및 사이트 간 연결 구성: Azure Portal](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
2. 역할 및 기능을 설치 합니다. 다음 기능이 필요 합니다.

- 역할

      Internet Information Services
      Web Management Tools
      IIS Management Console
      World Wide Web Services
      Application Development
      .NET Extensibility 3.5
      .NET Extensibility 4.5
      ASP.NET 3.5
      ASP.NET 4.5
      ISAPI Extensions
      ISAPI Filters
      Common HTTP Features
      Default Document
      Directory Browsing
      HTTP Errors
      Static Content
      [Note: Do not install WebDAV Publishing]
      Health and Diagnostics
      HTTP Logging
      Request Monitor
      Performance
      Static Content Compression
      Security
      Request Filtering
      Windows Authentication

- 기능:

      .NET Framework 3.5 (includes .NET 2.0 and 3.0)
      .NET Framework 4.5 Advanced Services
      ASP.NET 4.5
      WCF Services
      HTTP Activation [Note: This is required.]
      TCP Port Sharing
      Windows Process Activation Service
      Process Model
      .NET Environment
      Configuration APIs
      Dynamic Content Compression

## <a name="install-and-configure-includessmdsshort_mdincludesssmdsshort-mdmd-web-application"></a>웹 응용 프로그램 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 설치 및 구성

을 설치 하 고 구성 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]하려면 다음 단계를 완료 해야 합니다.

1. SQL Server 2019 포함 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 기능을 설치 합니다.
2. 관리 인스턴스에 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 데이터베이스를 만듭니다.
3. 용 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]웹 응용 프로그램을 만들고 구성 합니다.
  
**SQL Server 2019 설치**

SQL Server 설치 설치 마법사 또는 명령 프롬프트를 사용 하 여를 설치 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]합니다.

1. Setup.exe를 두 번 클릭하고 설치 마법사의 단계를 따릅니다.

2. 기능 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 선택 페이지의 공유 기능에서를 선택 합니다.
[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], 어셈블리, Windows PowerShell 스냅인, 웹 애플리케이션과 서비스의 폴더 및 파일이 설치됩니다.

    ![mds-SQLServer2019-MI-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "SQLServer2019-MI_SQLFeatureSelection")  

**데이터베이스 및 웹 사이트 설정**

1. Microsoft Azure Virtual Network를 연결 하 여 관리 되는 인스턴스에 연결할 수 있는지 확인 합니다.

    ![SQLServer2019-MI-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "SQLServer2019-MI_P2SVPNConnect")  

2. 를 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]시작 합니다. 왼쪽 창에서 **데이터베이스 구성** 을 클릭 합니다.

3. **데이터베이스 만들기**를 클릭 한 다음 **데이터베이스 만들기** 마법사에서 다음을 클릭 합니다.

4. **데이터베이스 서버** 페이지에서 **SQL Server 인스턴스** 를 채우고 **인증 유형을** 선택한 다음 **연결 테스트** 를 클릭 하 여 인증 유형에 대 한 자격 증명을 사용 하 여 데이터베이스에 연결할 수 있는지 확인 합니다. 선택. 다음을 클릭합니다.

   > [!NOTE]
   > - "Xxxxxxx.xxxxxxx.database.windows.net"과 같은 관리 되는 인스턴스의 SQL Server 인스턴스
   > - 관리 되는 인스턴스의 경우 **"SQL Server 계정"** 및 **"현재 사용자-Active Directory 통합"** 인증 유형을 지원 합니다.
   > - **현재 사용자 –** 인증 유형으로 통합 Active Directory 선택 하는 경우 **사용자 이름** 상자는 읽기 전용 이며 컴퓨터에 로그온 된 Windows 사용자 계정의 이름을 표시 합니다. Azure vm (가상 머신) [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 에서 SQL Server 2019를 실행 하는 경우 **사용자 이름** 상자에 vm의 로컬 관리자 계정에 대 한 vm 이름 및 사용자 이름이 표시 됩니다.

    인증에 관리 되는 인스턴스에 대 한 **"sysadmin"** 규칙이 포함 되어 있는지 확인 하세요.
![SQLServer2019-MI-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "SQLServer2019-MI_CreateDBConnect")  

5. **데이터베이스 이름** 필드에 이름을 입력합니다. 필요에 따라 Windows 데이터 정렬을 선택하려면 **SQL Server 기본 데이터 정렬** 확인란의 선택을 취소하고 **대/소문자 구분**과 같은 사용 가능한 옵션 중 하나 이상을 클릭합니다. **다음**을 클릭합니다.

    ![SQLServer2019-MI-CreatedDBName](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "SQLServer2019-MI_CreatedDBName")  

6. **사용자 이름** 필드에서에 대 한 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]기본 슈퍼 사용자가 될 사용자의 Windows 계정을 지정 합니다. 슈퍼 사용자는 모든 기능 영역에 액세스할 수 있으며 모든 모델을 추가, 삭제 및 업데이트할 수 있습니다.

    ![SQLServer2019-MI-CreateDBUserName](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "SQLServer2019-MI_createDBUserName")

7. **다음** 을 클릭하여 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 데이터베이스에 대한 설정 요약을 본 후에 다시 **다음** 을 클릭하여 데이터베이스를 만듭니다. **진행 후 마침** 페이지가 표시됩니다.

8. 데이터베이스가 생성되고 구성되면 **마침**을 클릭합니다.

    **데이터베이스 만들기 마법사**의 설정에 대 한 자세한 내용은 [ &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 데이터베이스 만들기 마법사 Configuration Manager&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)를 참조 하세요.

9. 의 **데이터베이스 구성** 페이지 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]에서 **데이터베이스 선택**을 클릭 합니다.

10. **연결**을 클릭 하 고 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 8 단계에서 만든 데이터베이스를 선택한 다음 **확인**을 클릭 합니다.

    ![SQLServer2019-MI-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "SQLServer2019-MI_connectDBName")

11. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]의 왼쪽 창에서 **웹 구성** 을 클릭합니다.

12. **웹 사이트** 목록 상자에서 **기본 웹 사이트**를 클릭한 다음 **만들기** 를 클릭하여 웹 애플리케이션을 만듭니다.
![SQLServer2019-MI 구성](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "SQLServer2019-MI_WebConfiguration")

   > [!NOTE] 
   > **기본 웹 사이트**를 선택할 경우 웹 애플리케이션을 만들어야 합니다. 목록 상자에서 **새 웹 사이트 만들기** 를 선택하면 애플리케이션이 자동으로 만들어집니다.

    

13. **응용 프로그램 풀** 섹션에서 다른 사용자 이름을 입력 하 고 암호를 입력 한 다음 확인을 클릭 합니다.
![mds-SQLServer2019-MI-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "SQLServer2019-MI_CreateWebApplication")

   > [!NOTE]
   > 사용자가 방금 만든 Active Directory 통합 인증을 사용 하 여 데이터베이스에 액세스할 수 있는지 확인 해야 합니다. 또는 나중에 web.config에서 연결을 변경 해야 합니다.

    

14. **웹 응용 프로그램 만들기** 대화 상자에 대 한 자세한 내용은 [Configuration Manager &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] &#41;웹 응용 프로그램 만들기 대화 상자](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)를 참조 하세요.

15. 웹 **응용** 프로그램 상자의 **웹 구성** 페이지에서 사용자가 만든 응용 프로그램을 클릭 한 다음 **데이터베이스와 응용 프로그램 연결** 섹션에서 **선택** 을 클릭 합니다.

16. **연결**을 클릭하고 웹 애플리케이션에 연결할 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 데이터베이스를 선택한 다음 **확인**을 클릭합니다.

    웹 사이트 설정을 마쳤습니다. 이제 **웹 구성** 페이지에 선택한 웹 사이트, 만든 웹 응용 프로그램 및 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 응용 프로그램과 관련 된 데이터베이스가 표시 됩니다.

    ![SQLServer2019-MI-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "SQLServer2019-MI_WebConfigSelectDB")

17. **적용**을 클릭합니다. **구성 완료** 메시지 상자가 표시됩니다. 메시지 상자에서 **확인**을 클릭하고 웹 애플리케이션을 시작합니다. 웹 사이트 주소 http://server 는 이름/웹 응용 프로그램/입니다.

## <a name="other-authentication-type-to-connect-managed-instance-database-on-web-application"></a>웹 응용 프로그램에서 관리 되는 인스턴스 데이터베이스를 연결 하는 기타 인증 유형

C:\Program Files\Microsoft SQL Server\150\Master Data Services\webapplication입니다. 아래에 web.config 파일을 가져올 수 있습니다 **.** 다른 인증 유형을 변경 하 여 관리 되는 인스턴스 데이터베이스에 연결 하도록 connectionString을 수정할 수 있습니다.

기본 인증 유형은 "**Active Directory Integrated**" 이며, 다음은 샘플 연결 문자열입니다.

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
```

Active Directory 암호 인증 및 SQL Server 인증도 지원 합니다. 다음은 샘플 연결 문자열입니다.

암호 인증 Active Directory

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
```

SQL Server 인증(SQL Server Authentication)

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
```

## <a name="upgrade-includessmdsshort_mdincludesssmdsshort-mdmd-and-database-version"></a>업그레이드 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 및 데이터베이스 버전

**업그레이드할[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]**

SQL Server 2019 **누적 업데이트**를 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 설치 하면이 자동으로 업데이트 됩니다.

**데이터베이스 버전 업그레이드**

2019 **누적 업데이트**SQL Server 설치 후 "클라이언트 버전이 데이터베이스 버전과 호환 되지 않습니다." 문제가 발생 하면 데이터베이스 버전을 업그레이드 해야 합니다.

![SQLServer2019-MI-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "SQLServer2019-MI_UpgradeDBPage")

1. 를 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]시작 합니다. 왼쪽 창에서 **데이터베이스 구성** 을 클릭 합니다.

2. 의 **데이터베이스 구성** 페이지 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]에서 **데이터베이스 선택**을 클릭 합니다.

3. **연결**을 클릭 하 고 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 웹 응용 프로그램에 연결 된 데이터베이스를 선택한 다음 **확인**을 클릭 합니다.

    ![SQLServer2019-MI-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "SQLServer2019-MI_ConnectDBName")

4. **데이터베이스 업그레이드** ...를 클릭 합니다. 단추

    ![mds-SQLServer2019-MI-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "SQLServer2019-MI_SelectUpgradeDB")

5. 데이터베이스 업그레이드 마법사의 **시작** 페이지 및 **업그레이드 검토** 페이지에서 **다음** 단추를 클릭 합니다.

    ![mds-SQLServer2019-MI-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "SQLServer2019-MI_UpgradeDBWizard")

6. 모든 작업이 완료 되 면 **마침** 단추를 클릭 합니다.

## <a name="see-also"></a>관련 항목

 [MDS(Master Data Services) 데이터베이스](../master-data-services/master-data-services-database.md) [웹 응용 프로그램 마스터 데이터 관리자](../master-data-services/master-data-manager-web-application.md) [데이터베이스 구성 페이지 &#40;Master Data Services 구성 관리자&#41; ](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md) [ &#40;MDS&#41; MDS(Master Data Services)의 새로운 기능](../master-data-services/what-s-new-in-master-data-services-mds.md)
