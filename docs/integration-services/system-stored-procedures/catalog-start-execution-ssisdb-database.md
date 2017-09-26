---
title: "catalog.start_execution (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 70359d539bc7b4fc6dd70de8bbb7e16be5d71208
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogstartexecution-ssisdb-database"></a>catalog.start_execution(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스를 시작합니다.  
  
## <a name="syntax"></a>구문  
  
```tsql  
start_execution [ @execution_id = ] execution_id [, [@retry_count = ] retry_count]  
```  
  
## <a name="arguments"></a>인수  
 [ @execution_id =] *execution_id*  
 실행 인스턴스의 고유 식별자입니다. *execution_id* 은 **bigint**합니다.
 
 [ @retry_count =] *retry_count*  
 실행이 실패 하면 재시도 횟수입니다. 실행 중인 스케일 아웃 하는 경우에 적용이 됩니다. 이 매개 변수는 선택 사항입니다. 그는 0으로 설정 되지 않은 경우 지정 합니다. *retry_count* 은 **int**합니다.
  
## <a name="remarks"></a>주의  
 실행은 단일 인스턴스의 패키지 실행 중에 패키지에서 사용할 매개 변수 값을 지정하는 데 사용됩니다. 실행 인스턴스가 생성된 후부터 시작되기 전까지 해당 프로젝트가 다시 배포될 수도 있습니다. 이 경우 실행 인스턴스는 오래된 프로젝트를 참조하게 되며, 이로 인해 저장 프로시저가 실패합니다.  
  
> [!NOTE]  
>  실행은 한 번만 시작할 수 있습니다. 생성 됨 상태 여야 합니다 실행 인스턴스를 시작 하려면 (값 `1` 에 **상태** 의 열은 [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) 보기).  
  
## <a name="example"></a>예제  
 다음 예에서는 catalog.create_execution을 호출하여 Child1.dtsx 패키지에 대한 실행 인스턴스를 만듭니다. Integration Services Project1에 패키지가 포함되어 있습니다. 이 예에서는 catalog.set_execution_parameter_value를 호출하여 Parameter1, Parameter2 및 LOGGING_LEVEL 매개 변수에 값을 설정합니다. 이 예에서는 catalog.start_execution을 호출하여 실행 인스턴스를 시작합니다.  
  
```  
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
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 및 MODIFY 권한, 프로젝트에 대한 READ 및 EXECUTE 권한, 해당되는 경우 참조된 환경에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   실행 식별자가 잘못된 경우  
  
-   실행이 이미 시작되었거나 이미 완료된 경우(실행은 한 번만 시작할 수 있음)  
  
-   프로젝트와 연결된 환경 참조가 잘못된 경우  
  
-   필요한 매개 변수 값을 설정하지 않은 경우  
  
-   실행 인스턴스와 연결된 프로젝트 버전이 오래된 경우(최신 버전의 프로젝트만 실행할 수 있음)  
  
  

