---
title: "서버 및 Reporting Services 데이터베이스 연결 문제 해결 | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8bbb88df-72fd-4c27-91b7-b255afedd345
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1b901ec323ee3aa021d9e581cb8a1aedbde3116b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="troubleshoot-server-and-database-connection-problems-with-reporting-services"></a>서버 및 Reporting services 데이터베이스 연결 문제 해결
이 항목을 사용하여 보고서 서버에 연결할 때 발생하는 문제를 해결할 수 있습니다. 이 항목에서는 "오류" 메시지에 대한 정보를 제공합니다. 데이터 원본 구성 및 보고서 서버 연결 정보 구성에 대한 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) 및 [보고서 서버 데이터베이스 연결 구성(SSRS 구성 관리자)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)를 참조하십시오.  
  
## <a name="cannot-create-a-connection-to-data-source-datasourcename-rserroropeningconnection"></a>데이터 원본 'datasourcename'에 대한 연결을 설정할 수 없습니다. (rsErrorOpeningConnection)  
이는 보고서에 데이터를 제공하는 외부 데이터 원본에 대한 연결을 보고서 서버에서 열 수 없을 때 일반적으로 발생하는 오류입니다. 이 오류는 근본 원인을 나타내는 두 번째 오류 메시지와 함께 표시됩니다. 다음 추가 오류가 **rsErrorOpeningConnection**과 함께 표시될 수 있습니다.  
  
### <a name="login-failed-for-user-username"></a>사용자 'UserName'이(가) 로그인하지 못했습니다.  
사용자에게 데이터 원본에 액세스할 권한이 없습니다. SQL Server 데이터베이스를 사용하는 경우 사용자에게 유효한 데이터베이스 사용자 로그인이 있는지 확인합니다. 데이터베이스 사용자 또는 SQL Server 로그인을 만드는 방법에 대한 자세한 내용은 [데이터베이스 사용자 만들기](../../relational-databases/security/authentication-access/create-a-database-user.md) 및 [SQL Server 로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)를 참조하십시오.  
  
### <a name="login-failed-for-user-nt-authorityanonymous-logon"></a>사용자 'NT AUTHORITY\ANONYMOUS LOGON'이(가) 로그인하지 못했습니다.  
이 오류는 자격 증명이 여러 컴퓨터 연결을 통해 전달되는 경우 발생합니다. Windows 인증을 사용 중이며 Kerberos 버전 5 프로토콜을 사용하지 않는 경우 두 대 이상의 컴퓨터 연결을 통해 자격 증명이 전달되면 이 오류가 발생합니다. 이 오류를 해결하려면 저장된 자격 증명 또는 입력 정보를 요청하는 자격 증명을 사용해 보십시오. 이 문제를 해결하는 방법에 대한 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)을 참조하십시오.  
  
### <a name="an-error-has-occurred-while-establishing-a-connection-to-the-server"></a>서버에 대한 연결을 구성하는 동안 오류가 발생했습니다.  
SQL Server에 연결할 때 기본 설정에서 SQL Server가 원격 연결을 허용하지 않기 때문에 이 오류가 발생할 수 있습니다. (공급자: 명명된 파이프 공급자, 오류: 40 - SQL Server에 대한 연결을 열 수 없습니다). 이 오류는 보고서 서버 데이터베이스를 호스팅하는 데이터베이스 엔진의 인스턴스에서 반환됩니다. 대부분의 경우 이 오류는 SQL Server 서비스가 중지되어 발생합니다. 또는 SQL Server Express with Advanced Services나 명명된 인스턴스를 사용하는 경우에는 보고서 서버 데이터베이스의 연결 문자열이나 보고서 서버 URL이 올바르지 않아 이 오류가 발생합니다. 이러한 문제를 해결하려면 다음을 수행하십시오.  
  
