---
title: "Integration Services 패키지 업그레이드 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Integration Services, migrating
- migrating packages [Integration Services]
ms.assetid: 68dbdf81-032c-4a73-99f6-41420e053980
caps.latest.revision: 54
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a2e3655bedbb24f2174a62c8792cd168e7642592
ms.openlocfilehash: b04ba24fd90ec81e735933a45fed18294d77ceab
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="upgrade-integration-services-packages"></a>Integration Services 패키지 업그레이드
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 인스턴스를 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]릴리스로 업그레이드할 때는 기존 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 패키지가 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 릴리스에서 사용되는 패키지 형식으로 자동 업그레이드되지 않습니다. 직접 업그레이드 방법을 선택하고 수동으로 패키지를 업그레이드해야 합니다.  
  
 참조를 프로젝트 배포 모델로 프로젝트를 변환할 때 패키지를 업그레이드에 대 한 내용은 [배포할 Integration Services (SSIS) 프로젝트 및 패키지](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)
  
## <a name="selecting-an-upgrade-method"></a>업그레이드 방법 선택  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 패키지를 업그레이드하는 방법에는 여러 가지가 있습니다. 이 중에는 임시적인 업그레이드도 있고, 영구적인 업그레이드도 있습니다. 다음 표에서는 이러한 방법을 각각 설명하고 해당 업그레이드가 임시적인지, 영구적인지를 보여 줍니다.  
  
> [!NOTE]  
>  최신 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]릴리스와 함께 설치되는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]dtexec [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]유틸리티(dtexec.exe)를 사용하여 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , **,** 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]패키지를 실행하면 임시 패키지 업그레이드로 인해 실행 시간이 늘어납니다. 실행 시간의 증가 비율은 패키지 크기에 따라 달라집니다. 실행 시간이 늘어나지 않도록 하려면 패키지를 실행하기 전에 업그레이드하는 것이 좋습니다.  
  
|업그레이드 방법|업그레이드 유형|  
|--------------------|---------------------|  
|최신 **릴리스와 함께 설치되는** dtexec [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티(dtexec.exe)를 사용하여 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 패키지를 실행합니다.<br /><br /> 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)를 참조하세요.|패키지 업그레이드는 일시적입니다.<br /><br /> 변경 내용을 저장할 수 없습니다.|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]패키지 파일을 엽니다.|패키지 업그레이드는 패키지를 저장하는 경우 영구적이고, 패키지를 저장하지 않는 경우에는 임시적입니다.|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 기존 프로젝트에 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]패키지를 추가합니다.|패키지 업그레이드는 영구적입니다.|  
|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 에서 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]이상 프로젝트 파일을 열고 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사를 사용하여 프로젝트의 여러 패키지를 업그레이드합니다.<br /><br /> 자세한 내용은 [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md) 및 [SSIS 패키지 업그레이드 마법사 F1 도움말](../../integration-services/ssis-package-upgrade-wizard-f1-help.md)을 참조하세요.|패키지 업그레이드는 영구적입니다.|  
|최신 <xref:Microsoft.SqlServer.Dts.Runtime.Application.Upgrade%2A> 메서드를 사용하여 하나 이상의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 업그레이드하는 방법에는 여러 가지가 있습니다.|패키지 업그레이드는 영구적입니다.|  
  
## <a name="custom-applications-and-custom-components"></a>사용자 지정 응용 프로그램 및 사용자 지정 구성 요소  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 사용자 지정 구성 요소는 현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 작동하지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 도구의 최신 릴리스를 사용하여 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssIS](../../includes/ssis-md.md)] 사용자 지정 구성 요소를 포함하는 패키지를 실행하고 관리합니다. 런타임 어셈블리를 버전 10.0.0.0([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)])에서 버전 11.0.0.0([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])으로 또는 버전 12.0.0.0([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])에서 버전 13.0.0.0([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])으로 리디렉션할 수 있도록 4개의 바인딩 리디렉션 규칙을 다음 파일에 추가했습니다.  
  
-   DTExec.exe.config  
  
-   dtshost.exe.config  
  
-   DTSWizard.exe.config  
  
-   DTUtil.exe.config  
  
