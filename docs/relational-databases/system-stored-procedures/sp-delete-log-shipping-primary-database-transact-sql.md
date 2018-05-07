---
title: sp_delete_log_shipping_primary_database (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 76a1b1ac129d33866984eb7a0f428149e4e299a2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spdeletelogshippingprimarydatabase-transact-sql"></a>sp_delete_log_shipping_primary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 백업 작업과 로컬 및 원격 기록을 포함하여 주 데이터베이스의 로그 전달을 제거합니다. 만이 저장된 프로시저를 사용 하 여 사용 하 여 보조 데이터베이스를 제거한 후 **sp_delete_log_shipping_primary_secondary**합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>인수  
 [  **@database =** ] '*데이터베이스*'  
 로그 전달 주 데이터베이스의 이름입니다. *데이터베이스* 은 **sysname**, 기본값은 없고 NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 **sp_delete_log_shipping_primary_database** 에서 실행 되어야 합니다는 **마스터** 주 서버의 데이터베이스입니다. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  지정한 주 데이터베이스에 대한 백업 작업을 삭제합니다.  
  
2.  로컬 모니터 레코드를 제거 **log_shipping_monitor_primary** 주 서버에 있습니다.  
  
3.  해당 항목을 제거 **log_shipping_monitor_history_detail** 및 **log_shipping_monitor_error_detail**합니다.  
  
4.  모니터 서버가 주 서버에서 다른 경우에서 모니터 레코드를 제거 **log_shipping_monitor_primary** 모니터 서버에 있습니다.  
  
5.  해당 항목을 제거 **log_shipping_monitor_history_detail** 및 **log_shipping_monitor_error_detail** 모니터 서버에 있습니다.  
  
6.  항목을 제거 **log_shipping_primary_databases** 이 주 데이터베이스에 대 한 합니다.  
  
7.  호출 **sp_delete_log_shipping_alert_job** 모니터 서버에 있습니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예제에서는 사용 하 여 **sp_delete_log_shipping_primary_database** 주 데이터베이스를 삭제 하려면 **AdventureWorks2012**합니다.  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 & #40;에 대 한 SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
