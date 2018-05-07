---
title: sp_pkeys (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_pkeys
- sp_pkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_pkeys
ms.assetid: e614c75d-847b-4726-8f6f-cd18de688eda
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d5321f34ae72051bc84a83dca70f12f772f22fc9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sppkeys-transact-sql"></a>sp_pkeys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 환경의 단일 테이블에 대한 기본 키 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_pkeys [ @table_name = ] 'name'       
    [ , [ @table_owner = ] 'owner' ]   
    [ , [ @table_qualifier = ] 'qualifier' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @table_name=] '*이름*'  
 정보를 반환 될 테이블이입니다. *이름* 은 **sysname**, 기본값은 없습니다. 와일드카드 패턴 일치는 지원되지 않습니다.  
  
 [ @table_owner=] '*소유자*'  
 지정된 테이블의 소유자를 지정합니다. *소유자* 은 **sysname**, 기본값은 NULL입니다. 와일드카드 패턴 일치는 지원되지 않습니다. 경우 *소유자* 을 지정 하지 않으면 기본 DBMS의 기본 테이블 표시 규칙이 적용 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 사용자가 지정된 이름의 테이블을 소유한 경우 해당 테이블의 열이 반환됩니다. 경우는 *소유자* 지정 하지 않으면 현재 사용자가 지정 된 테이블을 소유 하지 *이름*,이 프로시저는 지정 된 테이블에 대 한 찾습니다 *이름* 소유한는 데이터베이스 소유자입니다. 테이블이 있을 경우 해당 테이블의 열이 반환됩니다.  
  
 [ @table_qualifier=] '*한정자*'  
 테이블 식별자입니다. *한정자* 은 **sysname**, 기본값은 NULL입니다. 다양 한 DBMS 제품에서는 테이블에 대 한 세 부분으로 구성 된 이름 (*한정자 ***.*** 소유자 ***.*** 이름*). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|테이블 한정자의 이름입니다. 이 필드는 NULL이 될 수 있습니다.|  
|TABLE_OWNER|**sysname**|테이블 소유자의 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|TABLE_NAME|**sysname**|테이블 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 sysobjects 테이블에 나열된 테이블 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|COLUMN_NAME|**sysname**|반환된 TABLE_NAME의 각 열에 대한 열의 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 sys.columns 테이블에 나열된 열 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|KEY_SEQ|**smallint**|기본 키가 여러 열로 구성된 경우 열의 시퀀스 번호입니다.|  
|PK_NAME|**sysname**|기본 키 식별자입니다. 데이터 원본에 적용할 수 없을 경우에는 NULL을 반환합니다.|  
  
## <a name="remarks"></a>주의  
 sp_pkeys는 PRIMARY KEY 제약 조건을 사용하여 명시적으로 정의된 열에 대한 정보를 반환합니다. 모든 시스템이 명시적으로 명명된 기본 키를 지원하지는 않으므로 게이트웨이 구현자가 기본 키의 구성 요소를 결정합니다. 기본 키라는 용어는 테이블의 논리적 기본 키를 의미합니다. 논리적 기본 키로 나열되어 있는 모든 키는 키에 대해 정의된 고유 인덱스를 가집니다. 또한 이 고유 인덱스는 sp_statistics에서 반환됩니다.  
  
 Sp_pkeys 저장 프로시저는 ODBC의 SQLPrimaryKeys과 같습니다. 반환된 결과는 TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME 및 KEY_SEQ 순으로 정렬됩니다.  
  
## <a name="permissions"></a>Permissions  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `HumanResources.Department` 데이터베이스에 있는 `AdventureWorks2012` 테이블의 기본 키를 검색합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_pkeys @table_name = N'Department'  
    ,@table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `DimAccount` 데이터베이스에 있는 `AdventureWorksPDW2012` 테이블의 기본 키를 검색합니다. 테이블에 기본 키 없는지를 나타내는 0 개의 행을 반환 합니다.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_pkeys @table_name = N'DimAccount;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 저장된 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

