---
title: catalog.add_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: a25ebcc7-535e-4619-adf6-4e2b5a62ba37
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ddfe02301128ef54a4dcd91778b5ed736d2b12e8
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogadddatatap"></a>catalog.add_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  실행 패키지에 대한 패키지 데이터 흐름에서 구성 요소 출력에 데이터 탭을 추가합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.add_data_tap [ @execution_id = ] execution_id  
, [ @task_package_path = ] task_package_path  
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [ @execution_id = ] *execution_id*  
 패키지를 포함한 실행의 실행 ID입니다. *execution_id*는 **bigint**입니다.  
  
 [ @task_package_path = ] *task_package_path*  
 데이터 흐름 태스크의 패키지 경로입니다. 데이터 흐름 태스크에 대한 **PackagePath** 속성에서 이 경로를 지정합니다. 경로는 대/소문자를 구분합니다. 패키지 경로를 찾으려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 데이터 흐름 태스크를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **PackagePath** 속성이 **속성** 창에 표시됩니다.  
  
 *task_package_path*는 **nvarchar(max)** 입니다.  
  
 [ @dataflow_path_id_string = ] *dataflow_path_id_string*  
 데이터 흐름 경로의 ID 문자열입니다. 경로는 두 개의 데이터 흐름 구성 요소를 연결합니다. 경로에 대한 **IdentificationString** 속성에서 이 문자열을 지정합니다.  
  
 ID 문자열을 찾으려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 두 데이터 흐름 구성 요소 사이의 경로를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **IdentificationString** 속성이 **속성** 창에 표시됩니다.  
  
 *dataflow_path_id_string*은 **nvarchar(4000)** 입니다.  
  
 [ @data_filename = ] *data_filename*  
 탭 데이터를 저장하는 파일의 이름입니다. 데이터 흐름 태스크가 Foreach 루프 또는 For 루프 컨테이너 내부에서 실행되는 경우 각 루프 반복에 대한 탭 데이터가 개별 파일에 저장됩니다. 각 파일은 반복에 해당하는 번호가 접두사로 붙습니다.  
  
 파일은 기본적으로 \<*드라이브*>:\Program Files\Microsoft SQL Server\130\DTS\DataDumps 폴더에 저장됩니다.  
  
 *data_filename*은 **nvarchar(4000)** 입니다.  
  
 [ @max_rows = ] *max_rows*  
 데이터 탭 도중 캡처하는 행 수입니다. 이 값을 지정하지 않으면 모든 행이 캡처됩니다. *max_rows*는 **int**입니다.  
  
 [ @data_tap_id = ] *data_tap_id*  
 데이터 탭의 ID를 반환합니다. *data_tap_id*는 **bigint**입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 데이터 흐름 태스크 `'Paths[OLE DB Source.OLE DB Source Output]`의 데이터 흐름 경로 `\Package\Data Flow Task`에 데이터 탭을 만듭니다. 탭 데이터는 DataDumps 폴더(\<*드라이브*>:\Program Files\Microsoft SQL Server\130\DTS\DataDumps)의 `output0.txt` 파일에 저장됩니다.  
  
```sql
Declare @execution_id bigint  
Exec SSISDB.Catalog.create_execution @folder_name='Packages',@project_name='SSISPackages', @package_name='Package.dtsx',@reference_id=Null, @use32bitruntime=False, @execution_id=@execution_id OUTPUT  
  
Exec SSISDB.Catalog.set_execution_parameter_value @execution_id,50, 'LOGGING_LEVEL', 0  
  
Exec SSISDB.Catalog.add_data_tap @execution_id, @task_package_path='\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[OLE DB Source.OLE DB Source Output]', @data_filename = 'output0.txt'  
  
Exec SSISDB.Catalog.start_execution @execution_id  
```  
  
## <a name="remarks"></a>Remarks  
 데이터 탭을 추가하려면 실행 인스턴스가 생성됨 상태([catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 뷰의 **status** 열 값이 1임)여야 합니다. 실행 인스턴스를 실행하면 상태 값이 변경됩니다. [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)을 호출하여 실행을 만들 수 있습니다.  
  
 다음은 add_data_tap 저장 프로시저에 대한 고려 사항입니다.  
  
-   실행에 부모 패키지 하나와 자식 패키지 하나 이상이 포함된 경우 데이터 탭을 수행하려는 각 패키지에 대해 데이터 탭을 추가해야 합니다.  
  
-   패키지에 이름이 같은 데이터 흐름 태스크가 두 개 이상 포함되어 있는 경우 task_package_path는 탭된 구성 요소 출력이 포함된 데이터 흐름 태스크를 고유하게 식별합니다.  
  
-   추가한 데이터 탭은 패키지 실행 전에는 유효성이 검사되지 않습니다.  
  
-   데이터 탭 도중에 캡처되는 행 수를 제한하여 대용량 데이터 파일이 생성되지 않도록 하는 것이 좋습니다. 저장 프로시저가 실행되는 컴퓨터에 데이터 파일을 위한 저장 공간이 부족한 경우 패키지 실행이 중지되고 오류 메시지가 로그에 기록됩니다.  
  
-   add_data_tap 저장 프로시저를 실행하면 패키지의 성능에 영향을 미칩니다. 이 저장 프로시저는 데이터 문제 해결을 위해서만 실행하는 것이 좋습니다.  
  
-   탭 데이터가 저장되는 파일에 액세스하려면 저장 프로시저가 실행되는 컴퓨터에 대한 관리자여야 합니다. 또한 해당 데이터 탭이 있는 패키지가 포함된 실행을 시작한 사용자여야 합니다.  
  
## <a name="return-codes"></a>반환 코드  
 0(성공)  
  
 저장 프로시저가 실패하면 오류를 반환합니다.  
  
## <a name="result-set"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 MODIFY 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 저장 프로시저 실패 조건을 설명합니다.  
  
-   사용자에게 MODIFY 권한이 없습니다.  
  
-   지정된 패키지의 지정 구성 요소에 대한 데이터 탭이 이미 추가되었습니다.  
  
-   캡처할 행 수에 지정된 값이 잘못되었습니다.  
  
## <a name="requirements"></a>요구 사항  
  
## <a name="external-resources"></a>외부 리소스  
 raffael-alas.com의 블로그 항목 - [SSIS 2012: 데이터 탭 살펴보기](http://go.microsoft.com/fwlink/?LinkId=239983)  
  
## <a name="see-also"></a>참고 항목  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
