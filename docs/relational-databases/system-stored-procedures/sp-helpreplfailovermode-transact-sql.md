---
title: sp_helpreplfailovermode (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
author: stevestein
ms.author: sstein
ms.openlocfilehash: ff5bd9978be59f6a512ce4173b851692b9506d96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997559"
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  구독의 현재 장애 조치(Failover) 모드를 표시합니다. 이 저장 프로시저는 모든 데이터베이스의 구독자에서 실행됩니다. 장애 조치 모드에 대 한 자세한 내용은 참조 하세요. [업데이트할 수 있는 Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 이 구독자의 업데이트에 참여 하는 게시자의 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다. 게시하려면 게시자가 미리 구성되어 있어야 합니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publication = ] 'publication'` 이 구독자의 업데이트에 참여 하는 게시의 이름이입니다. *게시*됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @failover_mode_id = ] 'failover_mode_id' OUTPUT` 장애 조치 모드의 정수 값을 반환 하 고은 **출력** 매개 변수입니다. *failover_mode_id* 되는 **tinyint** 이며 기본값은 **0**합니다. 반환 **0** 즉시 업데이트 하 고 **1** 지연 업데이트에 대 한 합니다.  
  
 [ **@failover_mode=** ] **'***failover_mode***'OUTPUT**  
 구독자에서 데이터가 수정되는 모드를 반환합니다. *failover_mode* 되는 **nvarchar(10)** 이며 기본값은 NULL입니다. **출력** 매개 변수입니다.  
  
|값|설명|  
|-----------|-----------------|  
|**immediate**|즉시 업데이트: 구독자에서 수행되는 업데이트가 2단계 커밋 프로토콜(2PC)을 사용하여 즉시 게시자로 전파됩니다.|  
|**queued**|지연 업데이트: 구독자에서 수행되는 업데이트가 큐에 저장됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpreplfailovermode** 구독 즉시 업데이트를 사용 하도록 설정 된 장애 조치로 지연 업데이트에 오류가 발생 한 경우에 대 한 스냅숏 복제 또는 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_helpreplfailovermode**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_setreplfailovermode &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
