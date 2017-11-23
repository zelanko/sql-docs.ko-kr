---
title: sp_deletepeerrequesthistory (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_deletepeerrequesthistory
- sp_deletepeerrequesthistory_TSQL
helpviewer_keywords: sp_deletepeerrequesthistory
ms.assetid: 63a4ec6e-ce79-4bf1-9d37-5ac88f8d6beb
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9deb92cbdc9eff3e54efb1b37d18abc7bfc01252
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spdeletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  요청 기록을 포함 하 여 게시 상태 요청과 관련 된 기록을 삭제 ([MSpeer_request &#40; Transact SQL &#41; ](../../relational-databases/system-tables/mspeer-request-transact-sql.md)) 응답 기록 뿐 아니라 ([MSpeer_response &#40; Transact SQL &#41; ](../../relational-databases/system-tables/mspeer-response-transact-sql.md)). 이 저장된 프로시저는 피어 투 피어 복제 토폴로지에 참여 하는 게시자의 게시 데이터베이스에서 실행 됩니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=** ] **'***게시***'**  
 상태가 요청된 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@request_id=** ] *request_id*  
 해당 요청에 대한 모든 응답을 삭제하도록 개별 상태 요청을 지정합니다. *request_id* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@cutoff_date=** ] *cutoff_date*  
 해당 날짜 이전의 모든 응답 레코드를 삭제하도록 구분 날짜를 지정합니다. *cutoff_date* 은 **datetime**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_deletepeerrequesthistory** 피어 투 피어 트랜잭션 복제 토폴로지에 사용 됩니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 실행할 때 **sp_deletepeerrequesthistory**, 어느 *request_id* 또는 *cutoff_date* 지정 해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_deletepeerrequesthistory**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_helppeerrequests &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [sp_helppeerresponses &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [sp_requestpeerresponse &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
