---
description: sp_dropmergepublication(Transact-SQL)
title: sp_dropmergepublication (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0c787c7c2503f9182b704e83a04664d7d377cef4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538977"
---
# <a name="sp_dropmergepublication-transact-sql"></a>sp_dropmergepublication(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  병합 게시 및 이와 연관된 스냅샷 에이전트를 삭제합니다. 병합 게시를 삭제하기 전에 반드시 모든 구독을 삭제해야 합니다. 게시에 있는 아티클은 자동으로 삭제됩니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 삭제할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다. **All**인 경우 모든 기존 병합 게시가 제거 되며 여기에 연결 된 스냅숏 에이전트 작업도 제거 됩니다. *게시*에 특정 값을 지정 하는 경우 해당 게시 및 연결 된 스냅숏 에이전트 작업만 삭제 됩니다.  
  
`[ @ignore_distributor = ] ignore_distributor` 배포자에서 정리 태스크를 수행 하지 않고 게시를 삭제 하는 데 사용 됩니다. *ignore_distributor* 은 **bit**이며 기본값은 **0**입니다. 이 매개 변수는 배포자를 다시 설치할 때도 사용됩니다.  
  
`[ @reserved = ] reserved` 는 나중에 사용 하도록 예약 되어 있습니다. *reserved* 는 **bit**이며 기본값은 **0**입니다.  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata` 내부용 으로만 사용 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropmergepublication** 는 병합 복제에 사용 됩니다.  
  
 **sp_dropmergepublication** 는 게시와 연결 된 모든 아티클을 재귀적으로 삭제 한 다음 게시 자체를 삭제 합니다. 게시에 구독이 한 개 이상 있는 경우에는 게시를 제거할 수 없습니다. 구독을 제거 하는 방법에 대 한 자세한 내용은 [delete a Push subscription](../../relational-databases/replication/delete-a-push-subscription.md) 및 [Delete a Pull subscription](../../relational-databases/replication/delete-a-pull-subscription.md)을 참조 하세요.  
  
 게시를 삭제 하기 위해 **sp_dropmergepublication** 를 실행 해도 게시 데이터베이스의 게시 된 개체 또는 구독 데이터베이스의 해당 개체는 제거 되지 않습니다. \<object>필요한 경우 DROP을 사용 하 여 이러한 개체를 수동으로 제거 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_dropmergepublication**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 삭제](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Transact-sql&#41;sp_addmergepublication &#40;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
