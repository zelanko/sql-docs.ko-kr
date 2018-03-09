---
title: DB_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3ca4b497be936701205b2be245f76a52eb372c2a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
반환될 데이터베이스의 ID입니다. *database_id* 은 **int**, 기본값은 없습니다. ID를 지정하지 않으면 현재 데이터베이스 이름이 반환됩니다.
  
## <a name="return-types"></a>반환 형식
**nvarchar (128)**
  
## <a name="permissions"></a>Permissions  
하는 경우의 호출자 **DB_NAME** 데이터베이스의 소유자가 아니고 및 데이터베이스가 **마스터** 또는 **tempdb**, 해당 행을 보는 데 필요한 최소 권한으로 ALTER ANY DATABASE 또는 VIEW ANY DATABASE 서버 수준 사용 권한 또는 CREATE DATABASE 권한은 **마스터** 데이터베이스입니다. 호출자가 연결된 데이터베이스는 항상 **sys.databases**에서 볼 수 있습니다.
  
> [!IMPORTANT]  
>  기본적으로 public 역할 VIEW ANY DATABASE, 권한이 데이터베이스 정보를 볼 수 있는 모든 로그인을 허용 합니다. 데이터베이스를 검색 하는 기능에서의 로그인을 차단 하려면 public에서 VIEW ANY DATABASE 권한을 해지 하거나 개별 로그인에 대 한 VIEW ANY DATABASE 권한을 거부 합니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>3. 현재 데이터베이스 이름 반환  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>4. 데이터베이스 ID를 사용 하 여 데이터베이스의 이름을 반환합니다  
다음 예에서는 데이터베이스 이름 및 각 데이터베이스에 대 한 database_id 반환합니다.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>참고 항목
[DB_ID &#40; Transact SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)  
[메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

