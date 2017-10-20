---
title: catalog.set_customized_logging_level_value | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d83fb763-c7c6-4e20-bd10-0f995598b198
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 75ef405fe4550e81ec2d5178a1d3242d405755af
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetcustomizedlogginglevelvalue"></a>catalog.set_customized_logging_level_value
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  통계 또는 기존 사용자 지정 된 로깅 수준에 의해 기록 된 이벤트를 변경 합니다. 사용자 지정 된 로깅 수준에 대 한 자세한 내용은 참조 하십시오. [Integration services&#40; Ssis&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.set_customized_logging_level_value [ @level_name = ] level_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>인수  
 [ @level_name =] *level_name*  
 기존 이름 사용자 로깅 수준을 지정합니다.  
  
 *level_name* 은 **nvarchar (128)**합니다.  
  
 [ @property_name =] *property_name*  
 변경할 속성의 이름입니다. 유효한 값은 **프로필** 및 **이벤트**합니다.  
  
 *property_name* 은 **nvarchar (128)**합니다.  
  
 [ @property_value =] *property_value*  
 지정 된을의 지정된 된 속성에 대 한 새 값에는 로깅 수준을 사용자 지정합니다.  
  
 프로필 및 이벤트에 대 한 유효한 값 목록이 참조 [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md)합니다.  
  
 *property_value* 는 **bigint**합니다.  
  
## <a name="remarks"></a>주의  
  
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
  
  
