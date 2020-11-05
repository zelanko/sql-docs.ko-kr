---
description: sp_reinitmergepullsubscription(Transact-SQL)
title: sp_reinitmergepullsubscription (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergepullsubscription
- sp_reinitmergepullsubscription_TSQL
helpviewer_keywords:
- sp_reinitmergepullsubscription
ms.assetid: 48464bc9-60aa-4886-b526-163f010102b8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 06b65044129dd302d516eabe3b9c13f6352d3035
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364809"
---
# <a name="sp_reinitmergepullsubscription-transact-sql"></a>sp_reinitmergepullsubscription(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  다음 번 병합 에이전트 실행 시 병합 끌어오기 구독이 다시 초기화되도록 표시합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_reinitmergepullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자의 이름입니다. *publisher* 는 **sysname** 이며 기본값은 ALL입니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname** 이며 기본값은 ALL입니다.  
  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname** 이며 기본값은 ALL입니다.  
  
`[ @upload_first = ] 'upload_first'` 구독을 다시 초기화 하기 전에 구독자에서 변경 내용을 업로드 하는지 여부입니다. *upload_first* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **True** 이면 구독을 다시 초기화 하기 전에 변경 내용이 업로드 됩니다. **False** 이면 변경 내용이 업로드 되지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_reinitmergepullsubscription** 는 병합 복제에 사용 됩니다.  
  
 매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
## <a name="examples"></a>예  

### <a name="a-reinitialize-the-pull-subscription-and-lose-pending-changes"></a>A. 끌어오기 구독을 다시 초기화 하 고 보류 중인 변경 내용을 손실 합니다.

[!code-sql[HowTo#sp_reinitmergepullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_1.sql)]  
  
### <a name="b-reinitialize-the-pull-subscription-and-upload-pending-changes"></a>B. 끌어오기 구독을 다시 초기화 하 고 보류 중인 변경 내용을 업로드 합니다.

 [!code-sql[HowTo#sp_reinitmergepullsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_2.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_reinitmergepullsubscription** 을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