* SQL Server(**MSSQLSERVER**) 서비스가 시작되는지 확인합니다. 데이터베이스 엔진의 인스턴스를 호스팅하는 컴퓨터에서 시작, 관리 도구, 서비스를 차례로 클릭하고 SQL Server(**MSSQLSERVER**)로 스크롤합니다. 시작되지 않은 경우 이 서비스를 마우스 오른쪽 단추로 클릭하고 속성을 선택한 후 시작 유형에서 자동을 선택하고 적용, 시작을 차례로 클릭한 다음 확인을 클릭합니다.   
* 보고서 서버 URL 및 보고서 서버 데이터베이스 연결 문자열이 올바른지 확인합니다. Reporting Services 또는 데이터베이스 엔진이 명명된 인스턴스로 설치된 경우 설치 중 만들어지는 기본 연결 문자열에 인스턴스 이름이 포함됩니다. 예를 들어 DEVSRV01이라는 이름의 서버에 SQL Server Express with Advanced Services의 기본 인스턴스를 설치한 경우 보고서 관리자 URL은 DEVSRV01\Reports$SQLEXPRESS가 됩니다. 또한 연결 문자열의 데이터베이스 서버 이름은 DEVSRV01\SQLEXPRESS와 유사하게 됩니다. SQL Server Express에 대한 URL 및 데이터 원본 연결 문자열에 대한 자세한 내용은 [SQL Server Express with Advanced Services의 Reporting Services](http://technet.microsoft.com/library/ms365166(v=sql.105).aspx)를 참조하십시오. 보고서 서버 데이터베이스의 연결 문자열을 확인하려면 Reporting Services 구성 도구를 시작하고 데이터베이스 설치 페이지를 확인합니다.  
  
### <a name="a-connection-cannot-be-made-ensure-that-the-server-is-running"></a>연결할 수 없습니다. 서버가 실행 중인지 확인하십시오.  
ADOMD.NET 공급자에 의해 이 오류가 반환됩니다. 이 오류가 발생할 수 있는 이유에는 여러 가지가 있습니다. 서버를 "localhost"로 지정한 경우 다른 서버 이름을 지정해 보십시오. 이 오류는 새 연결에 메모리를 할당할 수 없는 경우에도 발생할 수 있습니다. 자세한 내용은 [기술 자료 문서 912017 - SQL Server 2005 Analysis Services의 인스턴스에 연결하는 경우 오류 메시지](http://support.microsoft.com/kb/912017)를 참조하십시오.  
  
오류에 "해당 호스트를 알 수 없습니다"도 포함된 경우 이는 Analysis Services 서버를 사용할 수 없거나 이 서버에서 연결을 거부함을 나타냅니다. Analysis Services 서버가 원격 컴퓨터에 명명된 인스턴스로 설치된 경우 SQL Server Browser 서비스를 실행하여 해당 인스턴스에 사용되는 포트 번호를 가져와야 할 수 있습니다.  
  
### <a name="report-services-soap-proxy-source"></a>(Report Services SOAP 프록시 원본)  
보고서 모델을 생성하는 동안 이 오류가 발생하고 추가 정보 섹션에 "SQL Server가 없거나 액세스가 거부되었습니다"가 포함되어 있는 경우 다음 상황이 발생한 것일 수 있습니다.  
* 데이터 원본에 대한 연결 문자열에 "localhost"가 포함되어 있습니다.  
* SQL Server 서비스에 대해 TCP/IP가 비활성화되어 있습니다.  
  
이 오류를 해결하려면 서버 이름을 사용하도록 연결 문자열을 수정하거나 서비스에서 TCP/IP를 활성화하면 됩니다. 다음 단계에 따라 TCP/IP를 활성화하십시오.  
  
1. SQL Server 구성 관리자를 시작합니다.  
2. **SQL Server 네트워크 구성**을 확장합니다.  
3. **MSSQLSERVER에 대한 프로토콜**을 선택합니다.  
4. **TCP/IP**를 마우스 오른쪽 단추로 클릭한 다음 **사용**을 선택합니다.  
5. **SQL Server 서비스**를 선택합니다.  
6. **SQL Server (MSSQLSERVER)**를 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 선택합니다.  
  
## <a name="wmi-error-when-connecting-to-a-report-server-in-management-studio"></a>Management Studio에서 보고서 서버에 연결할 때의 WMI 오류  
기본적으로 Management Studio는 Reporting Services WMI(Windows Management Instrumentation) 공급자를 사용하여 보고서 서버에 대한 연결을 구성합니다. WMI 공급자가 올바르게 설치되지 않으면 보고서 서버에 연결할 때 다음 오류가 발생합니다.  
  
에 연결할 수 없는 \<서버 이름 >. Reporting Services WMI 공급자가 설치되지 않았거나 잘못 구성되었습니다(Microsoft.SqlServer.Management.UI.RSClient).  
  
이 오류를 해결하려면 소프트웨어를 다시 설치해야 합니다. 다른 모든 경우에는 임시 해결 방법으로 다음과 같이 SOAP 끝점을 통해 보고서 서버에 연결할 수 있습니다.  
  
* Management Studio의 **서버에 연결** 대화 상자에서 **서버 이름**에 보고서 서버 URL을 입력합니다. 기본적으로 `http://<your server name>/reportserver`입니다. 또는 SQL Server 2008 Express with Advanced Services를 사용 중인 경우 `http://<your server name>/reportserver$sqlexpress`입니다.  
  
오류를 해결하여 WMI 공급자를 통해 연결하려면 설치 프로그램을 실행하여 Reporting Services를 복구하거나 Reporting Services를 다시 설치해야 합니다.  
  
## <a name="connection-error-where-login-failed-due-to-unknown-user-name-or-bad-password"></a>연결 오류, 알 수 없는 사용자 이름 또는 잘못된 암호로 인해 로그인 실패  
보고서 서버에서 보고서 서버 데이터베이스에 연결하는 데 도메인 계정을 사용하고 도메인 계정의 암호가 변경된 경우 **rsReportServerDatabaseLogonFailed** 오류가 발생할 수 있습니다.   
  
전체 오류 텍스트: "보고서 서버에서 보고서 서버 데이터베이스에 연결할 수 없습니다. 로그온하지 못했습니다(**rsReportServerDatabaseLogonFailed**). 로그온 실패: 알 수 없는 사용자 이름이거나 암호가 잘못되었습니다."  
  
암호를 다시 설정하는 경우 연결을 업데이트해야 합니다. 자세한 내용은 [보고서 서버 데이터베이스 연결 구성(SSRS 구성 관리자)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)을 참조하십시오.  
  
## <a name="the-report-server-cannot-open-a-connection-to-the-report-server-database-rsreportserverdatabaseunavailable"></a>보고서 서버에서 보고서 서버 데이터베이스에 연결할 수 없습니다. 합니다(rsReportServerDatabaseUnavailable).  
전체 메시지: 보고서 서버에서 보고서 서버 데이터베이스에 연결할 수 없습니다. 모든 요청과 처리를 수행하려면 데이터베이스에 연결해야 합니다(rsReportServerDatabaseUnavailable).  
이 오류는 서버에 대해 내부 저장소를 제공하는 SQL Server 관계형 데이터베이스에 보고서 서버가 연결할 수 없는 경우 발생합니다. 보고서 서버 데이터베이스에 대한 연결은 일반적으로 Reporting Services 구성 도구를 통해 관리됩니다. 도구를 실행하고 데이터베이스 설치 페이지로 이동하고 연결 정보를 수정할 수 있습니다. 도구를 사용하여 연결 정보를 업데이트하는 것이 가장 좋은 방법입니다. 도구를 사용하면 종속 설정이 업데이트되고 서비스가 다시 시작됩니다. 자세한 내용은 [보고서 서버 데이터베이스 연결 구성](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md) 및 [보고서 서버 서비스 계정 구성](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)을 참조하십시오.  
  
또한 이 오류는 보고서 서버 데이터베이스를 호스팅하는 데이터베이스 엔진 인스턴스가 원격 연결에 대해 구성되지 않은 경우 발생할 수 있습니다. 일부 버전의 SQL Server에서는 원격 연결이 기본적으로 설정되어 있습니다. 사용 중인 SQL Server 데이터베이스 엔진 인스턴스에서 해당 연결이 설정되어 있는지 여부를 확인하려면 SQL Server 구성 관리자 도구를 실행합니다. TCP/IP와 명명된 파이프를 모두 설정해야 합니다. 원격 서버는 두 프로토콜을 모두 사용합니다. 원격 연결을 설정하는 방법은 [원격 관리를 위한 보고서 서버 구성](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)의 "보고서 서버 데이터베이스에 대한 원격 연결을 구성하는 방법" 섹션을 참조하십시오.  
  
오류에 다음 추가 텍스트가 포함되어 있는 경우 데이터베이스 엔진 인스턴스를 실행하는 데 사용되는 계정에 대해 암호가 만료된 것입니다. "서버에 대한 연결을 구성하는 동안 오류가 발생했습니다. SQL Server에 연결할 때 기본 설정에서 SQL Server가 원격 연결을 허용하지 않기 때문에 이 오류가 발생할 수 있습니다. (**공급자: SQL Server 네트워크 인터페이스, 오류: 26 - 지정된 서버/인스턴스 찾기 오류)**." 이 오류를 해결하려면 암호를 다시 설정하십시오.   
  
## <a name="rpc-server-is-not-listening"></a>"RPC 서버가 수신 대기 중이 아닙니다."  
보고서 서버 서비스는 일부 작업을 위해 RPC(원격 프로시저 호출) 서버를 사용합니다. "RPC 서버가 수신 대기 중이 아닙니다" 오류가 발생하면 보고서 서버 서비스가 실행 중인지 확인합니다.  
  
## <a name="unexpected-error-general-network-error"></a>오류(일반 네트워크 오류)  
이 오류는 데이터 원본 연결 오류를 나타냅니다. 연결 문자열을 확인하고 데이터 원본에 액세스할 수 있는 권한이 있는지 확인해야 합니다. Windows 인증을 사용하여 데이터 원본에 액세스할 경우에는 데이터 원본을 호스팅하는 컴퓨터에 대한 액세스 권한이 있어야 합니다.  
  
## <a name="unable-to-grant-database-access-in-sharepoint-central-administration"></a>SharePoint 중앙 관리에서 데이터베이스 액세스 권한을 부여할 수 없습니다.  
Windows Vista 또는 Windows Server 2008에서 SharePoint 제품이나 기술과 통합되도록 Reporting Services를 구성한 경우 SharePoint 중앙 관리의 **데이터베이스 액세스 권한 부여** 페이지에서 액세스 권한을 부여하려 할 때 다음 오류 메시지가 표시될 수 있습니다. "컴퓨터에 대한 연결을 설정할 수 없습니다."  
  
이 문제는 Windows Vista 및 Windows Server 2008의 UAC(사용자 계정 컨트롤)에서 관리자 권한이 필요한 태스크를 수행할 때 관리자가 명시적으로 허용해야만 관리자 토큰을 승격 및 사용할 수 있도록 했기 때문에 발생합니다. 하지만 이 경우 Windows SharePoint Services 관리 서비스를 승격하여 SharePoint 구성 및 콘텐츠 데이터베이스에 대한 Reporting Services 서비스 계정 또는 계정 액세스 권한을 부여할 수 없습니다.  
  
SQL Server 2008 Reporting Services에서는 보고서 서버 서비스 계정에만 데이터베이스 액세스 권한이 필요합니다. SQL Server 2005 Reporting Services SP2에서는 보고서 서버 Windows 서비스 계정과 보고서 서버 웹 서비스 계정에 모두 데이터베이스 액세스 권한이 필요합니다. SQL Server 2008의 보고서 서버 서비스 계정에 대한 자세한 내용은 서비스 계정(Reporting Services 구성)을 참조하십시오.  
  
이 문제는 두 가지 방법으로 해결할 수 있습니다.   
1.  한 가지 방법은 UAC를 일시적으로 해제하고 SharePoint 중앙 관리를 사용하여 액세스 권한을 부여하는 것입니다.  
> [!IMPORTANT]  
> 이 문제를 해결하기 위해 UAC를 해제했다가 SharePoint 중앙 관리에서 데이터베이스 액세스 권한을 부여한 직후 UAC를 다시 설정하는 경우 각별히 주의해야 합니다. UAC를 해제하지 않으려는 경우에는 이 섹션에서 설명하는 두 번째 해결 방법을 사용하십시오. UAC에 대한 자세한 내용은 Windows 제품 설명서를 참조하십시오.  
2. 두 번째 해결 방법은 Reporting Services 서비스 계정에 대한 데이터베이스 액세스 권한을 수동으로 부여하는 것입니다. 다음 절차에 따라 Reporting Services 서비스 계정을 올바른 Windows 그룹 및 데이터베이스 역할에 추가하여 액세스 권한을 부여할 수 있습니다. 이 절차는 SQL Server 2008 Reporting Services의 보고서 서버 서비스 계정에 적용되며, SQL Server 2005 Reporting Services를 실행 중인 경우 보고서 서버 Windows 서비스 계정과 보고서 서버 웹 서비스 계정에 대한 절차를 수행합니다.   
  
### <a name="to-manually-grant-database-access"></a>데이터베이스 액세스 권한을 수동으로 부여하려면  
  
1. Reporting Services 컴퓨터의 WSS_WPG Windows 그룹에 보고서 서버 서비스 계정을 추가합니다.  
2. SharePoint 구성 및 콘텐츠 데이터베이스를 호스트하는 데이터베이스 인스턴스에 연결하고 보고서 서버 서비스 계정의 SQL 데이터베이스 로그인을 만듭니다.  
3. 다음 데이터베이스 역할에 SQL 데이터베이스 로그인을 추가합니다.  
  
* WSS 콘텐츠 데이터베이스의 db_owner 역할  
* SharePoint_Config 데이터베이스의 WSS_Content_Application_Pools 역할  
  
## <a name="unable-to-connect-to-the-reports-and-reportserver-directories-when-the-report-server-databases-are-created-on-a-virtual-sql-server-that-runs-in-a-microsoft-cluster-services-mscs-cluster"></a>MSCS(Microsoft Cluster Services) 클러스터에서 실행되는 가상 SQL Server에 보고서 서버 데이터베이스를 생성할 경우 /reports 및 /reportsserver 디렉터리에 연결할 수 없음  
MSCS 클러스터에서 실행되는 가상 SQL Server에 보고서 서버 데이터베이스인 **ReportServer** 및 **ReportServerTempDB**를 만드는 경우 `<domain>\<computer_name>$` 형식의 원격 이름을 SQL Server에 로그인으로 등록하지 못할 수 있습니다. 보고서 서버 서비스 계정을 연결 시 이 원격 이름이 필요한 계정으로 구성한 경우 사용자는 Reporting Services에서 /reports 및 /reportserver 디렉터리에 연결할 수 없습니다. 예를 들어, 기본 제공 Windows 계정 NetworkService에는 이 원격 이름이 필요합니다. 이 문제를 방지하려면 명시적 도메인 계정이나 SQL Server 로그인을 사용하여 보고서 서버 데이터베이스에 연결하십시오.  
    
  ## <a name="see-also"></a>관련 항목:  
[Reporting Services 및 파워 뷰 브라우저 지원](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[오류 및 이벤트(Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Reporting Services 보고서에서 데이터 검색 문제 해결](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Reporting Services 구독 및 배달 문제 해결](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


