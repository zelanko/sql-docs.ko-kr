---
title: 데이터 흐름 디버깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a67815d20a1275d8ae77042c89f76189748d336
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65713734"
---
# <a name="debugging-data-flow"></a>데이터 흐름 디버깅

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 데이터 흐름 문제를 해결하는 데 사용할 수 있는 기능과 도구가 포함됩니다.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 데이터 뷰어를 제공합니다.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 변환은 행 개수를 확인합니다.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 런타임에 진행률을 보고합니다.  
  
## <a name="data-viewers"></a>데이터 뷰어  
 데이터 뷰어는 두 구성 요소 간 데이터를 데이터 흐름으로 표시합니다. 데이터 뷰어는 데이터 원본에서 데이터가 추출되어 처음으로 데이터 흐름에 들어갈 때, 변환으로 데이터가 업데이트되기 전/후와 데이터가 해당 대상으로 로드되기 전에 데이터를 표시합니다.  
  
 데이터를 보려면 두 데이터 흐름 구성 요소를 연결하는 경로에 데이터 뷰어를 연결합니다. 데이터 흐름 구성 요소 간의 데이터를 확인하면 예기치 않은 데이터 값을 확인하고, 변환으로 열 값이 변경되는 방식을 확인하고, 변환이 실패하는 이유를 확인하는 등의 작업을 더 쉽게 수행할 수 있습니다. 예를 들어 참조 테이블에서 실패한 조회를 확인하고 이를 수정하기 위해 빈 열에 대해 기본 데이터를 제공하는 변환을 추가할 수 있습니다.  
  
 데이터 뷰어는 표에 데이터를 표시할 수 있습니다. 표를 사용하면 표시할 열을 선택할 수 있습니다. 선택한 열의 값은 표 형식으로 표시됩니다.  
  
 또한 경로에 여러 데이터 뷰어를 포함시킬 수 있습니다. 동일 데이터를 여러 형식으로 표시하거나(예: 데이터의 차트 뷰 및 표 뷰 만들기) 데이터의 여러 열에 대해 서로 다른 데이터 뷰어를 만들 수 있습니다.  
  
 데이터 뷰어를 경로에 추가하면 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 **데이터 흐름** 탭의 디자인 화면에서 경로 옆에 데이터 뷰어 아이콘을 추가합니다. 조건부 분할 변환과 같이 여러 출력을 포함할 수 있는 변환에는 각 경로에 데이터 뷰어가 포함될 수 있습니다.  
  
 런타임에 **데이터 뷰어** 창이 열리고 데이터 뷰어 형식으로 지정된 정보가 표시됩니다. 예를 들어 표 형식을 사용하는 데이터 뷰어는 선택된 열, 데이터 흐름 구성 요소로 전달된 출력 행의 수 및 표시된 행의 수에 대한 데이터를 표시합니다. 이 정보는 버퍼별로 표시되며 버퍼에 포함되는 행의 수는 데이터 흐름에서 행의 폭에 따라 결정됩니다.  
  
 **데이터 뷰어** 대화 상자에서 데이터를 클립보드로 복사하고, 테이블에서 모든 데이터를 삭제하고, 데이터 뷰어를 다시 구성하고, 데이터 흐름을 재개하고, 데이터 뷰어를 연결하거나 연결을 끊을 수 있습니다.  
  
#### <a name="to-add-a-data-viewer"></a>데이터 뷰어를 추가하려면  
  
