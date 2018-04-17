---
title: sp_tables (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_tables
- sp_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables
ms.assetid: 787a2fa5-87a1-49bd-938b-6043c245f46b
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e4a32e77f966630af880795eb3020335078cd7e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sptables-transact-sql"></a>sp_tables(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 환경에서 쿼리할 수 있는 개체의 목록을 반환합니다. 즉, 동의어 개체를 제외한 테이블 또는 보기입니다.  
  
> [!NOTE]  
>  동의어 기준 개체의 이름을 확인 하려면 쿼리는 [sys.synonyms](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_tables [ [ @table_name = ] 'name' ]   
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @table_type = ] "type" ]   
     [ , [@fUsePattern = ] 'fUsePattern'];  
```  
  
## <a name="arguments"></a>인수  
 [ **@table_name=** ] **'***name***'**  
 카탈로그 정보를 반환하는 데 사용되는 테이블입니다. *이름* 은 **nvarchar(384)**, 기본값은 NULL입니다. 와일드카드 패턴 일치가 지원됩니다.  
  
 [  **@table_owner=** ] **'***소유자***'**  
 카탈로그 정보를 반환하는 데 사용하는 테이블의 소유자입니다. *소유자* 은 **nvarchar(384)**, 기본값은 NULL입니다. 와일드카드 패턴 일치가 지원됩니다. 소유자를 지정하지 않은 경우 기본 DBMS의 기본 테이블 표시 유형 규칙이 적용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 사용자가 지정된 이름의 테이블을 소유한 경우 해당 테이블의 열이 반환됩니다. 소유자를 지정하지 않았으며 현재 사용자가 지정된 이름의 테이블을 소유하고 있지 않은 경우 이 프로시저는 데이터베이스 소유자가 소유한 지정된 이름의 테이블을 찾습니다. 테이블이 있을 경우 해당 테이블의 열이 반환됩니다.  
  
 [  **@table_qualifier=** ] **'***한정자***'**  
 테이블 한정자의 이름입니다. *한정자* 은 **sysname**, 기본값은 NULL입니다. 다양 한 DBMS 제품에서는 테이블에 대 한 세 부분으로 구성 된 이름 (*한정자***.*** 소유자***.*** 이름*). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
 [ **,** [  **@table_type=** ] **"'***형식***'**, **'**형식**'"** ]  
 쉼표로 구분된 값 목록으로서 지정된 테이블 유형의 모든 테이블에 대한 정보를 제공합니다. 여기에 **테이블**, **SYSTEMTABLE**, 및 **보기**합니다. *형식* 은 **varchar(100)**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  각 테이블 유형은 작은따옴표로 묶고, 전체 매개 변수는 큰따옴표로 묶어야 합니다. 테이블 유형은 대문자로 표시해야 합니다. SET QUOTED_IDENTIFIER가 ON이면 모든 작은따옴표는 큰따옴표로 바꾸고 전체 매개 변수는 작은따옴표로 묶어야 합니다.  
  
 [  **@fUsePattern =** ] **'***fUsePattern***'**  
 밑줄(_), 백분율(%) 및 대괄호([ 또는 ]) 문자를 와일드카드 문자로 해석할지 여부를 결정합니다. 유효한 값은 0(패턴 일치 해제)과 1(패턴 일치 설정)입니다. *fUsePattern* 은 **비트**, 기본값은 1입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|테이블 한정자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 데이터베이스 이름을 나타냅니다. 이 필드는 NULL이 될 수 있습니다.|  
|**TABLE_OWNER**|**sysname**|테이블 소유자 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 열은 테이블을 만든 데이터베이스 사용자의 이름을 나타냅니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다. 이 필드는 항상 값을 반환합니다.|  
|**TABLE_TYPE**|**varchar (32)**|테이블, 시스템 테이블 또는 뷰입니다.|  
|**설명**|**varchar(254)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 열의 값을 반환하지 않습니다.|  
  
## <a name="remarks"></a>주의  
 상호 운용성을 최대한 높이려면 게이트웨이 클라이언트가 SQL-92-표준 SQL 패턴 일치(% 및 _ 와일드카드 문자)만 허용해야 합니다.  
  
 현재 사용자의 특정 테이블에 대한 읽기 또는 쓰기 액세스에 대한 권한 정보는 항상 확인되지는 않습니다. 그렇기 때문에 액세스는 보장되지 않습니다. 이 결과 집합은 테이블 및 뷰뿐만 아니라 이러한 유형을 지원하는 DBMS 제품으로의 게이트웨이에 대한 동의어 및 별칭을 포함합니다. 경우는 서버 특성 **ACCESSIBLE_TABLES** 결과 대 한 집합에 Y **sp_server_info**, 현재 사용자가 액세스할 수 있는 테이블에만 반환 됩니다.  
  
 **sp_tables** 같습니다 **SQLTables** ODBC의 합니다. 반환 결과으로 정렬 **TABLE_TYPE**, **TABLE_QUALIFIER**, **TABLE_OWNER**, 및 **TABLE_NAME**합니다.  
  
## <a name="permissions"></a>Permissions  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>1. 현재 환경에서 쿼리할 수 있는 개체 목록 반환  
 다음 예에서는 현재 환경에서 쿼리할 수 있는 개체 목록을 반환합니다.  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="b-returning-information-about-the-tables-in-a-specified-schema"></a>2. 지정한 스키마의 테이블에 대한 정보 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Person` 스키마에 속한 테이블에 대한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_tables   
   @table_name = '%',  
   @table_owner = 'Person',  
   @table_qualifier = 'AdventureWorks2012';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>3. 현재 환경에서 쿼리할 수 있는 개체 목록 반환  
 다음 예에서는 현재 환경에서 쿼리할 수 있는 개체 목록을 반환합니다.  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="d-returning-information-about-the-tables-in-a-specified-schema"></a>4. 지정한 스키마의 테이블에 대한 정보 반환  
 차원 테이블에 대 한 정보를 반환 하는 다음 예제는 `AdventureWorksPDW201` 데이터베이스입니다.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_tables   
   @table_name = 'Dim%',  
   @table_owner = 'dbo',  
   @table_qualifier = 'AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.synonyms &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

