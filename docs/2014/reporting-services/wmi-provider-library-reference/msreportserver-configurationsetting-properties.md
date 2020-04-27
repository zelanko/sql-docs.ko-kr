---
title: MSReportServer_ConfigurationSetting 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Properties
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c3937d888089f06435fece25e791b10ebbab785
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097327"
---
# <a name="msreportserver_configurationsetting-properties"></a>MSReportServer_ConfigurationSetting 속성
  MSReportServer_ConfigurationSetting 클래스는 보고서 서버 인스턴스의 설치 및 런타임 매개 변수를 나타냅니다. 이 설정은 RRSReportServer.config 구성 파일에 저장됩니다.  
  
## <a name="public-properties"></a>Public 속성  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|보고서 서버가 보고서 서버 데이터베이스를 호스트하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스와 통신하는 데 사용하는 연결 풀 크기를 반환합니다. 읽기 전용입니다.|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|보고서 서버가 보고서 서버 데이터베이스를 호스트하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결하는 데 사용하는 로그온 계정을 지정합니다. 읽기 전용입니다.|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|보고서 서버 데이터베이스에 대한 로그온 시도가 실패할 때까지 기다리는 시간(초)을 지정합니다. 읽기 전용입니다.|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|보고서 서버가 Windows 서비스 계정, Windows 사용자 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하여 보고서 서버 데이터베이스에 액세스하는지 여부를 지정합니다. 읽기 전용입니다.|  
|[DatabaseName](configurationsetting-property-databasename.md)|보고서 서버 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정합니다.|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|명령이 실패하거나 제한 시간을 초과하기 전에 경과해야 하는 시간(초)을 지정합니다. 보고서 서버는 보고서의 데이터 원본이 아닌 SQL Server 카탈로그에 대해 프로세스 시간을 계산합니다.|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|보고서 서버 데이터베이스가 설치되어 있는 서버 이름을 지정합니다.|  
|[InstallationID 속성](configurationsetting-property-installationid.md)|특정 보고서 서버 인스턴스의 고유 식별자를 반환합니다.|  
|[InstanceName](configurationsetting-property-instancename.md)|특정 컴퓨터의 보고서 서버 인스턴스 이름을 지정합니다.|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|보고서 서버 인스턴스가 초기화되었는지 여부를 나타냅니다.  읽기 전용입니다.|  
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
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](msreportserver-configurationsetting-members.md)  
  
  
