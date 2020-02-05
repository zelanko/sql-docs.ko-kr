---
title: DBCC UPDATEUSAGE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATEUSAGE
- UPDATEUSAGE_TSQL
- DBCC_UPDATEUSAGE_TSQL
- DBCC UPDATEUSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- inaccurate page or row counts [SQL Server]
- space [SQL Server], usage reports
- updating space usage information
- updating row counts
- disk space [SQL Server], inaccurate counts
- counting pages
- reporting count inaccuracies
- updating page counts
- synchronization [SQL Server], inaccurate counts
- incorrect space usage reports [SQL Server]
- DBCC UPDATEUSAGE statement
- integrity [SQL Server], database objects
- counting rows
- row count accuracy [SQL Server]
- page count accuracy [SQL Server]
ms.assetid: b8752ecc-db45-4e23-aee7-13b8bc3cbae2
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7d983f2e7e370ec9fe385e6d46602c4703ca6d1e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68040457"
---
# <a name="dbcc-updateusage-transact-sql"></a>DBCC UPDATEUSAGE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

카탈로그 뷰의 부정확한 페이지와 행 개수를 보고하고 수정합니다. 이러한 부정확성으로 인해 sp_spaceused 시스템 저장 프로시저에서 정확하지 않은 공간 사용 보고서를 반환할 수 있습니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC UPDATEUSAGE   
(   { database_name | database_id | 0 }   
    [ , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } ] ]   
) [ WITH [ NO_INFOMSGS ] [ , ] [ COUNT_ROWS ] ]   
```  
  
## <a name="arguments"></a>인수  
*database_name* | *database_id* | 0  
공간 사용량 통계를 보고하고 수정할 데이터베이스의 이름 또는 ID입니다. 0을 지정하면 현재 데이터베이스가 사용됩니다. 데이터베이스 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 준수해야 합니다.  
  
*table_name* | *table_id* | *view_name* | *view_id*  
공간 사용 통계를 보고하고 수정할 테이블이나 인덱싱된 뷰의 이름 또는 ID입니다. 테이블 및 뷰 이름은 식별자 규칙을 따라야 합니다.  
  
*index_id* | *index_name*  
사용할 인덱스의 ID 또는 이름입니다. 이 인수를 지정하지 않으면 해당 문에서 지정한 테이블이나 뷰의 모든 인덱스를 처리합니다.  
  
WITH  
옵션을 지정할 수 있습니다.  
  
NO_INFOMSGS  
모든 정보 메시지를 표시하지 않습니다.  
  
COUNT_ROWS  
row count 열이 테이블이나 뷰에 있는 현재 행 개수로 업데이트되도록 지정합니다.  
  
## <a name="remarks"></a>설명  
DBCC UPDATEUSAGE는 테이블 또는 인덱스의 각 파티션에 대해 행, 사용된 페이지, 예약된 페이지, 리프 페이지 및 데이터 페이지의 개수를 수정합니다. 시스템 테이블에 부정확한 데이터가 없으면 DBCC UPDATEUSAGE는 데이터를 반환하지 않습니다. 부정확한 데이터를 검색 및 수정하고 WITH NO_INFOMSGS를 사용하지 않았으면 DBCC UPDATEUSAGE는 시스템 테이블에서 업데이트 중인 행과 열을 반환합니다.
  
페이지 또는 행 개수가 음수일 경우 이를 감지할 수 있도록 DBCC CHECKDB가 개선되었습니다. 감지가 되면 DBCC CHECKDB 출력에 경고와 함께 DBCC UPDATEUSAGE를 실행해 문제를 해결하라는 권장 메시지가 포함됩니다.
  
## <a name="best-practices"></a>모범 사례  
다음 방법을 사용하는 것이 좋습니다.
-   DBCC UPDATEUSAGE를 정기적으로 실행하지 마십시오. DBCC UPDATEUSAGE는 대형 테이블 또는 데이터베이스에 대해 실행하는 경우 시간이 오래 걸릴 수 있으므로 sp_spaceused에서 반환되는 값이 잘못되었다고 판단되는 경우를 제외하고는 사용하지 않아야 합니다.
-   데이터베이스에서 CREATE, ALTER 또는 DROP 문과 같은 DDL(데이터 정의 언어) 수정이 자주 발생하는 경우에만 DBCC UPDATEUSAGE를 정기적으로(예: 매주) 실행하십시오.  
  
## <a name="result-sets"></a>결과 집합  
DBCC UPDATEUSAGE는 다음을 반환합니다(값은 상황에 따라 다름).
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>사용 권한  
**sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-updating-page-or-row-counts-or-both-for-all-objects-in-the-current-database"></a>A. 현재 데이터베이스의 모든 개체에 대한 페이지나 행 개수 또는 두 가지 모두 업데이트  
다음 예에서는 데이터베이스 이름에 `0`을 지정하고 `DBCC UPDATEUSAGE`는 현재 데이터베이스에 대해 업데이트된 페이지 및 행 수 정보를 보고합니다.
  
```sql
DBCC UPDATEUSAGE (0);  
GO  
```  
  
### <a name="b-updating-page-or-row-counts-or-both-for-adventureworks-and-suppressing-informational-messages"></a>B. AdventureWorks에 대한 페이지나 행 개수 또는 두 가지를 모두 업데이트하고 정보 메시지를 표시 안 함  
다음 예에서는 데이터베이스 이름으로 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 지정하고 모든 정보 메시지를 표시하지 않습니다.
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012) WITH NO_INFOMSGS;   
GO  
```  
  
### <a name="c-updating-page-or-row-counts-or-both-for-the-employee-table"></a>C. Employee 테이블의 페이지나 행 개수 또는 두 가지를 모두 업데이트  
다음 예제에서는 `Employee` 데이터베이스의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 테이블에 대해 업데이트된 페이지 또는 행 수 정보를 보고합니다.
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012,'HumanResources.Employee');  
GO  
```  
  
### <a name="d-updating-page-or-row-counts-or-both-for-a-specific-index-in-a-table"></a>D. 테이블에 있는 특정 인덱스에 대한 페이지나 행 개수 또는 두 가지를 모두 업데이트  
 다음 예에서는 인덱스 이름으로 `IX_Employee_ManagerID`를 지정합니다.  
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012, 'HumanResources.Employee', IX_Employee_OrganizationLevel_OrganizationNode);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
[UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
  
  
