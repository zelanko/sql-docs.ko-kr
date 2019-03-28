---
title: sp_dropmergepublication (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 74b5ff58db964bff29e863eec39e76313220f556
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533095"
---
# <a name="spdropmergepublication-transact-sql"></a>sp_dropmergepublication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시 및 이와 연관된 스냅숏 에이전트를 삭제합니다. 병합 게시를 삭제하기 전에 반드시 모든 구독을 삭제해야 합니다. 게시에 있는 아티클은 자동으로 삭제됩니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 삭제할 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다. 하는 경우 **모든**, 기존의 모든 병합 게시와 연결 된 스냅숏 에이전트 작업 제거 됩니다. 특정 값을 지정 하는 경우 *게시*, 해당 게시 및 해당 관련된 스냅숏 에이전트 작업이 삭제 됩니다.  
  
`[ @ignore_distributor = ] ignore_distributor` 배포자에서 정리 태스크를 수행 하지 않고 게시를 삭제 하는 데 사용 합니다. *ignore_distributor* 됩니다 **비트**, 기본값은 **0**합니다. 이 매개 변수는 배포자를 다시 설치할 때도 사용됩니다.  
  
`[ @reserved = ] reserved` 나중에 사용 하도록 예약 되어 있습니다. *예약* 됩니다 **비트**, 기본값은 **0**합니다.  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata` 내부 전용입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropmergepublication** 병합 복제에 사용 됩니다.  
  
 **sp_dropmergepublication** 재귀적으로 게시와 연관 된 모든 문서를 삭제 한 다음 게시 자체를 삭제 합니다. 게시에 구독이 한 개 이상 있는 경우에는 게시를 제거할 수 없습니다. 구독을 제거 하는 방법에 대 한 정보를 참조 하세요 [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) 하 고 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)합니다.  
  
 실행 **sp_dropmergepublication** 게시를 삭제 하는 게시에서 개체가 제거 되지 게시 데이터베이스나 구독 데이터베이스에서 해당 개체입니다. 사용 하 여 \<개체 > 필요한 경우 이러한 개체를 수동으로 제거 하려면.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_dropmergepublication**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [게시 삭제](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
