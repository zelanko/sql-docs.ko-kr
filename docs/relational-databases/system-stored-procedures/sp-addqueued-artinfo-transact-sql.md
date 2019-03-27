---
title: sp_addqueued_artinfo (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addqueued_artinfo
- sp_addqueued_artinfo_TSQL
helpviewer_keywords:
- sp_addqueued_artinfo
ms.assetid: decdb6eb-3dcd-4053-a21d-fd367c3fbafb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e44891f5a16625cb6c3176fac8188fa568822add
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493186"
---
# <a name="spaddqueuedartinfo-transact-sql"></a>sp_addqueued_artinfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  
> [!IMPORTANT]  
>  합니다 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 프로시저를 대신 사용 해야 **sp_addqueued_artinfo**합니다. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 포함 된 스크립트를 생성 합니다 **sp_addqueued_artinfo** 하 고 **sp_addsynctrigger** 호출 합니다.  
  
 만듭니다는 [MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md) 아티클 구독 정보 (지연 업데이트 및 장애 조치로 지연 업데이트를 사용 하는 즉시 업데이트)을 추적 하는 데 사용 되는 구독자의 테이블입니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addqueued_artinfo [ @artid= ] 'artid'  
        , [ @article= ] 'article'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @dest_table= ] 'dest_table'  
        , [ @owner = ] 'owner'  
        , [ @cft_table= ] 'cft_table'  
```  
  
## <a name="arguments"></a>인수  
`[ @artid = ] 'artid'` 문서 ID의 이름 *artid* 됩니다 **int**, 기본값은 없습니다  
  
`[ @article = ] 'article'` 스크립팅할 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다  
  
`[ @publisher = ] 'publisher'` 게시자 서버의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시자 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publication = ] 'publication'` 스크립팅할 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @dest_table = ] _'dest_table'` 대상 테이블의 이름이입니다. *dest_table* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [**@owner =** ] **'**_owner_**'**  
 구독의 소유자입니다. *소유자* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @cft_table = ] 'cft_table'` 이 문서에 대 한 지연된 업데이트 충돌 테이블의 이름입니다. *cft_table*됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_addqueued_artinfo** 구독 초기화의 일부로 배포 에이전트에서 사용 됩니다. 일반적으로 사용자는 이 저장 프로시저를 실행하지 않습니다. 하지만 사용자가 구독을 수동으로 설정해야 하는 경우에는 유용할 수도 있습니다.  
  
 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) of **sp_addqueued_artinfo**합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_addqueued_artinfo**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [MSsubscription_articles &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
