---
title: sp_droprolemember (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_droprolemember_TSQL
- sp_droprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprolemember
ms.assetid: c2f19ab1-e742-4d56-ba8e-8ffd40cf4925
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a8fa0c5aa19b1ef09034b5419f0d47b784ff191e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spdroprolemember-transact-sql"></a>sp_droprolemember(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할에서 보안 계정을 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>인수  
 [  **@rolename =** ] **'***역할***'**  
 멤버를 제거할 역할의 이름입니다. *역할* 은 **sysname**, 기본값은 없습니다. *역할* 현재 데이터베이스에 존재 해야 합니다.  
  
 [  **@membername =** ] **'***security_account***'**  
 역할에서 제거될 보안 계정의 이름입니다. *security_account* 은 **sysname**, 기본값은 없습니다. *security_account* 데이터베이스 사용자, 다른 데이터베이스 역할, Windows 로그인 또는 Windows 그룹 일 수 있습니다. *security_account* 현재 데이터베이스에 존재 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 sp_droprolemember는 sysmembers 테이블에서 행을 삭제 하 여 데이터베이스 역할에서 구성원을 제거 합니다. 역할에서 멤버를 제거하는 경우 이 멤버는 해당 역할의 멤버 자격을 통해 부여 받은 모든 사용 권한을 잃게 됩니다.  
  
 고정된 서버 역할에서 사용자를 제거 하려면 sp_dropsrvrolemember를 사용 합니다. 사용자가 public 역할에서 제거할 수 없습니다 및 dbo 역할에서 제거할 수 없습니다.  
  
 Sp_helpuser의 멤버를 사용 하 여 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할 및 역할에 구성원을 추가 하려면 ALTER ROLE을 사용 합니다.  
  
## <a name="permissions"></a>Permissions  
 역할에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `JonB` 역할에서 `Sales`라는 사용자를 제거합니다.  
  
```  
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `JonB` 역할에서 `Sales`라는 사용자를 제거합니다.  
  
```  
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprole&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [sp_dropsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

