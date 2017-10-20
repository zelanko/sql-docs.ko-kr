---
title: "catalog.set_execution_parameter_value (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 055d86c9-befd-4e63-acb1-6dfe833549d2
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 7b13e7b1c28bad6e573e829183372da4bb62f92d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="catalogsetexecutionparametervalue-ssisdb-database"></a>catalog.set_execution_parameter_value(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스에 대한 매개 변수 값을 설정합니다.  
  
 실행 인스턴스가 시작된 후에는 매개 변수 값을 변경할 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
set_execution_parameter_value [ @execution_id = execution_id  
    , [ @object_type = ] object_type  
    , [ @parameter_name = ] parameter_name  
    , [ @parameter_value = ] parameter_value  
  
```  
  
## <a name="arguments"></a>인수  
 [ @execution_id =] *execution_id*  
 실행 인스턴스의 고유 식별자입니다. *execution_id* 은 **bigint**합니다.  
  
 [ @object_type =] *object_type*  
 매개 변수의 유형입니다.  
  
 다음 매개 변수 설정 *object_type* 50  
  
-   LOGGING_LEVEL  
  
-   CUSTOMIZED_LOGGING_LEVEL  
  
-   DUMP_ON_ERROR  
  
-   DUMP_ON_EVENT  
  
-   DUMP_EVENT_CODE  
  
-   CALLER_INFO  
  
-   SYNCHRONIZED  
  
 프로젝트 매개 변수를 나타내려면 값 `20`을 사용하고, 패키지 매개 변수를 나타내려면 값 `30`을 사용합니다.  
  
 *object_type* 은 **smallint**합니다.  
  
 [ @parameter_name =] *p a r a*  
 매개 변수의 이름입니다. *p a r a* 은 **nvarchar (128)**합니다.  
  
 [ @parameter_value =] *parameter_value*  
 매개 변수의 값입니다. *parameter_value* 은 **sql_variant**합니다.  
  
## <a name="remarks"></a>주의  
 주어진 실행에 사용된 매개 변수 값을 확인하려면 catalog.execution_parameter_values 뷰를 쿼리하십시오.  
  
 패키지 실행 도중 기록 될 정보의 범위를 지정 하려면 설정 *p a r a* 을 설정 하 고 LOGGING_LEVEL *parameter_value* 를 다음 값 중 하나입니다.  
  
 설정의 *object_type* 매개 변수를 50입니다.  
  
|Value|설명|  
|-----------|-----------------|  
|0|InclusionThresholdSetting<br /><br /> 로깅이 해제됩니다. 패키지 실행 상태에만 기록됩니다.|  
|1|Basic<br /><br /> 사용자 지정 이벤트 및 진단 이벤트 외의 모든 이벤트가 기록됩니다. 이 값은 기본값입니다.|  
|2|성능<br /><br /> 성능 통계와 OnError 및 OnWarning 이벤트만 기록됩니다.|  
|3|Verbose<br /><br /> 사용자 지정 이벤트 및 진단 이벤트를 포함한 모든 이벤트가 기록됩니다. <br />사용자 지정 이벤트는 Integration Services 태스크에 의해 기록되는 이벤트를 포함합니다. 자세한 내용은 참조 [Custom Messages for Logging](../../integration-services/performance/integration-services-ssis-logging.md#custom_messages)|  
|4|런타임 계보<br /><br /> 데이터 흐름에서 계보를 추적 하는 데 필요한 데이터를 수집 합니다.|  
|100|사용자 지정 로깅 수준<br /><br /> CUSTOMIZED_LOGGING_LEVEL 매개 변수에서 설정을 지정 합니다. 지정할 수 있는 값에 대 한 자세한 내용은 참조 하십시오. [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md)합니다.<br /><br /> 사용자 지정 된 로깅 수준에 대 한 자세한 내용은 참조 하십시오. [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)합니다.|  
  
 패키지 실행 도중 오류 발생 시 Integration Services 서버가 덤프 파일을 생성하도록 지정하려면 실행되지 않은 실행 인스턴스에 대해 다음 매개 변수 값을 설정하십시오.  
  
|매개 변수|Value|  
|---------------|-----------|  
|*execution_id*|실행 인스턴스의 고유 식별자|  
|*object_type*|50|  
|*p a r a*|‘DUMP_ON_ERROR|  
|*parameter_value*|1.|  
  
 패키지 실행 도중 이벤트 발생 시 Integration Services 서버가 덤프 파일을 생성하도록 지정하려면 실행되지 않은 실행 인스턴스에 대해 다음 매개 변수 값을 설정하십시오.  
  
|매개 변수|Value|  
|---------------|-----------|  
|*execution_id*|실행 인스턴스의 고유 식별자|  
|*object_type*|50|  
|*p a r a*|‘DUMP_ON_EVENT|  
|*parameter_value*|1|  
  
 패키지 실행 도중 Integration Services 서버에서 덤프 파일이 생성되도록 하는 이벤트를 지정하려면 실행되지 않은 실행 인스턴스에 대해 다음 매개 변수 값을 설정하십시오. 세미콜론을 사용하여 여러 이벤트 코드를 구분합니다.  
  
|매개 변수|Value|  
|---------------|-----------|  
|*execution_id*|실행 인스턴스의 고유 식별자|  
|*object_type*|50|  
|*p a r a*|DUMP_EVENT_CODE|  
|*parameter_value*|하나 이상의 이벤트 코드|  
  
## <a name="example"></a>예제  
 다음 예는 패키지 실행 도중 오류 발생 시 Integration Services 서버가 덤프 파일을 생성하도록 지정합니다.  
  
```  
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_ERROR',1  
  
```  
  
## <a name="example"></a>예제  
 다음 예는 패키지 실행 도중 이벤트 발생 시 Integration Services 서버가 덤프 파일을 생성하도록 지정하며 서버에서 파일이 생성되도록 하는 이벤트를 지정합니다.  
  
```  
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_EVENT',1  
  
declare @event_code nvarchar(50)  
set @event_code = '0xC020801C'  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_EVENT_CODE', @event_code  
```  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 및 MODIFY 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   실행 식별자가 잘못된 경우  
  
-   매개 변수 이름이 잘못된 경우  
  
-   매개 변수 값의 데이터 형식이 매개 변수의 데이터 형식과 일치하지 않는 경우  
  
## <a name="see-also"></a>관련 항목:  
 [catalog.execution_parameter_values &#40; SSISDB 데이터베이스 &#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)   
 [패키지 실행을 위한 덤프 파일 생성](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
