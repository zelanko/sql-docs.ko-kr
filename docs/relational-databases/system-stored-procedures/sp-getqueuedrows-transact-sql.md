---
description: sp_getqueuedrows(Transact-SQL)
title: sp_getqueuedrows (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getqueuedrows_TSQL
- sp_getqueuedrows
helpviewer_keywords:
- sp_getqueuedrows
ms.assetid: 139e834f-1988-4b4d-ac81-db1f89ea90e8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6948964a224d0dfe1d36324971608e649ec45d4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481269"
---
# <a name="sp_getqueuedrows-transact-sql"></a>sp_getqueuedrows(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  구독자에서 업데이트가 보류되어 큐에 있는 행을 검색합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_getqueuedrows [ @tablename = ] 'tablename'  
    [ , [ @owner = ] 'owner'  
    [ , [ @tranid = ] 'transaction_id' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @tablename = ] 'tablename'` 테이블의 이름입니다. *tablename* 은 **sysname**이며 기본값은 없습니다. 테이블은 지연 구독의 일부여야 합니다.  
  
`[ @owner = ] 'owner'` 구독 소유자입니다. *owner* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @tranid = ] 'transaction_id'` 트랜잭션 ID로 출력을 필터링 할 수 있습니다. *transaction_id* 은 **nvarchar (70)** 이며 기본값은 NULL입니다. 지정된 경우 큐에 있는 명령과 연결된 트랜잭션 ID를 표시합니다. NULL인 경우 큐에 있는 모든 명령을 표시합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 구독된 테이블에 대해 현재 지연 트랜잭션이 적어도 하나 이상 있는 행을 모두 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**동작**|**nvarchar (10)**|동기화가 일어날 때 수행할 동작의 유형입니다.<br /><br /> INS= 삽입<br /><br /> DEL = 삭제<br /><br /> UPD = 업데이트|  
|**Id**|**nvarchar (70)**|명령이 실행되는 트랜잭션 ID입니다.|  
|**table column1...n**||*Tablename*에 지정 된 테이블의 각 열에 대 한 값입니다.|  
|**msrepl_tran_version**|**uniqueidentifier**|이 열을 사용하여 복제된 데이터의 변경 사항을 추적하고 게시자에서 충돌 감지를 수행합니다. 이 열은 테이블에 자동으로 추가됩니다.|  
  
## <a name="remarks"></a>설명  
 **sp_getqueuedrows** 는 지연 업데이트에 참여 하는 구독자에서 사용 됩니다.  
  
 **sp_getqueuedrows** 는 지연 업데이트에 참여 한 구독 데이터베이스에서 지정 된 테이블의 행을 찾지만 현재 큐 판독기 에이전트에서 확인 되지 않았습니다.  
  
## <a name="permissions"></a>사용 권한  
 **sp_getqueuedrows** 에는 *tablename*에 지정 된 테이블에 대 한 SELECT 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [지연 업데이트 충돌 감지 및 해결](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
