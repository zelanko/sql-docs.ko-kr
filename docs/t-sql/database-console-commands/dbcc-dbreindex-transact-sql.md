---
title: DBCC DBREINDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC DBREINDEX
- DBREINDEX_TSQL
- DBREINDEX
- DBCC_DBREINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- index rebuilding [SQL Server]
- rebuilding indexes
- dynamic index rebuilding [SQL Server]
- DBCC DBREINDEX statement
ms.assetid: 6e929d09-ccb5-4855-a6af-b616022bc8f6
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 991c16eea9a651270ca299e72cafbc822465a9b3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-dbreindex-transact-sql"></a>DBCC DBREINDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] 지정한 데이터베이스의 테이블에 대해 하나 이상의 인덱스를 다시 작성합니다.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)를 사용합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)까지)
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC DBREINDEX   
(   
    table_name   
    [ , index_name [ , fillfactor ] ]  
)  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>인수  
 *table_name*  
 다시 작성할 지정 인덱스를 포함하는 테이블의 이름입니다. 테이블 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)*에 적용되는 규칙을 따라야 합니다.*  
  
 *index_name*  
 다시 작성할 인덱스의 이름입니다. 인덱스 이름은 식별자에 대한 규칙을 따라야 합니다. *index_name*을 지정한 경우 *table_name*을 지정해야 합니다. *index_name*을 지정하지 않거나 해당 이름이 " "이면 테이블의 모든 인덱스가 다시 작성됩니다.  
  
 *fillfactor*  
 인덱스를 만들거나 다시 작성할 때 데이터를 저장하는 데 사용할 각 인덱스 페이지의 공간에 대한 백분율입니다. *fillfactor*는 인덱스 생성 시 채우기 비율을 대체하여 클러스터형 인덱스를 다시 작성하기 때문에 다시 작성되는 인덱스 및 다른 모든 비클러스터형 인덱스의 새 기본값이 됩니다.  
 *fillfactor*가 0인 경우 DBCC DBREINDEX는 인덱스에 최근 지정한 채우기 비율 값을 사용합니다. 이 값은 **sys.indexes** 카탈로그 뷰에 저장됩니다.   
 *fillfactor*를 지정한 경우 *table_name* 및 *index_name*을 지정해야 합니다. *fillfactor*를 지정하지 않으면 기본 채우기 비율인 100이 사용됩니다. 자세한 내용은 [인덱스의 채우기 비율 지정](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)을 참조하세요.  
  
 WITH NO_INFOMSGS  
 심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>Remarks  
DBCC DBREINDEX는 테이블의 특정 인덱스나 테이블에 정의된 모든 인덱스를 다시 작성합니다. DBCC DBREINDEX는 인덱스를 동적으로 다시 작성할 수 있도록 하므로 PRIMARY KEY나 UNIQUE 제약 조건을 보장하는 인덱스를 다시 작성할 때 기존 제약 조건을 삭제하고 다시 만들 필요가 없습니다. 이는 테이블의 구조나 해당 제약 조건에 대한 정보가 없이도 인덱스를 다시 작성할 수 있음을 의미합니다. 이 과정은 테이블로 데이터를 대량 복사한 후 발생할 수 있습니다.

DBCC DBREINDEX를 사용하면 하나의 문으로 한 테이블에 대한 모든 인덱스를 다시 작성할 수 있으며 이는 DROP INDEX 및 CREATE INDEX 문을 여러 번 코딩하는 것보다 쉽습니다. 각 DROP INDEX와 CREATE INDEX 문이 원자성을 가지려면 트랜잭션을 사용해야 하는 반면 DBCC DBREINDEX는 하나의 문에서 작업이 수행되므로 자동으로 원자성을 갖습니다. 또한 DBCC DBREINDEX는 개별 DROP INDEX 및 CREATE INDEX 문보다 더 많은 최적화를 제공합니다.

DBCC INDEXDEFRAG 또는 REORGANIZE 옵션을 가진 ALTER INDEX와는 달리 DBCC DBREINDEX는 오프라인 작업입니다. 비클러스터형 인덱스를 다시 작성하는 경우 작업 중에 해당 테이블에 공유 잠금이 유지됩니다. 이렇게 하면 테이블을 수정할 수 없습니다. 클러스터형 인덱스를 다시 작성하는 경우 배타적 테이블 잠금이 설정됩니다. 이 작업은 테이블에 액세스할 수 없게 하므로 결과적으로 테이블을 오프라인 상태로 만듭니다. 온라인 상태로 인덱스를 다시 작성하거나 인덱스 다시 작성 작업 중에 병렬 처리 수준을 제어하려면 ALTER INDEX REBUILD 문에 ONLINE 옵션을 사용합니다.

인덱스를 다시 작성하거나 다시 구성하는 방법을 선택하는 데 대한 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하십시오.
  
## <a name="restrictions"></a>Restrictions  
DBCC DBREINDEX는 다음 개체에 대해 사용할 수 없습니다.
-   시스템 테이블  
-   공간 인덱스  
-   xVelocity 메모리 최적화 columnstore 인덱스  
  
## <a name="result-sets"></a>결과 집합  
NO_INFOMSGS가 지정되지 않은 한(테이블 이름이 지정되어야 함) DBCC DBREINDEX는 항상 다음을 반환합니다.
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>사용 권한  
호출자는 테이블을 소유하거나, **sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버여야 합니다.
  
## <a name="examples"></a>예  
### <a name="a-rebuilding-an-index"></a>1. 인덱스 다시 작성  
다음 예에서는 `Employee_EmployeeID` 데이터베이스의 `80` 테이블에 채우기 비율 `Employee`의 `AdventureWorks` 클러스터형 인덱스를 다시 작성하는 방법을 보여 줍니다.
  
```sql  
USE AdventureWorks2012;   
GO  
DBCC DBREINDEX ('HumanResources.Employee', PK_Employee_BusinessEntityID,80);  
GO  
```  
  
### <a name="b-rebuilding-all-indexes"></a>2. 모든 인덱스 다시 작성  
다음 예에서는 채우기 비율 값 `Employee`을 사용하여 `AdventureWorks`의 `70` 테이블에서 모든 인덱스를 다시 작성하는 방법을 보여 줍니다.
  
```sql
USE AdventureWorks2012;   
GO  
DBCC DBREINDEX ('HumanResources.Employee', ' ', 70);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  

