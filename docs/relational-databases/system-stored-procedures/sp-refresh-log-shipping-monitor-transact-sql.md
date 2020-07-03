---
title: sp_refresh_log_shipping_monitor (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 93abffe797a4507c9d3329f864e09753ca1f1da0
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891520"
---
# <a name="sp_refresh_log_shipping_monitor-transact-sql"></a>sp_refresh_log_shipping_monitor(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 저장 프로시저는 지정된 로그 전달 에이전트에 대해 주어진 주 서버 또는 보조 서버에서 최신 정보로 원격 모니터 테이블을 새로 고칩니다. 이 프로시저는 주 서버나 보조 서버에서 호출됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>인수  
`[ @agent_id = ] 'agent_id'`백업에 대 한 주 ID 이거나 복사 또는 복원에 대 한 보조 ID입니다. *agent_id* 은 **uniqueidentifier** 이며 NULL 일 수 없습니다.  
  
`[ @agent_type = ] 'agent_type'`로그 전달 작업의 유형입니다.  
  
 0 = 백업  
  
 1 = 복사  
  
 2 = 복원  
  
 *agent_type* 은 **tinyint** 이며 NULL 일 수 없습니다.  
  
`[ @database = ] 'database'`백업 또는 복원 에이전트에서 로깅하는 데 사용 하는 주 데이터베이스 또는 보조 데이터베이스입니다.  
  
`[ @mode ] n`모니터 데이터를 새로 고칠지 아니면 정리할 지를 지정 합니다. *M* 의 데이터 형식은 tinyint 이며 지원 되는 값은 다음과 같습니다.  
  
 1 = 새로 고침(기본값)  
  
 2 = 삭제  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 **sp_refresh_log_shipping_monitor** 는 아직 전송 되지 않은 세션 정보를 사용 하 여 **log_shipping_monitor_primary**, **log_shipping_monitor_secondary**, **log_shipping_monitor_history_detail**및 **log_shipping_monitor_error_detail** 테이블을 새로 고칩니다. 이렇게 하면 잠시 동안 모니터가 동기화되지 않는 동안에도 모니터 서버를 주 서버 또는 보조 서버와 동기화할 수 있습니다. 또한 필요하면 모니터 서버에서 모니터 정보를 지울 수 있습니다.  
  
 **sp_refresh_log_shipping_monitor** 는 주 서버 또는 보조 서버에 있는 **master** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
