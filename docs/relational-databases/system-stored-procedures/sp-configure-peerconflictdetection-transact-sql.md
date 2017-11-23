---
title: sp_configure_peerconflictdetection (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_configure_peerconflictdetection_TSQL
- sp_configure_peerconflictdetection
helpviewer_keywords: sp_configure_peerconflictdetection
ms.assetid: 45117cb2-3247-433f-ba3d-7fa19514b1c3
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1fed4cb47795554df26deb08f496edba86b5a4d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spconfigurepeerconflictdetection-transact-sql"></a>sp_configure_peerconflictdetection(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  피어 투 피어 트랜잭션 복제 토폴로지에 관련된 게시에 대한 충돌 감지를 구성합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)을(를) 참조하세요. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_configure_peerconflictdetection [ @publication = ] 'publication'  
    [ , [ @action = ] 'action']  
    [ , [ @originator_id = ] originator_id ]  
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @continue_onconflict = ] 'continue_onconflict']  
    [ , [ @local = ] 'local']  
    [ , [ @timeout = ] timeout ]  
  
```  
  
## <a name="arguments"></a>인수  
 [ @publication=] '*게시*'  
 충돌 감지를 구성할 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [ @action=] '*동작*'  
 이 게시에 대해 충돌 검색을 사용할지 여부를 지정합니다. *동작* 은 **nvarchar (5)**, 다음 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**사용 하도록 설정**|게시에 충돌 감지를 사용합니다.|  
|**사용 안 함**|게시에 충돌 감지를 사용하지 않습니다.|  
|NULL(기본값)||  
  
 [ @originator_id=] *originator_id*  
 피어 투 피어 토폴로지에 있는 노드의 ID를 지정합니다. *originator_id* 은 **int**, 기본값은 NULL입니다. 충돌 검색에이 ID를 사용 하는 경우 *동작* 로 설정 된 **사용**합니다. 토폴로지에 사용되지 않은 0이 아닌 양수 ID를 지정합니다. 이미 사용된 ID 목록을 보려면 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 시스템 테이블을 쿼리하십시오.  
  
 [ @conflict_retention=] *conflict_retention*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @continue_onconflict=] '*continue_onconflict*']  
 충돌이 검색된 후 배포 에이전트에서 변경 내용을 계속 처리할지 여부를 결정합니다. *continue_onconflict* 은 **nvarchar (5)** 기본값은 FALSE입니다.  
  
> [!CAUTION]  
>  기본값인 FALSE를 사용하는 것이 좋습니다. 이 옵션이 TRUE로 설정된 경우 배포 에이전트는 송신자 ID가 가장 높은 노드에서 충돌 행을 적용하여 토폴로지의 데이터를 일치시킵니다. 이 방법으로 데이터가 일치하게 되지 않는 경우도 있습니다. 충돌이 검색된 후 토폴로지의 일관성을 확인해야 합니다. 자세한 내용은 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)의 "충돌 처리"를 참조하십시오.  
  
 [ @local=] '*로컬*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @timeout=] *제한 시간*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_configure_peerconflictdetection은 피어 투 피어 트랜잭션 복제에 사용됩니다. 충돌 검색을 사용 하려면 모든 노드에서 실행 해야 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 설정 되거나 모든 노드에 대해 이상; 및 검색을 설정 해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [피어 투 피어 복제에서 충돌 검색](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
