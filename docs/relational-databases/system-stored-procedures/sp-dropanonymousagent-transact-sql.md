---
title: sp_dropanonymousagent (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 10b75c7c2e083a09dbebfc720487511397a1af90
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
 [  **@subid=**] *sub_id*  
 익명 구독에 관한 전역 식별자입니다. *sub_id* 은 **uniqueidentifier**, 기본값은 없습니다. 구독자에서이 식별자를 검색할 수 있습니다를 사용 하 여 **sp_helppullsubscription**합니다. 값은 **subid** 반환된 된 결과 집합의 필드는이 전역 식별자입니다.  
  
 [  **@type=**] *유형*  
 구독 유형입니다. *형식* 은 **int**, 기본값은 없습니다. 유효한 값은 **1** 또는 **2**합니다. 지정 **1**, 스냅숏 복제 또는 트랜잭션 복제 배포 에이전트를 사용 하는 경우. 지정 **2**경우 병합 에이전트를 사용 하 여 복제를 병합 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_dropanonymousagent** 모든 유형의 복제에 사용 됩니다.  
  
 이 저장 프로시저는 익명 구독 에이전트를 삭제할 때에만 사용하며 잘 알려진 구독 삭제에는 사용할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **db_owner** 고정된 데이터베이스 역할이 배포 데이터베이스에서 실행할 수 있는 **sp_dropanonymousagent**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
