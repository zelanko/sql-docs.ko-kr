---
title: catalog.set_customized_logging_level_value | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: d83fb763-c7c6-4e20-bd10-0f995598b198
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc237875d0ba5b4f28838609f6b172c55ffe0e90
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296744"
---
# <a name="catalogset_customized_logging_level_value"></a>catalog.set_customized_logging_level_value 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  기존 사용자 지정 로깅 수준에서 기록한 통계 또는 이벤트를 변경합니다. 사용자 지정 로깅 수준에 대한 자세한 내용은 [Integration Services &#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.set_customized_logging_level_value [ @level_name = ] level_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>인수  
 [ @level_name = ] *level_name*  
 기존 사용자 지정 로깅 수준의 이름입니다.  
  
 *level_name*은 **nvarchar(128)** 입니다.  
  
 [ @property_name = ] *property_name*  
 변경할 속성의 이름입니다. 유효한 값은 **PROFILE** 및 **EVENTS**입니다.  
  
 *property_name*은 **nvarchar(128)** 입니다.  
  
 [ @property_value = ] *property_value*  
 지정된 사용자 지정 로깅 수준의 지정된 속성에 대한 새 값입니다.  
  
 프로필 및 이벤트의 유효한 값 목록은 [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md)을 참조하세요.  
  
 *property_value*는 **bigint**입니다.  
  
## <a name="remarks"></a>설명  
  
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
  
  
