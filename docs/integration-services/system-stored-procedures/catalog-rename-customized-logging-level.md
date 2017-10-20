---
title: catalog.rename_customized_logging_level | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b1a57d5e-3f03-4901-8b2b-bb8b371b595b
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 00c2cd8fa5f8423a7791d663d02aecbf27b8ab41
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogrenamecustomizedlogginglevel"></a>catalog.rename_customized_logging_level
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  기존 사용자 지정 된 로깅 수준을 이름을 바꿉니다. 사용자 지정 된 로깅 수준에 대 한 자세한 내용은 참조 하십시오. [Integration services&#40; Ssis&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.rename_customized_logging_level [ @old_name = ] old_name  
    , [ @new_name = ] new_name  
```  
  
## <a name="arguments"></a>인수  
 [ @old_name =] *old_name*  
 기존 아티클의 이름 사용자의 이름을 바꾸려면 로깅 수준을 지정 합니다.  
  
 *old_name* 은 **nvarchar (128)**합니다.  
  
 [ @new_name =] *new_name*  
 새 이름이 지정된 된 로깅 수준을 사용자 지정합니다.  
  
 *new_name* 은 **nvarchar (128)**합니다.  
  
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
  
  
