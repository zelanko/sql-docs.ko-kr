---
title: sp_reinitpullsubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitpullsubscription_TSQL
- sp_reinitpullsubscription
helpviewer_keywords:
- sp_reinitpullsubscription
ms.assetid: 7d9abe49-ce92-47f3-82c9-aea749518c91
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b4187dbe3ac00830919b07920a720b89818c25d8
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533705"
---
# <a name="spreinitpullsubscription-transact-sql"></a>sp_reinitpullsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  다음 번 배포 에이전트가 실행될 때 트랜잭션 끌어오기 또는 익명 구독을 다시 초기화하도록 표시합니다. 이 저장 프로시저는 끌어오기 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_reinitpullsubscription [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시자 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 all 이며 모든 구독이 다시 초기화 하도록 표시입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_reinitpullsubscription** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_reinitpullsubscription** 피어 투 피어 트랜잭션 복제에 지원 되지 않습니다.  
  
 **sp_reinitpullsubscription** 배포 에이전트가 다음 실행 하는 동안 구독을 다시 초기화 하도록 구독자에서 호출할 수 있습니다.  
  
 값을 사용 하 여 생성 된 게시에 구독이 **false** 에 대 한 **@immediate_sync** 구독자에서 다시 초기화할 수 없습니다.  
  
 중 하나를 실행 하 여 끌어오기 구독을 다시 초기화할 수 있습니다 **sp_reinitpullsubscription** 구독자 또는 **sp_reinitsubscription** 게시자입니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_reinitpullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitpullsubscriptio_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_reinitpullsubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
