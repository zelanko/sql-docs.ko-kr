---
title: MSReportServer_ConfigurationSetting 메서드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Methods
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6d3fc7ae8ad4c3018bcc512296a670fdaac3b64e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097361"
---
# <a name="msreportserver_configurationsetting-methods"></a>MSReportServer_ConfigurationSetting 메서드
  보고서 서버 WMI 공급자의 MSReportServer_ConfigurationSetting 클래스는 다음과 같은 공용 메서드를 제공 합니다.  
  
## <a name="public-methods"></a>Public 메서드  
  
|||  
|-|-|  
|[BackupEncryptionKey](configurationsetting-method-backupencryptionkey.md)|인스턴스에 대한 암호화 키를 백업합니다. 암호화 키는 암호로 암호화되어 저장됩니다.|  
|[CreateSSLCertificateBinding 메서드 &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-createsslcertificatebinding.md)|SSL 인증서 바인딩을 만듭니다.|  
|[DeleteEncryptedInformation](configurationsetting-method-deleteencryptedinformation.md)|보고서 서버 데이터베이스에서 암호화된 정보를 삭제합니다.|  
|[DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md)|보고서 서버 데이터베이스에서 암호화 키를 삭제합니다.|  
|[GenerateDatabaseCreationScript](configurationsetting-method-generatedatabasecreationscript.md)|보고서 서버 데이터베이스를 만드는 데 사용할 수 있는 SQL 스크립트를 생성합니다.|  
|[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)|보고서 서버 데이터베이스에 사용자 권한을 부여하는 데 사용할 수 있는 SQL 스크립트를 생성합니다.|  
|[GenerateDatabaseUpgradeScript](configurationsetting-method-generatedatabaseupgradescript.md)|보고서 서버 데이터베이스를 업그레이드하는 데 사용할 수 있는 SQL 스크립트를 생성합니다.|  
|[GetAdminSiteUrl Method &#40;WMI&#41;](configurationsetting-method-getadminsiteurl.md)|중앙 관리 웹 사이트에 대한 절대 URL을 가져옵니다.|  
|[GetDatabaseVersionDisplayName](configurationsetting-method-getdatabaseversiondisplayname.md)|지정된 보고서 서버 데이터베이스 버전 문자열의 표시 이름을 가져옵니다.|  
|[InitializeReportServer](configurationsetting-method-initializereportserver.md)|지정된 보고서 서버 인스턴스를 초기화합니다.|  
|[ListInstalledSharePointVersions Method &#40;WMI&#41;](configurationsetting-method-listinstalledsharepointversions.md)|보고서 서버와 같은 컴퓨터에 설치 되어 있는 Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 버전을 나타내는 토큰 집합을 반환 합니다.|  
|[WMI MSReportServer_ConfigurationSetting &#40;ListIPAddresses 메서드&#41;](configurationsetting-method-listipaddresses.md)|[out] 컴퓨터의 IP 주소를 나열합니다.|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|해당 설치에 보안 정보에 대한 액세스 권한이 있는지 여부에 관계없이 보고서 서버 데이터베이스에 있는 보고서 서버 설치 목록을 반환합니다.|  
|[WMI MSReportServer_ConfigurationSetting &#40;ListReservedURLs 메서드&#41;](configurationsetting-method-listreservedurls.md)|보고서 서버의 모든 애플리케이션용으로 예약된 URL을 나열합니다.|  
|[ListSSLCertificateBindings 메서드 &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificatebindings.md)|HTTP.SYS에 있는 SSL 인증서 바인딩과 RSReportServer.config에서 예상되는 바인딩을 나열합니다.|  
|[ListSSLCertificates 메서드 &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificates.md)|컴퓨터에 설치된 SSL 인증서를 나열합니다.|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|새 암호화 키를 생성하고 이 새 키를 사용하여 보고서 서버 데이터베이스에 있는 모든 보안 정보를 다시 암호화합니다.|  
|[RemoveSSLCertificateBindings 메서드 &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-removesslcertificatebinding.md)|SSL 인증서 바인딩을 제거합니다.|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|보고서 서버 구성에서 무인 실행 계정 항목을 삭제합니다.|  
|[WMI MSReportServer_ConfigurationSetting&#41;RemoveURL 메서드 &#40;](configurationsetting-method-removeurl.md)|보고서 서버용으로 예약된 URL을 제거합니다.|  
|[WMI MSReportServer_ConfigurationSetting &#40;ReserveURL 메서드&#41;](configurationsetting-method-reserveurl.md)|지정된 애플리케이션에 대한 URL 예약을 추가합니다.|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|지정된 암호화 키를 보고서 서버 데이터베이스에 다시 적용합니다.|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|특정 보고서 서버 데이터베이스에 대한 보고서 서버 데이터베이스 연결을 설정합니다.|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|보고서 서버 데이터베이스 로그온 시도에 대한 기본 제한 시간 값을 지정합니다.|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|보고서 서버 데이터베이스 쿼리에 대한 기본 제한 시간 값을 지정합니다.|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|보고서 서버가 전자 메일을 보낼 때 사용할 전자 메일 배달 확장 프로그램을 구성합니다.|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|보고서 서버의 보안 연결 수준을 설정합니다.|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|보고서 서버 서비스를 설정하거나 해제합니다.|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|무인 모드로 보고서를 실행하는 데 사용되는 계정을 지정합니다.|  
|[WMI MSReportServer_ConfigurationSetting &#40;SetVirtualDirectory 메서드&#41;](configurationsetting-method-setvirtualdirectory.md)|애플리케이션의 가상 디렉터리를 설정합니다.|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|보고서 서버 서비스가 지정된 Windows 사용자로 실행되도록 하고 이 계정에 보고서 서버를 작동하기에 충분한 파일 시스템 사용 권한을 부여합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 클래스](msreportserver-configurationsetting-class.md)  
  
  
