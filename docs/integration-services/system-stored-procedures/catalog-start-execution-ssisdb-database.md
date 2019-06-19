---
title: catalog.start_execution(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 733e71edda284d8051cc1f641ae94a3518e6b0d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65715744"
---
# <a name="catalogstartexecution-ssisdb-database"></a>catalog.start_execution(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스를 시작합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.start_execution [@execution_id =] execution_id [, [@retry_count =] retry_count]  
```  
  
## <a name="arguments"></a>인수  
 [@execution_id =] *execution_id*  
 실행 인스턴스의 고유 식별자입니다. *execution_id*는 **bigint**입니다.
 
 [@retry_count =] *retry_count*  
 실행이 실패할 경우 다시 시도 횟수입니다. Scale Out에서 실행인 경우에만 적용됩니다. 이 매개 변수는 선택 사항입니다. 지정하지 않으면 해당 값이 0으로 설정됩니다. *retry_count*는 **int**입니다.
  
## <a name="remarks"></a>Remarks  
 실행은 단일 인스턴스의 패키지 실행 중에 패키지에서 사용할 매개 변수 값을 지정하는 데 사용됩니다. 실행 인스턴스가 생성된 후부터 시작되기 전까지 해당 프로젝트가 다시 배포될 수도 있습니다. 이 경우 실행 인스턴스는 오래된 프로젝트를 참조합니다. 이 잘못된 참조로 인해 저장 프로시저가 실패합니다.  
  
> [!NOTE]  
>  실행은 한 번만 시작할 수 있습니다. 실행 인스턴스를 시작하려면 해당 상태가 생성됨 상태([catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 뷰의 **status** 열 값 `1`에 해당)여야 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 catalog.create_execution을 호출하여 Child1.dtsx 패키지에 대한 실행 인스턴스를 만듭니다. Integration Services Project1에 패키지가 포함되어 있습니다. 이 예에서는 catalog.set_execution_parameter_value를 호출하여 Parameter1, Parameter2 및 LOGGING_LEVEL 매개 변수에 값을 설정합니다. 이 예에서는 catalog.start_execution을 호출하여 실행 인스턴스를 시작합니다.  
  
```sql
Declare @execution_id bigint  
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Child1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'TestDeply4', @project_name=N'Integration Services Project1', @use32bitruntime=False, @reference_id=Null  
Select @execution_id  
DECLARE @var0 sql_variant = N'Child1.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter1', @parameter_value=@var0  
DECLARE @var1 sql_variant = N'Child2.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter2', @parameter_value=@var1  
DECLARE @var2 smallint = 1  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var2  
EXEC [SSISDB].[catalog].[start_execution] @execution_id  
GO  
```  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 및 MODIFY 권한, 프로젝트에 대한 READ 및 EXECUTE 권한, 해당되는 경우 참조된 환경에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   실행 식별자가 잘못된 경우  
  
-   실행이 이미 시작되었거나 이미 완료된 경우(실행은 한 번만 시작할 수 있음)  
  
-   프로젝트와 연결된 환경 참조가 잘못된 경우  
  
-   필요한 매개 변수 값을 설정하지 않은 경우  
  
-   실행 인스턴스와 연결된 프로젝트 버전이 오래된 경우(최신 버전의 프로젝트만 실행할 수 있음)  
  
  
