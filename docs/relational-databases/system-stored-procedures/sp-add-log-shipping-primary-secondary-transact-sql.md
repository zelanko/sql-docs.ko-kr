---
title: sp_add_log_shipping_primary_secondary (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_secondary_TSQL
- sp_add_log_shipping_primary_secondary
dev_langs: TSQL
helpviewer_keywords: sp_add_log_shipping_primary_secondary
ms.assetid: 23b3e100-5318-410e-b8f3-51c89b2dd777
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44648eaceac290955b321dd36e78b5c80dea9e3b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spaddlogshippingprimarysecondary-transact-sql"></a>sp_add_log_shipping_primary_secondary(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 저장 프로시저는 주 서버의 보조 데이터베이스에 대한 항목을 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_log_shipping_primary_secondary  
[ @primary_database = ] 'primary_database',  
[ @secondary_server = ] 'secondary_server',   
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>인수  
 [  **@primary_database**  =] '*primary_database*'  
 주 서버의 데이터베이스 이름입니다. *primary_database* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@secondary_server**  =] '*secondary_server*',  
 보조 서버의 이름입니다. *secondary_server* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@secondary_database**  =] '*secondary_database*'  
 보조 데이터베이스의 이름입니다. *secondary_database* 은 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 **sp_add_log_shipping_primary_secondary** 에서 실행 되어야 합니다는 **마스터** 주 서버의 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예제에서는 사용 하 여 **sp_add_log_shipping_primary_secondary** 보조 데이터베이스에 대 한 항목을 추가 하도록 **LogShipAdventureWorks** FLATIRON 보조 서버에 있습니다.  
  
```  
EXEC master.dbo.sp_add_log_shipping_primary_secondary   
@primary_database = N'AdventureWorks'   
, @secondary_server = N'flatiron'   
, @secondary_database = N'LogShipAdventureWorks' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
