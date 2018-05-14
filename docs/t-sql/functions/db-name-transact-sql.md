---
title: DB_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DB_NAME
- DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database names [SQL Server], DB_NAME
- names [SQL Server], databases
- viewing database names
- displaying database names
- DB_NAME function
ms.assetid: e21fb33a-a3ea-49b0-bb6b-8f789a675a0e
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1c2a2e92fdef5cae1b2404d18c2c5fb18b3de1ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dbname-transact-sql"></a>DB_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

데이터베이스 이름을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>인수  
*database_id*  
반환될 데이터베이스의 ID입니다. *database_id*는 **int**이며 기본값은 없습니다. ID를 지정하지 않으면 현재 데이터베이스 이름이 반환됩니다.
  
## <a name="return-types"></a>반환 형식
**nvarchar(128)**
  
## <a name="permissions"></a>사용 권한  
**DB_NAME**의 호출자가 데이터베이스의 소유자가 아니고 데이터베이스가 **master** 또는 **tempdb**가 아닐 경우 해당 행을 보려면 최소한 서버 수준의 ALTER ANY DATABASE 또는 VIEW ANY DATABASE 권한이 있거나 **master** 데이터베이스에서 CREATE DATABASE 권한이 있어야 합니다. 호출자가 연결된 데이터베이스는 항상 **sys.databases**에서 볼 수 있습니다.
  
> [!IMPORTANT]  
>  기본적으로 public 역할에는 모든 로그인이 데이터베이스 정보를 보도록 허용하는 VIEW ANY DATABASE 권한이 있습니다. 특정 로그인이 데이터베이스를 검색하지 못하게 하려면 public에서 VIEW ANY DATABASE 권한을 REVOKE하거나 개별 로그인에 대해 VIEW ANY DATABASE 권한을 DENY합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-current-database-name"></a>1. 현재 데이터베이스 이름 반환  
다음 예에서는 현재 데이터베이스의 이름을 반환합니다.
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>2. 지정한 데이터베이스 ID의 데이터베이스 이름 반환  
다음 예에서는 데이터베이스 ID `3`의 데이터베이스 이름을 반환합니다.
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>3. 현재 데이터베이스 이름 반환  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>4. 데이터베이스 ID를 사용하여 데이터베이스의 이름을 반환합니다  
다음 예에서는 각 데이터베이스에 대해 데이터베이스 이름과 database_id를 반환합니다.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>관련 항목:
[DB_ID&#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

