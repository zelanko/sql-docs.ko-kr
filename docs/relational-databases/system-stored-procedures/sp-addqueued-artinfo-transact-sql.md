---
title: sp_addqueued_artinfo (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 25f91084afe2c2bdfc27bc0b2ad874bd87447b67
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68769013"
---
# <a name="sp_addqueued_artinfo-transact-sql"></a>sp_addqueued_artinfo(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  
  
> [!IMPORTANT]  
>  **Sp_addqueued_artinfo**대신 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 프로시저를 사용 해야 합니다. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) **sp_addqueued_artinfo** 및 **sp_addsynctrigger** 호출을 포함 하는 스크립트를 생성 합니다.  
  
 아티클 구독 정보를 추적 하는 데 사용 되는 구독자에 [MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md) 테이블을 만듭니다. 지연 업데이트 및 장애 조치 (Failover)로 지연 업데이트를 사용 하 여 즉시 업데이트 합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @artid = ] 'artid'`아티클 ID의 이름입니다. *artid* 은 **int**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`스크립팅할 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher = ] 'publisher'`게시자 서버의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`스크립팅할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @dest_table = ] _'dest_table'`대상 테이블의 이름입니다. *dest_table* 는 **sysname**이며 기본값은 없습니다.  
  
 [**@owner =** ] **'**_owner_**'**  
 구독의 소유자입니다. *owner* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @cft_table = ] 'cft_table'`이 아티클에 대 한 지연 업데이트 충돌 테이블의 이름입니다. *cft_table*는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addqueued_artinfo** 은 배포 에이전트에서 구독 초기화의 일부로 사용 됩니다. 일반적으로 사용자는 이 저장 프로시저를 실행하지 않습니다. 하지만 사용자가 구독을 수동으로 설정해야 하는 경우에는 유용할 수도 있습니다.  
  
 **sp_addqueued_artinfo**대신 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addqueued_artinfo**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 복제에 대 한 업데이트할 수 있는 구독](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Transact-sql&#41;sp_script_synctran_commands &#40;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [Transact-sql&#41;MSsubscription_articles &#40;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
