---
description: sp_addsynctriggers(Transact-SQL)
title: sp_addsynctriggers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsynctriggers_TSQL
- sp_addsynctriggers
helpviewer_keywords:
- sp_addsynctriggers
ms.assetid: e37d0c3b-19bf-4719-9535-96ba361372b3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 400b6ef96cd841c2115fcb13bd5e8b782816ce43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486273"
---
# <a name="sp_addsynctriggers-transact-sql"></a>sp_addsynctriggers(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  업데이트할 수 있는 모든 유형의 구독(즉시 업데이트, 대기 업데이트 및 장애 조치로 지연 업데이트를 사용하는 즉시 업데이트)에 사용되는 구독자에서 트리거를 만들 수 있습니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  **Sp_addsynctrigger**대신 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 프로시저를 사용 해야 합니다. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 은 **sp_addsynctrigger** 호출을 포함 하는 스크립트를 생성 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addsynctriggers [ @sub_table = ] 'sub_table'  
        , [ @sub_table_owner = ] 'sub_table_owner'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @ins_proc = ] 'ins_proc'   
        , [ @upd_proc = ] 'upd_proc'   
        , [ @del_proc = ] 'del_proc'   
        , [ @cftproc = ] 'cftproc'  
        , [ @proc_owner = ] 'proc_owner'  
    [ , [ @identity_col = ] 'identity_col' ]  
    [ , [ @ts_col = ] 'timestamp_col' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]   
        , [ @primary_key_bitmap = ] 'primary_key_bitmap'  
    [ , [ @identity_support = ] identity_support ]  
    [ , [ @independent_agent = ] independent_agent ]  
        , [ @distributor = ] 'distributor'   
    [ , [ @pubversion = ] pubversion  
```  
  
## <a name="arguments"></a>인수  
`[ @sub_table = ] 'sub_table'` 구독자 테이블의 이름입니다. *sub_table* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @sub_table_owner = ] 'sub_table_owner'` 구독자 테이블 소유자의 이름입니다. *sub_table_owner* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher = ] 'publisher'` 게시자 서버의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다. NULL인 경우 현재 데이터베이스가 사용됩니다.  
  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @ins_proc = ] 'ins_proc'` 게시자에서 동기 트랜잭션 삽입을 지 원하는 저장 프로시저의 이름입니다. *ins_proc* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @upd_proc = ] 'upd_proc'` 게시자에서 동기 트랜잭션 업데이트를 지 원하는 저장 프로시저의 이름입니다. *ins_proc* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @del_proc = ] 'del_proc'` 게시자에서 동기 트랜잭션 삭제를 지 원하는 저장 프로시저의 이름입니다. *ins_proc* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @cftproc = ] 'cftproc'` 지연 업데이트를 허용 하는 게시에 사용 되는 자동 생성 프로시저의 이름입니다. *cftproc* 는 **sysname**이며 기본값은 없습니다. 즉시 업데이트를 허용하는 게시의 경우 이 값은 NULL입니다. 이 매개 변수는 지연 업데이트(지연 업데이트 및 장애 조치로 지연 업데이트를 사용하는 즉시 업데이트)를 허용하는 게시에 적용됩니다.  
  
`[ @proc_owner = ] 'proc_owner'` 게시 업데이트를 위한 자동 생성 저장 프로시저 (큐에 대기 및/또는 즉시)가 생성 된 게시자의 사용자 계정을 지정 합니다. *proc_owner* 는 **sysname** 이며 기본값은 없습니다.  
  
`[ @identity_col = ] 'identity_col'` 게시자에 있는 id 열의 이름입니다. *identity_col* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @ts_col = ] 'timestamp_col'` 게시자에 있는 **타임 스탬프** 열의 이름입니다. *timestamp_col* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @filter_clause = ] 'filter_clause'` 는 가로 필터를 정의 하는 제한 (WHERE) 절입니다. 제약 조건 절을 입력할 때는 키워드인 WHERE를 생략합니다. *filter_clause*은 **nvarchar (4000)** 이며 기본값은 NULL입니다.  
  
`[ @primary_key_bitmap = ] 'primary_key_bitmap'` 테이블에 있는 기본 키 열의 비트 맵입니다. *primary_key_bitmap* 은 **varbinary (4000)** 이며 기본값은 없습니다.  
  
`[ @identity_support = ] identity_support` 지연 업데이트를 사용 하는 경우 자동 id 범위 처리를 사용 하거나 사용 하지 않도록 설정 합니다. *identity_support* 은 **bit**이며 기본값은 **0**입니다. **0** 은 id 범위를 지원 하지 않음을 의미 하 고 **1** 은 자동 id 범위 처리를 사용 하도록 설정 합니다.  
  
`[ @independent_agent = ] independent_agent` 이 게시에 대해 단일 배포 에이전트 (독립 에이전트)가 있는지, 게시 데이터베이스 및 구독 데이터베이스 쌍 (공유 에이전트) 당 하나 배포 에이전트 있는지를 나타냅니다. 이 값은 게시자에서 정의된 게시의 independent_agent 속성 값을 반영합니다. *independent_agent* 은 bit 이며 기본값은 **0**입니다. **0**인 경우 에이전트는 공유 에이전트입니다. **1**인 경우 에이전트는 독립 에이전트입니다.  
  
`[ @distributor = ] 'distributor'` 배포자의 이름입니다. *배포자* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @pubversion = ] pubversion` 게시자의 버전을 나타냅니다. *pubversion* 은 **int**이며 기본값은 1입니다. **1** 은 게시자 버전이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서비스 팩 2 이전 임을 의미 합니다. **2** 는 게시자가 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서비스 팩 3 (SP3) 이상 임을 의미 합니다. 게시자 버전이 SP3 이상이 면 *pubversion* 을 명시적으로 **2** 로 설정 해야 합니다 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addsynctriggers** 은 배포 에이전트에서 구독 초기화의 일부로 사용 됩니다. 일반적으로 사용자는 이 저장 프로시저를 실행하지 않지만 no-sync 구독을 수동으로 설정해야 하는 경우 유용할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addsynctriggers**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Transact-sql&#41;sp_script_synctran_commands &#40;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
