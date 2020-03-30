---
title: MSReportServer_ConfigurationSetting 속성 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Properties
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 634c5065730ea58905f89ac0454cdda53552a126
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65569094"
---
# <a name="msreportserver_configurationsetting-properties"></a>MSReportServer_ConfigurationSetting 속성
  MSReportServer_ConfigurationSetting 클래스는 보고서 서버 인스턴스의 설치 및 런타임 매개 변수를 나타냅니다. 이 설정은 RRSReportServer.config 구성 파일에 저장됩니다.  
  
## <a name="public-properties"></a>Public 속성  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|보고서 서버가 보고서 서버 데이터베이스를 호스트하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스와 통신하는 데 사용하는 연결 풀 크기를 반환합니다. 읽기 전용입니다.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|보고서 서버가 보고서 서버 데이터베이스를 호스트하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결하는 데 사용하는 로그온 계정을 지정합니다. 읽기 전용입니다.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|보고서 서버 데이터베이스에 대한 로그온 시도가 실패할 때까지 기다리는 시간(초)을 지정합니다. 읽기 전용입니다.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|보고서 서버가 Windows 서비스 계정, Windows 사용자 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하여 보고서 서버 데이터베이스에 액세스하는지 여부를 지정합니다. 읽기 전용입니다.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정합니다.|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|명령이 실패하거나 제한 시간을 초과하기 전에 경과해야 하는 시간(초)을 지정합니다. 보고서 서버는 보고서의 데이터 원본이 아닌 SQL Server 카탈로그에 대해 프로세스 시간을 계산합니다.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|보고서 서버 데이터베이스가 설치되어 있는 서버 이름을 지정합니다.|  
|[InstallationID 속성](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|특정 보고서 서버 인스턴스의 고유 식별자를 반환합니다.|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|특정 컴퓨터의 보고서 서버 인스턴스 이름을 지정합니다.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|보고서 서버 인스턴스가 초기화되었는지 여부를 나타냅니다.  읽기 전용입니다.|  
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
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  

  
