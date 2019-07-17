---
title: sp_reinitmergesubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergesubscription_TSQL
- sp_reinitmergesubscription
helpviewer_keywords:
- sp_reinitmergesubscription
ms.assetid: 249a4048-e885-48e0-a92a-6577f59de751
author: stevestein
ms.author: sstein
ms.openlocfilehash: 27c10f9d5fa04ae449bdcca84891f0f28376eeb6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075706"
---
# <a name="spreinitmergesubscription-transact-sql"></a>sp_reinitmergesubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 에이전트가 실행되는 다음 번에 병합 구독이 다시 초기화되도록 표시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_reinitmergesubscription [ [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber'  
    [ , [ @subscriber_db = ] 'subscriber_db'  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 **모든**합니다.  
  
`[ @subscriber = ] 'subscriber'` 구독자의 이름이입니다. *구독자* 됩니다 **sysname**, 기본값은 **모든**합니다.  
  
`[ @subscriber_db = ] 'subscriber_db'` 구독자 데이터베이스의 이름이입니다. *subscriber_db* 됩니다 **sysname**, 기본값은 **모든**합니다.  
  
`[ @upload_first = ] 'upload_first'` 구독을 다시 초기화 하기 전에 구독자의 변경 내용을 업로드할지 여부입니다. *upload_first* 됩니다 **nvarchar(5)** , 기본값은 FALSE입니다. 하는 경우 **true**, 구독을 다시 초기화 하기 전에 변경 내용을 업로드 합니다. 하는 경우 **false**, 변경 내용이 업로드 되지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_reinitmergesubscription** 병합 복제에 사용 됩니다.  
  
 **sp_reinitmergesubscription** 병합 구독 다시 초기화 하려면 게시자에서 호출할 수 있습니다. 스냅샷 에이전트도 다시 실행하는 것이 좋습니다.  
  
 매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_reinitmergepushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_1.sql)]  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_reinitmergepushsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_2.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_reinitmergesubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
