---
title: catalog.create_customized_logging_level | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 126fa0af811033bb0be035b1f4c550620c696bb3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreatecustomizedlogginglevel"></a>catalog.create_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  새 사용자 지정 된 로깅 수준을 만듭니다. 사용자 지정 된 로깅 수준에 대 한 자세한 내용은 참조 하십시오. [Integration services&#40; Ssis&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @event_value = ] event_value  
    , [ @level_id = ] level_id OUT   
```  
  
## <a name="arguments"></a>인수  
 [ @level_name =] *level_name*  
 새 기존에 대 한 이름을 사용자 로깅 수준을 지정합니다.  
  
 *level_name* 은 **nvarchar (128)**합니다.  
  
 [ @level_description =] *level_description*  
 새 기존에 대 한 설명을 사용자 로깅 수준을 지정합니다.  
  
 *level_description* 은 **nvarchar (1024)**합니다.  
  
 [ @profile_value =] *profile_value*  
 새 되도록 통계 사용자 로그에 로깅 수준을 지정 합니다.  
  
 통계에 대 한 유효한 값은 다음과 같습니다. 이러한 값에는 값에 해당 합니다.는 **통계** 탭은 **사용자 지정 된 로깅 수준 관리** 대화 상자.  
  
-   실행 = 0  
  
-   볼륨 = 1  
  
-   성능 = 2  
  
 *profile_value* 는 **bigint**합니다.  
  
 [ @event_value =] *event_value*  
 새 지정 하는 이벤트 로그에 로깅 수준을 사용자 지정 합니다.  
  
 이벤트에 대 한 유효한 값은 다음과 같습니다. 이러한 값에는 값에 해당 합니다.는 **이벤트** 탭은 **사용자 지정 된 로깅 수준 관리** 대화 상자.  
  
|이벤트를 이벤트 컨텍스트 없이|이벤트 컨텍스트를 사용 하 여 이벤트|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7 까지의 유형은<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> 진단 = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext = 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext 48 =|  
  
 *event_value* 는 **bigint**합니다.  
  
 [ @level_id =] *level_id* 아웃  
 새 id 사용자 로깅 수준을 지정합니다.  
  
 *level_id* 는 **bigint**합니다.  
  
## <a name="remarks"></a>주의  
 에 대 한 TRANSACT-SQL에서 여러 개의 값을 결합 하는 *profile_value* 또는 *event_value* 인수를이 예제를 실행 합니다. OnError (8) 및 (15) DiagnosticEx 이벤트를 계산 하는 공식은를 캡처하려면 *event_value* 은 `2^8 + 2^15 = 33024`합니다.  
  
## <a name="return-codes"></a>반환 코드  
 0(성공)  
  
 저장 프로시저가 실패하면 오류를 반환합니다.  
  
## <a name="result-set"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할의 멤버 자격  
  
-   **sysadmin** 서버 역할의 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 저장 프로시저 실패 조건을 설명합니다.  
  
-   사용자는 데 필요한 권한이 없습니다.  
  
  
