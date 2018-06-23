---
title: 사용자 지정 데이터 처리 확장 프로그램에 대한 연결 지정 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- IDbConnection interface, connection strings
- impersonation [Reporting Services]
- IDbConnectionExtension interface, connection strings
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- data processing extensions [Reporting Services], connections
ms.assetid: 2cddc9ea-0e28-4350-80ae-332412908e47
caps.latest.revision: 20
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: a1577c387561a74356bc31e9ce8058cf804b0235
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080829"
---
# <a name="specify-connections-for-custom-data-processing-extensions"></a>사용자 지정 데이터 처리 확장 프로그램에 대한 연결 지정
  보고서 서버에서 타사의 사용자 지정 데이터 처리 확장 프로그램을 만들거나 사용하여 지원되는 데이터 원본의 데이터 처리 기능을 향상시키거나 기본 설치된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 사용할 수 없는 추가 형식의 데이터 원본을 지원할 수 있습니다. 연결은 구현에 따라 다르게 처리됩니다. 데이터 처리 확장 프로그램에 사용될 수 있는 구현은 다음과 같습니다.  
  
-   사용자 지정 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자(DB2.NET, Oracle, ODP.NET 또는 Teradata 데이터 원본의 데이터에 액세스 중인 경우 사용자 지정 .NET 데이터 공급자를 사용 중일 수 있음)  
  
-   <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>을 지원하는 사용자 지정 데이터 처리 확장 프로그램  
  
-   <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>을 지원하는 사용자 지정 데이터 처리 확장 프로그램  
  
> [!NOTE]  
>  사용자 지정 데이터 처리 확장 프로그램의 구현 방법을 알아보려면 타사 공급자에게 문의하십시오.  
  
## <a name="impersonation-and-custom-data-processing-extensions"></a>가장과 사용자 지정 데이터 처리 확장 프로그램  
 사용자 지정 데이터 처리 확장 프로그램이 가장을 사용하여 데이터 원본에 연결하는 경우 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 또는 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> 인터페이스의 Open 메서드를 사용하여 연결을 요청합니다. 또는 사용자 ID 개체(System.Security.Principal.WindowsIdentity)를 저장한 다음 다른 데이터 처리 확장 프로그램 API에서 다시 사용할 수 있습니다.  
  
 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 모든 사용자 지정 데이터 처리 확장 프로그램은 사용자 가장에서 호출되었습니다. 이 버전에서는 Open 메서드만 사용자를 가장하는 동안 호출됩니다. 통합 보안을 요구하는 기존 데이터 처리 확장 프로그램이 있는 경우 Open 메서드를 사용하거나 사용자 ID 개체를 저장하도록 코드를 수정해야 합니다.  
  
## <a name="connections-for-custom-net-framework-data-providers"></a>사용자 지정 .NET Framework 데이터 공급자에 대한 연결  
 특정 데이터 원본을 사용하도록 보고서를 구성할 때는 데이터 원본 유형, 연결 문자열, 데이터 원본에 액세스하는 데 사용하는 자격 증명 등을 결정하는 속성을 설정합니다. 다음 표에서는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자에 지원되는 자격 증명 유형을 설명합니다. 보고서 데이터 원본 속성을 설정 하는 방법에 대 한 자세한 내용은 참조 [자격 증명을 지정 하 고 보고서 데이터 원본에 대 한 연결 정보](specify-credential-and-connection-information-for-report-data-sources.md)합니다.  
  
