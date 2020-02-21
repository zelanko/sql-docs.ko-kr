---
title: MSReportServer_ConfigurationSetting 멤버 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Members
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 134c115e48bd578f794ecce28d770ce955622f0b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65569163"
---
# <a name="msreportserver_configurationsetting-members"></a>MSReportServer_ConfigurationSetting 멤버
  MSReportServer_ConfigurationSetting 클래스에는 다음 속성 및 메서드가 포함되어 있습니다.  
  
## <a name="public-properties"></a>Public 속성  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|보고서 서버가 보고서 서버 데이터베이스를 호스트하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스와 통신하는 데 사용하는 연결 풀 크기를 반환합니다. 읽기 전용입니다.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|보고서 서버가 보고서 서버 데이터베이스를 호스트하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결하는 데 사용하는 로그인 계정을 지정합니다. 읽기 전용입니다.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|보고서 서버 데이터베이스에 대한 로그온 시도가 실패할 때까지 기다리는 시간(초)을 지정합니다. 읽기 전용입니다.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|보고서 서버가 Windows 서비스 계정, Windows 사용자 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하여 보고서 서버 데이터베이스에 액세스하는지 여부를 지정합니다. 읽기 전용입니다.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정합니다.|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|명령이 실패하거나 제한 시간을 초과하기 전에 경과해야 하는 시간(초)을 지정합니다. 보고서 서버는 보고서의 데이터 원본이 아닌 보고서 서버 데이터베이스에 대해 프로세스 시간을 잽니다.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|보고서 서버 데이터베이스가 설치되어 있는 서버 이름을 지정합니다.|  
|[InstallationID 속성](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|특정 보고서 서버 인스턴스의 고유 식별자를 반환합니다.|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|특정 컴퓨터의 보고서 서버 인스턴스 이름을 지정합니다.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|보고서 서버 인스턴스가 초기화되었는지 여부를 나타냅니다. 읽기 전용입니다.|  
|[IsSharePointIntegrated](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-issharepointintegrated.md)|보고서 서버가 SharePoint 통합 모드로 구성되어 있는지 여부를 나타냅니다.|  
|[IsWebServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswebserviceenabled.md)|보고서 서버 웹 서비스를 사용하는지 여부를 나타냅니다. 읽기 전용입니다.|  
|[IsWindowsServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswindowsserviceenabled.md)|보고서 서버 Windows 서비스를 사용하는지 여부를 나타냅니다. 읽기 전용입니다.|  
|[MachineAccountIdentity 속성&#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-machineaccountidentity.md)|보고서 서버가 설치되어 있는 컴퓨터의 컴퓨터 계정 ID를 가져옵니다.|  
|[PathName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-pathname.md)|보고서 서버 인스턴스의 설치 경로를 지정합니다.|  
|[SecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-secureconnectionlevel.md)|RSReportServer.config 파일에 지정된 보안 연결 수준을 반환합니다.|  
|[SenderEmailAddress](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-senderemailaddress.md)|보고서 서버에서 전자 메일을 보낼 때 사용하는 주소를 가져옵니다. 읽기 전용입니다.|  
|[SendUsingSMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-sendusingsmtpserver.md)|전자 메일 구성의 SendUsing 속성이 TRUE로 설정되어 있는지 여부를 지정합니다.|  
|[SMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-smtpserver.md)|RSReportServer.config 파일에서 SMTP 서버 속성을 가져옵니다. 읽기 전용입니다.|  
|[UnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-unattendedexecutionaccount.md)|보고서 서버가 무인 모드로 보고서를 실행할 때 가장하는 로그인 사용자 계정을 지정합니다. 읽기 전용입니다.|  
|[버전](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-version.md)|보고서 서버의 버전을 반환합니다.|  
|[VirtualDirectoryReportManager 속성&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportmanager.md)|보고서 관리자 애플리케이션의 가상 디렉터리를 반환합니다.|  
|[VirtualDirectoryReportServer 속성&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportserver.md)|보고서 서버 웹 서비스 애플리케이션의 가상 디렉터리를 반환합니다.|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-windowsserviceidentityactual.md)|보고서 서버 Windows 서비스가 실제로 실행되고 있는 ID를 반환합니다. 읽기 전용입니다.|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|보고서 서버 Windows 서비스를 실행하도록 마지막으로 구성된 ID를 반환합니다. 읽기 전용입니다.|  
  
## <a name="public-methods"></a>Public 메서드  
  
|||  
|-|-|  
|[BackupEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)|인스턴스에 대한 암호화 키를 백업합니다. 암호화 키는 암호로 암호화되어 저장됩니다.|  
|[CreateSSLCertificateBinding 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-createsslcertificatebinding.md)|SSL 인증서 바인딩을 만듭니다.|  
|[DeleteEncryptedInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptedinformation.md)|보고서 서버 데이터베이스에서 암호화된 정보를 삭제합니다.|  
|[DeleteEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptionkey.md)|보고서 서버 데이터베이스에서 암호화 키를 삭제합니다.|  
|[GenerateDatabaseCreationScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)|보고서 서버 데이터베이스를 만드는 데 사용할 수 있는 SQL 스크립트를 생성합니다.|  
|[GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)|보고서 서버 데이터베이스에 사용자 권한을 부여하는 데 사용할 수 있는 SQL 스크립트를 생성합니다.|  
|[GenerateDatabaseUpgradeScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)|보고서 서버 데이터베이스를 업그레이드하는 데 사용할 수 있는 SQL 스크립트를 생성합니다.|  
|[GetAdminSiteUrl 메서드&#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getadminsiteurl.md)|중앙 관리 웹 사이트에 대한 절대 URL을 가져옵니다.|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getdatabaseversiondisplayname.md)|지정된 보고서 서버 데이터베이스 버전 문자열의 표시 이름을 가져옵니다.|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-initializereportserver.md)|지정된 보고서 서버 인스턴스를 초기화합니다.|  
|[ListInstalledSharePointVersions 메서드&#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listinstalledsharepointversions.md)|보고서 서버와 같은 컴퓨터에 설치된 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 버전을 나타내는 토큰 세트를 반환합니다.|  
|[ListIPAddresses 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listipaddresses.md)|[out] 컴퓨터의 IP 주소를 나열합니다.|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreportserversindatabase.md)|해당 설치에 보안 정보에 대한 액세스 권한이 있는지 여부에 관계없이 보고서 서버 데이터베이스에 있는 보고서 서버 설치 목록을 반환합니다.|  
|[ListReservedURLs 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreservedurls.md)|보고서 서버의 모든 애플리케이션용으로 예약된 URL을 나열합니다.|  
|[ListSSLCertificateBindings 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificatebindings.md)|HTTP.SYS에 있는 SSL 인증서 바인딩과 rsreportserver.config에서 예상되는 바인딩을 나열합니다.|  
|[ListSSLCertificates 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificates.md)|컴퓨터에 설치된 SSL 인증서를 나열합니다.|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reencryptsecureinformation.md)|새 암호화 키를 생성하고 이 새 키를 사용하여 보고서 서버 데이터베이스에 있는 모든 보안 정보를 다시 암호화합니다.|  
|[RemoveSSLCertificateBindings 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removesslcertificatebinding.md)|SSL 인증서 바인딩을 제거합니다.|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeunattendedexecutionaccount.md)|보고서 서버 구성에서 무인 실행 계정 항목을 삭제합니다.|  
|[RemoveURL 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeurl.md)|보고서 서버용으로 예약된 URL을 제거합니다.|  
|[ReserveURL 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md)|지정된 애플리케이션에 대한 URL 예약을 추가합니다.|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-restoreencryptionkey.md)|지정된 암호화 키를 보고서 서버 데이터베이스에 다시 적용합니다.|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaseconnection.md)|특정 보고서 서버 데이터베이스에 대한 보고서 서버 데이터베이스 연결을 설정합니다.|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaselogontimeout.md)|보고서 서버 데이터베이스 로그온 시도에 대한 기본 제한 시간 값을 지정합니다.|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabasequerytimeout.md)|보고서 서버 데이터베이스 연결에 대한 기본 제한 시간 값을 지정합니다.|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setemailconfiguration.md)|보고서 서버가 전자 메일을 보낼 때 사용할 전자 메일 배달 확장 프로그램을 구성합니다.|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)|보고서 서버의 보안 연결 수준을 설정합니다.|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setservicestate.md)|보고서 서버 Windows 및 웹 서비스를 설정하거나 해제합니다.|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setunattendedexecutionaccount.md)|무인 모드로 보고서를 실행하는 데 사용되는 계정을 지정합니다.|  
|[SetVirtualDirectory 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md)|애플리케이션의 가상 디렉터리를 설정합니다.|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setwindowsserviceidentity.md)|보고서 서버 Windows 서비스가 지정된 Windows 사용자로 실행되도록 하고 이 계정에 보고서 서버를 작동하기에 충분한 파일 시스템 사용 권한을 부여합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 클래스](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
