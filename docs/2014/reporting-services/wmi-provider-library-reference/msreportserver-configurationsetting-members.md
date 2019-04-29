---
title: MSReportServer_ConfigurationSetting 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Members
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a83bdbce04c9be8813dafa0505d82339666bfb0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63020384"
---
# <a name="msreportserverconfigurationsetting-members"></a>MSReportServer_ConfigurationSetting 멤버
  MSReportServer_ConfigurationSetting 클래스에는 다음 속성 및 메서드가 포함되어 있습니다.  
  
## <a name="public-properties"></a>Public 속성  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|보고서 서버가 보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스와 통신하는 데 사용하는 연결 풀 크기를 반환합니다. 읽기 전용입니다.|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|보고서 서버가 보고서 서버 데이터베이스를 호스트하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결하는 데 사용하는 로그인 계정을 지정합니다. 읽기 전용입니다.|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|보고서 서버 데이터베이스에 대한 로그온 시도가 실패할 때까지 기다리는 시간(초)을 지정합니다. 읽기 전용입니다.|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|보고서 서버가 Windows 서비스 계정, Windows 사용자 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하여 보고서 서버 데이터베이스에 액세스하는지 여부를 지정합니다. 읽기 전용입니다.|  
|[DatabaseName](configurationsetting-property-databasename.md)|보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정합니다.|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|명령이 실패하거나 제한 시간을 초과하기 전에 경과해야 하는 시간(초)을 지정합니다. 보고서 서버는 보고서의 데이터 원본이 아닌 보고서 서버 데이터베이스에 대해 프로세스 시간을 잽니다.|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|보고서 서버 데이터베이스가 설치되어 있는 서버 이름을 지정합니다.|  
|[InstallationID 속성](configurationsetting-property-installationid.md)|특정 보고서 서버 인스턴스의 고유 식별자를 반환합니다.|  
|[InstanceName](configurationsetting-property-instancename.md)|특정 컴퓨터의 보고서 서버 인스턴스 이름을 지정합니다.|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|보고서 서버 인스턴스가 초기화되었는지 여부를 나타냅니다. 읽기 전용입니다.|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|보고서 서버가 SharePoint 통합 모드로 구성되어 있는지 여부를 나타냅니다.|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|보고서 서버 웹 서비스를 사용하는지 여부를 나타냅니다. 읽기 전용입니다.|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|보고서 서버 Windows 서비스를 사용하는지 여부를 나타냅니다. 읽기 전용입니다.|  
|[MachineAccountIdentity 속성&#40;WMI&#41;](configurationsetting-property-machineaccountidentity.md)|보고서 서버가 설치되어 있는 컴퓨터의 컴퓨터 계정 ID를 가져옵니다.|  
|[PathName](configurationsetting-property-pathname.md)|보고서 서버 인스턴스의 설치 경로를 지정합니다.|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|RSReportServer.config 파일에 지정된 보안 연결 수준을 반환합니다.|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|보고서 서버에서 전자 메일을 보낼 때 사용하는 주소를 가져옵니다. 읽기 전용입니다.|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|전자 메일 구성의 SendUsing 속성이 TRUE로 설정되어 있는지 여부를 지정합니다.|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|RSReportServer.config 파일에서 SMTP 서버 속성을 가져옵니다. 읽기 전용입니다.|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|보고서 서버가 무인 모드로 보고서를 실행할 때 가장하는 로그인 사용자 계정을 지정합니다. 읽기 전용입니다.|  
|[버전](configurationsetting-property-version.md)|보고서 서버의 버전을 반환합니다.|  
|[VirtualDirectoryReportManager 속성&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportmanager.md)|보고서 관리자 애플리케이션의 가상 디렉터리를 반환합니다.|  
|[VirtualDirectoryReportServer 속성&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportserver.md)|보고서 서버 웹 서비스 애플리케이션의 가상 디렉터리를 반환합니다.|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|보고서 서버 Windows 서비스가 실제로 실행되고 있는 ID를 반환합니다. 읽기 전용입니다.|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|보고서 서버 Windows 서비스를 실행하도록 마지막으로 구성된 ID를 반환합니다. 읽기 전용입니다.|  
  
## <a name="public-methods"></a>Public 메서드  
  
|||  
|-|-|  
|[BackupEncryptionKey](configurationsetting-method-backupencryptionkey.md)|인스턴스에 대한 암호화 키를 백업합니다. 암호화 키는 암호로 암호화되어 저장됩니다.|  
|[CreateSSLCertificateBinding 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-createsslcertificatebinding.md)|SSL 인증서 바인딩을 만듭니다.|  
|[DeleteEncryptedInformation](configurationsetting-method-deleteencryptedinformation.md)|보고서 서버 데이터베이스에서 암호화된 정보를 삭제합니다.|  
|[DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md)|보고서 서버 데이터베이스에서 암호화 키를 삭제합니다.|  
|[GenerateDatabaseCreationScript](configurationsetting-method-generatedatabasecreationscript.md)|보고서 서버 데이터베이스를 만드는 데 사용할 수 있는 SQL 스크립트를 생성합니다.|  
|[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)|보고서 서버 데이터베이스에 사용자 권한을 부여하는 데 사용할 수 있는 SQL 스크립트를 생성합니다.|  
|[GenerateDatabaseUpgradeScript](configurationsetting-method-generatedatabaseupgradescript.md)|보고서 서버 데이터베이스를 업그레이드하는 데 사용할 수 있는 SQL 스크립트를 생성합니다.|  
|[GetAdminSiteUrl 메서드&#40;WMI&#41;](configurationsetting-method-getadminsiteurl.md)|중앙 관리 웹 사이트에 대한 절대 URL을 가져옵니다.|  
|[GetDatabaseVersionDisplayName](configurationsetting-method-getdatabaseversiondisplayname.md)|지정된 보고서 서버 데이터베이스 버전 문자열의 표시 이름을 가져옵니다.|  
|[InitializeReportServer](configurationsetting-method-initializereportserver.md)|지정된 보고서 서버 인스턴스를 초기화합니다.|  
|[ListInstalledSharePointVersions 메서드&#40;WMI&#41;](configurationsetting-method-listinstalledsharepointversions.md)|보고서 서버와 같은 컴퓨터에 설치되어 있는 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 버전을 나타내는 토큰 집합을 반환합니다.|  
|[ListIPAddresses 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listipaddresses.md)|[out] 컴퓨터의 IP 주소를 나열합니다.|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|해당 설치에 보안 정보에 대한 액세스 권한이 있는지 여부에 관계없이 보고서 서버 데이터베이스에 있는 보고서 서버 설치 목록을 반환합니다.|  
|[ListReservedURLs 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listreservedurls.md)|보고서 서버의 모든 애플리케이션용으로 예약된 URL을 나열합니다.|  
|[ListSSLCertificateBindings 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificatebindings.md)|HTTP.SYS에 있는 SSL 인증서 바인딩과 rsreportserver.config에서 예상되는 바인딩을 나열합니다.|  
|[ListSSLCertificates 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificates.md)|컴퓨터에 설치된 SSL 인증서를 나열합니다.|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|새 암호화 키를 생성하고 이 새 키를 사용하여 보고서 서버 데이터베이스에 있는 모든 보안 정보를 다시 암호화합니다.|  
|[RemoveSSLCertificateBindings 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removesslcertificatebinding.md)|SSL 인증서 바인딩을 제거합니다.|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|보고서 서버 구성에서 무인 실행 계정 항목을 삭제합니다.|  
|[RemoveURL 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removeurl.md)|보고서 서버용으로 예약된 URL을 제거합니다.|  
|[ReserveURL 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-reserveurl.md)|지정된 애플리케이션에 대한 URL 예약을 추가합니다.|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|지정된 암호화 키를 보고서 서버 데이터베이스에 다시 적용합니다.|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|특정 보고서 서버 데이터베이스에 대한 보고서 서버 데이터베이스 연결을 설정합니다.|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|보고서 서버 데이터베이스 로그온 시도에 대한 기본 제한 시간 값을 지정합니다.|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|보고서 서버 데이터베이스 연결에 대한 기본 제한 시간 값을 지정합니다.|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|보고서 서버가 전자 메일을 보낼 때 사용할 전자 메일 배달 확장 프로그램을 구성합니다.|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|보고서 서버의 보안 연결 수준을 설정합니다.|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|보고서 서버 Windows 및 웹 서비스를 설정하거나 해제합니다.|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|무인 모드로 보고서를 실행하는 데 사용되는 계정을 지정합니다.|  
|[SetVirtualDirectory 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-setvirtualdirectory.md)|애플리케이션의 가상 디렉터리를 설정합니다.|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|보고서 서버 Windows 서비스가 지정된 Windows 사용자로 실행되도록 하고 이 계정에 보고서 서버를 작동하기에 충분한 파일 시스템 사용 권한을 부여합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [MSReportServer_ConfigurationSetting 클래스](msreportserver-configurationsetting-class.md)  
  
  
