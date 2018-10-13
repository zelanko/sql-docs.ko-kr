---
title: Integration Services 패키지 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, migrating
- migrating packages [Integration Services]
ms.assetid: 68dbdf81-032c-4a73-99f6-41420e053980
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d22744898dcc45ac213436afcdf25359ba24adec
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "49072207"
---
# <a name="upgrade-integration-services-packages"></a>Integration Services 패키지 업그레이드
  인스턴스를 업그레이드 하는 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 나 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 의 현재 릴리스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 기존 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 패키지는 현재 릴리스는 패키지 형식으로 자동 업그레이드 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 사용합니다. 직접 업그레이드 방법을 선택하고 수동으로 패키지를 업그레이드해야 합니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 패키지를 업그레이드할 때 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 모든 스크립트 태스크와 스크립트 구성 요소의 스크립트를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] VSTA([!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications)로 마이그레이션합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 스크립트 태스크나 스크립트 구성 요소의 스크립트는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] VSA([!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] for Applications)를 사용합니다. 마이그레이션 전에 스크립트에서 변경해야 할 내용과 스크립트 변환 실패에 대한 자세한 내용은 [VSTA로 스크립트 마이그레이션](../../sql-server/install/migrate-scripts-to-vsta.md)을 참조하세요.  
  
 프로젝트를 프로젝트 배포 모델로 변환할 때 패키지를 업그레이드하는 방법은 [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md)를 참조하십시오.  
  
## <a name="sql-server-2000-data-transformation-services-packages"></a>SQL Server 2000 데이터 변환 서비스 패키지  
 마이그레이션 또는 실행 Data Transformation Services (dts)도 지원 되지 않습니다 현재 릴리스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]합니다. 다음 DTS 기능이 더 이상 사용되지 않습니다.  
  
-   DTS 런타임  
  
-   DTS API  
  
-   DTS 패키지를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   다음 DTS 패키지 유지 관리 지원: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   DTS 2000 패키지 실행 태스크  
  
-   DTS 패키지의 업그레이드 관리자 검색입니다.  
  
 DTS 패키지를 마이그레이션하는 데 사용할 수 있는 옵션은 다음과 같습니다.  
  
-   패키지를 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 또는 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]로 마이그레이션한 다음 패키지를 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]로 업그레이드합니다.  
  
     [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 및 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]로의 DTS 패키지 마이그레이션에 대한 자세한 내용은 [데이터 변환 서비스 패키지 마이그레이션](http://go.microsoft.com/fwlink/?LinkId=251870)(2005) 및 [데이터 변환 서비스 패키지 마이그레이션](http://go.microsoft.com/fwlink/?LinkId=251871)(2008)을 참조하세요.  
  
-   [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]를 사용하여 DTS 패키지를 다시 만듭니다.  
  
     [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]의 새로운 기능에 대한 자세한 내용은 [새로운 기능&#40;Integration Services&#41;](../what-s-new-in-integration-services-in-sql-server-2016.md)을 참조하세요. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 구조에 대한 개요는 [Integration Services&#40;SSIS&#41; 패키지](../integration-services-ssis-packages.md)를 참조하세요.  
  
## <a name="selecting-an-upgrade-method"></a>업그레이드 방법 선택  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 패키지를 업그레이드하는 방법에는 여러 가지가 있습니다. 이 중에는 임시적인 업그레이드도 있고, 영구적인 업그레이드도 있습니다. 다음 표에서는 이러한 방법을 각각 설명하고 해당 업그레이드가 임시적인지, 영구적인지를 보여 줍니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 릴리스와 함께 설치되는 **dtexec** 유틸리티(dtexec.exe)를 사용하여 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 패키지를 실행하면 임시 패키지 업그레이드로 인해 실행 시간이 늘어납니다. 실행 시간의 증가 비율은 패키지 크기에 따라 달라집니다. 실행 시간이 늘어나지 않도록 하려면 패키지를 실행하기 전에 업그레이드하는 것이 좋습니다.  
  
|업그레이드 방법|업그레이드 유형|  
|--------------------|---------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 릴리스와 함께 설치되는 **dtexec** 유틸리티(dtexec.exe)를 사용하여 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 패키지를 실행합니다.<br /><br /> 자세한 내용은 [dtexec Utility](../packages/dtexec-utility.md)를 참조하세요.|패키지 업그레이드는 일시적입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 패키지의 경우 스크립트 마이그레이션은 일시적입니다.<br /><br /> 변경 내용을 저장할 수 없습니다.|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]패키지 파일을 엽니다.|패키지 업그레이드는 패키지를 저장하는 경우 영구적이고, 패키지를 저장하지 않는 경우에는 임시적입니다.<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 패키지의 경우 스크립트 업그레이드는 패키지를 저장하는 경우에는 영구적이고, 패키지를 저장하지 않는 경우에는 일시적입니다.|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서 기존 프로젝트에 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]패키지를 추가합니다.|패키지 업그레이드는 영구적입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 패키지의 경우 스크립트 마이그레이션은 영구적입니다.|  
|[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 에서 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 또는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]프로젝트 파일을 열고 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사를 사용하여 프로젝트의 여러 패키지를 업그레이드합니다.<br /><br /> 자세한 내용은 [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md) 및 [SSIS 패키지 업그레이드 마법사 F1 도움말](../ssis-package-upgrade-wizard-f1-help.md)을 참조하세요.|패키지 업그레이드는 영구적입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 패키지의 경우 스크립트 마이그레이션은 영구적입니다.|  
|최신 <xref:Microsoft.SqlServer.Dts.Runtime.Application.Upgrade%2A> 메서드를 사용하여 하나 이상의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 업그레이드하는 방법에는 여러 가지가 있습니다.|패키지 업그레이드는 영구적입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 패키지의 경우 스크립트 마이그레이션은 영구적입니다.|  
  
