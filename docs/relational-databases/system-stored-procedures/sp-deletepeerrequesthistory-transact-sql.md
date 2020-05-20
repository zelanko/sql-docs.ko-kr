---
title: sp_deletepeerrequesthistory (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletepeerrequesthistory
- sp_deletepeerrequesthistory_TSQL
helpviewer_keywords:
- sp_deletepeerrequesthistory
ms.assetid: 63a4ec6e-ce79-4bf1-9d37-5ac88f8d6beb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 986fd717ede9d8fb81bfb42a818921cf3d1b553e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830265"
---
# <a name="sp_deletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시 상태 요청과 관련 된 기록을 삭제 합니다. 여기에는 요청 기록 ([MSpeer_request &#40;transact-sql&#41;](../../relational-databases/system-tables/mspeer-request-transact-sql.md)) 뿐만 아니라 응답 기록 ([MSpeer_response &#40;transact-sql&#41;](../../relational-databases/system-tables/mspeer-response-transact-sql.md))이 포함 됩니다. 이 저장 프로시저는 피어 투 피어 복제 토폴로지에 참여 하는 게시자의 게시 데이터베이스에서 실행 됩니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`상태 요청이 수행 된 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @request_id = ] request_id`이 요청에 대 한 모든 응답을 삭제 하도록 개별 상태 요청을 지정 합니다. *request_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @cutoff_date = ] cutoff_date`이전의 모든 응답 레코드를 삭제 하기 전 까지의 구분 날짜를 지정 합니다. *cutoff_date* 은 **datetime**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_deletepeerrequesthistory** 은 피어 투 피어 트랜잭션 복제 토폴로지에서 사용 됩니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 **Sp_deletepeerrequesthistory**를 실행 하는 경우 *request_id* 또는 *cutoff_date* 를 지정 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_deletepeerrequesthistory**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_helppeerrequests &#40;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [Transact-sql&#41;sp_helppeerresponses &#40;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [Transact-sql&#41;sp_requestpeerresponse &#40;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
