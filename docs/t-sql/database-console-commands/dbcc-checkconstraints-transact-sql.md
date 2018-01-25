---
title: DBCC CHECKCONSTRAINTS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC CHECKCONSTRAINTS
- DBCC_CHECKCONSTRAINTS_TSQL
- CHECKCONSTRAINTS
- CHECKCONSTRAINTS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- DBCC CHECKCONSTRAINTS statement
- consistency [SQL Server], constraints
- checking constraint consistency
- constraints [SQL Server], consistency checks
- integrity [SQL Server], constraints
ms.assetid: da6c9cee-6687-46e8-b504-738551f9068b
caps.latest.revision: "45"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2ff75ba3c32d138d9124eba5cfe170cf146d5778
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-checkconstraints-transact-sql"></a>DBCC CHECKCONSTRAINTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

현재 데이터베이스의 지정한 테이블에서 특정 제약 조건이나 모든 제약 조건의 무결성을 확인합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC CHECKCONSTRAINTS  
[   
    (   
    table_name | table_id | constraint_name | constraint_id   
    )  
]  
    [ WITH   
    [ { ALL_CONSTRAINTS | ALL_ERRORMSGS } ]  
    [ , ] [ NO_INFOMSGS ]   
    ]  
```  
  
## <a name="arguments"></a>인수  
 *table_name* | *table_id* | *constraint_name* | *constraint_id*  
 검사할 테이블이나 제약 조건입니다. 때 *table_name* 또는 *table_id* 가 지정 하면 해당 테이블에 대해 설정 된 모든 제약 조건을 검사 됩니다. 때 *constraint_name* 또는 *constraint_id* 가 지정 하면 해당 제약 조건만 검사 합니다. 테이블 식별자도 제약 조건 식별자도 지정하지 않으면 현재 데이터베이스의 모든 테이블에 대해 설정된 모든 제약 조건을 검사합니다.  
 제약 조건 이름은 제약 조건이 속해 있는 테이블을 고유하게 식별합니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
 의 모든 멘션을  
 지정할 옵션을 활성화합니다.  
  
 ALL_CONSTRAINTS  
 테이블 이름을 지정하거나 모든 테이블을 검사하는 경우에는 해당 테이블에서 설정 및 해제된 모든 제약 조건을 확인합니다. 그렇지 않은 경우에는 설정된 제약 조건만 확인합니다. 제약 조건 이름이 지정된 경우에는 ALL_CONSTRAINTS가 적용되지 않습니다.  
  
 ALL_ERRORMSGS  
 검사 대상 테이블에서 제약 조건을 위반하는 모든 행을 반환합니다. 기본값은 처음 200개의 행입니다.  
  
 NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>주의  
DBCC CHECKCONSTRAINTS는 테이블의 모든 FOREIGN KEY 제약 조건 및 CHECK 제약 조건에 대한 쿼리를 생성 및 실행합니다.
  
예를 들어 외래 키 쿼리의 형식은 다음과 같습니다.
  
```sql
SELECT <columns>  
FROM <table_being_checked> LEFT JOIN <referenced_table>  
    ON <table_being_checked.fkey1> = <referenced_table.pkey1>   
    AND <table_being_checked.fkey2> = <referenced_table.pkey2>  
WHERE <table_being_checked.fkey1> IS NOT NULL   
    AND <referenced_table.pkey1> IS NULL  
    AND <table_being_checked.fkey2> IS NOT NULL  
    AND <referenced_table.pkey2> IS NULL  
