---
title: sp_helppeerresponses (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helppeerresponses_TSQL
- sp_helppeerresponses
helpviewer_keywords:
- sp_helppeerresponses
ms.assetid: e55789d1-43fb-4a37-9e5e-60ccef122a5d
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 312020da93e5df6ea6f2f4cf0fcc482e8f4b94bd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelppeerresponses-transact-sql"></a>sp_helppeerresponses(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  요청을 실행 하 여 시작 된 위치로 피어 투 피어 복제 토폴로지의 참가자 로부터 받은 특정 상태 요청에 대 한 모든 응답 반환 [sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 토폴로지에 게시 된 데이터베이스입니다. 이 저장 프로시저는 피어 투 피어 복제 토폴로지에 참여하는 게시자의 게시 데이터베이스에서 실행됩니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>인수  
 [ **@request_id**=] *request_id*  
 특정 상태 요청 ID입니다. *request_id* 은 **int**, 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|상태 요청의 ID입니다.|  
|**피어**|**sysname**|응답을 생성한 피어의 이름입니다.|  
|**peer_db**|**sysname**|응답을 생성한 피어의 데이터베이스 이름입니다.|  
|**received_date**|**datetime**|요청자가 요청을 보낸 피어로부터 응답을 받은 날짜 및 시간입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helppeerresponses** 피어 투 피어 트랜잭션 복제에 사용 됩니다.  
  
 **sp_helppeerresponses** 프로시저는 피어 투 피어 토폴로지에 게시 된 데이터베이스를 복원할 때 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_helppeerresponses**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_deletepeerrequesthistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
