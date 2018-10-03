---
title: sp_refresh_log_shipping_monitor (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4382dc4de4010944e60cb37640759e91a0fc2727
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851561"
---
# <a name="sprefreshlogshippingmonitor-transact-sql"></a>sp_refresh_log_shipping_monitor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 지정된 로그 전달 에이전트에 대해 주어진 주 서버 또는 보조 서버에서 최신 정보로 원격 모니터 테이블을 새로 고칩니다. 이 프로시저는 주 서버나 보조 서버에서 호출됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>인수  
 [ **@agent_id=** ] **'***agent_id***'**  
 백업의 경우 주 ID, 복사나 복원의 경우 보조 ID입니다. *agent_id* 됩니다 **uniqueidentifier** NULL 일 수 없습니다.  
  
 [ **@agent_type=** ] **'***agent_type***'**  
 로그 전달 작업의 유형입니다.  
  
 0 = 백업  
  
 1 = 복사  
  
 2 = 복원  
  
 *agent_type* 됩니다 **tinyint** NULL 일 수 없습니다.  
  
 [  **@database=** ] **'***데이터베이스***'**  
 백업 에이전트나 복원 에이전트가 기록하는 데 사용하는 주 데이터베이스 또는 보조 데이터베이스입니다.  
  
 [ **@mode** ] *n*  
 모니터 데이터를 새로 고칠 것인지 또는 지울 것인지 지정합니다. 데이터 형식이 *m* tinyint 이며 지원 되는 값:  
  
 1 = 새로 고침(기본값)  
  
 2 = 삭제  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 **sp_refresh_log_shipping_monitor** 새로 고침 합니다 **log_shipping_monitor_primary**를 **log_shipping_monitor_secondary**, **log_shipping_monitor_history_detail** , 및 **log_shipping_monitor_error_detail** 아직 전송 되지 않은 세션 정보를 사용 하 여 테이블입니다. 이렇게 하면 잠시 동안 모니터가 동기화되지 않는 동안에도 모니터 서버를 주 서버 또는 보조 서버와 동기화할 수 있습니다. 또한 필요하면 모니터 서버에서 모니터 정보를 지울 수 있습니다.  
  
 **sp_refresh_log_shipping_monitor** 에서 실행 되어야 합니다는 **마스터** 기본 또는 보조 서버의 데이터베이스입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
