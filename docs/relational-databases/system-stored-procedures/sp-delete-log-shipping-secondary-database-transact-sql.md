---
title: sp_delete_log_shipping_secondary_database (Transact SQL) | Microsoft Docs
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
- sp_delete_log_shipping_secondary_database_TSQL
- sp_delete_log_shipping_secondary_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_secondary_database
ms.assetid: c71b21c0-ec04-4fbd-9735-01128b736935
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d1a0406ce09b9a6b55193f3f935e6a3a95d17c3
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spdeletelogshippingsecondarydatabase-transact-sql"></a>sp_delete_log_shipping_secondary_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 보조 데이터베이스, 로컬 기록 및 원격 기록을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>인수  
 [ **@secondary_database =** ] '*secondary_database*'  
 보조 데이터베이스의 이름입니다. *secondary_database* 은 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 **sp_delete_log_shipping_secondary_database** 에서 실행 되어야 합니다는 **마스터** 보조 서버에서 데이터베이스.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 &#40;에 대 한 SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
