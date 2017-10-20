---
title: catalog.set_customized_logging_level_description | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 6ceaa39f-2439-457b-b99f-f12d88a1be32
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3899e02c6b1eaa2cc76ad4411d9be3aded817728
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetcustomizedloggingleveldescription"></a>catalog.set_customized_logging_level_description
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  기존 사용자 지정 된 로깅 수준에 대 한 설명을 변경합니다. 사용자 지정 된 로깅 수준에 대 한 자세한 내용은 참조 하십시오. [Integration services&#40; Ssis&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
set_customized_logging_level_description [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
  
```  
  
## <a name="arguments"></a>인수  
 [ @level_name =] *level_name*  
 기존 이름 사용자 로깅 수준을 지정합니다.  
  
 *level_name* 은 **nvarchar (128)**합니다.  
  
 [ @level_description =] *level_description*  
 지정 된 항목에 대 한 새 설명을 사용자 로깅 수준을 지정합니다.  
  
 *level_description* 은 **nvarchar (1024)**합니다.  
  
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
  
  
