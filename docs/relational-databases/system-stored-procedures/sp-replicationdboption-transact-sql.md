---
title: sp_replicationdboption (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9a88d295f6ae5ff0fcfab7121a4057dd84f75957
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
 복제 데이터베이스 옵션을 설정할 데이터베이스입니다. *db_name* 은 **sysname**, 기본값은 없습니다.  
  
 [**@optname=**] **'***optname***'**  
 설정 또는 해제할 복제 데이터베이스 옵션입니다. *optname* 은 **sysname**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**병합 게시**|병합 게시용으로 데이터베이스를 사용할 수 있습니다.|  
|**게시**|다른 유형의 게시용으로 데이터베이스를 사용할 수 있습니다.|  
|**구독**|데이터베이스는 구독 데이터베이스입니다.|  
|**백업으로 동기화**|통합 백업용으로 데이터베이스를 사용할 수 있습니다. 자세한 내용은 참조 [트랜잭션 복제에 대해 통합 백업을 사용 하도록 설정 &#40;Replication TRANSACT-SQL Programming&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)합니다.|  
  
 [  **@value=**] **'***값***'**  
 지정된 복제 데이터베이스 옵션의 설정 또는 해제 여부를 나타냅니다. *값* 은 **sysname**, 수 및 **true** 또는 **false**합니다. 이 값이 **false** 및 *optname* 은 **병합 게시**, 병합 게시 된 데이터베이스에 대 한 구독도 삭제 됩니다.  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 이 저장 프로시저가 배포자에 연결되지 않고 실행되는지 여부를 표시합니다. *ignore_distributor* 은 **비트**, 기본값은 **0**은 배포자에 연결 하 고 해야 게시 데이터베이스의 새 상태로 업데이트 합니다. 값 **1** 지정할 수만 배포자는 액세스할 수 있는지 및 **sp_replicationdboption** 게시를 해제 하는 데 사용 되 고 있습니다.  
  
 [  **@from_scripting=**] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_replicationdboption** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 이 프로시저는 지정된 옵션에 따라 특정 복제 시스템 테이블, 보안 계정 등을 만들거나 삭제합니다. 해당 범주는 비트를 설정의 **master.sysdatabases** 시스템 테이블 및 필요한 시스템 테이블을 만듭니다.  
  
 게시를 해제하려면 게시 데이터베이스가 온라인 상태여야 합니다. 게시 데이터베이스용으로 데이터베이스 스냅숏이 있으면 게시를 해제하기 전에 이 데이터베이스 스냅숏을 먼저 삭제해야 합니다. 데이터베이스 스냅숏은 데이터베이스의 읽기 전용 오프라인 사본이며 복제 스냅숏과 연관되어 있지 않습니다. 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)을 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_replicationdboption**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 삭제](../../relational-databases/replication/publish/delete-a-publication.md)   
 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.sysdatabases &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
