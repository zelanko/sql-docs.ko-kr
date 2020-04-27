---
title: 데이터 흐름 탭 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2d847adf-4b3d-4949-a195-ef43de275077
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a1938f2389f64d7a869ae924690b8b22fa209f82
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059913"
---
# <a name="data-flow-taps"></a>데이터 흐름 탭
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)]에는 런타임에 패키지의 데이터 흐름 경로에서 데이터 탭을 추가하고, 데이터 탭의 출력을 외부 파일에 전달할 수 있는 새로운 기능이 도입되었습니다. 이 기능을 사용하려면 프로젝트 배포 모델을 사용하여 SSIS 프로젝트를 SSIS 서버에 배포해야 합니다. 서버에 패키지를 배포한 후에는 패키지를 실행하기 전에 SSISDB 데이터베이스에 대해 T-SQL 스크립트를 실행하여 데이터 탭을 추가해야 합니다. 다음은 예제 시나리오입니다.  
  
1.  [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) 저장 프로시저를 사용하여 패키지의 실행 인스턴스를 만듭니다.  
  
2.  [catalog.add_data_tap](/sql/integration-services/system-stored-procedures/catalog-add-data-tap) 또는 [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid) 저장 프로시저를 사용하여 데이터 탭을 추가합니다.  
  
3.  [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)을 사용하여 패키지의 실행 인스턴스를 시작합니다.  
  
 다음은 위의 시나리오에 설명된 단계를 수행하는 예제 SQL 스크립트입니다.  
  
```  
  
Declare @execid bigint  
EXEC [SSISDB].[catalog].[create_execution] @folder_name=N'ETL Folder', @project_name=N'ETL Project', @package_name=N'Package.dtsx', @execution_id=@execid OUTPUT  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt'  
EXEC [SSISDB].[catalog].[start_execution] @execid  
  
```  
  
 create_execution 저장 프로시저의 폴더 이름, 프로젝트 이름 및 패키지 이름 매개 변수는 Integration Services 카탈로그의 폴더, 프로젝트 및 패키지 이름에 해당합니다. 다음 그림에 표시된 것처럼 폴더, 프로젝트 및 패키지 이름을 가져와서 SQL Server Management Studio에서 create_execution 호출을 사용할 수 있습니다. 여기에 SSIS 프로젝트가 나타나지 않으면 프로젝트를 SSIS 서버에 아직 배포하지 않았을 수 있습니다. Visual Studio에서 SSIS 프로젝트를 마우스 오른쪽 단추로 클릭하고 배포를 클릭하여 예상되는 SSIS 서버에 프로젝트를 배포합니다.  
  
 SQL 문을 입력하는 대신 다음 단계를 수행하여 실행 패키지 스크립트를 생성할 수 있습니다.  
  
1.  **Package.dtsx** 를 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다.  
  
2.  **스크립트** 도구 모음 단추를 클릭하여 스크립트를 생성합니다.  
  
3.  이제 start_execution을 호출하기 전에 add_data_tap 문을 추가합니다.  
  
 add_data_tap 저장 프로시저의 task_package_path 매개 변수는 Visual Studio 데이터 흐름 태스크의 PackagePath 속성에 해당합니다. Visual Studio에서 **데이터 흐름 태스크**를 마우스 오른쪽 단추로 클릭하고 **속성** 을 클릭하여 속성 창을 시작합니다.  **PackagePath** 속성 값을 확인하여 add_data_tap 저장 프로시저 호출에 대한 task_package_path 매개 변수 값으로 사용합니다.  
  
 add_data_tap 저장 프로시저의 dataflow_path_id_string 매개 변수는 데이터 탭을 추가할 데이터 흐름 경로의 IdentificationString 속성에 해당합니다. dataflow_path_id_string을 가져오려면 데이터 흐름 경로(데이터 흐름의 태스크 사이에 있는 화살표)를 클릭하고 속성 창에서 **IdentificationString** 속성 값을 확인합니다.  
  
 스크립트를 실행하면 출력 파일은 \<Program Files>\Microsoft SQL Server\110\DTS\DataDumps에 저장됩니다. 해당 이름을 가진 파일이 이미 있으면 접미사(예: output[1].txt)로 새 파일이 만들어집니다.  
  
 앞에서 설명한 대로 add_data_tap 저장 프로시저를 사용하는 대신 [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid)저장 프로시저를 사용할 수도 있습니다. 이 저장 프로시저는 task_package_path 대신 데이터 흐름 태스크의 ID를 매개 변수로 사용합니다. Visual Studio의 속성 창에서 데이터 흐름 태스크의 ID를 가져올 수 있습니다.  
  
## <a name="removing-a-data-tap"></a>데이터 탭 제거  
 [catalog.remove_data_tap](/sql/integration-services/system-stored-procedures/catalog-remove-data-tap) 저장 프로시저를 사용하여 실행을 시작하기 전에 데이터 탭을 제거할 수 있습니다. 이 저장 프로시저는 add_data_tap 저장 프로시저의 출력으로 가져올 수 있는 데이터 탭의 ID를 매개 변수로 사용합니다.  
  
```  
  
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
  
```  
  
## <a name="listing-all-data-taps"></a>모든 데이터 탭 나열  
 catalog.execution_data_taps 뷰를 사용하여 모든 데이터 탭을 나열할 수도 있습니다. 다음 예에서는 사양 실행 인스턴스(ID: 54)의 데이터 탭을 추출합니다.  
  
```  
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
## <a name="performance-consideration"></a>성능 고려 사항  
 자세한 로깅 수준을 사용하도록 설정하고 데이터 탭을 추가하면 데이터 통합 솔루션에서 수행되는 I/O 작업이 증가합니다. 따라서 문제 해결을 위해서만 데이터 탭을 추가하는 것이 좋습니다.  
  
## <a name="video"></a>비디오  
 이 [TechNet 비디오](https://technet.microsoft.com/sqlserver/dn600163) 에서는 프로그래밍 방식으로 패키지를 디버깅하고 런타임에 일부 결과를 캡처하는 데 도움이 되도록 SQL Server 2012 SSISDB 카탈로그에 데이터 탭을 추가/사용하는 방법을 보여 줍니다. 이러한 데이터 탭을 나열/제거하는 방법과 함께 SSIS 패키지의 데이터 탭을 사용하기 위한 최선의 구현 방법에 대해서도 설명합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [데이터 흐름 디버깅](troubleshooting/debugging-data-flow.md)  
  
 [패키지 실행 문제 해결 도구](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
