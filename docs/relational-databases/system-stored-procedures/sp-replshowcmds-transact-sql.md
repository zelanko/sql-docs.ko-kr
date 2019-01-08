---
title: sp_replshowcmds (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 18ccbda41c5b7683c33bc0258a05738ab227ec69
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813321"
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복제용으로 표시된 트랜잭션에 대한 명령을 읽을 수 있는 형식으로 반환합니다. **sp_replshowcmds** 로그에서 복제 된 트랜잭션을 클라이언트 연결 (현재 연결 포함) 읽고 있지 않은 경우에 실행할 수 있습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>인수  
 [ **@maxtrans** =] *maxtrans*  
 정보를 반환할 트랜잭션의 수입니다. *maxtrans* 은 **int**, 기본값은 **1**에 복제 보류 중인 트랜잭션의 최대 수를 지정 하는 **sp_replshowcmds** 정보를 반환합니다.  
  
## <a name="result-sets"></a>결과 집합  
 **sp_replshowcmds** 가 실행 되는 게시 데이터베이스에 대 한 정보를 반환 하는 진단 프로시저입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|명령의 시퀀스 번호입니다.|  
|**originator_id**|**int**|항상 명령 보낸 사람의 ID **0**합니다.|  
|**publisher_database_id**|**int**|항상 게시자 데이터베이스의 ID **0**합니다.|  
|**article_id**|**int**|아티클의 ID입니다.|  
|**type**|**int**|명령의 유형입니다.|  
|**명령**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 명령입니다.|  
  
## <a name="remarks"></a>Remarks  
 **sp_replshowcmds** 트랜잭션 복제에 사용 됩니다.  
  
 사용 하 여 **sp_replshowcmds**를 볼 수 있습니다 하는 트랜잭션은 현재 (트랜잭션 트랜잭션 로그에 남아 있는 배포자에 전송 되지 않은) 배포 되지 합니다.  
  
 실행 하는 클라이언트 **sp_replshowcmds** 하 고 **sp_replcmds** 동일한 데이터베이스 내 18752 오류를 수신 합니다.  
  
 이 오류를 방지 하려면 첫 번째 클라이언트가 연결을 끊거나 로그 판독기는 클라이언트의 역할을 실행 하 여 해제 되어야 합니다 **sp_replflush**합니다. 로그 판독기에서의 모든 클라이언트 연결이 끊어진 후 **sp_replshowcmds** 성공적으로 실행할 수 있습니다.  
  
> [!NOTE]  
>  **sp_replshowcmds** 복제 관련 문제 해결을 위해서만 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_replshowcmds**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [오류 메시지](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
