---
title: DB_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5aa5e2a60189a82fb60cd416b7f87b35824e236f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68118976"
---
# <a name="db_name-transact-sql"></a>DB_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 함수는 지정된 데이터베이스의 이름을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>인수  
*database_id*  

반환될 이름 `DB_NAME`의 데이터베이스 ID입니다. `DB_NAME`에 대한 호출이 *database_id*를 생략하는 경우 `DB_NAME`는 현재 데이터베이스의 이름을 반환합니다.
  
## <a name="return-types"></a>반환 형식
**nvarchar(128)**
  
## <a name="permissions"></a>사용 권한  

`DB_NAME`의 호출자가 특정 비**마스터** 또는 비**tempdb** 데이터베이스를 소유하지 않는 경우 최소한 `ALTER ANY DATABASE` 또는 `VIEW ANY DATABASE` 서버 수준 사용 권한이 해당 `DB_ID` 행을 확인하는 데 필요합니다. **마스터** 데이터베이스의 경우 `DB_ID`는 최소한 `CREATE DATABASE` 사용 권한이 필요합니다. 호출자가 연결하는 데이터베이스는 항상 **sys.databases**에 나타납니다.
  
> [!IMPORTANT]  
>  기본적으로 public 역할에는 모든 로그인이 데이터베이스 정보를 보도록 허용하는 `VIEW ANY DATABASE` 권한이 있습니다. 로그인이 데이터베이스를 검색하지 않게 하려면 public에서 `VIEW ANY DATABASE` 권한을 `REVOKE`하거나 로그인에 대한 `DENY` 권한을 `VIEW ANY DATABASE`합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-current-database-name"></a>A. 현재 데이터베이스 이름 반환  
이 예에서는 현재 데이터베이스의 이름을 반환합니다.
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. 지정한 데이터베이스 ID의 데이터베이스 이름 반환  
이 예에서는 데이터베이스 ID `3`의 데이터베이스 이름을 반환합니다.
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. 현재 데이터베이스 이름 반환  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. 데이터베이스 ID를 사용하여 데이터베이스의 이름을 반환합니다  
이 예에서는 각 데이터베이스에 대해 데이터베이스 이름과 database_id를 반환합니다.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>참고 항목
[DB_ID&#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

