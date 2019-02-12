---
title: Reporting Services WMI 공급자 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- Reporting Services WMI Provider
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services]
- programming [Reporting Services]
ms.assetid: 22cfbeb8-4ea3-4182-8f54-3341c771e87b
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 688e72a1493a39217d786c312269a36778187306
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040594"
---
# <a name="access-the-reporting-services-wmi-provider"></a>Reporting Services WMI 공급자 액세스
  Reporting Services WMI 공급자는 스크립팅을 통해 기본 모드 보고서 서버 인스턴스를 관리하기 위해 두 WMI 클래스를 제공합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 릴리스부터는 WMI 공급자가 기본 모드 보고서 서버에 대해서만 지원됩니다. SharePoint 모드 보고서 서버는 SharePoint 중앙 관리 페이지 및 PowerShell 스크립트를 사용하여 관리할 수 있습니다.  
  
|클래스|Namespace|Description|  
|-----------|---------------|-----------------|  
|MSReportServer_Instance|root\Microsoft\SqlServer\ReportServer\RS_*\<EncodedInstanceName>* \v11|클라이언트에서 설치된 보고서 서버에 연결하는 데 필요한 기본 정보를 제공합니다.|  
|MSReportServer_ConfigurationSetting|root\Microsoft\SqlServer\ReportServer\RS_*\<EncodedInstanceName>* \v11\Admin|보고서 서버 인스턴스의 설치 및 런타임 매개 변수를 나타냅니다. 이러한 매개 변수는 보고서 서버의 구성 파일에 저장됩니다.<br /><br /> **\*\* 중요 \*\*** 이 클래스는 관리 권한이 있어야만 액세스할 수 있습니다.|  
  
 각 보고서 서버 인스턴스에 대해 위의 각 클래스 인스턴스가 만들어집니다. 모든 Microsoft 또는 타사 도구를 사용하여 .NET Framework 자체에서 제공하는 WMI 프로그래밍 인터페이스를 포함하여 보고서 서버에서 제공하는 WMI 개체에 액세스할 수 있습니다. 이 항목에서는 PowerShell 명령 [Get-WmiObject](https://technet.microsoft.com/library/dd315295.aspx)를 사용하여 WMI 클래스 인스턴스에 액세스하고 사용하는 방법을 설명합니다.  
  
## <a name="determine-the-instance-name-in-the-namespace-string"></a>네임스페이스 문자열에서 인스턴스 이름 결정  
 Reporting Services WMI 클래스의 네임스페이스 경로에 있는 인스턴스 이름은 명명된 Reporting Services 인스턴스를 설치할 때 지정하는 인스턴스 이름의 인코딩입니다. 즉, 인스턴스 이름의 특수 문자가 인코딩됩니다. 예를 들어 밑줄(_)은 "_5f"로 인코딩되므로 인스턴스 이름 "My_Instance"는 WMI 네임스페이스 경로에서 "My_5fInstance"로 인코딩됩니다.  
  
 WMI 네임스페이스 경로에 보고서 서버 인스턴스의 인코딩된 인스턴스 이름을 나열하려면 다음 PowerShell 명령을 사용합니다.  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace root\Microsoft\SqlServer\ReportServer  -class __Namespace -ComputerName hostname | select Name  
```  
  
## <a name="access-the-wmi-classes-using-powershell"></a>PowerShell을 사용하여 WMI 클래스 액세스  
 WMI 클래스에 액세스하려면 다음 명령을 실행합니다.  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace <namespacename> -class <classname> -ComputerName <hostname>  
```  
  
 예를 들어 myrshost 호스트의 기본 보고서 서버 인스턴스에서 MSReportServer_ConfigurationSetting 클래스에 액세스하려면 다음 명령을 실행합니다. 이 명령을 제대로 수행하려면 기본 보고서 서버 인스턴스가 myrshost에 설치되어 있어야 합니다.  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERER\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost  
```  
  
 이 명령 구문은 모든 클래스 속성 이름 및 값을 출력합니다. 기본 보고서 서버 인스턴스(RS_MSSQLSERVER)의 네임스페이스에서 클래스에 액세스하더라도 MSReportServer_ConfigurationSetting 클래스의 모든 인스턴스가 반환됩니다. 예를 들어 기본 보고서 서버 인스턴스 및 SHAREPOINT라는 명명된 보고서 서버 인스턴스와 함께 myrshost가 설치되어 있는 경우 이 명령은 두 WMI 개체를 반환하고 두 보고서 서버 인스턴스의 속성 이름과 값을 출력합니다.  
  
 여러 인스턴스가 반환되는 경우 특정 클래스 인스턴스를 반환하려면 –Filter 매개 변수를 사용하여 InstanceName 등의 고유 값을 가진 속성에 따라 결과를 필터링합니다. 예를 들어 기본 보고서 서버 인스턴스의 WMI 개체만 반환하려면 다음 명령을 사용합니다.  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='MSSQLSERVER'"  
```  
  
## <a name="query-the-available-methods-and-properties"></a>사용 가능한 메서드 및 속성 쿼리  
 Reporting Services WMI 클래스 중 하나에서 사용할 수 있는 메서드 및 속성을 보려면 Get-WmiObject의 결과를 Get-Member 명령으로 전달합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost | Get-Member  
```  
  
 Reporting Services WMI 클래스의 메서드와 속성에 대 한 설명서를 참조 하십시오.  
  
## <a name="use-a-wmi-method-or-property"></a>WMI 메서드 또는 속성 사용  
 Reporting Services 클래스에 대한 WMI 개체가 있고 사용 가능한 메서드와 속성을 알면 이러한 메서드와 속성을 사용할 수 있습니다. 예를 들어 SharePoint 통합 모드에 SHAREPOINT라는 명명된 보고서 서버 인스턴스가 있는 경우 다음 명령 시퀀스를 사용하여 SharePoint 중앙 관리 사이트의 URL을 검색합니다.  
  
```  
PS C:\windows\system32> $rsconfig = Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='SHAREPOINT'"  
PS C:\windows\system32> $rsconfig.GetAdminSiteUrl()  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services WMI 공급자 라이브러리 참조&#40;SSRS&#41;](../wmi-provider-library-reference/reporting-services-wmi-provider-library-reference-ssrs.md)   
 [RSReportServer 구성 파일](../report-server/rsreportserver-config-configuration-file.md)  
  
  
