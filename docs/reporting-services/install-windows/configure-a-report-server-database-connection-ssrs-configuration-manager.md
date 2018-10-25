---
title: 보고서 서버 데이터베이스 연결 구성(SSRS 구성 관리자) | Microsoft Docs
author: markingmyname
ms.author: maghan
manager: kfile
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.date: 09/20/2017
ms.openlocfilehash: eed0c630bca54b28e78f2c59c5a14fca6e77da54
ms.sourcegitcommit: 2da0c34f981c83d7f1d37435c80aea9d489724d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782322"
---
# <a name="configure-a-report-server-database-connection--ssrs-configuration-manager"></a>보고서 서버 데이터베이스 연결 구성(SSRS 구성 관리자)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

각 보고서 서버 인스턴스에는 보고서 서버에서 관리하는 보고서, 보고서 모델, 공유 데이터 원본, 리소스 및 메타데이터를 저장하는 보고서 서버 데이터베이스에 대한 연결이 필요합니다. 기본 구성을 설치하는 경우 보고서 서버를 설치하는 동안 초기 연결을 만들 수 있습니다. 대부분의 경우 설치를 완료한 다음에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 연결을 구성합니다. 언제라도 연결을 수정하여 계정 유형을 변경하거나 자격 증명을 다시 설정할 수 있습니다. 데이터베이스를 만들고 연결을 구성하기 위한 단계별 지침은 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)를 참조하세요.

 다음과 같은 상황에서 보고서 서버 데이터베이스 연결을 구성해야 합니다.  
  
-   처음 사용하기 위해 보고서 서버 구성  
  
-   보고서 서버에서 다른 보고서 서버 데이터베이스를 사용하도록 구성  
  
-   데이터베이스 연결에 사용되는 사용자 계정 또는 암호 변경. 계정 정보가 RSReportServer.config 파일에 저장되어 있는 경우에는 데이터베이스 연결만 업데이트하면 됩니다. 연결 시 Windows 통합 보안을 자격 증명 유형으로 사용하는 서비스 계정을 사용하는 경우에는 암호가 저장되지 않으므로 연결 정보를 업데이트할 필요가 없습니다. 계정 변경에 대한 자세한 내용은 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)를 참조하세요.  
  
-   보고서 서버 스케일 아웃 배포 구성. 스케일 아웃 배포를 구성하려면 보고서 서버 데이터베이스에 대해 다중 연결을 만들어야 합니다. 이러한 다중 단계 작업을 수행하는 방법은 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)을 참조하세요.  
  
## <a name="how-reporting-services-connects-to-the-database-engine"></a>Reporting Services가 데이터베이스 엔진에 연결되는 방식  
 보고서 서버 데이터베이스에 대한 보고서 서버 액세스는 자격 증명과 연결 정보, 해당 데이터베이스를 사용하는 보고서 서버 인스턴스에 유효한 암호화 키에 따라 달라집니다. 중요한 데이터를 저장 및 검색하려면 유효한 암호화 키가 있어야 합니다. 암호화 키는 데이터베이스를 처음 구성할 때 자동으로 생성됩니다. 키가 생성된 후 보고서 서버 서비스 ID를 변경하는 경우에는 해당 키를 업데이트해야 합니다. 암호화 키 작업에 대한 자세한 내용은 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)를 참조하세요.  
  
 보고서 서버 데이터베이스는 보고서 서버에 의해서만 액세스되는 내부 구성 요소이므로 보고서 서버 데이터베이스에 대해 지정된 자격 증명과 연결 정보는 보고서 서버에만 사용됩니다. 따라서 보고서를 요청하는 사용자에게는 보고서 서버 데이터베이스에 대한 데이터베이스 권한이나 데이터베이스 로그인이 필요하지 않습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 **System.Data.SqlClient** 를 사용하여 보고서 서버 데이터베이스를 호스트하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 로컬 인스턴스를 사용하고 있는 경우 보고서 서버에서는 공유 메모리를 사용하여 연결을 설정합니다. 보고서 서버 데이터베이스에 원격 데이터베이스 서버를 사용하고 있는 경우 사용하고 있는 에디션에 따라 원격 연결을 설정해야 할 수도 있습니다. Enterprise Edition을 사용하고 있는 경우에는 기본적으로 TCP/IP에 대한 원격 연결이 설정되어 있습니다.  
  
 인스턴스가 원격 연결을 허용하는지 확인하려면 **시작**, **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**, **SQL Server 구성 관리자**를 차례로 클릭한 다음 각 서비스에 대해 TCP/IP 프로토콜이 설정되어 있는지 확인합니다.  
  
 원격 연결을 설정하면 클라이언트 및 서버 프로토콜도 설정됩니다. 프로토콜이 설정되었는지 확인하려면 **시작**, **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**, **SQL Server 구성 관리자**, **SQL Server 네트워크 구성**, **MSSQLSERVER에 대한 프로토콜**을 차례로 클릭합니다. 자세한 내용은 [온라인 설명서의](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) 서버 네트워크 프로토콜 설정 또는 해제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 참조하세요.  
  
