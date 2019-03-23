---
title: 배포 및 저장 프로시저를 사용 하 여 SSIS 패키지 실행 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 60914b0c-1f65-45f8-8132-0ca331749fcc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 611f5c14390e2d30f275f76af21db8eae6fbcb3e
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58383192"
---
# <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>저장 프로시저를 사용하여 SSIS 패키지 배포 및 실행
  프로젝트 배포 모델을 사용하도록 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 구성하면 [!INCLUDE[ssIS](../includes/ssis-md.md)] 카탈로그의 저장 프로시저를 사용하여 프로젝트를 배포하고 패키지를 실행할 수 있습니다. 프로젝트 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하십시오.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 사용하여 프로젝트를 배포하고 패키지를 실행할 수도 있습니다. 자세한 내용은 **참고 항목** 섹션의 항목을 참조하십시오.  
  
> [!TIP]
>  다음을 수행하여 아래 절차에 나열된 저장 프로시저에 대한 Transact-SQL 문을 쉽게 생성할 수 있습니다. 단, catalog.deploy_project는 예외입니다.  
> 
>  1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **Integration Services 카탈로그** 노드를 확장하고 실행할 패키지로 이동합니다.  
> 2.  패키지를 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다.  
> 3.  필요에 따라 **고급** 탭에서 로깅 수준 등의 옵션을 설정하거나 매개 변수 값과 연결 관리자 속성을 설정합니다.  
> 
>      로깅 수준에 대한 자세한 내용은 [SSIS 서버에서 패키지 실행에 대한 로깅 설정](../../2014/integration-services/enable-logging-for-package-execution-on-the-ssis-server.md)을 참조하십시오.  
> 4.  **확인** 을 클릭하여 패키지를 실행하기 전에 **스크립트**를 클릭합니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 쿼리 편집기 창에 Transact-SQL이 나타납니다.  
  
## <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>저장 프로시저를 사용하여 패키지를 배포하고 실행하려면  
  
1.  [catalog.deploy_project&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database)를 호출하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 대한 패키지를 포함하는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 배포합니다.  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트 배포 파일의 이진 콘텐츠를 검색하려면 *@project_stream* 매개 변수에 대해 SELECT 문을 OPENROWSET 함수 및 BULK 행 집합 공급자와 함께 사용합니다. BULK 행 집합 공급자를 사용하여 파일에서 데이터를 읽을 수 있습니다. BULK 행 집합 공급자에 대한 SINGLE_BLOB 인수는 데이터 파일의 내용을 varbinary(max) 형식의 단일 행, 단일 열 행 집합으로 반환합니다. 자세한 내용은 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)을 참조하세요.  
  
     다음 예에서는 SSISPackages_ProjectDeployment 프로젝트를 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버의 SSIS Packages 폴더에 배포합니다. 프로젝트 파일(SSISPackage_ProjectDeployment.ispac)에서 이진 데이터를 읽어서 varbinary(max) 형식의 *@ProjectBinary* 매개 변수에 저장합니다. *@ProjectBinary* 매개 변수 값이 *@project_stream* 매개 변수에 할당됩니다.  
  
    ```  
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database)을 호출하여 프로젝트 실행 인스턴스를 만들고 필요에 따라 [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)를 호출하여 런타임 매개 변수 값을 설정합니다.  
  
     다음 예에서는 catalog.create_execution이 SSISPackage_ProjectDeployment 프로젝트에 포함된 package.dtsx에 대한 실행 인스턴스를 만듭니다. 프로젝트는 SSIS Packages 폴더에 있습니다. 저장 프로시저에서 반환된 execution_id가 catalog.set_execution_parameter_value 호출에 사용됩니다. 이 두 번째 저장 프로시저는 LOGGING_LEVEL 매개 변수를 3(자세한 로깅)으로 설정하고 Parameter1이라는 패키지 매개 변수의 값을 1로 설정합니다.  
  
     LOGGING_LEVEL과 같은 매개 변수의 object_type 값은 50입니다. 패키지 매개 변수의 object_type 값은 30입니다.  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)을 호출하여 패키지를 실행합니다.  
  
     다음 예에서는 패키지 실행 시작을 위해 catalog.start_execution 호출이 Transact-SQL에 추가됩니다. catalog.create_execution 저장 프로시저에서 반환된 execution_id가 사용됩니다.  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
## <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>저장 프로시저를 사용하여 서버 간에 프로젝트를 배포하려면  
 [catalog.get_project&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database) 및 [catalog.deploy_project&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database) 저장 프로시저를 사용하여 서버 간에 프로젝트를 배포할 수 있습니다.  
  
 저장 프로시저를 실행하기 전에 다음을 수행해야 합니다.  
  
-   연결된 서버 개체를 만듭니다. 자세한 내용은 [연결된 서버 만들기&#40;SQL Server 데이터베이스 엔진&#41;](../database-engine/sql-server-database-engine-overview.md)를 참조하세요.  
  
     **연결된 서버 속성** 대화 상자의 **서버 옵션** 페이지에서 **RPC** 와 **RPC 내보내기** 를 **True**로 설정합니다. **RPC에 대한 분산 트랜잭션 승격 설정** 도 **False**로 설정합니다.  
  
-   개체 탐색기의 **연결된 서버** 에서 **공급자** 노드를 확장하고 공급자를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭하여 연결된 서버에 대해 선택된 공급자에 동적 매개 변수를 사용하도록 설정합니다. **동적 매개 변수** 옆에서 **사용**을 선택합니다.  
  
-   DTC(Distributed Transaction Coordinator)가 두 서버에서 모두 시작되었는지 확인합니다.  
  
 catalog.get_project를 호출하여 프로젝트에 대한 이진값을 반환하고 catalog.deploy_project를 호출합니다. catalog.get_project에서 반환된 값이 varbinary(max) 형식의 테이블 변수에 삽입됩니다. 연결된 서버에서는 varbinary(max) 형식의 결과를 반환할 수 없습니다.  
  
 다음 예에서는 catalog.get_project가 연결된 서버의 SSISPackages 프로젝트에 대한 이진값을 반환합니다. catalog.deploy_project가 로컬 서버의 DestFolder 폴더에 프로젝트를 배포합니다.  
  
```  
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 서버에 프로젝트 배포](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [SQL Server Data Tools에서 패키지 실행](../../2014/integration-services/run-a-package-in-sql-server-data-tools.md)   
 [SQL Server Management Studio를 사용하여 SSIS 서버에서 패키지 실행](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  
