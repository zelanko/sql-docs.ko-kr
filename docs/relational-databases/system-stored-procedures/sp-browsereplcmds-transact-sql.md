---
description: sp_browsereplcmds(Transact-SQL)
title: sp_browsereplcmds (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsereplcmds_TSQL
- sp_browsereplcmds
helpviewer_keywords:
- sp_browsereplcmds
ms.assetid: 30abcb41-1d18-4f43-a692-4c80914c0450
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 39fafe6f0e36d0c88ebb74285e8c8206977f73bd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548245"
---
# <a name="sp_browsereplcmds-transact-sql"></a>sp_browsereplcmds(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  배포 데이터베이스에 복제되어 저장된 결과 집합을 읽을 수 있는 버전으로 반환합니다. 이 결과 집합은 진단 도구에서 사용됩니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## <a name="arguments"></a>인수  
`[ @xact_seqno_start = ] 'xact_seqno_start'` 반환할 가장 작은 값의 정확한 시퀀스 번호를 지정 합니다. *xact_seqno_start* 은 **nchar (22)** 이며 기본값은은 x 00000000000000000000입니다.  
  
`[ @xact_seqno_end = ] 'xact_seqno_end'` 반환할 가장 높은 정확한 시퀀스 번호를 지정 합니다. *xact_seqno_end* 은 **nchar (22)** 이며 기본값은 0xffffffffffffffffffff입니다.  
  
`[ @originator_id = ] 'originator_id'` 지정 된 *originator_id* 의 명령이 반환 되는지 여부를 지정 합니다. *originator_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @publisher_database_id = ] 'publisher_database_id'` 지정 된 *publisher_database_id* 의 명령이 반환 되는지 여부를 지정 합니다. *publisher_database_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @article_id = ] 'article_id'` 지정 된 *article_id* 의 명령이 반환 되는지 여부를 지정 합니다. *article_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @command_id = ] command_id` 는 디코딩할 [transact-sql&#41;&#40;MSrepl_commands ](../../relational-databases/system-tables/msrepl-commands-transact-sql.md) 의 명령 위치입니다. *command_id* 은 **int**이며 기본값은 NULL입니다. 지정 된 경우 다른 모든 매개 변수를 지정 해야 하 고 *xact_seqno_start* *xact_seqno_end*와 동일 해야 합니다.  
  
`[ @agent_id = ] agent_id` 특정 복제 에이전트에 대 한 명령만 반환 하도록 지정 합니다. *agent_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @compatibility_level = ] compatibility_level`Compatibility_level int 인 버전 이며 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본값은 *compatibility_level* 900만입니다 **int**.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|명령의 시퀀스 번호입니다.|  
|**originator_srvname**|**sysname**|트랜잭션이 시작된 서버입니다.|  
|**originator_db**|**sysname**|트랜잭션이 시작된 데이터베이스입니다.|  
|**article_id**|**int**|아티클의 ID입니다.|  
|**type**|**int**|명령의 유형입니다.|  
|**partial_command**|**bit**|부분 명령인지 여부를 나타냅니다.|  
|**hashkey**|**int**|내부적으로만 사용됩니다.|  
|**originator_publication_id**|**int**|트랜잭션이 시작된 게시의 ID입니다.|  
|**originator_db_version**|**int**|트랜잭션이 시작된 데이터베이스의 버전입니다.|  
|**originator_lsn**|**varbinary(16)**|원본 게시에서 명령의 LSN(로그 시퀀스 번호)을 식별합니다. 피어 투 피어 트랜잭션 복제에 사용됩니다.|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 명령입니다.|  
|**command_id**|**int**|[MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)명령의 ID입니다.|  
  
 긴 명령은 결과 집합에서 여러 행으로 분할될 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **sp_browsereplcmds** 은 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 배포 데이터베이스에서 **sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 또는 **replmonitor** 고정 데이터베이스 역할의 멤버만 **sp_browsereplcmds**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_replcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [Transact-sql&#41;sp_replshowcmds &#40;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