## <a name="defining-a-report-server-database-connection"></a>보고서 서버 데이터베이스 연결 정의  
 연결을 구성하려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자 또는 **rsconfig** 명령줄 유틸리티를 사용해야 합니다. 보고서 서버에는 다음 연결 정보가 필요합니다.  
  
-   보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 이름  
  
-   보고서 서버 데이터베이스의 이름. 처음으로 연결을 만드는 경우 보고서 서버 데이터베이스를 새로 만들거나 기존 데이터베이스를 선택할 수 있습니다. 자세한 내용은 [보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)를 참조하세요.  
  
-   자격 증명 유형. 서비스 계정, Windows 도메인 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인을 사용할 수 있습니다.  
  
-   사용자 이름 및 암호. Windows 도메인 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하는 경우에만 필요합니다.  
  
 제공하는 자격 증명에는 보고서 서버 데이터베이스에 대한 액세스 권한을 부여해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하면 이 단계가 자동으로 수행됩니다. 데이터베이스에 액세스하는 데 필요한 권한에 대한 자세한 내용은 이 항목의 "데이터베이스 권한" 섹션을 참조하십시오.  
  
### <a name="storing-database-connection-information"></a>데이터베이스 연결 정보 저장  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 다음 RSreportserver.config 설정에 연결 정보를 저장 및 암호화합니다. 이러한 설정에 대해 암호화된 값을 만들려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구 또는 rsconfig 유틸리티를 사용해야 어야 합니다.  
  
 모든 연결 유형에 대해 모든 값이 설정되는 것은 아닙니다. 기본값을 사용하여 연결을 구성하는 경우, 즉 서비스 계정을 사용하여 연결을 만드는 경우에는 다음과 같이 \<**LogonUser**>, \<**LogonDomain**> 및 \<**LogonCred**>가 비게 됩니다.  
  
```  
<Dsn></Dsn>  
<ConnectionType></ConnectionType>  
<LogonUser></LogonUser>  
<LogonDomain></LogonDomain>  
<LogonCred></LogonCred>  
```  
  
 연결에서 특정 Windows 계정이나 데이터베이스 로그인을 사용하도록 구성한 다음 이후에 해당 계정이나 로그인을 변경하면 저장된 값을 업데이트해야 합니다.  
  
### <a name="choosing-a-credential-type"></a>자격 증명 유형 선택  
 보고서 서버 데이터베이스에 대한 연결에 사용할 수 있는 자격 증명에는 3가지 유형이 있습니다.  
  
-   Windows 통합 보안. 보고서 서버 서비스 계정을 사용합니다. 보고서 서버는 단일 서비스로 구현되므로 서비스가 실행되는 계정에만 데이터베이스 액세스 권한이 필요합니다.  
  
-   Windows 사용자 계정. 보고서 서버와 보고서 서버 데이터베이스가 같은 컴퓨터에 설치되어 있는 경우에는 로컬 계정을 사용할 수 있습니다. 그렇지 않은 경우에는 도메인 계정을 사용해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인  
  
> [!NOTE]  
>  보고서 서버 데이터베이스 연결에는 사용자 지정 인증 확장 프로그램을 사용할 수 없습니다. 이 확장 프로그램은 보고서 서버의 보안 주체를 인증하는 데에만 사용됩니다. 또한 이 프로그램은 보고서 서버 데이터베이스에 연결하거나 보고서에 내용을 제공하는 외부 데이터 원본에 연결할 때는 아무 영향도 주지 않습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 Windows 인증이 구성되어 있고 이 인스턴스가 보고서 서버 컴퓨터와 같은 도메인이나 트러스트된 도메인에 있는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 통해 연결 속성으로 관리되는 서비스 계정 또는 도메인 사용자 계정을 사용하도록 연결을 구성할 수 있습니다. 데이터베이스 서버가 다른 도메인에 있거나 작업 그룹 보안을 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 로그인을 사용하도록 연결을 구성해야 합니다. 이 경우 연결을 암호화해야 합니다.  
  
