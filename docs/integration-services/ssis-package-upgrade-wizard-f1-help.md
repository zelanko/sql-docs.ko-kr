---
title: "SSIS 패키지 업그레이드 마법사 F1 도움말 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.is.upgradewizard.ssisupgradewizard.f1
- sql13.is.upgradewizard.selectsourcelocation.f1
- sql13.is.upgradewizard.selectdestinationlocation.f1
- sql13.is.upgradewizard.selectpackagemgtoptions.f1
- sql13.is.upgradewizard.selectpackages.f1
- sql13.is.upgradewizard.completewizard.f1
- sql13.is.upgradewizard.upgradingpackage.f1
ms.assetid: 7fe886ff-1ea5-48d5-9d20-d5da36dd1cd7
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59869c0fdcb73fc30ee9bc763e8665f05f71df90
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="ssis-package-upgrade-wizard-f1-help"></a>SSIS 패키지 업그레이드 마법사 F1 도움말
  SSIS 패키지 업그레이드 마법사를 사용하여 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)](으)로 만든 패키지를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 현재 릴리스에 대한 패키지 형식으로 업그레이드할 수 있습니다.  
  
 **SSIS 패키지 업그레이드 마법사를 실행하려면**  
  
-   [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  

## <a name="ssis-upgrade-wizard"></a>SSIS 업그레이드 마법사
  
### <a name="options"></a>변수  
 **이 페이지를 다시 표시 안 함**  
 다음에 마법사를 열 때 시작 페이지를 표시하지 않습니다.  
 
## <a name="select-source-location-page"></a>[원본 위치 선택] 페이지
 **원본 위치 선택** 페이지를 사용하여 패키지를 업그레이드할 원본을 지정할 수 있습니다.  
  
> [!NOTE]  
>  이 페이지는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 또는 명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 패키지 업그레이드 마법사를 실행한 경우에만 사용할 수 있습니다.  
  
### <a name="static-options"></a>정적 옵션  
 **패키지 원본**  
 업그레이드할 패키지를 포함하는 저장소 위치를 선택합니다. 이 옵션에는 다음 표에 나열된 값이 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 시스템**|업그레이드할 패키지가 로컬 컴퓨터의 폴더에 있음을 나타냅니다.<br /><br /> 이러한 패키지를 업그레이드하기 전에 마법사가 원래 패키지를 백업하도록 하려면 원래 패키지를 파일 시스템에 저장해야 합니다. 자세한 내용은 방법 도움말 항목을 참조하십시오.|  
|**SSIS 패키지 저장소**|업그레이드할 패키지가 패키지 저장소에 있음을 나타냅니다. 패키지 저장소는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 관리하는 파일 시스템 폴더 집합으로 구성됩니다. 자세한 내용은 [패키지 관리&#40;SSIS 서비스&#41;](../integration-services/service/package-management-ssis-service.md)를 참조하세요.<br /><br /> 이 값을 선택하면 해당 **패키지 원본** 동적 옵션이 표시됩니다.|  
|**Microsoft SQL Server**|업그레이드할 패키지가 기존 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 있음을 나타냅니다.<br /><br /> 이 값을 선택하면 해당 **패키지 원본** 동적 옵션이 표시됩니다.|  
  
 **Folder**  
 업그레이드할 패키지를 포함하는 폴더의 이름을 입력하거나 **찾아보기** 를 클릭하여 폴더를 찾습니다.  
  
 **찾아보기**  
 업그레이드할 패키지를 포함하는 폴더를 찾습니다.  
  
### <a name="package-source-dynamic-options"></a>패키지 원본 동적 옵션  
  
#### <a name="package-source--ssis-package-store"></a>패키지 원본 = SSIS 패키지 저장소  
 **Server**  
 업그레이드할 패키지가 있는 서버의 이름을 입력하거나 목록에서 이 서버를 선택합니다.  
  
#### <a name="package-source--microsoft-sql-server"></a>패키지 원본 = Microsoft SQL Server  
 **Server**  
 업그레이드할 패키지가 있는 서버의 이름을 입력하거나 목록에서 이 서버를 선택합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하여 서버에 연결하려면 선택합니다.  
  
 **SQL Server 인증 사용**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 연결하려면 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
 **User name**  
 서버에 연결할 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증에 사용할 사용자 이름을 입력합니다.  
  
 **암호**  
 서버에 연결할 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증에 사용할 암호를 입력합니다.  
 
## <a name="select-destination-location-page"></a>[대상 위치 선택] 페이지
 **대상 위치 선택** 페이지를 사용하여 업그레이드된 패키지를 저장할 대상을 지정할 수 있습니다.  
  
> [!NOTE]  
>  이 페이지는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 또는 명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 패키지 업그레이드 마법사를 실행한 경우에만 사용할 수 있습니다.  
 
### <a name="static-options"></a>정적 옵션  
 **원본 위치에 저장**  
 업그레이드된 패키지를 마법사의 **원본 위치 선택** 페이지에서 지정한 것과 동일한 위치에 저장합니다.  
  
 원래 패키지가 파일 시스템에 저장되는 상태에서 마법사가 이러한 패키지를 백업하도록 하려면 **원본 위치에 저장** 옵션을 선택합니다. 자세한 내용은 [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)를 참조하세요.  
  
 **새 대상 위치 선택**  
 업그레이드된 패키지를 이 페이지에서 지정한 대상 위치에 저장합니다.  
  
 **패키지 원본**  
 업그레이드 패키지를 저장할 위치를 지정합니다. 이 옵션에는 다음 표에 나열된 값이 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 시스템**|업그레이드된 패키지를 로컬 컴퓨터의 폴더에 저장함을 나타냅니다.|  
|**SSIS 패키지 저장소**|업그레이드된 패키지를 Integration Services 패키지 저장소에 저장함을 나타냅니다. 패키지 저장소는 Integration Services 서비스에서 관리하는 파일 시스템 폴더 집합으로 구성됩니다. 자세한 내용은 [패키지 관리&#40;SSIS 서비스&#41;](../integration-services/service/package-management-ssis-service.md)를 참조하세요.<br /><br /> 이 값을 선택하면 해당 **패키지 원본** 동적 옵션이 표시됩니다.|  
|**Microsoft SQL Server**|업그레이드된 패키지를 기존 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 저장함을 나타냅니다.<br /><br /> 이 값을 선택하면 해당 **패키지 원본** 동적 옵션이 표시됩니다.|  
  
 **Folder**  
 업그레이드된 패키지를 저장할 폴더의 이름을 입력하거나 **찾아보기** 를 클릭하여 폴더를 찾습니다.  
  
 **찾아보기**  
 업그레이드된 패키지를 저장할 폴더를 찾습니다.  
  
### <a name="package-source-dynamic-options"></a>패키지 원본 동적 옵션  
  
#### <a name="package-source--ssis-package-store"></a>패키지 원본 = SSIS 패키지 저장소  
 **Server**  
 업그레이드 패키지를 저장할 서버의 이름을 입력하거나 목록에서 서버를 선택합니다.  
  
#### <a name="package-source--microsoft-sql-server"></a>패키지 원본 = Microsoft SQL Server  
 **Server**  
 업그레이드 패키지를 저장할 서버의 이름을 입력하거나 목록에서 이 서버를 선택합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하여 서버에 연결하려면 선택합니다.  
  
 **SQL Server 인증 사용**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 연결하려면 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
 **User name**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 연결할 때 사용할 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 연결할 때 사용할 암호를 입력합니다.  
 
## <a name="select-package-management-options-page"></a>[패키지 관리 옵션 선택] 페이지
  **패키지 관리 옵션 선택** 페이지를 사용하여 패키지 업그레이드 옵션을 지정할 수 있습니다.  
  
 **SSIS 패키지 업그레이드 마법사를 실행하려면**  
  
-   [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
### <a name="options"></a>변수  
 **새 공급자 이름을 사용하도록 연결 문자열 업데이트**  
 연결 문자열이 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]현재 버전의 다음 공급자에 대해 다음 이름을 사용하도록 업데이트합니다.  
  
-   OLE DB Provider for [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 업그레이드 마법사는 연결 관리자에 저장된 연결 문자열만 업데이트하며 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 식 언어 또는 스크립트 태스크의 코드를 사용하여 동적으로 생성된 연결 문자열은 업데이트하지 않습니다.  
  
 **업그레이드 패키지 유효성 검사**  
 업그레이드 패키지의 유효성을 검사하고 유효성 검사를 통과한 업그레이드 패키지만 저장합니다.  
  
 이 옵션을 선택하지 않으면 마법사는 업그레이드 패키지의 유효성을 검사하지 않습니다. 따라서 마법사는 패키지의 유효성 여부와 관계없이 모든 업그레이드 패키지를 저장합니다. 마법사는 마법사의 **대상 위치 선택** 페이지에서 지정한 대상에 업그레이드 패키지를 저장합니다.  
  
 유효성 검사로 인해 업그레이드 프로세스의 소요 시간이 늘어납니다. 성공적으로 업그레이드될 가능성이 높은 큰 패키지의 경우에는 이 옵션을 선택하지 않는 것이 좋습니다.  
  
 **새 패키지 ID 만들기**  
 업그레이드 패키지의 새 패키지 ID를 만듭니다.  
  
 **패키지 업그레이드 실패 시 업그레이드 프로세스 계속**  
 특정 패키지를 업그레이드할 수 없는 경우 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 업그레이드 마법사가 나머지 패키지를 계속 업그레이드하도록 지정합니다.  
  
 **패키지 이름 충돌**  
 마법사가 동일한 이름의 패키지를 처리하는 방법을 지정합니다. 이 옵션에는 다음 표에 나열된 값이 있습니다.  
  
 **기존 패키지 파일 덮어쓰기**  
 기존 패키지를 동일한 이름의 업그레이드 패키지로 바꿉니다.  
  
 **업그레이드 패키지 이름에 숫자 접미사 추가**  
 업그레이드 패키지의 이름에 숫자 접미사를 추가합니다.  
  
 **패키지 업그레이드 안 함**  
 패키지가 업그레이드되지 않도록 하고 마법사 완료 시 오류를 표시합니다.  
  
 이러한 옵션은 마법사의 **대상 위치 선택** 페이지에서 **원본 위치에 저장** 옵션을 선택한 경우 사용할 수 없습니다.  
  
 **구성 무시**  
 패키지 업그레이드를 사용 하는 동안 패키지 구성을 로드하지 않습니다. 이 옵션을 선택하면 패키지를 업그레이드 하는 데 필요한 시간이 줄어듭니다.  
  
 **원래 패키지 백업**  
 마법사가 **SSISBackupFolder** 폴더에 원래 패키지를 백업하도록 합니다. 마법사는 원래 패키지 및 업그레이드된 패키지가 포함된 폴더에 하위 폴더로 **SSISBackupFolder** 폴더를 만듭니다.  
  
> [!NOTE]  
>  이 옵션은 원래 패키지 및 업그레이드된 패키지가 파일 시스템의 동일한 폴더에 저장되도록 지정한 경우에만 사용할 수 있습니다.  

## <a name="select-packages-page"></a>[패키지 선택] 페이지
  **패키지 선택** 페이지를 사용하여 업그레이드할 패키지를 선택할 수 있습니다. 이 페이지에는 마법사의 **원본 위치 선택** 페이지에서 지정한 위치에 저장된 패키지가 나열됩니다.  
  
### <a name="options"></a>변수  
 **기존 패키지 이름**  
 업그레이드할 하나 이상의 패키지를 선택합니다.  
  
 **업그레이드 패키지 이름**  
 대상 패키지 이름을 입력하거나 마법사에서 제공하는 기본 이름을 사용합니다.  
  
> [!NOTE]  
>  패키지를 업그레이드한 후 대상 패키지 이름을 변경할 수도 있습니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 또는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 업그레이드된 패키지를 열고 패키지 이름을 변경합니다.  
  
 **암호**  
 선택한 업그레이드 패키지의 암호를 해독하는 데 사용되는 암호를 지정합니다.  
  
 **선택 항목에 적용**  
 선택한 업그레이드 패키지의 암호를 해독하기 위해 지정한 암호를 적용합니다.  
 
## <a name="complete-the-wizard-page"></a>[마법사 완료] 페이지
  **마법사 완료** 페이지를 사용하여 선택한 패키지 업그레이드 옵션을 검토하고 확인할 수 있습니다. 이는 뒤로 돌아가 이 마법사 세션의 옵션을 변경할 수 있는 마지막 마법사 페이지입니다.  
  
### <a name="options"></a>변수  
 **옵션 요약**  
 마법사에서 선택한 업그레이드 옵션을 검토합니다. 옵션을 변경하려면 **뒤로** 를 클릭하여 이전 마법사 페이지로 돌아갑니다.
 
## <a name="upgrading-the-packages-page"></a>[패키지 업그레이드] 페이지
  **패키지 업그레이드** 페이지를 사용하여 패키지 업그레이드의 진행률을 보고 업그레이드 프로세스를 중단할 수 있습니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 업그레이드 마법사는 선택된 패키지를 하나씩 업그레이드합니다.  
  
### <a name="options"></a>변수  
 **메시지 창**  
 업그레이드 프로세스 중 진행 메시지 및 요약 정보를 표시합니다.  
  
 **동작**  
 업그레이드 동작을 봅니다.  
  
 **상태**  
 각 동작의 결과를 봅니다.  
  
 **메시지**  
 각 동작에서 생성된 오류 메시지를 봅니다.  
  
 **중지**  
 패키지 업그레이드를 중지합니다.  
  
 **보고서**  
 패키지 업그레이드 결과가 포함된 보고서의 처리 옵션을 선택합니다.  
  
-   보고서를 온라인으로 봅니다.  
  
-   보고서를 파일에 저장합니다.  
  
-   보고서를 클립보드에 복사합니다.  
  
-   보고서를 전자 메일 메시지로 보냅니다.  

## <a name="view-upgraded-packages"></a>업그레이드된 패키지 보기
### <a name="view-upgraded-packages-that-were-saved-to-a-sql-server-database-or-to-the-package-store"></a>SQL Server 데이터베이스 또는 패키지 저장소에 저장된 업그레이드된 패키지 보기
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]의 개체 탐색기에서 로컬 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]인스턴스에 연결한 다음 **저장된 패키지** 노드를 확장하여 업그레이드된 패키지를 확인합니다.  
  
### <a name="view-upgraded-packages-that-were-upgraded-from-sql-server-data-tools"></a>SQL Server Data Tools에서 업그레이드된 패키지 보기  
  
[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 솔루션 탐색기에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 연 다음 **SSIS 패키지** 노드를 확장하여 업그레이드된 패키지를 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 패키지 업그레이드](../integration-services/install-windows/upgrade-integration-services-packages.md)  
  
  
