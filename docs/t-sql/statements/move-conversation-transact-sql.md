---
title: MOVE CONVERSATION (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs: TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7367254b7dad104c7503c33777d26316a542b4ca
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="move-conversation-transact-sql"></a>MOVE CONVERSATION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  대화를 다른 대화 그룹으로 이동합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
MOVE CONVERSATION conversation_handle  
   TO conversation_group_id  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *conversation_handle*  
 이동할 대화의 대화 핸들을 포함하는 변수 또는 상수입니다. *conversation_handle* 형식 이어야 합니다 **uniqueidentifier**합니다.  
  
 *conversation_group_id*  
 대화가 이동될 대화 그룹의 식별자를 포함하는 변수 또는 상수입니다. *conversation_group_id* 형식 이어야 합니다 **uniqueidentifier**합니다.  
  
## <a name="remarks"></a>주의  
 MOVE CONVERSATION 문은 이동 하 여 지정 된 대화 *conversation_handle* 로 식별 되는 대화 그룹에 *conversation_group_id*합니다. 같은 큐와 연관된 대화 그룹 간에만 대화를 재지정할 수 있습니다.  
  
> [!IMPORTANT]  
>  위의 문은 세미콜론으로 종료 해야 MOVE CONVERSATION 문이 일괄 처리 또는 저장된 프로시저의 첫 번째 문이 아닌 경우 (**;**), [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 종결자입니다.  
  
 MOVE CONVERSATION 문은 연결 된 대화 그룹을 잠급니다 *conversation_handle* 및로 지정한 대화 그룹 *conversation_group_id* 트랜잭션이 될 때까지 문을 포함 하는 커밋 또는 롤백합니다.  
  
 MOVE CONVERSATION은 사용자 정의 함수에 유효하지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 대화를 이동하려면 현재 사용자가 대화 및 대화 그룹의 소유자, sysadmin 고정 서버 역할의 멤버 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 대화를 다른 대화 그룹으로 이동합니다.  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER,  
        @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_handle =  
    <retrieve conversation handle from database> ;  
SET @conversation_group_id =  
    <retrieve conversation group ID from database> ;  
  
MOVE CONVERSATION @conversation_handle TO @conversation_group_id ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [BEGIN DIALOG conversation&#40; Transact SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40; Transact SQL &#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [END CONVERSATION &#40; Transact SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
