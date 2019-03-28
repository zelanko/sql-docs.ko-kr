---
title: sp_cleanup_log_shipping_history (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cleanup_log_shipping_history_TSQL
- sp_cleanup_log_shipping_history
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cleanup_log_shipping_history
ms.assetid: 96d236a9-1d0e-4f83-a4d3-f825b7381e46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5247959cacb4df4fd51275c3f826280bffbb9fd
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538485"
---
# <a name="spcleanuplogshippinghistory-transact-sql"></a>sp_cleanup_log_shipping_history(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 보존 기간을 기준으로 로컬 및 모니터 서버에서 기록을 정리합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cleanup_log_shipping_history  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>인수  
`[ @agent_id = ] 'agent_id',` 백업에 대 한 주 ID 또는 복사 또는 복원에 대 한 보조 ID입니다. *agent_id* 됩니다 **uniqueidentifier** NULL 일 수 없습니다.  
  
`[ @agent_type = ] 'agent_type'` 로그 전달 작업의 형식입니다. 0 = 백업, 1 = 복사, 2 = 복원입니다. *agent_type* 됩니다 **tinyint** NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 **sp_cleanup_log_shipping_history** 에서 실행 해야 합니다 **마스터** 로그 전달 서버에 데이터베이스입니다. 이 저장된 프로시저의 복사본을 로컬 및 원격 정리 **log_shipping_monitor_history_detail** 하 고 **log_shipping_monitor_error_detail** 기록 보존 기간을 기준으로 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
