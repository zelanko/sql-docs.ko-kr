---
description: sp_replication_agent_checkup(Transact-SQL)
title: sp_replication_agent_checkup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replication_agent_checkup_TSQL
- sp_replication_agent_checkup
helpviewer_keywords:
- sp_replication_agent_checkup
ms.assetid: 50357c2e-71aa-4e13-9e2e-0977a3655cc9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5bcd42ae639fad4b50feb6aac829a39abc9a1cad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485736"
---
# <a name="sp_replication_agent_checkup-transact-sql"></a>sp_replication_agent_checkup(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  실행되고 있으나 지정된 하트비트 간격 내에서 기록을 작성하지 않은 복제 에이전트에 대한 각 배포 데이터베이스를 확인합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>인수  
`[ @heartbeat_interval = ] 'heartbeat_interval'` 진행률 메시지를 기록 하지 않고 에이전트를 진행할 수 있는 최대 시간 (분)입니다. *heartbeat_interval* 은 **int**이며 기본값은 10 분입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **sp_replication_agent_checkup** 는 주의 대상으로 검색 된 각 에이전트에 대해 오류 14151을 발생 시킵니다. 또한 에이전트에 대한 실패 기록 메시지를 기록합니다.  
  
## <a name="remarks"></a>설명  
 **sp_replication_agent_checkup** 는 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_replication_agent_checkup**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
