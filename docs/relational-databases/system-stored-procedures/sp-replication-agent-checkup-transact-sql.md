---
title: sp_replication_agent_checkup (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_replication_agent_checkup_TSQL
- sp_replication_agent_checkup
helpviewer_keywords:
- sp_replication_agent_checkup
ms.assetid: 50357c2e-71aa-4e13-9e2e-0977a3655cc9
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8fcb953c182dd6f4e9726a45a6fbf10efd8584cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32995630"
---
# <a name="spreplicationagentcheckup-transact-sql"></a>sp_replication_agent_checkup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  실행되고 있으나 지정된 하트비트 간격 내에서 기록을 작성하지 않은 복제 에이전트에 대한 각 배포 데이터베이스를 확인합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@heartbeat_interval** =] **'***heartbeat_interval***'**  
 진행률 메시지를 기록하지 않고 에이전트를 실행할 수 있는 최대 시간(분)입니다. *heartbeat_interval* 은 **int**, 기본값은 10 분입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **sp_replication_agent_checkup** 주의 대상으로 하는 각 에이전트에 대해 14151 오류를 발생 시킵니다. 또한 에이전트에 대한 실패 기록 메시지를 기록합니다.  
  
## <a name="remarks"></a>주의  
 **sp_replication_agent_checkup** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_replication_agent_checkup**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
