---
title: 업그레이드 관리자 (명령 프롬프트)를 실행 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], running
- command prompt [Upgrade Advisor]
- UpgradeAdvisorWizardCmd utility
- XML formats [Upgrade Advisor]
ms.assetid: 7c83049b-9227-4723-9b7f-66288bc6bd1d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 997d637d109c04dbecb3105538f51fa6ece0518f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092437"
---
# <a name="running-upgrade-advisor-command-prompt"></a>업그레이드 관리자 실행(명령 프롬프트)
  사용 된 **UpgradeAdvisorWizardCmd** 명령 프롬프트에서 업그레이드 관리자를 실행 하는 유틸리티입니다. XML 형식, 또는 쉼표로 구분된 값을 사용하는 파일로 결과를 받을 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
      UpgradeAdvisorWizardCmd [ -? ]  |   
    [ -ConfigFilefilename | <server_info> ]  
    [ -SqlUserlogin_id-SqlPasswordpassword ]  
    [ -CSV ]  
  
where <server_info> is any combination of the following:  
        -Serverserver_name-Instanceinstance_name-ASInstanceAS_instance_name-RSInstanceRS_instance_name  
```  
  
## <a name="arguments"></a>인수  
 **-?**  
 명령 구문을 표시합니다.  
  
 **-ConfigFile** _filename_  
 경로 이름 및 실행할 때 사용할 설정이 포함 된 XML 파일의 파일 이름을 합니다 **UpgradeAdvisorWizardCmd** 유틸리티입니다.  
  
 *<server_info>*  
 분석할 컴퓨터와 인스턴스를 지정합니다. 구성 파일을 사용하지 않는 경우 이 옵션을 사용하십시오.  
  
 *< 자유롭게 >* 다음 네 개의 인수의 조합일 수 있습니다.  
  
 **-Server** _server_name_  
 분석할 컴퓨터의 이름을 지정합니다. 로컬 컴퓨터(기본값) 또는 원격 컴퓨터일 수 있습니다.  
  
 **-Instance** _instance_name_  
 분석할 인스턴스의 이름을 지정합니다. 기본값은 없습니다. 이 매개 변수를 지정하지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 검색되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스에 대한 값은 MSSQLSERVER입니다. 명명된 인스턴스의 경우 인스턴스 이름을 사용합니다.  
  
 **-ASInstance**  _AS_instance_name_  
 분석할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 지정합니다. 기본값은 없습니다. 이 값을 지정하지 않으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]가 검색되지 않습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 기본 인스턴스에 대한 값은 MSSQLServerOLAPService입니다. 명명된 인스턴스의 경우 인스턴스 이름을 사용합니다.  
  
 **-RSInstance**  _RS_instance_name_  
 분석할 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스의 이름을 지정합니다. 기본값은 없습니다. 이 값을 지정하지 않으면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]가 검색되지 않습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 기본 인스턴스에 대한 값은 ReportServer입니다. 명명된 인스턴스의 경우 인스턴스 이름을 사용합니다.  
  
 **-SqlUser** _login_id_  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 이 값은 업그레이드 관리자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인입니다. 로그인을 지정하지 않으면 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다.  
  
 **-SqlPassword** _password_  
 사용 하는 경우는 **-SqlUser** 인수에이 인수를 사용 하 여 암호를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 합니다.  
  
 **-CSV**  
 표준 XML 결과 외에 쉼표로 구분된 값을 사용하여 .csv 파일로도 결과를 제공하도록 지정합니다. 결과 내 문서에 기록 됩니다\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor\110\Reports 폴더입니다.  
  
## <a name="return-values"></a>반환 값  
 다음 표에서 값입니다 **UpgradeAdvisorWizardCmd** 반환 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|분석이 성공했으며 업그레이드 문제가 발견되지 않았습니다.|  
|양의 정수|분석이 성공했으며 업그레이드 문제가 발견되었습니다.|  
|음의 정수|분석하지 못했습니다.|  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 사용자 이름과 암호를 제외하고 분석을 실행하는 데 필요한 모든 정보는 XML 구성 파일로 제공될 수 있습니다. 이 XML 구성 파일은 템플릿에 문서화되어 있습니다. 구성 파일을 사용하지 않는 경우에는 컴퓨터 이름과 인스턴스 이름을 지정하여 기본 설정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 설치된 구성 요소를 분석할 수 있습니다. 기본 구성 파일 설정에 대한 자세한 내용은 이 항목 뒷부분의 "요소 설명" 표를 참조하십시오.  
  
## <a name="configuration-file-template"></a>구성 파일 템플릿  
 다음 XML을 템플릿으로 사용하여 사용자가 원하는 구성 파일을 만들 수 있습니다. 사용자 조직의 요구 사항에 맞게 템플릿을 수정할 수 있습니다.  
  
```xml  
<Configuration>  
    <Server> </Server>  
    <Instance></Instance>  
    <Components>  
        <SQLServer>  
            <Databases>  
                <Database></Database>  
            </Databases>  
            <TraceFiles>  
                <TraceFile></TraceFile>  
            </TraceFiles>  
            <BatchFiles>  
                <BatchFile></BatchFile>  
            </BatchFiles>  
            <BatchSeparator></BatchSeparator>  
        </SQLServer>  
        <AnalysisServices>  
            <ASInstance></ASInstance>  
            <Databases>  
                <Database></Database>  
            </Databases>  
        </AnalysisServices>  
        <ReportingServices>  
            <RSInstance></RSInstance>  
        </ReportingServices>  
        <IntegrationServices>  
            <PackagePath></PackagePath>  
        </IntegrationServices>  
    </Components>  
