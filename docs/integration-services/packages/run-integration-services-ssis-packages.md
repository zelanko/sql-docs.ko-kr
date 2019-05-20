---
title: Integration Services(SSIS) 패키지 실행 | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageexecute.f1
- sql13.ssis.ssms.executepackage.f1
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fb256646e7bf71a2829cfa35ef70184d0b267748
ms.sourcegitcommit: 8d288ca178e30549d793c40510c4e1988130afb0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65805258"
---
# <a name="run-integration-services-ssis-packages"></a>Integration Services(SSIS) 패키지 실행

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행하려면 해당 패키지가 저장된 위치에 따라 여러 도구 중 하나를 사용할 수 있습니다. 도구는 다음 표에 나열되어 있습니다.  

> [!NOTE]
> 이 문서에서는 SSIS 패키지를 일반적으로 실행하는 방법 및 온-프레미스에서 패키지를 실행하는 방법을 설명합니다. 또한 다음 플랫폼에서 SSIS 패키지를 실행할 수도 있습니다.
> - **Microsoft Azure 클라우드** 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md) 및 [Azure에서 SSIS 패키지 실행](../lift-shift/ssis-azure-run-packages.md)을 참조하세요.
> - **Linux** 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 패키지를 저장하려면 프로젝트 배포 모델을 사용하여 프로젝트를 서버에 배포합니다. 자세한 내용은 [Integration Services(SSIS) 프로젝트 및 패키지 배포](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하세요.  
  
 SSIS 패키지 저장소, msdb 데이터베이스 또는 파일 시스템에 패키지를 저장하려면 패키지 배포 모델을 사용합니다. 자세한 내용은 [레거시 패키지 배포&#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)를 참조하세요.  
  
|도구|Integration Services 서버에 저장된 패키지|SSIS 패키지 저장소 또는 msdb 데이터베이스에 저장된 패키지|SSIS 패키지 저장소에 포함되는 위치 외부에 있는 파일 시스템에 저장된 패키지|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|아니오|아니오<br /><br /> 그러나 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소(msdb 데이터베이스 포함)에서 프로젝트에 기존 패키지를 추가할 수 있습니다. 이러한 방식으로 프로젝트에 기존 패키지를 추가하면 파일 시스템에 패키지의 로컬 복사본을 만들 수 있습니다.|예|  
|**SQL Server Management Studio(Integration Services 서버를 호스트하는 데이터베이스 엔진의 인스턴스에 연결된 경우)**<br /><br /> 자세한 내용은 [Execute Package Dialog Box](#execute_package_dialog)를 참조하세요.|예|아니오<br /><br /> 그러나 이러한 위치에서 서버에 패키지를 가져올 수 있습니다.|아니오<br /><br /> 그러나 파일 시스템에서 서버에 패키지를 가져올 수 있습니다.|
|**SQL Server Management Studio(규모 확장 마스터로 사용되는 Integration Services 서버를 호스트하는 데이터베이스 엔진의 인스턴스에 연결된 경우)**<br /><br /> 자세한 내용은 [규모 확장 시 패키지 실행](../../integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.|예|아니오|아니오|
|**SQL Server Management Studio(SSIS 패키지 저장소를 관리하는 Integration Services 서비스에 연결된 경우)**|아니오|예|아니오<br /><br /> 그러나 파일 시스템에서 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소로 패키지를 가져올 수 있습니다.|  
|**dtexec**<br /><br /> 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)를 참조하세요.|예|예|예|  
|**dtexecui**<br /><br /> 자세한 내용은 [패키지 실행 유틸리티&#40;DtExecUI&#41; UI 참조](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)를 참조하세요.|아니오|예|예|  
|**SQL Server 에이전트**<br /><br /> 패키지를 예약하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 사용합니다.<br /><br /> 자세한 내용은 [SQL Server Agent Jobs for Packages](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)을 참조하세요.|예|예|예|  
|**기본 제공 저장 프로시저**<br /><br /> 자세한 내용은 [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)을 참조하세요.|예|아니오|아니오|  
| **<xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스의 형식 및 멤버를 사용하여 관리되는 API**|예|아니오|아니오|  
| **<xref:Microsoft.SqlServer.Dts.Runtime> 네임스페이스의 형식 및 멤버를 사용하여 관리되는 API**|현재는 아님|예|예|  

## <a name="execution-and-logging"></a>실행 및 로깅  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 대한 로깅을 활성화할 수 있으며 로그 파일에서 런타임 정보를 확인할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
 작업 보고서를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포되어 실행되는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 모니터링할 수 있습니다. 이 보고서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용할 수 있습니다. 자세한 내용은 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)을(를) 참조하세요.  
  
## <a name="run-a-package-in-sql-server-data-tools"></a>SQL Server Data Tools에서 패키지 실행
  패키지는 개발, 디버깅 및 테스팅이 이루어지는 동안 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 일반적으로 실행됩니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지를 실행하는 경우 패키지는 항상 즉시 실행됩니다.  
  
 패키지를 실행하는 동안 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 **진행률** 탭에 패키지 실행 진행률을 표시합니다. 패키지 및 패키지의 태스크 및 컨테이너의 시작 시각 및 종료 시각을 볼 수 있으며 또한 패키지 내의 실패한 모든 태스크 및 컨테이너에 대한 정보를 볼 수 있습니다. 패키지 실행이 종료되면 **실행 결과** 탭에서 런타임 정보를 확인할 수 있습니다. 자세한 내용은 [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md)항목의 "진행률 보고" 섹션을 참조하십시오.  
  
 **디자인 타임 배포**. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 패키지를 실행하면 패키지가 빌드된 다음 폴더에 배포됩니다. 패키지를 실행하기 전에 패키지가 배포되는 폴더를 지정할 수 있습니다. 폴더를 지정하지 않으면 **bin** 폴더가 기본적으로 사용됩니다. 이러한 종류의 배포를 디자인 타임 배포라고 부릅니다.  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>SQL Server Data Tools에서 패키지를 실행하려면  
  
1.  솔루션 탐색기에서 솔루션에 여러 프로젝트가 포함되어 있는 경우 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 폴더를 마우스 오른쪽 단추로 클릭한 다음 **시작 개체로 설정** 을 클릭하여 시작 프로젝트를 설정합니다.  
  
2.  솔루션 탐색기에서 프로젝트에 여러 패키지가 포함되어 있는 경우 패키지를 마우스 오른쪽 단추로 클릭한 다음 **시작 개체로 설정** 을 클릭하여 시작 패키지를 설정합니다.  
  
3.  패키지를 실행하려면 다음 절차 중 하나를 따릅니다.  
  
    -   실행하려는 패키지를 연 다음 메뉴 모음에서 **디버깅 시작** 을 클릭하거나 F5 키를 누릅니다. 패키지 실행이 완료된 다음 Shift+F5를 눌러서 디자인 모드로 돌아갑니다.  
  
    -   솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭한 다음 **패키지 실행**을 클릭합니다.  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>디자인 타임 배포를 위한 다른 폴더를 지정하려면  
  
1.  솔루션 탐색기에서 실행할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **\<프로젝트 이름> 속성 페이지** 대화 상자에서 **빌드**를 클릭합니다.  
  
3.  OutputPath 속성의 값을 업데이트하여 디자인 타임 배포에 사용할 폴더를 지정하고 **확인**을 클릭합니다.  


## <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 SSIS 서버에서 패키지 실행
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포한 후에는 서버에서 패키지를 실행할 수 있습니다.  
  
 작업 보고서를 사용하여 서버에서 실행되었거나 현재 실행 중인 패키지에 대한 정보를 볼 수 있습니다. 자세한 내용은 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)을(를) 참조하세요.  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 서버에서 패키지를 실행하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카탈로그가 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 **Integration Services 카탈로그** 노드와 **SSISDB** 노드를 차례로 확장하고, 배포한 프로젝트에 포함된 패키지로 이동합니다.  
  
3.  패키지 이름을 마우스 오른쪽 단추로 클릭하고 **실행**을 선택합니다.  
  
4.  **패키지 실행**대화 상자의 **매개 변수**, **연결 관리자** 및 **고급** 탭의 설정을 사용하여 패키지 실행을 구성합니다.  
  
5.  **확인** 을 클릭하여 패키지를 실행합니다.  
  
     -또는-  
  
     저장 프로시저를 사용하여 패키지를 실행합니다. **스크립트** 를 클릭하여 실행 인스턴스를 만들고 실행 인스턴스를 시작하는 Transact-SQL 문을 생성합니다. 문에는 catalog.create_execution, catalog.set_execution_parameter_value에 대한 호출과 catalog.start_execution 저장 프로시저가 포함되어 있습니다. 이러한 저장 프로시저에 대한 자세한 내용은 [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) 및 [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)을 참조하세요.  

## <a name="execute_package_dialog"></a> Execute Package Dialog Box
  **패키지 실행** 대화 상자를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 저장된 패키지를 실행할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 환경 변수에 값이 저장된 매개 변수를 포함할 수 있습니다. 이러한 패키지를 실행하려면 먼저 환경 변수 값을 제공하는 데 사용할 환경을 지정해야 합니다. 프로젝트에 여러 환경을 포함할 수는 있지만 실행할 때는 하나의 환경만 사용하여 환경 변수 값을 바인딩할 수 있습니다. 패키지에 사용되는 환경 변수가 없는 경우에는 환경이 필요하지 않습니다.  
  
 수행 작업  
  
-   [패키지 실행 대화 상자 열기](#open_dialog)  
  
-   [일반 페이지에서 옵션 설정](#general)  
  
-   [매개 변수 탭에서 옵션 설정](#parameters)  
  
-   [연결 관리자 탭에서 옵션 설정](#connection)  
  
-   [고급 탭에서 옵션 설정](#advanced)  
  
-   [패키지 실행 대화 상자의 옵션 스크립팅](#script)  
  
###  <a name="open_dialog"></a> 패키지 실행 대화 상자 열기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결합니다.  
  
     SSISDB 데이터베이스를 호스팅하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 노드를 표시합니다.  
  
3.  **SSISDB** 노드를 확장합니다.  
  
4.  실행할 패키지가 들어 있는 폴더를 확장합니다.  
  
5.  패키지를 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다.  
  
###  <a name="general"></a> 일반 페이지에서 옵션 설정  
 **환경** 을 선택하여 패키지 실행 시 적용할 환경을 지정합니다.  
  
###  <a name="parameters"></a> 매개 변수 탭에서 옵션 설정  
 **매개 변수** 탭에서 패키지 실행 시 사용되는 매개 변수 값을 수정합니다.  
  
###  <a name="connection"></a> 연결 관리자 탭에서 옵션 설정  
 연결 관리자 탭에서 패키지 연결 관리자 속성을 설정합니다.  
  
###  <a name="advanced"></a> 고급 탭에서 옵션 설정  
 고급 탭에서 속성 및 기타 패키지 설정을 관리합니다.  
  
 **추가**, **편집**, **제거**  
 속성을 추가, 편집 또는 제거하려면 클릭합니다.  
  
 **로깅 수준**  
 패키지 실행에 대한 로깅 수준을 선택합니다. 자세한 내용은 [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)를 참조하세요.  
  
 **오류 덤프**  
 패키지 실행 시 오류가 발생할 경우 덤프 파일을 생성할지 여부를 지정합니다. 자세한 내용은 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)을 참조하세요.  
  
 **32비트 런타임**  
 패키지가 32비트 시스템에서 실행되도록 지정합니다.  
  
###  <a name="script"></a> 패키지 실행 대화 상자의 옵션 스크립팅  
 **패키지 실행** 대화 상자에 있는 동안 도구 모음의 **스크립트** 단추를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 작성할 수도 있습니다. 생성된 스크립트는 **패키지 실행** 대화 상자에서 선택한 것과 동일한 옵션으로 [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) 저장 프로시저를 호출합니다. 이 스크립트는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 새 스크립트 창에 표시됩니다.  

## <a name="see-also"></a>참고 항목  
 [dtexec 유틸리티](../../integration-services/packages/dtexec-utility.md)   
[SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  
