---
title: sp_reinitpullsubscription (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 6f9021ec9b71694fc6567db5edf79965e09fd3c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304918"
---
# <a name="sp_reinitpullsubscription-transact-sql"></a>sp_reinitpullsubscription(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  다음 번 배포 에이전트가 실행될 때 트랜잭션 끌어오기 또는 익명 구독을 다시 초기화하도록 표시합니다. 이 저장 프로시저는 끌어오기 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_reinitpullsubscription [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 모든 구독을 다시 초기화 하도록 표시 하는 all입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_reinitpullsubscription** 은 트랜잭션 복제에 사용 됩니다.  
  
 피어 투 피어 트랜잭션 복제에 대해서는 **sp_reinitpullsubscription** 지원 되지 않습니다.  
  
 다음에 배포 에이전트를 실행 하는 동안 구독을 다시 초기화 하기 위해 구독자에서 **sp_reinitpullsubscription** 를 호출할 수 있습니다.  
  
 ** \@Immediate_sync** 에 대해 **false** 값을 사용 하 여 만든 게시에 대 한 구독은 구독자에서 다시 초기화할 수 없습니다.  
  
 구독자에서 **sp_reinitpullsubscription** 실행 하거나 게시자에서 **sp_reinitsubscription** 하 여 끌어오기 구독을 다시 초기화할 수 있습니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_reinitpullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitpullsubscriptio_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_reinitpullsubscription**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
