---
title: sp_delete_log_shipping_alert_job (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_alert_job
- sp_delete_log_shipping_alert_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_alert_job
ms.assetid: 5d6c7f07-a163-48fa-8c1f-abc252043dde
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b2a41f6d453fd1d029426afb5753f558a73ba08
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spdeletelogshippingalertjob-transact-sql"></a>sp_delete_log_shipping_alert_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  작업은 있지만 모니터링할 주 데이터베이스나 보조 데이터베이스가 더 이상 없는 경우 로그 전달 모니터 서버에서 경고 작업을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_log_shipping_alert_job  
  
```  
  
## <a name="arguments"></a>인수  
 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 **sp_delete_log_shipping_alert_job** 에서 실행 되어야 합니다는 **마스터** 모니터 서버에는 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예에서는 실행 **sp_delete_log_shipping_alert_job** 경고 작업을 삭제 하 합니다.  
  
```  
USE master;  
GO  
EXEC sp_delete_log_shipping_alert_job;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 & #40;에 대 한 SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