-   [데이터 흐름에 데이터 뷰어 추가](#add_viewer)  
  
## <a name="row-counts"></a>행 개수  
 경로를 통해 전달된 행 개수가 **디자이너의** 데이터 흐름 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭의 디자인 화면에서 경로 옆에 표시됩니다. 데이터가 경로를 통해 이동하는 동안 개수가 주기적으로 업데이트됩니다.  
  
 또한 행 개수 변환을 데이터 흐름에 추가하여 변수에서 마지막 행 개수를 캡처할 수 있습니다. 자세한 내용은 [Row Count Transformation](../../integration-services/data-flow/transformations/row-count-transformation.md)을 참조하세요.  
  
## <a name="progress-reporting"></a>진행률 보고  
 패키지를 실행할 때 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 상태를 나타내는 색으로 각 데이터 흐름 구성 요소를 표시하여 **데이터 흐름** 탭의 디자인 화면에 진행률을 표시합니다. 각 구성 요소에서 해당 작업 수행을 시작하면 색이 노란색으로 바뀌고, 성공적으로 완료되면 녹색으로 바뀝니다. 빨간색은 구성 요소가 실패했음을 나타냅니다.  
  
 다음 표에서는 색 구분 기능에 대해 설명합니다.  
  
|색|설명|  
|-----------|-----------------|  
|색 없음|데이터 흐름 엔진의 호출을 대기 중입니다.|  
|노란색|변환 수행, 데이터 추출 또는 데이터 로드 중입니다.|  
|녹색|성공적으로 실행되었습니다.|  
|red|실행 중 오류가 발생했습니다.|  

## <a name="analysis-of-data-flow"></a>데이터 흐름 분석
   [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) **SSISDB** 데이터베이스 뷰를 사용하여 패키지의 데이터 흐름을 분석할 수 있습니다. 이 뷰는 데이터 흐름 구성 요소가 다운스트림 구성 요소에 데이터를 전송할 때마다 행을 표시합니다. 이 정보를 사용하여 각 구성 요소로 보내진 행을 자세하게 파악할 수 있습니다.  
  
> [!NOTE]  
>  catalog.execution_data_statistics 뷰를 사용하여 정보를 캡처하려면 로깅 수준을 **자세히** 로 설정해야 합니다.  
  
 다음 예에서는 패키지의 구성 요소 간에 보내진 행 수를 표시합니다.  
  
```sql
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name   
```  
  
 다음 예에서는 특정 실행 중 각 구성 요소가 보낸 밀리초당 행 수를 계산합니다. 계산되는 값은 다음과 같습니다.  
  
-   **total_rows** - 구성 요소가 보낸 모든 행의 합계  
  
-   **wall_clock_time_ms** - 각 구성 요소에 대한 총 실행 경과 시간(밀리초)  
  
-   **num_rows_per_millisecond** - 각 구성 요소가 보낸 밀리초당 행 수  
  
 **HAVING** 절은 계산에서 0으로 나누기 오류를 방지하기 위해 사용됩니다.  
  
```sql  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
```  

## <a name="configure-an-error-output-in-a-data-flow-component"></a>데이터 흐름 구성 요소에서 오류 출력 구성
  많은 데이터 흐름 구성 요소가 오류 출력을 지원하며 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 구성 요소에 따라 오류 출력을 다르게 구성할 수 있는 방법을 제공합니다. 오류 출력을 구성하는 것 외에도 오류 출력의 열을 구성할 수도 있습니다. 이 작업에는 구성 요소에서 추가한 **ErrorCode** 및 **ErrorColumn** 열의 구성이 포함됩니다.  
  
### <a name="configuring-an-error-output"></a>오류 출력 구성  
 다음 두 가지 옵션을 사용하여 오류 출력을 구성할 수 있습니다.  
  
-   **오류 출력 구성** 대화 상자를 사용합니다. 이 대화 상자를 사용하면 오류 출력을 지원하는 데이터 흐름 구성 요소의 오류 출력을 구성할 수 있습니다.  
  
-   구성 요소의 편집기 대화 상자를 사용합니다. 일부 구성 요소는 해당 편집기 대화 상자에서 직접 오류 출력을 구성할 수 있습니다. 그러나 ADO.NET 원본, 열 가져오기 변환, OLE DB 명령 변환 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 대상의 편집기 대화 상자에서는 오류 출력을 구성할 수 없습니다.  
  
 다음 절차에서는 이러한 대화 상자를 사용하여 오류 출력을 구성하는 방법을 설명합니다.  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>오류 출력 구성 대화 상자를 사용하여 오류 출력을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **데이터 흐름** 탭을 클릭합니다.  
  
4.  오류의 원본에 해당하는 구성 요소에서 빨간 색 화살표로 표시된 오류 출력을 데이터 흐름의 다른 구성 요소로 끌어다 놓습니다.  
  
5.  구성 요소 입력의 각 열에 대해 **오류 출력 구성** 대화 상자의 **오류** 및 **잘림** 열에 있는 동작을 선택합니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>구성 요소의 편집기 대화 상자를 사용하여 오류 출력을 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **데이터 흐름** 탭을 클릭합니다.  
  
4.  오류 출력을 구성할 데이터 흐름 구성 요소를 두 번 클릭한 다음 구성 요소에 따라 다음 단계 중 하나를 수행합니다.  
  
    -   **오류 출력 구성**을 클릭합니다.  
  
    -   **오류 출력**을 클릭합니다.  
  
5.  각 열에 대한 **오류** 옵션을 설정합니다.  
  
6.  각 열에 대한 **잘림** 옵션을 설정합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
### <a name="configuring-error-output-columns"></a>오류 출력 열 구성  
 오류 출력 열을 구성하려면 **고급 편집기** 대화 상자의 **입/출력 속성** 탭을 사용해야 합니다.  
  
#### <a name="to-configure-error-output-columns"></a>오류 출력 열을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **데이터 흐름** 탭을 클릭합니다.  
  
4.  구성하려는 오류 출력 열이 있는 구성 요소를 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 클릭합니다.  
  
5.  **입/출력 속성** 탭을 클릭하고 **\<구성 요소 이름> 오류 출력**을 확장한 다음 **출력 열**을 확장합니다.  
  
6.  열을 클릭하고 속성을 업데이트합니다.  
  
    > [!NOTE]  
    >  열 목록은 구성 요소 입력 내의 열, 이전 오류 출력에서 추가한 **ErrorCode** 및 **ErrorColumn** 열, 현재 구성 요소에서 추가한 **ErrorCode** 및 **ErrorColumn** 열을 포함합니다.  
  
7.  **확인.**  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  

## <a name="add_viewer"></a> 데이터 흐름에 데이터 뷰어 추가
  이 항목에서는 데이터 흐름에 데이터 뷰어를 추가 및 구성하는 방법에 대해 설명합니다. 데이터 뷰어는 두 데이터 흐름 구성 요소 간에 이동하는 데이터를 표시합니다. 예를 들어 데이터 뷰어는 데이터 흐름 변환으로 데이터가 수정되기 전의 데이터 원본에서 추출한 데이터를 표시할 수 있습니다.  
  
 경로는 하나의 데이터 흐름 구성 요소의 출력을 다른 구성 요소의 입력에 연결함으로써 데이터 흐름의 구성 요소를 연결합니다.  
  
 패키지에 데이터 뷰어를 추가하려면 패키지에 데이터 흐름 태스크 및 최소한 두 개 이상의 연결된 데이터 흐름 구성 요소가 포함되어 있어야 합니다.  
  
 데이터 뷰어를 오류 출력에 추가하여 오류가 발생한 열의 오류 및 이름 설명을 봅니다. 기본적으로 오류 출력은 오류 및 열에 대한 숫자 식별자만 포함합니다.  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>데이터 흐름에 데이터 뷰어를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 이 아직 활성화되어 있지 않으면 탭을 클릭합니다.  
  
4.  데이터 흐름 태스크를 클릭하여 데이터 뷰어를 첨부할 데이터 흐름을 선택하고 **데이터 흐름** 탭을 클릭합니다.  
  
5.  두 데이터 흐름 구성 요소 간 경로를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.  
  
6.  **일반** 페이지에서 경로 속성을 보고 편집할 수 있습니다. 예를 들어 **PathAnnotation** 드롭다운 목록에서 경로 옆에 표시되는 주석을 선택할 수 있습니다.  
  
7.  **메타데이터** 페이지에서 열 메타데이터를 보고 메타데이터를 클립보드로 복사할 수 있습니다.  
  
8.  **데이터 뷰어** 페이지에서 **데이터 뷰어 사용**을 클릭합니다.  
  
9. 표시할 열 영역에서 데이터 뷰어에 표시할 열을 선택합니다. 기본적으로 사용 가능한 열이 모두 선택되어 **표시된 열** 목록에 나열됩니다. 사용하지 않을 열을 선택하고 왼쪽 화살표를 클릭하여 **사용되지 않은 열** 목록으로 이동합니다.  
  
    > [!NOTE]  
    >  표에서 DT_DATE, DT_DBTIME2, DT_FILETIME, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 및 DT_DBTIMESTAMPOFFSET 데이터 형식을 나타내는 값은 ISO 8601 형식 문자열로 표시되고 **T** 구분 기호는 공백 구분 기호로 대체됩니다. DT_DATE 및 DT_FILETIME 데이터 형식을 나타내는 값은 7자리의 소수 자릿수 초를 갖습니다. DT_FILETIME 데이터 형식은 3자리의 소수 자릿수 초만 저장하기 때문에 표에는 나머지 4자리가 0으로 표시됩니다. DT_DBTIMESTAMP 데이터 형식을 나타내는 값은 3자리의 소수 자릿수 초를 갖습니다. DT_DBTIME2, DT_DBTIMESTAMP2 및 DT_DBTIMESTAMPOFFSET 데이터 형식을 나타내는 값의 경우 소수 자릿수 초의 자릿수는 열의 데이터 형식에 대해 지정된 소수 자릿수에 해당합니다. ISO 8601 형식에 대한 자세한 내용은 [Date and Time Formats](https://msdn.microsoft.com/library/bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39)을 참조하십시오. 데이터 형식에 대한 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
10. **확인**을 클릭합니다.  

## <a name="data-flow-taps"></a>데이터 흐름 탭
 런타임에 패키지의 데이터 흐름 경로에서 데이터 탭을 추가하고 데이터 탭의 출력을 외부 파일에 전달할 수 있습니다. 이 기능을 사용하려면 프로젝트 배포 모델을 사용하여 SSIS 프로젝트를 SSIS 서버에 배포해야 합니다. 서버에 패키지를 배포한 후에는 패키지를 실행하기 전에 SSISDB 데이터베이스에 대해 T-SQL 스크립트를 실행하여 데이터 탭을 추가해야 합니다. 다음은 예제 시나리오입니다.  
  
1.  [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) 저장 프로시저를 사용하여 패키지의 실행 인스턴스를 만듭니다.  
  
2.  [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md) 또는 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md) 저장 프로시저를 사용하여 데이터 탭을 추가합니다.  
  
3.  [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)을 사용하여 패키지의 실행 인스턴스를 시작합니다.  
  
 다음은 위의 시나리오에 설명된 단계를 수행하는 예제 SQL 스크립트입니다.  
  
```sql
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
  
 앞에서 설명한 대로 add_data_tap 저장 프로시저를 사용하는 대신 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)저장 프로시저를 사용할 수도 있습니다. 이 저장 프로시저는 task_package_path 대신 데이터 흐름 태스크의 ID를 매개 변수로 사용합니다. Visual Studio의 속성 창에서 데이터 흐름 태스크의 ID를 가져올 수 있습니다.  
  
### <a name="removing-a-data-tap"></a>데이터 탭 제거  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md) 저장 프로시저를 사용하여 실행을 시작하기 전에 데이터 탭을 제거할 수 있습니다. 이 저장 프로시저는 add_data_tap 저장 프로시저의 출력으로 가져올 수 있는 데이터 탭의 ID를 매개 변수로 사용합니다.  
  
```sql
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
```  
  
### <a name="listing-all-data-taps"></a>모든 데이터 탭 나열  
 catalog.execution_data_taps 뷰를 사용하여 모든 데이터 탭을 나열할 수도 있습니다. 다음 예에서는 사양 실행 인스턴스(ID: 54)의 데이터 탭을 추출합니다.  
  
```sql 
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
### <a name="performance-consideration"></a>성능 고려 사항  
 자세한 로깅 수준을 사용하도록 설정하고 데이터 탭을 추가하면 데이터 통합 솔루션에서 수행되는 I/O 작업이 증가합니다. 따라서 문제 해결을 위해서만 데이터 탭을 추가하는 것이 좋습니다.  
  
### <a name="video"></a>비디오  
 이 [TechNet 비디오](https://technet.microsoft.com/sqlserver/dn600163) 에서는 프로그래밍 방식으로 패키지를 디버깅하고 런타임에 일부 결과를 캡처하는 데 도움이 되도록 SQL Server 2012 SSISDB 카탈로그에 데이터 탭을 추가/사용하는 방법을 보여 줍니다. 이러한 데이터 탭을 나열/제거하는 방법과 함께 SSIS 패키지의 데이터 탭을 사용하기 위한 최선의 구현 방법에 대해서도 설명합니다.  
 
## <a name="see-also"></a>참고 항목  
 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)  
  
  
