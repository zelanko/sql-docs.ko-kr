---
title: sp_replicationdboption (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4c0837db9666ab6b49aee30b81b5585cbf5d5ee0
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056769"
---
# <a name="sp_replicationdboption-transact-sql"></a>sp_replicationdboption(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  지정된 데이터베이스에 대한 복제 데이터베이스 옵션을 설정합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자 또는 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] 'dbname'` 복제 데이터베이스 옵션이 설정 되는 데이터베이스입니다. *db_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @optname = ] 'optname'`은 사용 하거나 사용 하지 않도록 설정 하는 복제 데이터베이스 옵션입니다. *optname* 는 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**병합 게시**|병합 게시용으로 데이터베이스를 사용할 수 있습니다.|  
|**publish**|다른 유형의 게시용으로 데이터베이스를 사용할 수 있습니다.|  
|**subscribe**|데이터베이스는 구독 데이터베이스입니다.|  
|**백업과 동기화**|통합 백업용으로 데이터베이스를 사용할 수 있습니다. 자세한 내용은 [트랜잭션 &#40;복제 복제 transact-sql 프로그래밍&#41;에 대해 통합 백업 사용](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)을 참조 하세요.|  
  
지정 된 복제 데이터베이스 옵션을 사용 하거나 사용 하지 않도록 설정할지 여부를 `[ @value = ] 'value'` 합니다. *value* 는 **sysname**이며 **true** 또는 **false**일 수 있습니다. 이 값이 **false** 이 고 *optname* 가 **merge publish**이면 병합 게시 된 데이터베이스에 대 한 구독도 삭제 됩니다.  
  
`[ @ignore_distributor = ] ignore_distributor`이 저장 프로시저가 배포자에 연결 되지 않고 실행 되는지 여부를 나타냅니다. *ignore_distributor* 은 **bit**이며 기본값은 **0**입니다. 즉, 배포자가 게시 데이터베이스의 새 상태로 연결 되어 업데이트 되어야 합니다. 값 **1** 은 배포자에 액세스할 수 없고 게시를 사용 하지 않도록 설정 하는 **sp_replicationdboption** 사용 되는 경우에만 지정 해야 합니다.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_replicationdboption** 는 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 이 프로시저는 지정된 옵션에 따라 특정 복제 시스템 테이블, 보안 계정 등을 만들거나 삭제합니다. **Master. 데이터베이스** 시스템 테이블에서 해당 **is_published** (transacational 또는 스냅숏 복제), **is_merge_published** (병합 복제) 또는 **is_distributor** 비트를 설정 하 고 필요한 시스템 테이블을 만듭니다.  
  
 게시를 해제하려면 게시 데이터베이스가 온라인 상태여야 합니다. 게시 데이터베이스용으로 데이터베이스 스냅샷이 있으면 게시를 해제하기 전에 이 데이터베이스 스냅샷을 먼저 삭제해야 합니다. 데이터베이스 스냅샷은 데이터베이스의 읽기 전용 오프라인 사본이며 복제 스냅샷과 연관되어 있지 않습니다. 자세한 내용은 [데이터베이스 스냅샷&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_replicationdboption**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시  삭제](../../relational-databases/replication/publish/delete-a-publication.md)  
 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
