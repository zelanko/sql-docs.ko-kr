---
title: "테이블 잘라내기 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRUNCATE
- TRUNCATE TABLE
- TRUNCATE_TSQL
- TRUNCATE_TABLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row removal [SQL Server], TRUNCATE TABLE statement
- table truncating [SQL Server]
- removing rows
- TRUNCATE TABLE statement
- deleting rows
- dropping rows
ms.assetid: 3d544eed-3993-4055-983d-ea334f8c5c58
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 1d393c67c8489765aa92c861bc28c8e4d0e2eea4
ms.contentlocale: ko-kr
ms.lasthandoff: 10/04/2017

---
# <a name="truncate-table-transact-sql"></a>TRUNCATE TABLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  개별 행 삭제를 기록 하지 않고 테이블 또는 테이블의 지정 된 파티션이에서 모든 행을 제거 합니다. TRUNCATE TABLE은 기능상으로 WHERE 절이 없는 DELETE 문과 동일하지만 더 빠르고 시스템 및 트랜잭션 로그 리소스를 덜 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  
  
TRUNCATE TABLE   
    [ { database_name .[ schema_name ] . | schema_name . } ]  
    table_name  
    [ WITH ( PARTITIONS ( { <partition_number_expression> | <range> }   
    [ , ...n ] ) ) ]  
[ ; ]  
  