##### <a name="using-service-accounts-and-integrated-security"></a>서비스 계정 및 통합 보안 사용  
 Windows 통합 보안을 사용하면 보고서 서버 서비스 계정을 통해 연결할 수 있습니다. 이 계정에는 보고서 서버 데이터베이스에 대한 로그인 권한이 부여됩니다. 이 유형은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 기본 구성으로 설치하는 경우 설치 프로그램에서 선택하는 기본 자격 증명 유형입니다.  
  
 서비스 계정은 보고서 서버 데이터베이스 연결을 최소한의 수준으로 유지 관리하는 트러스트된 계정입니다. 서비스 계정에서는 Windows 통합 보안을 사용하여 연결을 설정하기 때문에 자격 증명을 저장할 필요가 없습니다. 그러나 기본 제공 계정을 도메인 계정으로 전환하는 등 이후에 서비스 계정 암호나 ID를 변경하는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 변경해야 합니다. 이 도구는 데이터베이스 권한을 자동으로 업데이트하여 수정된 계정 정보를 사용합니다. 자세한 내용은 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)를 참조하세요.  
  
 데이터베이스 연결에서 서비스 계정을 사용하도록 구성하는 경우 보고서 서버 데이터베이스가 원격 컴퓨터에 있으면 해당 계정에 네트워크 사용 권한이 있어야 합니다. 보고서 서버 데이터베이스가 방화벽 뒤에 있는 다른 도메인에 있거나 도메인 보안 대신 작업 그룹 보안을 사용하는 경우에는 서비스 계정을 사용하지 말고 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용자 계정을 사용하십시오.  
  
##### <a name="using-a-domain-user-account"></a>도메인 사용자 계정 사용  
 보고서 서버 데이터베이스에 대한 보고서 서버 연결에 대해 Windows 사용자 계정을 지정할 수 있습니다. 로컬 계정이나 도메인 계정을 사용하는 경우에는 암호나 계정을 변경할 때마다 보고서 서버 데이터베이스 연결을 업데이트해야 합니다. 항상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 연결을 업데이트하십시오.  
  
##### <a name="using-a-sql-server-login"></a>SQL Server 로그인 사용  
 보고서 서버 데이터베이스 연결에 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하도록 지정할 수 있습니다. 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하고 있고, 보고서 서버 데이터베이스가 원격 컴퓨터에 있는 경우에는 IPSec를 사용하여 서버 간 데이터 전송을 보호해야 합니다. 데이터베이스 로그인을 사용하는 경우에는 암호나 계정을 변경할 때마다 보고서 서버 데이터베이스 연결을 업데이트해야 합니다.  
  
### <a name="database-permissions"></a>데이터베이스 권한  
 보고서 서버 데이터베이스 연결에 사용되는 계정에는 다음 역할이 부여됩니다.  
  
-   **ReportServer** 데이터베이스에 대한 **public** 및 **RSExecRole** 역할  
  
-   **master** , **msdb**및 **ReportServerTempDB**데이터베이스에 대한 **RSExecRole** 역할  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 연결을 만들거나 수정하는 경우에는 이러한 권한이 자동으로 부여됩니다. rsconfig 유틸리티를 사용하는 경우 연결에 대해 다른 계정을 지정하면 해당 새 계정에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 업데이트해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 스크립트 파일을 만들어 보고서 서버에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 업데이트할 수 있습니다.  
  
### <a name="verifying-the-database-name"></a>데이터베이스 이름 확인  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 특정 보고서 서버 인스턴스에서 사용하는 보고서 서버 데이터베이스를 확인할 수 있습니다. 이름을 찾으려면 보고서 서버 인스턴스에 연결한 다음 데이터베이스 설치 페이지를 엽니다.  
  
## <a name="using-a-different-report-server-database-or-moving-a-report-server-database"></a>다른 보고서 서버 데이터베이스 사용 또는 보고서 서버 데이터베이스 이동  
 연결 정보를 변경하여 보고서 서버 인스턴스에서 다른 보고서 서버 데이터베이스를 사용하도록 구성할 수 있습니다. 프로덕션 보고서 서버를 배포할 때 주로 데이터베이스를 전환합니다. 테스트 보고서 서버 데이터베이스에서 프로덕션 보고서 서버 데이터베이스로 전환하는 작업은 일반적으로 프로덕션 서버를 전달하는 방법입니다. 보고서 서버 데이터베이스를 다른 컴퓨터로 이동할 수도 있습니다. 자세한 내용은 [온라인 설명서의](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md) Reporting Services 업그레이드 및 마이그레이션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
## <a name="configuring-multiple-reports-servers-to-use-the-same-report-server-database"></a>여러 보고서 서버에서 동일한 보고서 서버 데이터베이스를 사용하도록 구성  
 여러 보고서 서버에서 동일한 보고서 서버 데이터베이스를 사용하도록 구성할 수 있습니다. 이 배포 구성을 스케일 아웃 배포라고 합니다. 서버 클러스터에서 보고서 서버를 여러 개 실행하려는 경우 이 구성이 반드시 필요합니다. 그러나 서비스 응용 프로그램을 분할하거나 새 보고서 서버 인스턴스의 설치 및 설정을 테스트한 다음 이를 기존 보고서 서버 설치와 비교하려는 경우에도 이 설정을 사용할 수 있습니다. 자세한 내용은 [기본 모드 보고서 서버 확장 배포 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)을 참조하세요.  

## <a name="next-steps"></a>다음 단계

[보고서 서버 데이터베이스 만들기](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
[Reporting Services 기본 모드 보고서 서버 관리](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[보고서 서버 서비스 계정 구성](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