## <a name="custom-applications-and-custom-components"></a>사용자 지정 응용 프로그램 및 사용자 지정 구성 요소  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 사용자 지정 구성 요소는 현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 작동하지 않습니다.  
  
 현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 도구를 사용하여 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssIS](../../includes/ssis-md.md)] 사용자 지정 구성 요소가 포함된 패키지를 실행 및 관리할 수 있습니다. 버전 10.0.0.0([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)])에서 버전 11.0.0.0([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])으로 런타임 어셈블리를 리디렉션할 수 있도록 4개의 바인딩 리디렉션 규칙을 다음 파일에 추가했습니다.  
  
-   DTExec.exe.config  
  
-   dtshost.exe.config  
  
-   DTSWizard.exe.config  
  
-   DTUtil.exe.config  
  
-   DTExecUI.exe.config  
  
 사용 하도록 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 포함 된 패키지를 디자인 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 하 고 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 에 있는 devenv.exe.config 파일을 수정 해야 하는 사용자 지정 구성 요소  *\<드라이브 >*: files\ Microsoft Visual Studio 10.0\Common7\IDE 합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]용 런타임을 사용하여 빌드된 사용자 지정 응용 프로그램으로 이러한 패키지를 사용하려면 실행 파일에 대한 *.exe.config 파일의 구성 섹션에 리디렉션 파일을 포함하십시오. 규칙은 런타임 어셈블리를 버전11.0.0.0([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])으로 리디렉션합니다. 어셈블리 버전 리디렉션에 대한 자세한 내용은 [\<runtime>용 \<assemblyBinding>요소](http://msdn.microsoft.com/library/twy1dw1e.aspx)를 참조하세요.  
  
### <a name="locating-the-assemblies"></a>어셈블리 찾기  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 어셈블리는 .NET 4.0으로 업그레이드되었습니다. *\<드라이브>*:\Windows\Microsoft.NET\assembly에는 .NET 4에 대한 별도의 전역 어셈블리 캐시가 있습니다. 이 경로, 주로 GAC_MSIL 폴더에서 모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 어셈블리를 찾을 수 있습니다.  
  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서와 같이 핵심 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 확장성 .dll 파일도 *\<드라이브>*:\Program Files\Microsoft SQL Server\100\SDK\Assemblies에 있습니다.  
  
## <a name="understanding-sql-server-package-upgrade-results"></a>SQL Server 패키지 업그레이드 결과 이해  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 패키지에 포함된 대부분의 구성 요소 및 기능은 패키지 업그레이드 프로세스 중에 현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 구성 요소 및 기능으로 원활하게 변환됩니다. 하지만 업그레이드되지 않거나 업그레이드 결과에 주의해야 하는 몇 가지 구성 요소 및 기능이 있습니다. 다음 표에서는 이러한 구성 요소 및 기능을 보여 줍니다.  
  
> [!NOTE]  
>  이 표에 나열된 문제가 발생한 패키지를 확인하려면 업그레이드 관리자를 실행하십시오. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
|구성 요소 또는 기능|업그레이드 결과|  
|--------------------------|---------------------|  
|연결 문자열|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 패키지의 경우 특정 공급자의 이름이 변경되어 연결 문자열에 필요한 값이 달라졌습니다. 연결 문자열을 업데이트하려면 다음 절차 중 하나를 따르십시오.<br /><br /> - [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 업그레이드 마법사를 사용하여 패키지를 업그레이드하고 **새 공급자 이름을 사용하도록 연결 문자열 업데이트** 옵션을 선택합니다.<br /><br /> - [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 옵션 대화 상자에 있는 일반 페이지에서 **새 공급자 이름을 사용하도록 연결 문자열 업데이트** 옵션을 선택합니다. 이 옵션에 대한 자세한 내용은 [General Page](../general-page-of-integration-services-designers-options.md)를 참조하십시오.<br /><br /> - [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 열고 ConnectionString 속성의 텍스트를 수동으로 변경합니다.<br /><br /> 참고: 연결 문자열이 구성 파일 또는 데이터 원본 파일에 저장되어 있거나 식에서 `ConnectionString` 속성을 설정하는 경우에는 앞의 절차를 사용하여 연결 문자열을 업데이트할 수 없습니다. 이런 경우 연결 문자열을 업데이트하려면 파일 또는 식을 수동으로 업데이트해야 합니다.<br /><br /> 사용 가능한 데이터 소스에 대한 자세한 내용은 [데이터 소스](../connection-manager/data-sources.md)를 참조하세요.|  
|조회 변환|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 패키지의 경우 업그레이드 프로세스에서는 조회 변환을 현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]로 자동 업그레이드합니다. 하지만 이러한 구성 요소의 현재 버전에는 일부 유용한 기능이 추가되었습니다.<br /><br /> 자세한 내용은 [Lookup Transformation](../data-flow/transformations/lookup-transformation.md)을 참조하세요.|  
|스크립트 태스크 및 스크립트 구성 요소|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 패키지의 경우 업그레이드 프로세스에서는 스크립트 태스크 및 스크립트 구성 요소의 스크립트를 VSA에서 VSTA로 자동 마이그레이션합니다.<br /><br /> 마이그레이션 전에 스크립트에서 변경해야 할 내용과 스크립트 변환 실패에 대한 자세한 내용은 [VSTA로 스크립트 마이그레이션](../../sql-server/install/migrate-scripts-to-vsta.md)을 참조하세요.|  
  
### <a name="scripts-that-depend-on-adodbdll"></a>ADODB.dll을 사용하는 스크립트  
 ADODB.dll을 명시적으로 참조하는 스크립트 태스크 및 스크립트 구성 요소 스크립트는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 가 설치되지 않은 시스템에서 실행되거나 업그레이드되지 않을 수 있습니다. 이러한 스크립트 태스크 또는 스크립트 구성 요소 스크립트를 업그레이드하려면 ADODB.dll에 대한 종속성을 제거하는 것이 좋습니다.  Ado.Net은 VB 및 C# 스크립트와 같은 관리 코드에 대한 권장 대안입니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
-   msdn.microsoft.com의 기술 문서, [SQL Server 2012로 SSIS를 업그레이드하기 위한 5가지 팁](http://go.microsoft.com/fwlink/?LinkId=235321)  
  
-   blogs.msdn.com의 블로그 항목 - [기존 사용자 지정 SSIS 확장 프로그램 및 응용 프로그램을 Denali에서 사용되도록 설정](http://go.microsoft.com/fwlink/?LinkId=238157)  
  
-   channel9.msdn.com의 웹 캐스트 - [SSIS 패키지를 SQL Server 2012로 업그레이드](http://go.microsoft.com/fwlink/?LinkId=258674)  
  
  
