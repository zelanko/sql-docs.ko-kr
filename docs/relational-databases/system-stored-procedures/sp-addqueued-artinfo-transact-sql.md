---
title: sp_addqueued_artinfo (Transact SQL) | Microsoft Docs
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
- sp_addqueued_artinfo
- sp_addqueued_artinfo_TSQL
helpviewer_keywords:
- sp_addqueued_artinfo
ms.assetid: decdb6eb-3dcd-4053-a21d-fd367c3fbafb
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 54f86a0ef91cda13cce706f0bd96941f5bc5bc86
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddqueuedartinfo-transact-sql"></a>sp_addqueued_artinfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  
> [!IMPORTANT]  
>  [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 프로시저를 대신 사용 해야 **sp_addqueued_artinfo**합니다. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 포함 하는 스크립트를 생성 된 **sp_addqueued_artinfo** 및 **sp_addsynctrigger** 호출 합니다.  
  
 만듭니다는 [MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md) 아티클 구독 정보 (지연 업데이트 및 장애 조치로 지연 업데이트를 사용 하는 즉시 업데이트)를 추적 하는 데 사용 되는 구독자의 테이블입니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
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
 [  **@artid=** ] **'***artid***'**  
 아티클 ID의 이름입니다. *artid* 은 **int**, 기본값은 없습니다  
  
 [  **@article=**] **'***문서***'**  
 스크립팅할 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 없습니다  
  
 [ **@publisher=**] **'***publisher***'**  
 게시자 서버의 이름입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 게시자 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publication=**] **'***publication***'**  
 스크립팅할 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@dest_table=** ] *' dest_table * * * '**  
 대상 테이블의 이름입니다. *dest_table* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@owner =** ] **'***소유자***'**  
 구독의 소유자입니다. *소유자* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@cft_table=** ] **'***cft_table***'**  
 이 아티클에 대한 지연 업데이트 충돌 테이블의 이름입니다. *cft_table*은 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_addqueued_artinfo** 구독 초기화의 일부로 배포 에이전트에서 사용 됩니다. 일반적으로 사용자는 이 저장 프로시저를 실행하지 않습니다. 하지만 사용자가 구독을 수동으로 설정해야 하는 경우에는 유용할 수도 있습니다.  
  
 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 대신 **sp_addqueued_artinfo**합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_addqueued_artinfo**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [MSsubscription_articles &#40;Transact SQL&#41;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
