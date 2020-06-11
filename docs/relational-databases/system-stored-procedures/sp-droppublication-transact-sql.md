---
title: sp_droppublication (Transact-sql) | Microsoft Docs
description: 게시 및 이와 연결된 스냅샷 에이전트를 삭제합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행 됩니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppublication_TSQL
- sp_droppublication
helpviewer_keywords:
- sp_droppublication
ms.assetid: b52b37e6-4fec-40cf-abba-7dce4ff395fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 46faa94ed9a85433b9212856ea5d95f43fb01972
ms.sourcegitcommit: 19ff45e8a2f4193fe8827f39258d8040a88befc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83807799"
---
# <a name="sp_droppublication-transact-sql"></a>sp_droppublication(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  게시 및 이와 연결된 스냅샷 에이전트를 삭제합니다. 게시를 삭제하기 전에 반드시 모든 구독을 삭제해야 합니다. 게시에 있는 아티클은 자동으로 삭제됩니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droppublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`삭제할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다. **All** 을 지정 하면 구독이 있는 게시를 제외 하 고 게시 데이터베이스에서 모든 게시가 삭제 됩니다.  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_droppublication** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_droppublication** 는 게시와 연결 된 모든 아티클을 재귀적으로 삭제 한 다음 게시 자체를 삭제 합니다. 게시에 구독이 한 개 이상 있는 경우에는 게시를 제거할 수 없습니다. 구독을 제거 하는 방법에 대 한 자세한 내용은 [delete a Push subscription](../../relational-databases/replication/delete-a-push-subscription.md) 및 [Delete a Pull subscription](../../relational-databases/replication/delete-a-pull-subscription.md)을 참조 하세요.  
  
 게시를 삭제 하기 위해 **sp_droppublication** 를 실행 해도 게시 데이터베이스의 게시 된 개체 또는 구독 데이터베이스의 해당 개체는 제거 되지 않습니다. \<필요한 경우 DROP object>를 사용 하 여 이러한 개체를 수동으로 제거 합니다.  
  
## <a name="permissions"></a>권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_droppublication**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 [!code-sql[HowTo#sp_droppublication](../../relational-databases/replication/codesnippet/tsql/sp-droppublication-trans_1.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [게시 삭제](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Transact-sql&#41;sp_addpublication &#40;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [Transact-sql&#41;sp_changepublication &#40;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [Transact-sql&#41;sp_helppublication &#40;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