|자격 증명|Connections|  
|-----------------|-----------------|  
|통합 보안|데이터 공급자에서 지원할 경우 Windows 통합 보안을 사용할 수 있습니다. 요청은 현재 사용자의 자격 증명을 사용하여 보내집니다.<br /><br /> 연결 문자열을 정의할 때는 통합된 보안을 지정 하는 인수를 포함 하십시오 수 (예를 들어 한 연결을 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본 포함 될 수 있습니다 `Integrated Security=SSPI` 연결 문자열에).|  
|Windows 인증|데이터 공급자에서 지원할 경우 Windows 도메인 사용자 계정을 사용할 수 있습니다. 보고서 서버에서는 데이터 처리 확장 프로그램이 호출되기 전에 사용자 계정을 가장합니다.<br /><br /> 연결 문자열을 정의할 때는 통합된 보안을 지정 하는 인수를 포함 하십시오 수 (예를 들어 한 연결을 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본 포함 될 수 있습니다 `Integrated Security=SSPI` 연결 문자열에).|  
|데이터베이스 자격 증명|사용자 지정 .NET 데이터 공급자를 통해 만들어진 연결의 경우 데이터베이스 인증이 지원되지 않습니다. 보고서 서버에서 모든 경우의 연결이 실패합니다.|  
|자격 증명 사용 안 함|사용자 지정 .NET 데이터 공급자에 자격 증명 사용 안 함 옵션을 사용할 수 있습니다. 무인 실행 계정을 지정하면 연결 문자열에 따라 사용되는 자격 증명이 결정됩니다. 보고서 서버는 무인 실행 계정을 가장하여 연결합니다.<br /><br /> 무인 실행 계정을 정의하지 않은 경우 보고서 서버에서 연결이 실패합니다. 계정 정의 하는 방법에 대 한 자세한 내용은 참조 [무인 실행 계정을 구성 &#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)합니다.|  
  
## <a name="connections-for-idbconnection"></a>IDbConnection에 대한 연결  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>만 지원하는 사용자 지정 데이터 처리 확장 프로그램을 사용하는 경우 다음과 같은 방법으로 연결을 지정해야 합니다.  
  
1.  무인 실행 계정을 구성합니다. 이 계정을 구성 하는 것은 사용 하 여 만든 연결에 필요 `IDbConnection`합니다. 보고서 서버에서는 연결할 때 계정을 가장합니다.  
  
2.  **자격 증명 사용 안 함**을 사용하도록 보고서의 데이터 원본 속성을 구성합니다.  
  
3.  데이터 원본에 연결하는 데 사용하는 자격 증명을 연결 문자열에 넣습니다.  
  
 사용 하는 경우 `IDbConnection`, 자격 증명 유형은 지원 되지 않습니다: 보안, Windows 사용자 계정 및 데이터베이스 자격 증명을 통합 합니다. 데이터 원본 연결이 이러한 옵션을 사용할 경우 보고서 서버에서 연결이 실패합니다.  
  
## <a name="connections-for-idbconnectionextension"></a>IDbConnectionExtension에 대한 연결  
 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>을 지원하는 사용자 지정 데이터 처리 확장 프로그램을 사용하는 경우 다음과 같은 방법으로 연결을 지정할 수 있습니다.  
  
|자격 증명|Connections|  
|-----------------|-----------------|  
|통합 보안|Windows 통합된 보안 사용 하는 사용자 지정 데이터 처리 확장 프로그램을 사용할 수 데이터 공급자에서 지원 가능한 경우 `IDbConnectionExtension`합니다.<br /><br /> 연결 문자열을 정의할 때는 통합된 보안을 지정 하는 인수를 포함 하십시오 수 (예를 들어 한 연결을 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본 포함 될 수 있습니다 `Integrated Security=SSPI` 연결 문자열에).|  
|Windows 인증|사용 하는 사용자 지정 데이터 처리 확장 프로그램에 대 한 Windows 도메인 사용자 계정을 사용할 수 데이터 공급자에서 지원 가능한 경우 `IDbConnectionExtension`합니다.<br /><br /> 보고서 서버에서는 데이터 처리 확장 프로그램이 호출되기 전에 사용자 계정을 가장합니다. 연결 문자열을 정의할 때는 통합된 보안을 지정 하는 인수를 포함 하십시오 수 (예를 들어 한 연결을 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본 포함 될 수 있습니다 `Integrated Security=SSPI` 연결 문자열에).|  
|데이터베이스 자격 증명|데이터베이스 인증을 사용하여 `IDbConnectionExtension`을 사용하는 사용자 지정 데이터 처리 확장 프로그램에 대한 연결을 구성할 수 있습니다.|  
|자격 증명 사용 안 함|무인 실행 계정을 지정하면 연결 문자열에 따라 사용되는 자격 증명이 결정됩니다.<br /><br /> 무인 실행 계정을 정의하지 않은 경우 보고서 서버에서 연결이 실패합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [무인된 실행 계정을 구성 &#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](specify-credential-and-connection-information-for-report-data-sources.md)   
 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [데이터 처리 확장 프로그램 구현](../extensions/data-processing/implementing-a-data-processing-extension.md)   
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)   
 [만들기, 삭제 또는 공유 데이터 원본을 수정 &#40;보고서 관리자&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [보고서에 대 한 데이터 원본 속성 구성 &#40;보고서 관리자&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  