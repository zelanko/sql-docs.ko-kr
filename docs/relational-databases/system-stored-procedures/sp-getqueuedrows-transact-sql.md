---
title: sp_getqueuedrows (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_getqueuedrows_TSQL
- sp_getqueuedrows
helpviewer_keywords:
- sp_getqueuedrows
ms.assetid: 139e834f-1988-4b4d-ac81-db1f89ea90e8
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 229f47fe354f84717cd833c2203544b8ddd237a3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spgetqueuedrows-transact-sql"></a>sp_getqueuedrows(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  구독자에서 업데이트가 보류되어 큐에 있는 행을 검색합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_getqueuedrows [ @tablename = ] 'tablename'  
    [ , [ @owner = ] 'owner'  
    [ , [ @tranid = ] 'transaction_id' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@tablename =**] **'***tablename***'**  
 테이블의 이름입니다. *tablename* 은 **sysname**, 기본값은 없습니다. 테이블은 지연 구독의 일부여야 합니다.  
  
 [  **@owner =**] **'***소유자***'**  
 구독 소유자입니다. *소유자* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@tranid =** ] **'***transaction_id***'**  
 트랜잭션 ID로 출력을 필터링할 수 있습니다. *transaction_id* 은 **nvarchar (70)**, 기본값은 NULL입니다. 지정된 경우 큐에 있는 명령과 연결된 트랜잭션 ID를 표시합니다. NULL인 경우 큐에 있는 모든 명령을 표시합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 구독된 테이블에 대해 현재 지연 트랜잭션이 적어도 하나 이상 있는 행을 모두 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**작업**|**nvarchar(10)**|동기화가 일어날 때 수행할 동작의 유형입니다.<br /><br /> INS= 삽입<br /><br /> DEL = 삭제<br /><br /> UPD = 업데이트|  
|**Tranid**|**nvarchar (70)**|명령이 실행되는 트랜잭션 ID입니다.|  
|**테이블 열 1... n**||에 지정 된 테이블의 각 열에 대 한 값 *tablename*합니다.|  
|**msrepl_tran_version**|**uniqueidentifier**|이 열을 사용하여 복제된 데이터의 변경 사항을 추적하고 게시자에서 충돌 감지를 수행합니다. 이 열은 테이블에 자동으로 추가됩니다.|  
  
## <a name="remarks"></a>주의  
 **sp_getqueuedrows** 지연 업데이트 구독자에서 사용 됩니다.  
  
 **sp_getqueuedrows** 구독에서 지정된 된 테이블의 행을 데이터베이스를 찾습니다는 지연된 업데이트에 참여 하지만 현재 해결 하지 못한 큐 판독기 에이전트에 의해 합니다.  
  
## <a name="permissions"></a>Permissions  
 **sp_getqueuedrows** 에 지정 된 테이블에 대 한 SELECT 권한이 필요 *tablename*합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [지연 업데이트 충돌 감지 및 해결](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