</Configuration>  
```  
  
## <a name="element-descriptions"></a>요소 설명  
  
|태그|정의|발생 빈도|  
|---------|----------------|----------------|  
|`Configuration`|업그레이드 관리자 구성 파일에 대한 부모 요소입니다.|구성 파일마다 한 번 지정해야 합니다.|  
|`Server`|분석할 서버의 이름입니다.|구성 파일마다 한 번만 지정할 수 있습니다(옵션). 기본값은 로컬 컴퓨터입니다.|  
|`Instance`|분석할 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 이름입니다.|구성 파일마다 한 번만 지정할 수 있습니다(옵션). 기본값은 기본 인스턴스입니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 요소나 `IntegrationServices` 요소가 서버에 있는 경우에는 구성 파일마다 한 번 지정해야 합니다|  
|`Components`|분석할 구성 요소를 지정하는 요소를 포함합니다.|구성 파일마다 한 번 지정해야 합니다.|  
|`SQLServer`|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 대한 분석 설정을 포함합니다.|구성 파일마다 한 번만 지정할 수 있습니다(옵션). 지정하지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 데이터베이스가 분석되지 않습니다.|  
|`Databases` 요소용 `SQLServer`|분석할 데이터베이스의 목록을 포함합니다.|`SQLServer` 요소마다 한 번만 지정할 수 있습니다(옵션). 이 요소가 없으면 인스턴스의 모든 데이터베이스가 분석됩니다.|  
|`Database` 요소용 `SQLServer`|분석할 데이터베이스의 이름을 지정합니다.|`Databases` 요소가 있는 경우 한 번 이상 필요합니다. `Database` 요소에 "*" 값이 포함되면 인스턴스의 모든 데이터베이스가 분석됩니다. 기본값은 없습니다.|  
|`TraceFiles`|분석할 추적 파일의 목록을 포함합니다.|`SQLServer` 요소마다 한 번만 지정할 수 있습니다(옵션).|  
|`TraceFile`|분석할 추적 파일의 경로와 이름을 지정합니다.|`TraceFiles` 요소가 있는 경우 한 번 이상 필요합니다. 기본값은 없습니다.|  
|`BatchFiles`|분석할 배치 파일의 목록을 포함합니다.|`SQLServer` 요소마다 한 번만 지정할 수 있습니다(옵션).|  
|`BatchFile`|분석할 배치 파일을 지정합니다. 여러 개일 수 있습니다.|`BatchFiles` 요소가 있는 경우 한 번 이상 필요합니다. 기본값은 없습니다.|  
|`BatchSeparator`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배치 파일에 사용되는 일괄 처리 구분 기호를 지정합니다.|`SQLServer` 요소마다 한 번만 지정할 수 있습니다(옵션). 기본값은 GO입니다.|  
|`AnalysisServices`|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 분석 설정을 포함합니다.|구성 파일마다 한 번만 지정할 수 있습니다(옵션). 지정하지 않으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스가 분석되지 않습니다.|  
|`ASInstance`|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 이름을 지정합니다.|각 `AnalysisServices` 요소 당 한 번씩만 필요합니다. 기본값은 없습니다.|  
|`Databases` 요소용 `Analysis Services`|분석할 데이터베이스의 목록을 포함합니다.|`AnalysisServices` 요소마다 한 번만 지정할 수 있습니다(옵션). 이 요소가 없으면 인스턴스의 모든 데이터베이스가 분석됩니다.|  
|`Database` 요소용 `AnalysisServices`|분석할 데이터베이스의 이름을 지정합니다.|`Databases` 요소가 있는 경우 한 번 이상 필요합니다. `Database` 요소에 "*" 값이 포함되면 인스턴스의 모든 데이터베이스가 분석됩니다. 기본값은 없습니다.|  
|`ReportingServices`|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대해 분석을 실행하도록 지정합니다.|구성 파일마다 한 번만 지정할 수 있습니다(옵션). 지정하지 않으면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]가 분석되지 않습니다.|  
|`RSInstance`|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스 이름을 지정합니다.|각 `ReportingServices` 요소 당 한 번씩만 필요합니다. 기본값은 없습니다.|  
|`IntegrationServices`|에 대 한 분석 설정을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]합니다.|구성 파일마다 한 번만 지정할 수 있습니다(옵션). 지정하지 않으면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]가 분석되지 않습니다.|  
|`PackagePath`|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 집합의 경로를 지정합니다.|`IntegrationServices` 요소마다 한 번만 지정할 수 있습니다(옵션). 이 요소가 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 분석이 수행되며 외부에서 저장된 패키지는 분석되지 않습니다. 기본값은 없습니다.|  
  
## <a name="examples"></a>예  
  
### <a name="a-run-upgrade-advisor-using-a-configuration-file"></a>1. 구성 파일을 사용하여 업그레이드 관리자 실행  
 다음 예에서는 분석할 대상을 지정하는 구성 파일을 사용하여 명령 프롬프트에서 업그레이드 관리자를 실행하는 방법을 보여 줍니다. 이 예에서는 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결합니다.  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"  
```  
  
### <a name="b-run-upgrade-advisor-using-default-configuration-settings"></a>2. 기본 구성 설정을 사용하여 업그레이드 관리자 실행  
 다음 예에서는 기본 구성 설정과 Windows 인증을 사용하여 명령 프롬프트에서 업그레이드 관리자를 실행하는 방법을 보여 줍니다.  
  
```  
UpgradeAdvisorWizardCmd -Server MyServer -Instance MyInst   
```  
  
### <a name="c-run-upgrade-advisor-using-includessnoversionincludesssnoversion-mdmd-authentication"></a>3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 업그레이드 관리자 실행  
 다음 예에서는 구성 파일을 사용하여 명령 프롬프트에서 업그레이드 관리자를 실행하는 방법을 보여 줍니다. 이 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 이름과 암호를 지정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"   
    -SqlUser "MyUserName" -SqlPassword "QweRTy-55"  
```  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 문제 해결](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [업그레이드 관리자를 사용 하 여 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [업그레이드 관리자 실행 &#40;사용자 인터페이스&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)  
  
  
