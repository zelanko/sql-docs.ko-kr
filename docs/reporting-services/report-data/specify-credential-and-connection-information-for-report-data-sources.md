---
title: 보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정 | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- Windows authentication [Reporting Services]
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- unattended report processing [Reporting Services]
- reports [Reporting Services], security
- remote data sources [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- prompted credentials [Reporting Services]
- multiple connections
- stored credentials [Reporting Services]
- security [Reporting Services], data sources
- Windows integrated security [Reporting Services]
ms.assetid: fee1a663-a313-424a-aed2-5082bfd114b3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d6b5041b07551ba8bbd23cc3f737fc0c09d72ff1
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65575346"
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정
  보고서 서버에서는 자격 증명을 사용하여 보고서에 내용을 제공하거나 데이터 기반 구독에 받는 사람 정보를 제공하는 외부 데이터 원본에 연결합니다. Windows 인증, 데이터베이스 인증, 인증 안 함 또는 사용자 지정 인증을 사용하는 자격 증명을 지정할 수 있습니다. 네트워크를 통해 연결 요청을 보낼 경우 보고서 서버에서는 사용자 계정 또는 무인 실행 계정을 가장하게 됩니다. 연결 요청이 이루어지는 보안 컨텍스트에 대한 자세한 내용은 이 항목의 [데이터 원본 구성 및 네트워크 연결](#DataSourceConfigurationConnections) 을 더 참조하십시오.  
  
> [!NOTE]  
>  자격 증명은 보고서 서버에 액세스하는 사용자를 인증하는 데도 사용됩니다. 보고서 서버에 대해 사용자를 인증하는 방법은 다른 항목에서 제공합니다.  
  
 외부 데이터 원본에 대한 연결은 사용자가 보고서를 만들 때 정의됩니다. 이것은 보고서가 게시된 후 별도로 관리할 수 있습니다. 사용자가 동적 목록에서 데이터 원본을 선택할 수 있도록 하는 정적 연결 문자열 또는 식을 지정할 수 있습니다. 데이터 원본 유형 및 연결 문자열을 지정하는 방법은 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="when-credentials-are-used-in-report-builder"></a>보고서 작성기에서 자격 증명이 사용된 경우  
 보고서 작성기에서 자격 증명은 주로 보고서 서버에 연결할 때 또는 포함된 데이터 원본 작성, 데이터 세트 쿼리 실행 또는 보고서 미리 보기와 같은 데이터 관련 태스크를 위해 사용됩니다. 자격 증명은 보고서에 저장되지 않습니다. 자격 증명은 보고서 서버나 로컬 클라이언트에서 별도로 관리됩니다. 다음 목록에서는 제공해야 하는 자격 증명 유형, 자격 증명이 저장되는 위치 및 사용 방법을 설명합니다.  
  
-   Reporting Services 로그인 대화 상자에 입력하는 서버 자격 증명을 보고합니다.  
  
     보고서 서버나 SharePoint 사이트로 처음 저장, 게시 또는 이동할 때 자격 증명을 입력해야 할 수도 있습니다. 입력한 자격 증명은 보고서 작성기 세션이 종료될 때까지 사용됩니다. 이러한 자격 증명을 저장하도록 선택한 경우에는 해당 자격 증명이 사용자 설정과 함께 컴퓨터에 안전하게 저장됩니다. 이후의 보고서 작성기 세션에서 저장된 자격 증명은 같은 보고서 서버나 SharePoint 사이트에 연결하는 데 사용됩니다. 보고서 서버 관리자나 SharePoint 관리자는 사용할 자격 증명 유형을 지정합니다.  
  
-   포함된 데이터 원본에 대한 [데이터 원본 속성 대화 상자, 자격 증명&#40;보고서 작성기&#41;](https://msdn.microsoft.com/library/4531f09f-d653-4c05-a120-d7788838bc99) 페이지에 입력하는 데이터 원본 자격 증명  
  
     보고서 서버에서는 이러한 자격 증명을 외부 데이터 원본으로 데이터를 연결하는 데 사용합니다. 일부 데이터 원본 유형의 경우 자격 증명을 보고서 서버에 안전하게 저장할 수 있습니다. 이러한 자격 증명을 사용하면 다른 사용자가 기본 데이터 연결에 자격 증명을 제공하지 않고 보고서를 실행할 수 있습니다.  
  
-   데이터 세트 쿼리를 실행하거나, 데이터 세트 필드를 새로 고치거나, 보고서를 미리 볼 때 **데이터 원본 자격 증명 입력 대화 상자**에 입력하는 데이터 원본 자격 증명입니다.  
  
     이러한 자격 증명은 보고서 작성기에서 외부 데이터 원본으로 데이터를 연결하거나 자격 증명을 요구하도록 구성된 보고서를 미리 볼 때 사용합니다. 이 대화 상자에 입력한 자격 증명은 보고서 서버에 저장되지 않으며 다른 사용자가 사용할 수 없습니다. 보고서 작성기는 보고서 편집 세션 중에 자격 증명을 캐시하므로 쿼리를 실행하거나 보고서를 미리 볼 때마다 자격 증명을 입력하지 않아도 됩니다.  
  
     공유 데이터 원본에 대해서는 **암호 저장** 옵션을 사용하여 자격 증명을 사용자 설정과 함께 컴퓨터에 로컬로 저장할 수 있습니다. 보고서 작성기는 해당 외부 데이터 원본에 연결할 때마다 저장된 자격 증명을 사용합니다.  
  
 자세한 내용은 [데이터 원본 속성 대화 상자, 일반&#40;보고서 작성기&#41;](https://msdn.microsoft.com/library/b956f43a-8426-4679-acc1-00f405d5ff5b) 및 [보고서 작성기에서 보고서 미리 보기](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)를 참조하세요.  
  
## <a name="using-remote-data-sources"></a>원격 데이터 원본 사용  
 보고서가 원격 데이터베이스 서버에서 데이터를 검색하는 경우 다음 사항을 확인합니다.  
  
-   데이터베이스 서버에 제공된 자격 증명이 유효한지 여부. Windows 사용자 자격 증명을 사용하는 경우 사용자에게 서버 및 데이터베이스에 대한 사용 권한이 있는지 확인합니다.  
  
-   데이터베이스 서버에 사용되는 포트가 열려 있는지 여부. 외부 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스에 액세스하거나 보고서 서버 데이터베이스가 외부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 경우 외부 컴퓨터에서 포트 1433 및 1434를 열어야 합니다. 포트를 연 후에는 서버를 다시 시작해야 합니다. 자세한 내용은 [데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)을 참조하세요.  
  
-   원격 연결을 사용할 수 있는지 여부. 외부 컴퓨터의 SQL Server 관계형 데이터베이스에 액세스하는 경우 SQL Server 구성 관리자 도구를 사용하여 TCP를 통한 원격 연결을 사용할 수 있는지 확인할 수 있습니다.  
  
## <a name="ways-to-specify-credentials-for-connecting-to-remote-data-sources"></a>원격 데이터 원본에 연결하기 위한 자격 증명을 지정하는 방법  
 보고서에 내용을 제공하는 데이터 원본은 일반적으로 원격 서버에 호스팅됩니다. 보고서를 위한 데이터를 검색하려면 보고서 서버에서 사용자가 미리 제공하거나 런타임에 가져온 자격 증명 집합을 사용하여 서버에 연결해야 합니다. 데이터 원본을 구성할 때 다음과 같은 방법으로 자격 증명을 지정할 수 있습니다.  
  
-   사용자에게 자격 증명을 입력하도록 메시지 표시  
  
-   자격 증명을 저장합니다.  
  
-   Windows 통합 보안을 사용합니다.  
  
-   자격 증명을 사용하지 않습니다.  
  
 네트워크 환경에 따라 지원할 수 있는 연결 종류가 결정됩니다. 예를 들어 Kerberos 버전 5 프로토콜을 사용할 수 있는 경우 Windows 인증에서 사용 가능한 위임 및 가장 기능을 통해 여러 서버 간 연결을 지원할 수 있습니다. 네트워크에서 이러한 보안 기능을 지원하지 않는 경우 연결 제약 조건을 해결해야 합니다. 위임 및 가장을 사용할 수 없는 경우에는 만료되기 전에 Windows 자격 증명을 단일 컴퓨터 연결을 통해 전달할 수 있습니다. 클라이언트 컴퓨터에서 보고서 서버 컴퓨터로의 사용자 연결은 첫 번째 연결로 간주됩니다. 사용자가 원격 서버에서 데이터를 검색하는 보고서를 열면 해당 로그인은 두 번째 연결로 간주되며 위임을 사용할 수 없을 때 통합 보안을 사용하도록 연결을 지정한 경우 이 연결은 실패합니다.  
  
 클라이언트 컴퓨터에서 외부 보고서 데이터 원본으로의 왕복을 완료하는 데 여러 연결이 필요한 경우 성공적으로 연결을 수행하려면 다음 전략을 사용합니다.  
  
-   자격 증명을 제한 없이 다른 컴퓨터에 위임할 수 있도록 사용자 도메인에서 가장 및 위임 기능을 사용할 수 있도록 설정합니다.  
  
-   저장된 자격 증명 또는 입력 정보를 요청하는 자격 증명을 사용하여 보고서 데이터를 위한 외부 데이터 원본을 쿼리합니다. 자격 증명은 Windows 도메인 계정이거나 데이터베이스 로그인일 수 있습니다.  
  
### <a name="prompted-credentials"></a>입력 정보를 요청하는 자격 증명  
 입력 정보를 요청하는 자격 증명을 사용하도록 보고서 데이터 원본 연결을 구성하면 보고서에 액세스하는 각 사용자가 사용자 이름과 암호를 입력해야 데이터를 검색할 수 있습니다. 이 방법은 기밀 데이터를 포함하는 보고서에 사용하는 것이 좋습니다. 입력 정보를 요청하는 자격 증명은 요청 시 실행되는 보고서에만 사용할 수 있습니다. 입력 정보를 요청하는 자격 증명은 Windows 계정이거나 데이터베이스 로그인일 수 있습니다. Windows 인증을 사용하려면 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용**을 선택해야 합니다. 그렇지 않으면 보고서 서버가 사용자 인증을 위해 자격 증명을 데이터베이스 서버로 전달합니다. 제공된 자격 증명을 데이터베이스 서버가 인증할 수 없는 경우 연결이 실패합니다.  
  
### <a name="windows-integrated-security"></a>Windows 통합 보안  
 **Windows 통합 보안** 옵션을 사용하는 경우 보고서 서버에서는 보고서에 액세스하는 사용자의 보안 토큰을 외부 데이터 원본을 호스팅하는 서버로 전달합니다. 이 경우 사용자 이름이나 암호를 입력하라는 메시지가 표시되지 않습니다. 이 방법은 가장 및 위임 기능을 사용할 수 있는 경우 권장됩니다. 이러한 기능을 사용할 수 없는 경우에는 액세스할 모든 서버가 동일한 컴퓨터에 있을 때만 이 방법을 사용해야 합니다.  
  
### <a name="stored-credentials"></a>저장된 자격 증명  
 외부 데이터 원본에 액세스하는 데 사용되는 자격 증명을 저장할 수 있습니다. 자격 증명은 보고서 서버 데이터베이스에 해독 가능한 암호화 상태로 저장됩니다. 보고서에 사용되는 각 데이터 원본에 대해 저장된 자격 증명 집합을 하나씩 지정할 수 있습니다. 사용자가 제공하는 자격 증명은 보고서를 실행하는 모든 사용자에 대해 동일한 데이터를 검색합니다.  
  
 저장된 자격 증명은 원격 데이터베이스 서버에 액세스하는 전략의 일부로 사용하는 것이 좋습니다. 저장된 자격 증명은 구독을 지원하거나 보고서 기록 생성 일정 또는 보고서 스냅숏 새로 고침 일정을 예약할 경우에 필요합니다. 보고서를 백그라운드 프로세스로 실행하는 경우 보고서 서버는 보고서를 실행하는 에이전트입니다. 사용자 컨텍스트가 없으므로 보고서 서버에서는 데이터 원본에 연결하기 위해 보고서 서버 데이터베이스에서 자격 증명 정보를 가져와야 합니다.  
  
 지정하는 사용자 이름과 암호는 Windows 자격 증명이나 데이터베이스 로그인이 될 수 있습니다. Windows 자격 증명을 지정하면 보고서 서버에서는 이후 인증을 위해 자격 증명을 Windows로 전달합니다. 그렇게 하지 않으면 보고서 서버에서 인증을 위해 자격 증명을 데이터베이스 서버로 전달합니다.  
  
#### <a name="how-to-grant-allow-log-on-locally-permissions-to-domain-user-accounts"></a>도메인 사용자 계정에 "로컬 로그온 허용" 권한을 부여하는 방법  
 저장된 자격 증명을 사용하여 외부 데이터 원본에 연결하는 경우 Windows 도메인 사용자 계정에는 로컬로 로그온할 수 있는 권한이 있어야 합니다. 이 권한이 있으면 보고서 서버가 보고서 서버의 사용자를 가장하고 가장된 사용자로서 외부 데이터 원본에 요청을 보낼 수 있습니다.  
  
 이 권한을 부여하려면 다음을 수행하십시오.  
  
1.  보고서 서버 컴퓨터의 **관리 도구**에서 **로컬 보안 정책**을 엽니다.  
  
2.  **보안 설정**에서 **로컬 정책**을 확장한 다음 **사용자 권한 할당**을 클릭합니다.  
  
3.  세부 정보 창에서 **로컬 로그온 허용** , **속성**을 차례로 마우스 오른쪽 단추로 클릭합니다.  
  
4.  **사용자 또는 그룹 추가**를 클릭합니다.  
  
5.  **위치**를 클릭하고 검색할 도메인 또는 다른 위치를 지정한 다음 **확인**을 클릭합니다.  
  
6.  대화형 로그인을 허용할 Windows 계정을 입력한 다음 **확인**을 클릭합니다.  
  
7.  **로컬 로그온 허용 등록 정보** 대화 상자에서 **확인**을 클릭합니다.  
  
8.  선택한 계정에 다음과 같은 거부 권한도 없는지 확인합니다.  
  
    1.  **로컬 로그온 거부** , **속성**을 차례로 마우스 오른쪽 단추로 클릭합니다.  
  
    2.  계정이 나열되면 계정을 선택한 다음 **제거**를 클릭합니다.  
  
#### <a name="using-impersonation-with-stored-credentials"></a>저장된 자격 증명으로 가장 사용  
 자격 증명을 사용하여 다른 사용자의 ID를 가장할 수도 있습니다. SQL Server 데이터베이스의 경우 가장 옵션을 사용하면 [SETUSER](../../t-sql/statements/setuser-transact-sql.md) 함수가 설정됩니다.  
  
> [!IMPORTANT]  
>  구독을 지원하거나 일정을 사용하여 보고서 기록을 생성 또는 보고서 실행 스냅숏을 새로 고치는 보고서에 대해서는 가장을 사용하지 마십시오.  
  
### <a name="no-credentials"></a>자격 증명 사용 안 함  
 데이터 원본 연결에서 자격 증명을 사용하지 않도록 구성할 수 있습니다. 항상 자격 증명을 사용하여 데이터 원본에 액세스하는 것이 좋으므로, 자격 증명 사용 안 함은 되도록 사용하지 않는 것이 좋습니다. 그러나 다음과 같은 경우에는 자격 증명 없이 보고서를 실행할 수 있습니다.  
  
-   원격 데이터 원본에는 자격 증명이 필요하지 않습니다.  
  
-   자격 증명이 연결 문자열로 전달된 경우(보안 연결에만 권장)  
  
-   보고서가 부모 보고서의 자격 증명을 사용하는 하위 보고서인 경우  
  
 이러한 조건에서는 보고서 서버에서 사용자가 미리 정의해야 하는 무인 실행 계정을 사용하여 원격 데이터 원본에 연결합니다. 보고서 서버는 해당 서비스 자격 증명을 사용하여 원격 서버에 연결하지 않으므로 보고서 서버가 연결에 사용할 수 있는 계정을 지정해야 합니다. 이 계정을 만드는 방법은 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)을 참조하세요.  
  
## <a name="user-name-and-password-login"></a>사용자 이름 및 암호 로그인  
 **이 사용자 이름 및 암호 사용**을 선택할 경우 사용자 이름과 암호를 제공해야 데이터 원본에 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 경우 데이터베이스 로그인에 대해 자격 증명을 사용할 수 있습니다. 자격 증명은 인증을 위해 데이터 원본으로 전달됩니다.  
  
##  <a name="DataSourceConfigurationConnections"></a> 데이터 원본 구성 및 네트워크 연결  
 다음 표에서는 자격 증명 유형과 데이터 처리 확장 프로그램의 특정 조합에 따른 연결 방법을 보여 줍니다. 사용자 지정 데이터 처리 확장 프로그램을 사용하는 경우 [사용자 지정 데이터 처리 확장 프로그램에 대한 연결 지정](../../reporting-services/report-data/specify-connections-for-custom-data-processing-extensions.md)을 참조하세요.  
  
|**형식**|**네트워크 연결에 대한 컨텍스트**|**데이터 원본 유형**<br /><br /> **(SQL Server, Oracle, ODBC, OLE DB, Analysis Services, XML, SAP NetWeaver BI, Hyperion Essbase)**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|통합 보안|현재 사용자를 가장합니다.|모든 데이터 원본 유형에 대해 현재 사용자 계정을 사용하여 연결합니다.|  
|Windows 자격 증명|지정한 사용자를 가장합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC 및 OLE DB의 경우: 가장된 사용자 계정을 사용하여 연결합니다.|  
|데이터베이스 자격 증명|무인 실행 계정 또는 서비스 계정을 가장합니다.<br /><br /> Reporting Services는 서비스 ID를 사용하여 연결 요청을 보낼 경우 관리자 권한을 제거합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC 및 OLE DB의 경우:<br /><br /> 사용자 이름과 암호를 연결 문자열에 추가합니다.<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 경우:<br /><br /> TCP/IP 프로토콜을 사용할 경우 연결되고 그렇지 않을 경우 연결에 실패합니다.<br /><br /> XML의 경우<br /><br /> 데이터베이스 자격 증명을 사용할 경우 보고서 서버에서 연결에 실패합니다.|  
|없음|무인 실행 계정을 가장합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC 및 OLE DB의 경우:<br /><br /> 연결 문자열에 정의된 자격 증명을 사용합니다. 무인 실행 계정이 정의되어 있지 않으면 보고서 서버에서 연결에 실패합니다.<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 경우:<br /><br /> 무인 실행 계정이 정의되어 있더라도 자격 증명을 지정하지 않으면 항상 연결에 실패합니다.<br /><br /> XML의 경우<br /><br /> 무인 실행 계정이 정의되어 있는 경우 익명 사용자로 연결하고, 그렇지 않으면 연결에 실패합니다.|  
  
## <a name="setting-credentials-programmatically"></a>프로그래밍 방식으로 자격 증명 설정  
 코드에 자격 증명을 설정하여 보고서 및 보고서 서버에 대한 액세스를 제어할 수 있습니다. 자세한 내용은 [Data Sources and Connection Methods](../../reporting-services/report-server-web-service/methods/data-sources-and-connection-methods.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)   
 [데이터 연결, 데이터 원본 및 연결 문자열&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [보고서 데이터 원본 관리](../../reporting-services/report-data/manage-report-data-sources.md)   
 [보고서의 데이터 원본 속성 구성](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
