---
title: sp_delete_log_shipping_primary_database (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9f1b5625ed09cb3c5e9d753477b61fdd1e898590
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760084"
---
# <a name="sp_delete_log_shipping_primary_database-transact-sql"></a>sp_delete_log_shipping_primary_database(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 저장 프로시저는 백업 작업과 로컬 및 원격 기록을 포함하여 주 데이터베이스의 로그 전달을 제거합니다. **Sp_delete_log_shipping_primary_secondary**를 사용 하 여 보조 데이터베이스를 제거한 후에만이 저장 프로시저를 사용 하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>인수  
`[ @database = ] 'database'`로그 전달 주 데이터베이스의 이름입니다. *데이터베이스* 는 **sysname**이며 기본값은 없고 NULL 일 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 **sp_delete_log_shipping_primary_database** 는 주 서버의 **master** 데이터베이스에서 실행 해야 합니다. 이 저장 프로시저는 다음을 수행합니다.  
  
1.  지정한 주 데이터베이스에 대한 백업 작업을 삭제합니다.  
  
2.  주 서버의 **log_shipping_monitor_primary** 에서 로컬 모니터 레코드를 제거 합니다.  
  
3.  **Log_shipping_monitor_history_detail** 및 **log_shipping_monitor_error_detail**에서 해당 항목을 제거 합니다.  
  
4.  모니터 서버가 주 서버와 다른 경우는 모니터 서버에서 **log_shipping_monitor_primary** 의 모니터 레코드를 제거 합니다.  
  
5.  모니터 서버에서 **log_shipping_monitor_history_detail** 및 **log_shipping_monitor_error_detail** 의 해당 항목을 제거 합니다.  
  
6.  이 주 데이터베이스에 대 한 **log_shipping_primary_databases** 의 항목을 제거 합니다.  
  
7.  모니터 서버에서 **sp_delete_log_shipping_alert_job** 를 호출 합니다.  

## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예제  
 이 예에서는 **sp_delete_log_shipping_primary_database** 를 사용 하 여 주 데이터베이스 **AdventureWorks2012**을 삭제 하는 방법을 보여 줍니다.  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
