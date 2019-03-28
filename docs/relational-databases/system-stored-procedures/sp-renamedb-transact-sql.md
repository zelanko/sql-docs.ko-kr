---
title: sp_renamedb (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_renamedb
- sp_renamedb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_renamedb
ms.assetid: 7dd9d4ff-20e1-4857-9a8e-a5bff767cf76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dd46309ebd44bdd16da132b9aef1c903ad1f4b78
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528345"
---
# <a name="sprenamedb-transact-sql"></a>sp_renamedb(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  데이터베이스의 이름을 변경합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 ALTER DATABASE MODIFY NAME을 사용하십시오. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_renamedb [ @dbname = ] 'old_name' , [ @newname = ] 'new_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] 'old_name'` 데이터베이스의 현재 이름이입니다. *old_name* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @newname = ] 'new_name'` 데이터베이스의 새 이름이입니다. *new_name* 식별자에 대 한 규칙을 따라야 합니다. *new_name* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 수(실패)  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **sysadmin** 하거나 **dbcreator** 고정 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Accounting` 데이터베이스를 만든 후 데이터베이스의 이름을 `Financial`로 변경합니다. 그런 다음 `sys.databases` 카탈로그 뷰를 쿼리하여 데이터베이스의 새 이름을 확인합니다.  
  
```  
USE master;  
GO  
CREATE DATABASE Accounting;  
GO  
EXEC sp_renamedb N'Accounting', N'Financial';  
GO  
SELECT name, database_id, modified_date  
FROM sys.databases  
WHERE name = N'Financial';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_changedbowner&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_helpdb &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
