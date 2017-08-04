---
title: "catalog.create_execution (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 95c07e2550330ff9a2ac1cc70107d11147ae53dd
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 실행 인스턴스를 만듭니다.  
  
 이 저장 프로시저는 기본 서버 로깅 수준을 사용합니다.  
  
## <a name="syntax"></a>구문  
  
```tsql  
create_execution [ @folder_name = folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id ]  
  [  , [ @use32bitruntime = ] use32bitruntime ] 
  [  , [ @runinscaleout = ] runinscaleout ]
  [  , [ @useanyworker = ] useanyworker ] 
     , [ @execution_id = ] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name =] *folder_name*  
 실행할 패키지가 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar (128)**합니다.  
  
 [ @project_name =] *project_name*  
 실행할 패키지가 포함된 프로젝트의 이름입니다. *project_name* 은 **nvarchar (128)**합니다.  
  
 [ @package_name =] *package_name*  
 실행할 패키지의 이름입니다. *package_name* 은 **nvarchar (260)**합니다.  
  
 [ @reference_id =] *reference_id*  
 환경 참조의 고유 식별자입니다. 이 매개 변수는 선택 사항입니다. *reference_id* 은 **bigint**합니다.  
  
 [ @use32bitruntime =] *use32bitruntime*  
 64비트 운영 체제에서 32비트 런타임을 사용하여 패키지를 실행해야 하는지 여부를 나타냅니다. 64 비트 운영 체제에서 실행 될 때 32 비트 런타임 사용 하 여 패키지를 실행할 1의 값을 사용 합니다. 64비트 운영 체제에서 실행할 때 64비트 런타임으로 패키지를 실행하려면 값 0을 사용합니다. 이 매개 변수는 선택 사항입니다. *Use32bitruntime* 은 **비트**합니다.  
 
 [ @runinscaleout =] *runinscaleout*  
 범위 확장의 실행 여부를 나타냅니다. 스케일 아웃에 패키지를 실행 하려면 1의 값을 사용 합니다. 스케일 아웃 하지 않고 패키지를 실행 하려면 0의 값을 사용 합니다. 이 매개 변수는 선택 사항입니다. [SSISDB]에서 DEFAULT_EXECUTION_MODE에 설정 됩니다. [catalog]입니다. [catalog_properties]를 지정 하지 않은 경우입니다. *runinscaleout* 은 **비트**합니다. 
 
 [ @useanyworker =] *useanyworker*  
  실행 작업을 수행 하는 스케일 아웃 작업자 허용 되는지 여부를 나타냅니다. 값 1 사용 하 여 스케일 아웃 작업자를 사용 하 여 패키지를 실행 합니다. 일부 스케일 아웃 작업자 패키지를 실행할 수 있는지를 나타내는 0의 값을 사용 합니다. 이 매개 변수는 선택 사항입니다. 그는 1로 설정 되지 않은 경우 지정 합니다. *useanyworker* 은 **비트**합니다. 
  
 [ @execution_id =] *execution_id*  
 실행 인스턴스의 고유 식별자를 반환합니다. *execution_id* 은 **bigint**합니다.  

  
## <a name="remarks"></a>주의  
 실행은 단일 인스턴스의 패키지 실행 중에 패키지에서 사용할 매개 변수 값을 지정하는 데 사용됩니다.  
  
 환경 참조가 지정 된 경우는 *reference_id* 매개 변수를 저장된 프로시저는 리터럴 값 또는 해당 환경 변수에서 참조 된 값을 가진 프로젝트 및 패키지 매개 변수를 채웁니다. 환경 참조가 지정되면 패키지를 실행하는 동안 기본 매개 변수 값이 사용됩니다. 실행의 특정 인스턴스에 사용 되는 값 정확 하 게 확인 하려면는 *execution_id* 출력 매개 변수 값이 저장된 프로시저 및 쿼리는 [execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) 보기.  
  
 진입점 패키지로 표시된 패키지만 실행에 지정할 수 있습니다. 진입점이 아닌 패키지를 지정하면 실행에 실패합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 catalog.create_execution을 호출 스케일 아웃에 없는 여 Child1.dtsx 패키지에 대 한 실행 인스턴스를 만듭니다. Integration Services Project1에 패키지가 포함되어 있습니다. 이 예에서는 catalog.set_execution_parameter_value를 호출하여 Parameter1, Parameter2 및 LOGGING_LEVEL 매개 변수에 값을 설정합니다. 이 예에서는 catalog.start_execution을 호출하여 실행 인스턴스를 시작합니다.  
  
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
 InclusionThresholdSetting  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 및 EXECUTE 권한과 해당되는 경우 참조된 환경에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  

 경우 @runinscaleout 이 1 이면 저장된 프로시저에 필요한 권한 중 하나:
 
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할

-   멤버 자격에는 **ssis_cluster_executor** 데이터베이스 역할

-   멤버 자격에는 **sysadmin** 서버 역할
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생할 수 있는 몇 가지 조건에 대해 설명합니다.  
  
-   패키지가 없습니다.  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   환경 참조 *reference_id*를 사용할 수 없습니다.  
  
-   지정된 패키지가 진입점 패키지가 아닌 경우  
  
-   참조된 환경 변수의 데이터 형식이 프로젝트 또는 패키지 매개 변수의 데이터 형식과 다른 경우  
  
-   프로젝트 또는 패키지에 값이 필요한 매개 변수가 있지만 할당된 값이 없는 경우  
  
-   환경을 참조 하는 환경에서 참조 된 환경 변수를 찾을 수 없습니다 *reference_id*를 지정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [catalog.start_execution &#40; SSISDB 데이터베이스 &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [catalog.add_execution_worker &#40; SSISDB 데이터베이스 &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  

