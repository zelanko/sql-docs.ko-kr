---
title: catalog.set_customized_logging_level_description | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 6ceaa39f-2439-457b-b99f-f12d88a1be32
author: chugugrace
ms.author: chugu
ms.openlocfilehash: beb078f6888f9ea89654922c1667a0e9a60448f5
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053577"
---
# <a name="catalogset_customized_logging_level_description"></a>catalog.set_customized_logging_level_description 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  기존 사용자 지정된 로깅 수준에 대한 설명을 변경합니다. 사용자 지정 로깅 수준에 대한 자세한 내용은 [Integration Services &#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.set_customized_logging_level_description [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
```  
  
## <a name="arguments"></a>인수  
 [ @level_name = ] *level_name*  
 기존 사용자 지정 로깅 수준의 이름입니다.  
  
 *level_name*은 **nvarchar(128)** 입니다.  
  
 [ @level_description = ] *level_description*  
 지정된 사용자 지정 로깅 수준의 새 설명입니다.  
  
 *level_description*은 **nvarchar(1024)** 입니다.  
  
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
  
  
