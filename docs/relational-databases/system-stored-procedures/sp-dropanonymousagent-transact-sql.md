---
title: sp_dropanonymousagent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 8c9a025beaf1d9701411668a13fa78273105d30c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717322"
---
# <a name="sp_dropanonymousagent-transact-sql"></a>sp_dropanonymousagent(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  배포자의 복제 모니터링을 위한 익명 에이전트를 게시자에서 삭제합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>인수  
`[ @subid = ] sub_id`익명 구독의 전역 식별자입니다. *sub_id* 은 **uniqueidentifier**이며 기본값은 없습니다. 이 식별자는 **sp_helppullsubscription**을 사용 하 여 구독자에서 검색할 수 있습니다. 반환 된 결과 집합의 **subid** 필드 값은이 전역 식별자입니다.  
  
`[ @type = ] type`구독의 유형입니다. *형식은* **int**이며 기본값은 없습니다. 유효한 값은 **1** 또는 **2**입니다. 배포 에이전트를 사용 하는 스냅숏 복제 또는 트랜잭션 복제 인 경우 **1**을 지정 합니다. 병합 에이전트를 사용 하는 병합 복제의 경우 **2**를 지정 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropanonymousagent** 은 모든 유형의 복제에 사용 됩니다.  
  
 이 저장 프로시저는 익명 구독 에이전트를 삭제할 때에만 사용하며 잘 알려진 구독 삭제에는 사용할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 배포 데이터베이스에서 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_dropanonymousagent**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
