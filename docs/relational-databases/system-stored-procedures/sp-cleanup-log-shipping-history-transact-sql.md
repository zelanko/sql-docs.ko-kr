---
description: sp_cleanup_log_shipping_history(Transact-SQL)
title: sp_cleanup_log_shipping_history (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 42edf059f077f0896cd3c62b1420658c982b3d5a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486155"
---
# <a name="sp_cleanup_log_shipping_history-transact-sql"></a>sp_cleanup_log_shipping_history(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 저장 프로시저는 보존 기간을 기준으로 로컬 및 모니터 서버에서 기록을 정리합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cleanup_log_shipping_history  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>인수  
`[ @agent_id = ] 'agent_id',` 백업에 대 한 주 ID 이거나 복사 또는 복원에 대 한 보조 ID입니다. *agent_id* 은 **uniqueidentifier** 이며 NULL 일 수 없습니다.  
  
`[ @agent_type = ] 'agent_type'` 로그 전달 작업의 유형입니다. 0 = 백업, 1 = 복사, 2 = 복원입니다. *agent_type* 은 **tinyint** 이며 NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 **sp_cleanup_log_shipping_history** 는 모든 로그 전달 서버의 **master** 데이터베이스에서 실행 해야 합니다. 이 저장 프로시저는 기록 보존 기간에 따라 **log_shipping_monitor_history_detail** 및 **log_shipping_monitor_error_detail** 의 로컬 및 원격 복사본을 정리 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
