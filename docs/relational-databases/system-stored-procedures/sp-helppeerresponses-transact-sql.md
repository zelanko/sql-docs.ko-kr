---
description: sp_helppeerresponses(Transact-SQL)
title: sp_helppeerresponses (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerresponses_TSQL
- sp_helppeerresponses
helpviewer_keywords:
- sp_helppeerresponses
ms.assetid: e55789d1-43fb-4a37-9e5e-60ccef122a5d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1b3918d773984223c450e11ead71d045bf21db6d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535133"
---
# <a name="sp_helppeerresponses-transact-sql"></a>sp_helppeerresponses(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  피어 투 피어 복제 토폴로지의 참가자 로부터 받은 특정 상태 요청에 대 한 모든 응답을 반환 합니다. 여기서 요청은 토폴로지에 게시 된 데이터베이스에서 [sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 를 실행 하 여 시작 됩니다. 이 저장 프로시저는 피어 투 피어 복제 토폴로지에 참여하는 게시자의 게시 데이터베이스에서 실행됩니다. 자세한 내용은 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>인수  
`[ @request_id = ] request_id` 특정 상태 요청의 ID입니다. *request_id* 는 **int**이며 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|상태 요청의 ID입니다.|  
|**피어는**|**sysname**|응답을 생성한 피어의 이름입니다.|  
|**peer_db**|**sysname**|응답을 생성한 피어의 데이터베이스 이름입니다.|  
|**received_date**|**datetime**|요청자가 요청을 보낸 피어로부터 응답을 받은 날짜 및 시간입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helppeerresponses** 은 피어 투 피어 트랜잭션 복제에 사용 됩니다.  
  
 **sp_helppeerresponses** 프로시저는 피어 투 피어 토폴로지에 게시 된 데이터베이스를 복원할 때 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helppeerresponses**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_deletepeerrequesthistory &#40;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [Transact-sql&#41;sp_helppeerrequests &#40;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
