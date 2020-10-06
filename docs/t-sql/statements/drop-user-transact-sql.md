---
description: DROP USER(Transact-SQL)
title: DROP USER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_USER_TSQL
- DROP USER
dev_langs:
- TSQL
helpviewer_keywords:
- dropping users
- DROP USER statement
- deleting users
- database user removal [SQL Server]
- removing users
- users [SQL Server], removing
ms.assetid: d6e0e21a-7568-4321-b6d6-bcfba183a719
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f5afe06027e489fb7b9971edd1fcc81853e4f93
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91498253"
---
# <a name="drop-user-transact-sql"></a>DROP USER(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스에서 사용자를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP USER [ IF EXISTS ] user_name  
```  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
DROP USER user_name  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *IF EXISTS*  
 **Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] through [current version](https://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).  
  
 Conditionally drops the user only if it already exists.  
  
 *user_name*  
 Specifies the name by which the user is identified inside this database.  
  
## Remarks  
 Users that own securables cannot be dropped from the database. Before dropping a database user that owns securables, you must first drop or transfer ownership of those securables.  
  
 The guest user cannot be dropped, but guest user can be disabled by revoking its CONNECT permission by executing REVOKE CONNECT FROM GUEST within any database other than master or tempdb.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## Permissions  
 Requires ALTER ANY USER permission on the database.  
  
## Examples  
 The following example removes database user `AbolrousHazem` from the `AdventureWorks2012` database.  
  
```sql  
DROP USER AbolrousHazem;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [ALTER USER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
