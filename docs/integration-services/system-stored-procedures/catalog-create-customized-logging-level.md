---
title: catalog.create_customized_logging_level | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 20b3ba0a-126f-49bf-b70f-61b2a0fcb750
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 974cafa87b1b8fc7472e214dd84fb24f158f45bf
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053407"
---
# <a name="catalogcreate_customized_logging_level"></a>catalog.create_customized_logging_level 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  새 사용자 지정된 로깅 수준을 만듭니다. 사용자 지정 로깅 수준에 대한 자세한 내용은 [Integration Services &#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.create_customized_logging_level [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
    , [ @profile_value = ] profile_value  
    , [ @events_value = ] events_value  
    , [ @level_id = ] level_id OUT   
```  
  
## <a name="arguments"></a>인수  
 [ @level_name = ] *level_name*  
 새 기존 사용자 지정된 로깅 수준의 이름입니다.  
  
 *level_name*은 **nvarchar(128)** 입니다.  
  
 [ @level_description = ] *level_description*  
 새 기존 사용자 지정된 로깅 수준에 대한 설명입니다.  
  
 *level_description*은 **nvarchar(max)** 입니다.  
  
 [ @profile_value = ] *profile_value*  
 로그할 새 사용자 지정된 로깅 수준에 대해 원하는 통계입니다.  
  
 통계에 유효한 값은 다음과 같습니다. 이러한 값은 **사용자 지정된 로깅 수준 관리** 대화 상자의 **통계** 탭에 있는 값입니다.  
  
-   실행 = 0  
  
-   볼륨 = 1  
  
-   성능 = 2    
  
 *profile_value*는 **bigint**입니다.  
  
 [ @events_value = ] *events_value*  
 로그할 새 사용자 지정된 로깅 수준에 대해 원하는 이벤트입니다.  
  
 이벤트에 유효한 값은 다음과 같습니다. 이러한 값은 **사용자 지정된 로깅 수준 관리** 대화 상자의 **이벤트** 탭에 있는 값입니다.  
  
|이벤트 컨텍스트가 없는 이벤트|이벤트 컨텍스트가 있는 이벤트|  
|----------------------------------|-------------------------------|  
|OnVariableValueChanged = 0<br /><br /> OnExecutionStatusChanged = 1<br /><br /> OnPreExecute = 2<br /><br /> OnPostExecute = 3<br /><br /> OnPreValidate = 4<br /><br /> OnPostValidate = 5<br /><br /> OnWarning = 6<br /><br /> OnInformation = 7<br /><br /> OnError = 8<br /><br /> OnTaskFailed = 9<br /><br /> OnProgress = 10<br /><br /> OnQueryCancel = 11<br /><br /> OnBreakpointHit = 12<br /><br /> OnCustomEvent = 13<br /><br /> Diagnostic = 14<br /><br /> DiagnosticEx = 15<br /><br /> NonDiagnostic = 16|OnVariableValueChanged_IncludeContext = 32<br /><br /> OnExecutionStatusChanged_IncludeContext = 33<br /><br /> OnPreExecute_IncludeContext = 34<br /><br /> OnPostExecute_IncludeContext = 35<br /><br /> OnPreValidate_IncludeContext = 36<br /><br /> OnPostValidate_IncludeContext = 37<br /><br /> OnWarning_IncludeContext = 38<br /><br /> OnInformation_IncludeContext = 39<br /><br /> OnError_IncludeContext = 40<br /><br /> OnTaskFailed_IncludeContext = 41<br /><br /> OnProgress_IncludeContext = 42<br /><br /> OnQueryCancel_IncludeContext= 43<br /><br /> OnBreakpointHit_IncludeContext = 44<br /><br /> OnCustomEvent_IncludeContext = 45<br /><br /> Diagnostic_IncludeContext = 46<br /><br /> DiagnosticEx_IncludeContext = 47<br /><br /> NonDiagnostic_IncludeContext = 48|  
  
 *event_value*는 **bigint**입니다.  
  
 [ @level_id = ] *level_id* OUT  
 새 사용자 로깅 수준에 대한 ID입니다.  
  
 *level_id*는 **bigint**입니다.  
  
## <a name="remarks"></a>설명  
 Transact-SQL에서 *profile_value* 또는 *event_value* 인수에 대한 여러 값을 결합하려면, 다음 예제를 따릅니다. OnError (8) 및 DiagnosticEx (15) 이벤트를 캡처하기 위해 *events_value*를 계산하는 수식은 `2^8 + 2^15 = 33024`입니다.  
  
## <a name="return-codes"></a>반환 코드  
 0(성공)  
  
 저장 프로시저가 실패하면 오류를 반환합니다.  
  
## <a name="result-set"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할의 멤버 자격  
  
-   **sysadmin** 서버 역할의 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 저장 프로시저 실패 조건을 설명합니다.  
  
-   사용자에게 필요한 권한이 없습니다.  
  
  
