---
title: sp_helppeerrequests (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5b9e2a370c9acc9c22dac7e5e60ceb10e08e46ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68137621"
---
# <a name="sp_helppeerrequests-transact-sql"></a>sp_helppeerrequests(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  피어 투 피어 복제 토폴로지의 참가자가 받은 모든 상태 요청에 대 한 정보를 반환 합니다. 이러한 요청은 토폴로지에 게시 된 데이터베이스에서 [sp_requestpeerresponse &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 를 실행 하 여 시작 됩니다. 이 저장 프로시저는 피어 투 피어 복제 토폴로지에 참여하는 게시자의 게시 데이터베이스에서 실행됩니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`상태 요청이 전송 된 피어 투 피어 토폴로지의 게시 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @description = ] 'description'`개별 상태 요청을 식별 하는 데 사용할 수 있는 값입니다 .이 값을 사용 하면 [sp_requestpeerresponse &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)를 호출할 때 제공 된 사용자 정의 정보를 기준으로 반환 된 응답을 필터링 할 수 있습니다. *설명은* **nvarchar (4000)** 이며 기본값은 **%** 입니다. 기본적으로 게시에 대한 모든 상태 요청이 반환됩니다. 이 매개 변수는 *설명*에 제공 된 값과 일치 하는 설명으로 상태 요청만 반환 하는 데 사용 됩니다. 여기서 문자열은 [LIKE &#40;transact-sql&#41;](../../t-sql/language-elements/like-transact-sql.md) 절을 사용 하 여 일치 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|요청을 식별합니다.|  
|**게시물**|**sysname**|상태 요청이 전송된 게시의 이름입니다.|  
|**sent_date**|**datetime**|상태 요청이 전송된 날짜와 시간입니다.|  
|**한**|**nvarchar(4000)**|개별 상태 요청을 식별하기 위해 사용할 수 있는 사용자 정의 정보입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helppeerrequests** 은 피어 투 피어 트랜잭션 복제에 사용 됩니다.  
  
 **sp_helppeerrequests** 는 피어 투 피어 토폴로지에 게시 된 데이터베이스를 복원할 때 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helppeerrequests**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_deletepeerrequesthistory &#40;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [Transact-sql&#41;sp_helppeerresponses &#40;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
