---
title: sp_helppeerrequests (Transact SQL) | Microsoft Docs
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
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords: sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d2ea35c01385de46ded538c98faf701e34d3892
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelppeerrequests-transact-sql"></a>sp_helppeerrequests(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  실행 하 여 이러한 요청을 시작한 하는 피어 투 피어 복제 토폴로지의 참가자 들이 받은 모든 상태 요청에 대 한 정보를 반환 [sp_requestpeerresponse &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 토폴로지에 게시 된 데이터베이스입니다. 이 저장 프로시저는 피어 투 피어 복제 토폴로지에 참여하는 게시자의 게시 데이터베이스에서 실행됩니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication** =] **'***게시***'**  
 상태 요청이 전송된 피어 투 피어 토폴로지의 게시 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@description** =] **'***설명***'**  
 호출할 때 제공 되는 사용자 정의 정보에 따라 반환 된 응답을 필터링 할 수 있는 개별 상태 요청을 식별 하는 데 사용할 수 있는 값 [sp_requestpeerresponse &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). *설명* 은 **nvarchar (4000)**, 기본값은  **%** 합니다. 기본적으로 게시에 대한 모든 상태 요청이 반환됩니다. 이 매개 변수는 제공 된 값이 일치 하는 설명을 가진 상태 요청만 반환 하는 데 사용 되 *설명*문자열 일치를 사용 하 여 여기서는 [같은 &#40; Transact SQL &#41; ](../../t-sql/language-elements/like-transact-sql.md) 절.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**id**|**int**|요청을 식별합니다.|  
|**게시**|**sysname**|상태 요청이 전송된 게시의 이름입니다.|  
|**sent_date**|**datetime**|상태 요청이 전송된 날짜와 시간입니다.|  
|**설명**|**nvarchar(4000)**|개별 상태 요청을 식별하기 위해 사용할 수 있는 사용자 정의 정보입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helppeerrequests** 피어 투 피어 트랜잭션 복제에 사용 됩니다.  
  
 **sp_helppeerrequests** 피어 투 피어 토폴로지에 게시 된 데이터베이스를 복원 하는 경우에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_helppeerrequests**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_deletepeerrequesthistory &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
