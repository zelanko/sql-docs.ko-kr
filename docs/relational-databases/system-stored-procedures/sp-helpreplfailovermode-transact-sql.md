---
description: sp_helpreplfailovermode(Transact-SQL)
title: sp_helpreplfailovermode (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5503291dc5011366ab6fe3b4a2d60b0a1310ba79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489293"
---
# <a name="sp_helpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  구독의 현재 장애 조치(Failover) 모드를 표시합니다. 이 저장 프로시저는 모든 데이터베이스의 구독자에서 실행됩니다. 장애 조치 (failover) 모드에 대 한 자세한 내용은 [트랜잭션 복제를 위한 업데이트할](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)수 있는 구독을 참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 이 구독자의 업데이트에 참여 하 고 있는 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다. 게시하려면 게시자가 미리 구성되어 있어야 합니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'` 이 구독자의 업데이트에 참여 하는 게시의 이름입니다. *게시*는 **sysname**이며 기본값은 없습니다.  
  
`[ @failover_mode_id = ] 'failover_mode_id' OUTPUT` 장애 조치 (failover) 모드의 정수 값을 반환 하 고 **출력** 매개 변수입니다. *failover_mode_id* 은 **tinyint** 이며 기본값은 **0**입니다. 즉시 업데이트의 경우 **0** 을 반환 하 고 지연 업데이트의 경우 **1** 을 반환 합니다.  
  
`[ @failover_mode = ] 'failover_mode' OUTPUT` 구독자에서 데이터가 수정 되는 모드를 반환 합니다. *failover_mode* 은 **nvarchar (10)** 이며 기본값은 NULL입니다. 는 **OUTPUT** 매개 변수입니다.  
  
|값|설명|  
|-----------|-----------------|  
|**관련이**|즉시 업데이트: 구독자에서 수행되는 업데이트가 2단계 커밋 프로토콜(2PC)을 사용하여 즉시 게시자로 전파됩니다.|  
|**넣었습니다**|지연 업데이트: 구독자에서 수행되는 업데이트가 큐에 저장됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 장애 조치 (failover)로 지연 업데이트를 사용 하 여 즉시 업데이트를 사용 하도록 설정 하는 스냅숏 복제 또는 트랜잭션 복제에는 **sp_helpreplfailovermode** 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helpreplfailovermode**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_setreplfailovermode &#40;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
