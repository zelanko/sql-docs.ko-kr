---
description: sp_special_columns(Transact-SQL)
title: sp_special_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_special_columns_TSQL
- sp_special_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_special_columns
ms.assetid: 0b0993f8-73e0-402b-8c6c-1b0963956f5d
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2f734caf4a42e8565c95badf4e4ff98ee1e8b50c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541538"
---
# <a name="sp_special_columns-transact-sql"></a>sp_special_columns(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  테이블의 행을 고유하게 식별하는 열의 최적 집합을 반환합니다. 또한 트랜잭션에 의해 행의 값이 업데이트될 때 자동으로 업데이트되는 열을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_special_columns [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 [ @table_name =] '*table_name*'  
 카탈로그 정보를 반환하는 데 사용되는 테이블의 이름입니다. *name* 은 **sysname**이며 기본값은 없습니다. 와일드카드 패턴 일치는 지원되지 않습니다.  
  
 [ @table_owner =] '*table_owner*'  
 카탈로그 정보를 반환하는 데 사용하는 테이블의 소유자입니다. *owner* 는 **sysname**이며 기본값은 NULL입니다. 와일드카드 패턴 일치는 지원되지 않습니다. *Owner* 를 지정 하지 않은 경우 기본 DBMS의 기본 테이블 표시 규칙이 적용 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 사용자가 지정된 이름의 테이블을 소유한 경우 해당 테이블의 열이 반환됩니다. *Owner* 를 지정 하지 않은 경우 현재 사용자가 지정 된 *이름의*테이블을 소유 하 고 있지 않은 경우이 프로시저는 데이터베이스 소유자가 소유한 지정 된 *이름의* 테이블을 찾습니다. 테이블이 있으면 해당 열이 반환됩니다.  
  
 [ @qualifier =] '*한정자*'  
 테이블 한정자의 이름입니다. *한정자* 는 **sysname**이며 기본값은 NULL입니다. 다양 한 DBMS 제품에서 테이블 (*qualifier.owner.name*)에 대 한 세 부분으로 구성 되는 이름을 지원 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
 [ @col_type =] '*col_type*'  
 열 유형입니다. *col_type* 은 **char (** 1 **)** 이 고 기본값은 r입니다. r 유형은 열에서 값을 검색 하 여 지정 된 테이블의 모든 행을 고유 하 게 식별할 수 있는 최적의 열 또는 열 집합을 반환 합니다. 열은 이 목적을 위해 특별히 구성된 의사 열 또는 테이블의 고유한 인덱스 열이 될 수 있습니다. V 유형은 지정된 테이블에 열이 있는 경우 해당 열을 반환합니다. 이 열은 트랜잭션에 의해 행의 값이 업데이트될 때 데이터 원본에 의해 자동으로 업데이트됩니다.  
  
 [ @scope =] '*범위*'  
 ROWID에 필요한 최소 범위입니다. *범위* 는 **char (** 1 **)** 이며 기본값은 T입니다. C 범위는 ROWID가 해당 행에 있을 때만 유효 하도록 지정 합니다. T 범위는 전체 트랜잭션에 대해 ROWID가 유효하도록 지정합니다.  
  
 [ @nullable =] '*nullable*'  
 특수 열이 Null 값을 허용할 수 있는지 여부입니다. *nullable* 은 **char (** 1 **)** 이며 기본값은 U입니다. O는 null 값을 허용 하지 않는 특수 열을 지정 합니다. U는 부분적으로 Null을 허용하는 열을 지정합니다.  
  
 [ @ODBCVer =] '*ODBCVer*'  
 사용하고 있는 ODBC 버전입니다. *ODBCVer* 은 **int (** 4 **)** 이며 기본값은 2입니다. 이 값은 ODBC 버전 2를 나타냅니다. ODBC 버전 2.0과 ODBC 버전 3.0의 차이에 대한 자세한 내용은 ODBC 버전 3.0에 관한 ODBC SQLSpecialColumns 사양을 참조하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|SCOPE|**smallint**|행 ID의 실제 범위로 0, 1 또는 2가 될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 항상 0을 반환 합니다. 이 필드는 항상 값을 반환합니다.<br /><br /> 0 = SQL_SCOPE_CURROW. 행 ID는 해당 행에 있는 동안에만 유효하도록 보장됩니다. 행 ID를 사용하여 나중에 다시 선택하는 경우 행이 업데이트되거나 다른 트랜잭션에 의해 삭제되면 그 행을 반환하지 않을 수도 있습니다.<br /><br /> 1 = SQL_SCOPE_TRANSACTION. 행 ID는 현재 트랜잭션 기간 동안 유효하도록 보장됩니다.<br /><br /> 2 = SQL_SCOPE_SESSION. 행 ID는 트랜잭션 경계와 상관없이 세션 기간 동안 유효하도록 보장됩니다.|  
|COLUMN_NAME|**sysname**|반환 된 *테이블*의 각 열에 대 한 열 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|DATA_TYPE|**smallint**|ODBC SQL 데이터 형식입니다.|  
|TYPE_NAME|**sysname**|데이터 원본 종속 데이터 형식 이름입니다. 예를 들어 **char**, **varchar**, **money**또는 **text**입니다.|  
|PRECISION|**정수**|데이터 원본의 행 전체 자릿수입니다. 이 필드는 항상 값을 반환합니다.|  
|LENGTH|**정수**|데이터 원본에서 이진 형식의 데이터 형식에 필요한 길이 (바이트)입니다 (예: **char (** 10)의 경우 10, **정수**의 경우 4, **smallint**의 경우 2 **)**.|  
|SCALE|**smallint**|데이터 원본의 소수 자릿수입니다. 소수 자릿수가 적용되지 않는 데이터 형식에 대해서는 NULL이 반환됩니다.|  
|PSEUDO_COLUMN|**smallint**|열이 의사(pseudo) 열인지 여부를 나타냅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 항상 1을 반환합니다.<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>설명  
 sp_special_columns는 ODBC의 SQLSpecialColumns와 동일합니다. 반환되는 값은 SCOPE에 의해 순서가 정해집니다.  
  
## <a name="permissions"></a>사용 권한  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `HumanResources.Department` 테이블의 행을 고유하게 식별하는 열에 대한 정보를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_special_columns @table_name = 'Department'   
    ,@table_owner = 'HumanResources';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;카탈로그 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
