---
title: sp_dropmergepullsubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropmergepullsubscription
- sp_dropmergepullsubscription_TSQL
helpviewer_keywords:
- sp_dropmergepullsubscription
ms.assetid: 9301dd80-72f7-4adb-9b13-87e7f9114248
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1fa2a31c5ef60b869fe387e4a3ac8155a73d3690
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43017959"
---
# <a name="spdropmergepullsubscription-transact-sql"></a>sp_dropmergepullsubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 끌어오기 구독을 삭제합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmergepullsubscription [ @publication= ] 'publication'   
        , [ @publisher= ] 'publisher'   
        , [ @publisher_db= ] 'publisher_db'   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 필수 항목입니다. 값을 지정 **모든** 모든 게시에 대 한 구독을 제거 하려면  
  
 [ **@publisher=**] **'***publisher***'**  
 게시자의 이름입니다. *게시자*됩니다 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 필수 항목입니다.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 게시자 데이터베이스의 이름입니다. *publisher_db*됩니다 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 필수 항목입니다.  
  
 [  **@reserved=**] **'***예약 된***'**  
 나중에 사용하도록 예약되었습니다. *예약* 됩니다 **비트**, 기본값은 **0**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropmergepullsubscription** 병합 복제에 사용 됩니다.  
  
 **sp_dropmergepullsubscription** 병합 에이전트에서 생성 되지 않습니다 하지만 해당 병합 끌어오기 구독에 대 한 병합 에이전트를 삭제 **sp_addmergepullsubscription**합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepullsubscrip_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 병합 끌어오기 구독을 만든 사용자를 실행할 수 있습니다 **sp_dropmergepullsubscription**합니다. 합니다 **db_owner** 고정된 데이터베이스 역할은 실행할 수만 **sp_dropmergepullsubscription** 병합 끌어오기 구독을 만든 사용자가이 역할에 속한 경우.  
  
## <a name="see-also"></a>관련 항목  
 [끌어오기 구독 삭제](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)  
  
  