<range> ::=  
<partition_number_expression> TO <partition_number_expression>  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
TRUNCATE TABLE [ { database_name . [ schema_name ] . | schema_name . ] table_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이 속한 스키마의 이름입니다.  
  
 *table_name*  
 잘라내거나 모든 행을 제거할 테이블의 이름입니다. *table_name* 은 리터럴이어야 합니다. *table_name* 일 수 없습니다는 **OBJECT_ID** 함수 또는 변수입니다.  
  
 와 (파티션 ({ \< *partition_number_expression*> | \< *범위*>} [,...n]))  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 자를 파티션이나 모든 행이 제거되는 파티션을 지정합니다. 테이블이 분할 되지 않은 경우는 **와 파티션** 인수에는 오류가 생성 됩니다. 경우는 **와 파티션** 절을 제공 하지 않으면, 전체 테이블이 잘립니다.  
  
 *\<partition_number_expression >* 다음과 같은 방법으로 지정할 수 있습니다. 
  
-   예를 들어의 파티션 번호를 제공 합니다.`WITH (PARTITIONS (2))`  
  
-   예를 들어 쉼표로 구분 된 여러 개별 파티션의 파티션 번호를 제공 합니다.`WITH (PARTITIONS (1, 5))`  
  
-   예를 들어 범위와 개별 파티션을 모두를 제공 합니다.`WITH (PARTITIONS (2, 4, 6 TO 8))`  
  
-   *\<범위 >* 로 구분 된 파티션 번호로 지정할 수 있습니다 **TO**, 예:`WITH (PARTITIONS (6 TO 8))`  
  
 분할된 된 테이블을 자를 테이블과 인덱스가 정렬 되어야 합니다 (동일한 파티션 함수에 분할).  
  
## <a name="remarks"></a>주의  
 DELETE 문과 비교하여 TRUNCATE TABLE에는 다음과 같은 이점이 있습니다.  
  
-   트랜잭션 로그 공간을 덜 사용합니다.  
  
     DELETE 문은 행을 한번에 하나씩 제거하고 삭제된 각 행에 대해 트랜잭션 로그에 항목을 기록합니다. 반면 TRUNCATE TABLE은 테이블의 데이터를 저장하는 데 사용되는 데이터 페이지의 할당을 취소하는 방식으로 데이터를 제거하며 페이지 할당 취소만을 트랜잭션 로그에 기록합니다.  
  
-   일반적으로 적은 수의 잠금이 사용됩니다.  
  
     행 잠금을 사용하여 DELETE 문을 실행하면 삭제를 위해 테이블의 각 행이 잠깁니다. TRUNCATE TABLE은 항상 테이블(스키마(SCH-M) 잠금 포함)과 페이지를 잠그지만 각 행은 잠그지 않습니다.  
  
-   빈 페이지는 예외 없이 테이블에 남습니다.  
  
     DELETE 문이 실행된 후에도 테이블은 계속 빈 페이지를 포함할 수 있습니다. 예를 들어, 힙의 빈 페이지는 최소한 배타적인(LCK_M_X) 테이블 잠금이 있어야만 할당 취소할 수 있으므로 삭제를 위해 테이블 잠금을 사용하지 않는 경우 테이블(힙)에는 빈 페이지가 많이 남게 됩니다. 인덱스의 경우도 삭제 작업 후에 빈 페이지가 남을 수 있지만 이러한 페이지는 백그라운드 정리 프로세스에 의해 신속하게 할당 취소됩니다.  
  
 TRUNCATE TABLE은 테이블에서 모든 행을 제거하지만 테이블 구조와 테이블의 열, 제약 조건, 인덱스 등은 그대로 남습니다. 테이블 정의 및 테이블의 데이터를 제거하려면 DROP TABLE 문을 사용하세요.  
  
 테이블에 ID 열이 포함되어 있으면 해당 열의 카운터는 열에 대한 초기값으로 다시 설정됩니다. 초기값이 정의되어 있지 않으면 기본값인 1이 사용됩니다. ID 카운터를 보존하려면 DELETE를 대신 사용하세요.  
  
## <a name="restrictions"></a>제한 사항  
 다음과 같은 테이블에서는 TRUNCATE TABLE 문을 사용할 수 없습니다.  
  
-   FOREIGN KEY 제약 조건에 의해 참조됩니다. 자신을 참조하는 외래 키가 있는 테이블을 잘라낼 수 있습니다.  
  
-   인덱싱된 뷰에 참여합니다.  
  
-   트랜잭션 복제 또는 병합 복제에 의해 게시됩니다.  
  
 이런 특징을 한 개 이상 갖고 있는 테이블의 경우 DELETE 문을 대신 사용하세요.  
  
 TRUNCATE TABLE은 개별 행 삭제를 기록하지 않기 때문에 트리거를 실행할 수 없습니다. 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)를 참조하세요. 
 
 [!INCLUDE[sssdwfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[sspdw](../../includes/sspdw-md.md)]:

- TRUNCATE TABLE 설명 문 내에서 허용 되지 않습니다.

- TRUNCATE TABLE 트랜잭션 내에서 실행 될 수 없습니다.
  
## <a name="truncating-large-tables"></a>대형 테이블 잘라내기  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 삭제 또는 삭제에 필요한 모든 익스텐트에서 동시 잠금이 없는 한 128 익스텐트를 갖고 있는 테이블을 자를 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 필요한 최소 사용 권한은 ALTER 켜져 *table_name*합니다. TRUNCATE TABLE 권한은 테이블 소유자, sysadmin 고정 서버 역할 멤버 및 db_owner 및 db_ddladmin 고정 데이터베이스 역할의 기본 권한이며 위임할 수 없습니다. 하지만 저장 프로시저와 같은 모듈 내에 TRUNCATE TABLE 문을 통합한 뒤 EXECUTE AS 절을 사용하여 적절한 권한을 모듈에 허용할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-truncate-a-table"></a>1. 테이블 자르기  
 다음 예에서는 `JobCandidate` 테이블의 모든 데이터를 제거합니다. `SELECT` 문이 `TRUNCATE TABLE` 문 앞과 뒤에 포함되어 결과를 비교합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT COUNT(*) AS BeforeTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
TRUNCATE TABLE HumanResources.JobCandidate;  
GO  
SELECT COUNT(*) AS AfterTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
```  
  
### <a name="b-truncate-table-partitions"></a>2. 테이블 파티션 자르기  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 다음 예에서는 분할된 테이블의 지정된 파티션을 자릅니다. `WITH (PARTITIONS (2, 4, 6 TO 8))` 구문은 파티션 번호 2, 4, 6, 7, 8이 잘리도록 합니다.  
  
```  
TRUNCATE TABLE PartitionTable1   
WITH (PARTITIONS (2, 4, 6 TO 8));  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP table&#40; Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
  
  