-   DTExecUI.exe.config  
  
 사용 하도록 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 포함 된 패키지를 디자인 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에 있는 devenv.exe.config 파일을 수정 해야 하는 사용자 지정 구성 요소  *\<드라이브 >*: files\microsoft Visual Studio 10.0\Common7\IDE 합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]용 런타임을 사용하여 빌드된 사용자 지정 응용 프로그램으로 이러한 패키지를 사용하려면 실행 파일에 대한 *.exe.config 파일의 구성 섹션에 리디렉션 파일을 포함하십시오. 규칙은 런타임 어셈블리를 버전 13.0.0.0([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])으로 리디렉션합니다. 어셈블리 버전 리디렉션에 대 한 자세한 내용은 참조 [ \<assemblyBinding > 요소에 대 한 \<런타임 >](http://msdn.microsoft.com/library/twy1dw1e.aspx)합니다.  
  
### <a name="locating-the-assemblies"></a>어셈블리 찾기  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 어셈블리는 .NET 4.0으로 업그레이드되었습니다. .NET 4에에 대 한 별도 전역 어셈블리 캐시가  *\<드라이브 >*: \Windows\Microsoft.NET\assembly 합니다. 이 경로, 주로 GAC_MSIL 폴더에서 모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 어셈블리를 찾을 수 있습니다.  
  
 이전 버전의와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 핵심 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 확장성.dll 파일에도 있습니다  *\<드라이브 >*: files\microsoft SQL Server\130\SDK\Assemblies 합니다.  
  
## <a name="understanding-sql-server-package-upgrade-results"></a>SQL Server 패키지 업그레이드 결과 이해  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 패키지에 포함된 대부분의 구성 요소 및 기능은 패키지 업그레이드 프로세스 중에 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]릴리스의 해당 구성 요소 및 기능으로 원활하게 변환됩니다. 하지만 업그레이드되지 않거나 업그레이드 결과에 주의해야 하는 몇 가지 구성 요소 및 기능이 있습니다. 다음 표에서는 이러한 구성 요소 및 기능을 보여 줍니다.  
  
> [!NOTE]  
>  이 표에 나열된 문제가 발생한 패키지를 확인하려면 업그레이드 관리자를 실행하십시오.  
  
|구성 요소 또는 기능|업그레이드 결과|  
|--------------------------|---------------------|  
|연결 문자열|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 패키지의 경우 특정 공급자의 이름이 변경되어 연결 문자열에 필요한 값이 달라졌습니다. 연결 문자열을 업데이트하려면 다음 절차 중 하나를 따르십시오.<br /><br /> [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사를 사용하여 패키지를 업그레이드하고 **새 공급자 이름을 사용하도록 연결 문자열 업데이트** 옵션을 선택합니다.<br /><br /> [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 옵션 대화 상자에 있는 일반 페이지에서 **새 공급자 이름을 사용하도록 연결 문자열 업데이트** 옵션을 선택합니다. 이 옵션에 대 한 자세한 내용은 일반 페이지를 참조 하십시오.<br /><br /> [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 열고 ConnectionString 속성의 텍스트를 수동으로 변경합니다.<br /><br /> 참고: 연결 문자열이 구성 파일 또는 데이터 원본 파일에 저장되어 있거나 식에서 **ConnectionString** 속성을 설정하는 경우에는 앞의 절차를 사용하여 연결 문자열을 업데이트할 수 없습니다. 이런 경우 연결 문자열을 업데이트하려면 파일 또는 식을 수동으로 업데이트해야 합니다.<br /><br /> 사용 가능한 데이터 소스에 대한 자세한 내용은 [데이터 소스](../../integration-services/connection-manager/data-sources.md)를 참조하세요.|  
  
### <a name="scripts-that-depend-on-adodbdll"></a>ADODB.dll을 사용하는 스크립트  
 ADODB.dll을 명시적으로 참조하는 스크립트 태스크 및 스크립트 구성 요소 스크립트는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 가 설치되지 않은 시스템에서 실행되거나 업그레이드되지 않을 수 있습니다. 이러한 스크립트 태스크 또는 스크립트 구성 요소 스크립트를 업그레이드하려면 ADODB.dll에 대한 종속성을 제거하는 것이 좋습니다.  Ado.Net은 VB 및 C# 스크립트와 같은 관리 코드에 대한 권장 대안입니다.  
  
  
