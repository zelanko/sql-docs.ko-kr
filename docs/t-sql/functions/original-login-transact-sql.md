---
title: ORIGINAL_LOGIN (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs: TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c49c887b85ae6c5314420f8ba93e6b1f11604818
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="originallogin-transact-sql"></a>ORIGINAL_LOGIN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 연결된 로그인의 이름을 반환합니다. 이 함수를 사용하여 명시적 또는 암시적 컨텍스트 전환이 많이 있는 세션의 원래 로그인 ID를 반환할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>반환 형식  
 **sysname**  
  
## <a name="remarks"></a>주의  
 이 함수는 원래 연결 컨텍스트의 ID를 감사하는 데 유용할 수 있습니다. 반면와 같은 함수가 [SESSION_USER](../../t-sql/functions/session-user-transact-sql.md) 및 [CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md) 인스턴스에최초로연결한로그인의id를반환하는현재실행중인컨텍스트ORIGINAL_LOGIN반환[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]해당 세션에서 합니다.  
  
 에 NULL을 반환 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 세션의 실행 컨텍스트를 문의 호출자에서 `login1`로 전환합니다. `SUSER_SNAME` 및 `ORIGINAL_LOGIN` 함수를 사용하여 현재 세션 사용자(컨텍스트가 전환되는 대상 사용자)와 원래 로그인 계정을 반환할 수 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
--Create a temporary login and user.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE USER user1 FOR LOGIN login1;  
GO  
--Execute a context switch to the temporary login account.  
DECLARE @original_login sysname;  
DECLARE @current_context sysname;  
EXECUTE AS LOGIN = 'login1';  
SET @original_login = ORIGINAL_LOGIN();  
SET @current_context = SUSER_SNAME();  
SELECT 'The current executing context is: '+ @current_context;  
SELECT 'The original login in this session was: '+ @original_login  
GO  
-- Return to the original execution context  
-- and remove the temporary principal.  
REVERT;  
GO  
DROP LOGIN login1;  
DROP USER user1;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [실행 AS &#40; Transact SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [되돌리기 &#40; Transact SQL &#41;](../../t-sql/statements/revert-transact-sql.md)  
  
  
