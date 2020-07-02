---
title: sp_dropsubscription (Transact-sql) | Microsoft Docs
description: 게시자에서 아티클, 게시 또는 구독에 대 한 구독을 삭제 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행 됩니다.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropsubscription
- sp_dropsubscription_TSQL
helpviewer_keywords:
- sp_dropsubscription
ms.assetid: 7551f345-5510-4684-ab53-f9057249d13a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3ef0707d0e2f2770a241ad22be567fed16ad9e3b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783030"
---
# <a name="sp_dropsubscription-transact-sql"></a>sp_dropsubscription(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  게시자에서 특정 아티클에 대한 구독, 게시 또는 구독 집합을 삭제합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
        , [ @subscriber= ] 'subscriber'  
    [ , [ @destination_db= ] 'destination_db' ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`연결 된 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 NULL입니다. **All**인 경우 지정 된 구독자의 모든 게시에 대 한 모든 구독이 취소 됩니다. *게시* 는 필수 매개 변수입니다.  
  
`[ @article = ] 'article'`아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 NULL입니다. **All**인 경우 지정 된 각 게시 및 구독자에 대 한 모든 아티클에 대 한 구독이 삭제 됩니다. 즉시 업데이트를 허용 하는 게시의 경우 **모두** 를 사용 합니다.  
  
`[ @subscriber = ] 'subscriber'`구독을 삭제할 구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 없습니다. All **인 경우 모든**구독자에 대 한 모든 구독이 삭제 됩니다.  
  
`[ @destination_db = ] 'destination_db'`대상 데이터베이스의 이름입니다. *destination_db* 는 **sysname**이며 기본값은 NULL입니다. NULL인 경우 해당 구독자에서 모든 구독이 삭제됩니다.  
  
`[ @ignore_distributor = ] ignore_distributor`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @reserved = ] 'reserved'`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropsubscription** 는 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 즉시 동기화 게시에서 아티클에 관한 구독을 삭제한 경우에는 게시에서 모든 아티클에 대한 구독을 삭제한 다음, 모두 한꺼번에 다시 추가하지 않는 한 다시 추가할 수 없습니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropsubscription-tran_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버, **db_owner** 고정 데이터베이스 역할의 멤버 또는 구독을 만든 사용자만 **sp_dropsubscription**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [밀어넣기 구독 삭제](../../relational-databases/replication/delete-a-push-subscription.md)   
 [Transact-sql&#41;sp_addsubscription &#40;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_changesubstatus &#40;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [Transact-sql&#41;sp_helpsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
