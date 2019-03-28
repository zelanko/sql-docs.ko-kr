---
title: sp_replicationdboption (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 153c2e2b8c75c21451dca3b673129a059d78e3a6
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527335"
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [**@dbname=**] **'***dbname***'**  
 복제 데이터베이스 옵션을 설정할 데이터베이스입니다. *db_name* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [**@optname=**] **'***optname***'**  
 설정 또는 해제할 복제 데이터베이스 옵션입니다. *optname* 됩니다 **sysname**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**병합 게시**|병합 게시용으로 데이터베이스를 사용할 수 있습니다.|  
|**publish**|다른 유형의 게시용으로 데이터베이스를 사용할 수 있습니다.|  
|**subscribe**|데이터베이스는 구독 데이터베이스입니다.|  
|**백업을 사용 하 여 동기화**|통합 백업용으로 데이터베이스를 사용할 수 있습니다. 자세한 내용은 [트랜잭션 복제에 대해 통합 백업 사용 &#40;복제 TRANSACT-SQL 프로그래밍&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)합니다.|  
  
`[ @value = ] 'value'` 지정 된 복제 데이터베이스 옵션을 사용할지 여부입니다. *값* 은 **sysname**, 수 및 **true** 하거나 **false**합니다. 이 값이 **false** 하 고 *optname* 됩니다 **병합 게시**, 병합 게시 데이터베이스에 대 한 구독도 삭제 됩니다.  
  
`[ @ignore_distributor = ] ignore_distributor` 이 저장된 프로시저는 배포자에 연결 하지 않고 실행 되는지 여부를 나타냅니다. *ignore_distributor* 됩니다 **비트**, 기본값은 **0**은 배포자에 연결 되어 있고 게시 데이터베이스의 새 상태를 업데이트 합니다. 값 **1** 지정할 수만 배포자 액세스할 수 없는 경우와 **sp_replicationdboption** 게시를 사용 하지 않도록 설정 하는 데 사용 되는 합니다.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_replicationdboption** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 이 프로시저는 지정된 옵션에 따라 특정 복제 시스템 테이블, 보안 계정 등을 만들거나 삭제합니다. 해당 범주는 비트를 설정 합니다 **master.sysdatabases** 시스템 테이블 및 필요한 시스템 테이블을 만듭니다.  
  
 게시를 해제하려면 게시 데이터베이스가 온라인 상태여야 합니다. 게시 데이터베이스용으로 데이터베이스 스냅숏이 있으면 게시를 해제하기 전에 이 데이터베이스 스냅숏을 먼저 삭제해야 합니다. 데이터베이스 스냅숏은 데이터베이스의 읽기 전용 오프라인 사본이며 복제 스냅숏과 연관되어 있지 않습니다. 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_replicationdboption**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 삭제](../../relational-databases/replication/publish/delete-a-publication.md)   
 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.sysdatabases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