```  
  
쿼리 데이터는 임시 테이블에 저장됩니다. 요청한 모든 테이블이나 제약 조건의 검사가 끝나면 결과 집합이 반환됩니다.
DBCC CHECKCONSTRAINTS는 FOREIGN KEY와 CHECK 제약 조건의 무결성을 검사하지만 테이블의 디스크에서 데이터 구조의 무결성은 검사하지 않습니다. 사용 하 여 이러한 데이터 구조 검사를 수행할 수 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 및 [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)합니다.
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
경우 *table_name* 또는 *table_id* 지정 된 시스템 버전 관리에 사용 하도록 설정 하 고, DBCC CHECKCONSTRAINTS은 또한 지정된 된 테이블에서 임시 데이터 일관성 검사를 수행 합니다. 때 *NO_INFOMSGS* 를 지정 하지 않으면이 명령은 출력에 별도 줄에 각 일관성 위반을 반환 합니다. 출력의 형식이 됩니다. ([pkcol1] [pkcol2]...) = (\<pkcol1_value >, \<pkcol2_value >...) 및 \<무엇이 잘못 된 임시 테이블 레코드 > 합니다.
  
|확인|실패 한 경우 출력에서 추가 정보|  
|-----------|-----------------------------------------------|  
|PeriodEndColumn ≥ PeriodStartColumn (현재)|[sys_end] = '{0}' AND MAX(DATETIME2) = '9999-12-31 23:59:59.99999'|  
|PeriodEndColumn ≥ PeriodStartColumn (현재, 기록)|[sys_start] = '{0}' AND [sys_end] = '{1}'|  
|PeriodStartColumn < current_utc_time (현재)|[sys_start] = ' {'이 (0) 및 SYSUTCTIME|  
|PeriodEndColumn < current_utc_time (기록)|[sys_end] = '{0}' AND SYSUTCTIME|  
|겹치는 항목이 있습니다|(sys_start1, sys_end1), (sys_start2 sys_end2) 두에 대 한 레코드를 중첩 합니다.<br /><br /> 겹치는 레코드 2 개 이상의 출력에 각 겹침 쌍을 보여 주는 여러 행 포함 됩니다.|  
  
제약 조건 이름 또는 constraint_id만 임시 일관성 검사를 실행 하기 위해 지정할 방법이 없습니다.
  
## <a name="result-sets"></a>결과 집합  
DBCC CHECKCONSTRAINTS는 다음 열이 있는 행 집합을 반환합니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|테이블 이름|**varchar**|테이블 이름입니다.|  
|Constraint Name|**varchar**|위반된 제약 조건의 이름입니다.|  
|위치|**varchar**|제약 조건을 위반한 행을 식별하는 열 값 할당입니다.<br /><br /> 이 열의 값은 제약 조건을 위반한 행을 쿼리하는 SELECT 문의 WHERE 절에 사용될 수 있습니다.|  
  
## <a name="permissions"></a>Permissions  
**sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-checking-a-table"></a>1. 테이블 검사  
다음은 `Table1` 데이터베이스에 있는 `AdventureWorks` 테이블의 제약 조건 무결성을 검사하는 예입니다.
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (Col1 int, Col2 char (30));  
GO  
INSERT INTO Table1 VALUES (100, 'Hello');  
GO  
ALTER TABLE Table1 WITH NOCHECK ADD CONSTRAINT chkTab1 CHECK (Col1 > 100);  
GO  
DBCC CHECKCONSTRAINTS(Table1);  
GO  
```  
  
### <a name="b-checking-a-specific-constraint"></a>2. 특정 제약 조건 검사  
다음은 `CK_ProductCostHistory_EndDate` 제약 조건의 무결성을 검사하는 예입니다.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC CHECKCONSTRAINTS ('Production.CK_ProductCostHistory_EndDate');  
GO  
```  
  
### <a name="c-checking-all-enabled-and-disabled-constraints-on-all-tables"></a>3. 모든 테이블에서 설정 및 해제된 모든 제약 조건 검사  
 다음은 현재 데이터베이스의 모든 테이블에 설정 및 해제된 모든 제약 조건의 무결성을 검사하는 예입니다.  
  
```sql  
DBCC CHECKCONSTRAINTS WITH ALL_CONSTRAINTS;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
[DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[DBCC CHECKTABLE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
