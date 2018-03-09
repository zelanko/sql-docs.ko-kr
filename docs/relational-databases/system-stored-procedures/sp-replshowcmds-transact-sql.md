---
title: sp_replshowcmds (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7e949d3372266ca3857204e5d6bc5e35111855a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
 [  **@maxtrans**  =] *maxtrans*  
 정보를 반환할 트랜잭션의 수입니다. *maxtrans* 은 **int**, 기본값은 **1**, 복제를 보류 중인 트랜잭션의 최대 수를 지정 하는 **sp_replshowcmds** 정보를 반환 합니다.  
  
## <a name="result-sets"></a>결과 집합  
 **sp_replshowcmds** 가 실행 되는 게시 데이터베이스에 대 한 정보를 반환 하는 진단 프로시저입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|명령의 시퀀스 번호입니다.|  
|**originator_id**|**int**|항상 명령 보낸 사람의 ID **0**합니다.|  
|**publisher_database_id**|**int**|항상 게시자 데이터베이스의 ID **0**합니다.|  
|**article_id**|**int**|아티클의 ID입니다.|  
|**유형**|**int**|명령의 유형입니다.|  
|**명령**|**nvarchar (1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 명령입니다.|  
  
## <a name="remarks"></a>주의  
 **sp_replshowcmds** 트랜잭션 복제에 사용 됩니다.  
  
 사용 하 여 **sp_replshowcmds**를 볼 수의 트랜잭션은 현재 (트랜잭션 트랜잭션 로그에에서 남아 있는 배포자에 게 전송 되지 않은) 배포 되지 않습니다.  
  
 실행 하는 클라이언트 **sp_replshowcmds** 및 **sp_replcmds** 동일한 데이터베이스 내 18752 오류를 받게 됩니다.  
  
 이 오류를 방지 하려면 첫 번째 클라이언트가 연결을 끊거나 클라이언트 로그 판독기로 서의 역할을 실행 하 여 해제 되어야 **sp_replflush**합니다. 로그 판독기에서의 모든 클라이언트 연결이 끊어진 후 **sp_replshowcmds** 성공적으로 실행할 수 있습니다.  
  
> [!NOTE]  
>  **sp_replshowcmds** 복제 관련 문제를 해결 하기 위해서만 적용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_replshowcmds**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [오류 메시지](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
