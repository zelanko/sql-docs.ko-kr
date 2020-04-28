---
title: sp_renamedb (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: eebf9be216d61163c018e0d43075e636cb383d28
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006929"
---
# <a name="sp_renamedb-transact-sql"></a>sp_renamedb(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  데이터베이스의 이름을 변경합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 ALTER DATABASE MODIFY NAME을 사용하십시오. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_renamedb [ @dbname = ] 'old_name' , [ @newname = ] 'new_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] 'old_name'`데이터베이스의 현재 이름입니다. *old_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @newname = ] 'new_name'`데이터베이스의 새 이름입니다. *new_name* 는 식별자에 대 한 규칙을 따라야 합니다. *new_name* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 0이 아닌 수(실패)  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 또는 **dbcreator** 고정 서버 역할의 멤버 자격이 필요 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Transact-sql&#41;sp_changedbowner &#40;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [Transact-sql&#41;sp_helpdb &#40;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
