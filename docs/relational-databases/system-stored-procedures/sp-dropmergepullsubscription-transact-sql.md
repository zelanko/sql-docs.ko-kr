---
title: sp_dropmergepullsubscription (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepullsubscription
- sp_dropmergepullsubscription_TSQL
helpviewer_keywords:
- sp_dropmergepullsubscription
ms.assetid: 9301dd80-72f7-4adb-9b13-87e7f9114248
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1a22fdc297c4ce7310b8d71b65dbe1cd4e0abf04
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830067"
---
# <a name="sp_dropmergepullsubscription-transact-sql"></a>sp_dropmergepullsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 끌어오기 구독을 삭제합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergepullsubscription [ @publication= ] 'publication'   
        , [ @publisher= ] 'publisher'   
        , [ @publisher_db= ] 'publisher_db'   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 필수입니다. 모든 게시에 대 한 구독을 제거 하려면 **all** 값을 지정 합니다.  
  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher*는 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 필수입니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db*는 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 필수입니다.  
  
`[ @reserved = ] 'reserved'`는 나중에 사용 하도록 예약 되어 있습니다. *reserved* 는 **bit**이며 기본값은 **0**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_dropmergepullsubscription** 는 병합 복제에 사용 됩니다.  
  
 **sp_addmergepullsubscription**에서 병합 에이전트 생성 되지 않은 경우에도이 병합 끌어오기 구독에 대 한 병합 에이전트를 **sp_dropmergepullsubscription** 삭제 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepullsubscrip_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버나 병합 끌어오기 구독을 만든 사용자만 **sp_dropmergepullsubscription**을 실행할 수 있습니다. **Db_owner** 고정 데이터베이스 역할은 병합 끌어오기 구독을 만든 사용자가이 역할에 속하는 경우에만 **sp_dropmergepullsubscription** 을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [끌어오기 구독 삭제](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [Transact-sql&#41;sp_addmergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_changemergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergepullsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)  
  
  
