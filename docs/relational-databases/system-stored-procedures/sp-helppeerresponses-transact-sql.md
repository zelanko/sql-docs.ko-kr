---
title: sp_helppeerresponses (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_helppeerresponses_TSQL
- sp_helppeerresponses
helpviewer_keywords:
- sp_helppeerresponses
ms.assetid: e55789d1-43fb-4a37-9e5e-60ccef122a5d
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4488ece6abf924700f173c6753fec679d6967758
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024683"
---
# <a name="sphelppeerresponses-transact-sql"></a>sp_helppeerresponses(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  요청을 실행 하 여 시작 된 위치로 피어 투 피어 복제 토폴로지에서 참가자 로부터 받은 특정 상태 요청에 대 한 모든 응답을 반환 합니다 [sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 토폴로지에서 게시 된 데이터베이스입니다. 이 저장 프로시저는 피어 투 피어 복제 토폴로지에 참여하는 게시자의 게시 데이터베이스에서 실행됩니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>인수  
 [ **@request_id**=] *request_id*  
 특정 상태 요청 ID입니다. *request_id* 됩니다 **int**, 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|상태 요청의 ID입니다.|  
|**피어**|**sysname**|응답을 생성한 피어의 이름입니다.|  
|**peer_db**|**sysname**|응답을 생성한 피어의 데이터베이스 이름입니다.|  
|**received_date**|**datetime**|요청자가 요청을 보낸 피어로부터 응답을 받은 날짜 및 시간입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_helppeerresponses** 피어 투 피어 트랜잭션 복제에 사용 됩니다.  
  
 **sp_helppeerresponses** 절차 피어 투 피어 토폴로지에 게시 된 데이터베이스를 복원할 때 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_helppeerresponses**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_deletepeerrequesthistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
