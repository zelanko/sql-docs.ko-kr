---
title: sp_droppublication (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_droppublication_TSQL
- sp_droppublication
helpviewer_keywords:
- sp_droppublication
ms.assetid: b52b37e6-4fec-40cf-abba-7dce4ff395fd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 66bb9fbb43647b6566ef641f63b047b84e37c1bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669471"
---
# <a name="spdroppublication-transact-sql"></a>sp_droppublication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시 및 이와 연결된 스냅숏 에이전트를 삭제합니다. 게시를 삭제하기 전에 반드시 모든 구독을 삭제해야 합니다. 게시에 있는 아티클은 자동으로 삭제됩니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droppublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=** ] **'***게시***'**  
 삭제할 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다. 하는 경우 **모든** 지정 된 경우 구독을 사용 하 여 제외 하 고, 게시 데이터베이스에서 모든 게시가 삭제 됩니다.  
  
 [  **@ignore_distributor =** ] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_droppublication** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_droppublication** 재귀적으로 게시와 연결 된 모든 문서를 삭제 한 다음 게시 자체를 삭제 합니다. 게시에 구독이 한 개 이상 있는 경우에는 게시를 제거할 수 없습니다. 구독을 제거 하는 방법에 대 한 정보를 참조 하세요 [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) 하 고 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)합니다.  
  
 실행 **sp_droppublication** 게시를 삭제 하는 게시에서 개체가 제거 되지 게시 데이터베이스나 구독 데이터베이스에서 해당 개체입니다. 사용 하 여 \<개체 > 필요한 경우 이러한 개체를 수동으로 제거 하려면.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_droppublication**합니다.  
  
## <a name="examples"></a>예  
 [!code-sql[HowTo#sp_droppublication](../../relational-databases/replication/codesnippet/tsql/sp-droppublication-trans_1.sql)]  
  
## <a name="see-also"></a>관련 항목  
 [게시 삭제](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
