---
description: sp_pkeys(Transact-SQL)
title: sp_pkeys (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_pkeys
- sp_pkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_pkeys
ms.assetid: e614c75d-847b-4726-8f6f-cd18de688eda
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a291d4b76a7fe141234a43c458b865a1d956381
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493108"
---
# <a name="sp_pkeys-transact-sql"></a>sp_pkeys(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 환경의 단일 테이블에 대한 기본 키 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_pkeys [ @table_name = ] 'name'       
    [ , [ @table_owner = ] 'owner' ]   
    [ , [ @table_qualifier = ] 'qualifier' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @table_name =] '*name*'  
 정보를 반환할 테이블입니다. *name* 은 **sysname**이며 기본값은 없습니다. 와일드카드 패턴 일치는 지원되지 않습니다.  
  
 [ @table_owner =] '*owner*'  
 지정된 테이블의 소유자를 지정합니다. *owner* 는 **sysname**이며 기본값은 NULL입니다. 와일드카드 패턴 일치는 지원되지 않습니다. *Owner* 를 지정 하지 않은 경우 기본 DBMS의 기본 테이블 표시 규칙이 적용 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 사용자가 지정된 이름의 테이블을 소유한 경우 해당 테이블의 열이 반환됩니다. *Owner* 를 지정 하지 않은 경우 현재 사용자가 지정 된 *이름의*테이블을 소유 하 고 있지 않은 경우이 프로시저는 데이터베이스 소유자가 소유한 지정 된 *이름의* 테이블을 찾습니다. 테이블이 있을 경우 해당 테이블의 열이 반환됩니다.  
  
 [ @table_qualifier =] '*한정자*'  
 테이블 식별자입니다. *한정자* 는 **sysname**이며 기본값은 NULL입니다. 다양 한 DBMS 제품에서 테이블에 대해 세 부분으로 구성 되는 이름 (_한정자_)을 지원**합니다.** _소유자_**.** _이름_). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|테이블 한정자의 이름입니다. 이 필드는 NULL이 될 수 있습니다.|  
|TABLE_OWNER|**sysname**|테이블 소유자의 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|TABLE_NAME|**sysname**|테이블 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 sysobjects 테이블에 나열된 테이블 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|COLUMN_NAME|**sysname**|반환된 TABLE_NAME의 각 열에 대한 열의 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 sys.columns 테이블에 나열된 열 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|KEY_SEQ|**smallint**|기본 키가 여러 열로 구성된 경우 열의 시퀀스 번호입니다.|  
|PK_NAME|**sysname**|기본 키 식별자입니다. 데이터 원본에 적용할 수 없을 경우에는 NULL을 반환합니다.|  
  
## <a name="remarks"></a>설명  
 sp_pkeys는 PRIMARY KEY 제약 조건을 사용하여 명시적으로 정의된 열에 대한 정보를 반환합니다. 모든 시스템이 명시적으로 명명된 기본 키를 지원하지는 않으므로 게이트웨이 구현자가 기본 키의 구성 요소를 결정합니다. 기본 키라는 용어는 테이블의 논리적 기본 키를 의미합니다. 논리적 기본 키로 나열되어 있는 모든 키는 키에 대해 정의된 고유 인덱스를 가집니다. 또한 이 고유 인덱스는 sp_statistics에서 반환됩니다.  
  
 sp_pkeys 저장 프로시저는 ODBC의 SQLPrimaryKeys와 동일합니다. 반환된 결과는 TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME 및 KEY_SEQ 순으로 정렬됩니다.  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `HumanResources.Department` 데이터베이스에 있는 `AdventureWorks2012` 테이블의 기본 키를 검색합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_pkeys @table_name = N'Department'  
    ,@table_owner = N'HumanResources';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `DimAccount` 데이터베이스에 있는 `AdventureWorksPDW2012` 테이블의 기본 키를 검색합니다. 테이블에 기본 키가 없음을 나타내는 0 행을 반환 합니다.  
  
```sql  
-- Uses AdventureWorks  
  
EXEC sp_pkeys @table_name = N'DimAccount';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;카탈로그 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

