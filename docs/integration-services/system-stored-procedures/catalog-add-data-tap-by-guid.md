---
title: catalog.add_data_tap_by_guid | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: ed9d7fa3-61a1-4e21-ba43-1ead7dfc74eb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bbe729ebef5d156f6c946e0c5cda62c1cefdcd81
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65717200"
---
# <a name="catalogadddatatapbyguid"></a>catalog.add_data_tap_by_guid 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  실행 인스턴스에 대한 패키지 데이터 흐름에서 특정 데이터 흐름 경로에 데이터 탭을 추가합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog add_data_tap_by_guid [ @execution_id = ] execution_id  
, [ @dataflow_task_guid = ] dataflow_task_guid   
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>인수  
 [ @execution_id = ] *execution_id*  
 패키지를 포함한 실행의 실행 ID입니다. *execution_id*는 **bigint**입니다.  
  
 [ @dataflow_task_guid = ] *dataflow_task_guid*  
 탭할 데이터 흐름 경로를 포함하는 패키지 내 데이터 태스크 흐름의 ID입니다. *dataflow_task_guid*는 **uniqueidentifier**입니다.  
  
 [ @dataflow_path_id_string = ] *dataflow_path_id_string*  
 데이터 흐름 경로의 ID 문자열입니다. 경로는 두 개의 데이터 흐름 구성 요소를 연결합니다. 경로에 대한 **IdentificationString** 속성에서 이 문자열을 지정합니다.  
  
 ID 문자열을 찾으려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 두 데이터 흐름 구성 요소 사이의 경로를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **IdentificationString** 속성이 **속성** 창에 표시됩니다.  
  
 *dataflow_path_id_string*은 **nvarchar(4000)** 입니다.  
  
 [ @data_filename = ] *data_filename*  
 탭 데이터를 저장하는 파일의 이름입니다. 데이터 흐름 태스크가 Foreach 루프 또는 For 루프 컨테이너 내부에서 실행되는 경우 각 루프 반복에 대한 탭 데이터가 개별 파일에 저장됩니다. 각 파일은 반복에 해당하는 번호가 접두사로 붙습니다. 데이터 탭 파일은 "*\<SQL Server 설치 폴더>* \130\DTS\\" 폴더에 기록됩니다. *data_filename*은 **nvarchar(4000)** 입니다.  
  
 [ @max_rows = ] max_rows  
 데이터 탭 도중 캡처하는 행 수입니다. 이 값을 지정하지 않으면 모든 행이 캡처됩니다. max_rows는 **int**입니다.  
  
 [ @data_tap_id = ] *data_tap_id*  
 데이터 탭의 ID입니다. *data_tap_id*는 **bigint**입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 데이터 흐름 태스크(`Paths[SRC DimDCVentor.OLE DB Source Output]`)의 데이터 흐름 경로(`{D978A2E4-E05D-4374-9B05-50178A8817E8}`)에 데이터 탭을 만듭니다. 탭 데이터는 DCVendorOutput.csv 파일에 저장됩니다.  
  
```sql
exec catalog.add_data_tap_by_guid   @execution_id,   
'{D978A2E4-E05D-4374-9B05-50178A8817E8}',   
'Paths[SRC DimDCVentor.OLE DB Source Output]',   
'D:\demos\datafiles\DCVendorOutput.csv'  
```  
  
## <a name="remarks"></a>Remarks  
 데이터 탭을 추가하려면 실행 인스턴스가 생성됨 상태([catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 뷰의 **status** 열 값이 1임)여야 합니다. 실행 인스턴스를 실행하면 상태 값이 변경됩니다. [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)을 호출하여 실행을 만들 수 있습니다.  
  
 다음은 add_data_tap_by_guid 저장 프로시저에 대한 고려 사항입니다.  
  
-   추가한 데이터 탭은 패키지 실행 전에는 유효성이 검사되지 않습니다.  
  
-   데이터 탭 도중에 캡처되는 행 수를 제한하여 대용량 데이터 파일이 생성되지 않도록 하는 것이 좋습니다. 저장 프로시저가 실행되는 컴퓨터에 데이터 파일에 대한 저장 공간이 부족한 경우 저장 프로시저 실행이 중지됩니다.  
  
-   add_data_tap_by_guid 저장 프로시저를 실행하면 패키지의 성능에 영향을 미칩니다. 이 저장 프로시저는 데이터 문제 해결을 위해서만 실행하는 것이 좋습니다.  
  
-   탭 데이터가 저장되는 파일에 액세스하려면 저장 프로시저가 실행되는 컴퓨터에 대한 관리자 권한이 있거나, 데이터 탭이 있는 패키지가 포함된 실행을 시작한 사용자여야 합니다.  
  
## <a name="return-codes"></a>반환 코드  
 0(성공)  
  
 저장 프로시저가 실패하면 오류를 반환합니다.  
  
## <a name="result-set"></a>결과 집합  
 없음  
  
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
  
## <a name="see-also"></a>참고 항목  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
  
  
