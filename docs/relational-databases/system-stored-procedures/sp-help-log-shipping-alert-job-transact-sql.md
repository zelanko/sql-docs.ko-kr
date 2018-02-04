---
title: sp_help_log_shipping_alert_job (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_alert_job_TSQL
- sp_help_log_shipping_alert_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_alert_job
ms.assetid: 4d4b4577-c393-4961-b2d3-b56e980b787b
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 142e0549a6a8469b802fde02c608b283b5bc4364
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sphelplogshippingalertjob-transact-sql"></a>sp_help_log_shipping_alert_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 로그 전달 모니터에서 경고 작업의 작업 ID를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_log_shipping_alert_job  
  
```  
  
## <a name="arguments"></a>인수  
 InclusionThresholdSetting  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 이 저장 프로시저 반환 된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 ID는 로그 전달 경고 작업입니다. 로그 전달 경고 작업이 없으면 빈 결과 집합을 반환합니다.  
  
## <a name="remarks"></a>주의  
 **sp_help_log_shipping_alert_job** 에서 실행 되어야 합니다는 **마스터** 모니터 서버에는 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 &#40;에 대 한 SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
