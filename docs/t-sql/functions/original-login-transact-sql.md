---
title: ORIGINAL_LOGIN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ff9f53c6dd3e0029f2627545c7654ded3219abbe
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67914528"
---
# <a name="original_login-transact-sql"></a>ORIGINAL_LOGIN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 연결된 로그인의 이름을 반환합니다. 이 함수를 사용하여 명시적 또는 암시적 컨텍스트 전환이 많이 있는 세션의 원래 로그인 ID를 반환할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>반환 형식  
 **sysname**  
  
## <a name="remarks"></a>설명  
 이 함수는 원래 연결 컨텍스트의 ID를 감사하는 데 유용할 수 있습니다. [SESSION_USER](../../t-sql/functions/session-user-transact-sql.md) 및 [CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md)와 같은 함수가 현재 실행 중인 컨텍스트를 반환하는 반면에 ORIGINAL_LOGIN은 해당 세션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 인스턴스에 최초로 연결한 로그인의 ID를 반환합니다.  
 
  
## <a name="examples"></a>예  
 다음 예에서는 현재 세션의 실행 컨텍스트를 문의 호출자에서 `login1`로 전환합니다. `SUSER_SNAME` 및 `ORIGINAL_LOGIN` 함수를 사용하여 현재 세션 사용자(컨텍스트가 전환되는 대상 사용자)와 원래 로그인 계정을 반환할 수 있습니다. 
 
  >[!NOTE]
  > ORIGINAL_LOGIN 함수는 Azure SQL Database에서 지원되지만, *로그인으로 실행*은 Azure SQL Database에서 지원되지 않으므로 다음 스크립트가 실패합니다. 
  
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
  
## <a name="see-also"></a>참고 항목  
 [EXECUTE AS&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)  
  
  
