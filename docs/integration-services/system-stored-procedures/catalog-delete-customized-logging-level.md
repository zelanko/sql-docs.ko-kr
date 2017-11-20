---
title: catalog.delete_customized_logging_level | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 0aec1e34-f30b-4e5f-bba1-c26665cf2da6
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a2c53009bfbd2f0876d4cf0a01cf8fa2b5bc738e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeletecustomizedlogginglevel"></a>catalog.delete_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  기존 사용자 지정 된 로깅 수준을 삭제합니다. 사용자 지정 된 로깅 수준에 대 한 자세한 내용은 참조 하십시오. [Integration services&#40; Ssis&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
delete_customized_logging_level [ @level_name = ] level_name  
  
```  
  
## <a name="arguments"></a>인수  
 [ @level_name =] *level_name*  
 기존 아티클의 이름에는 로깅 수준을 삭제 하려면 사용자 지정 합니다.  
  
 *level_name* 은 **nvarchar (128)**합니다.  
  
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
  
  

