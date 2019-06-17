---
title: sp_dropanonymousagent (Transact-SQL) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 2128e980384561a128eb4c2683043190f27a84b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822216"
---
# <a name="spdropanonymousagent-transact-sql"></a>sp_dropanonymousagent(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  배포자의 복제 모니터링을 위한 익명 에이전트를 게시자에서 삭제합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>인수  
`[ @subid = ] sub_id` 익명 구독에 대 한 전역 식별자가입니다. *sub_id* 됩니다 **uniqueidentifier**, 기본값은 없습니다. 구독자에서이 식별자를 검색할 수 있습니다 사용 하 여 **sp_helppullsubscription**합니다. 값을 **subid** 반환된 된 결과 집합의 필드는이 전역 식별자입니다.  
  
`[ @type = ] type` 구독의 유형이입니다. *형식* 됩니다 **int**, 기본값은 없습니다. 유효한 값은 **1** 하거나 **2**합니다. 지정할 **1**는 스냅숏 복제 또는 트랜잭션 복제 배포 에이전트를 사용 하는 경우. 지정할 **2**경우 병합 에이전트를 사용 하 여 복제를 병합 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropanonymousagent** 모든 유형의 복제에 사용 됩니다.  
  
 이 저장 프로시저는 익명 구독 에이전트를 삭제할 때에만 사용하며 잘 알려진 구독 삭제에는 사용할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **db_owner** 고정된 데이터베이스 역할의 배포 데이터베이스에서 실행할 수 있습니다 **sp_dropanonymousagent**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
