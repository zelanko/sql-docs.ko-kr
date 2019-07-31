---
title: 테이블 힌트(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TABLE_HINT_TSQL
- Table Hint
dev_langs:
- TSQL
helpviewer_keywords:
- SERIALIZABLE table hint
- UPDLOCK table hint
- HOLDLOCK table hint
- TABLOCKX table hint
- READUNCOMMITTED table hint
- hints [SQL Server], tables
- READCOMMITTEDLOCK table hint
- FORCESCAN table hint
- ROWLOCK table hint
- XLOCK table hint
- NOLOCK table hint
- READPAST table hint
- NOWAIT table hint
- FORCESEEK table hint
- table hints [SQL Server]
- TABLOCK table hint
- REPEATABLEREAD table hint
- READ COMMITTED table hint
- NOEXPAND table hint
- PAGLOCK table hint
ms.assetid: 8bf1316f-c0ef-49d0-90a7-3946bc8e7a89
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9c09ce1ef34e7355651be0aab473ca39bd2dae1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901969"
---
# <a name="hints-transact-sql---table"></a>힌트(Transact-SQL) - 테이블
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  테이블 힌트는 잠금 메서드, 하나 이상의 인덱스, Table Scan 또는 Index Seek와 같은 쿼리 처리 연산이나 기타 옵션을 지정하여 DML(데이터 조작 언어) 문이 실행되는 동안 쿼리 최적화 프로그램의 기본 동작을 무시합니다. 테이블 힌트는 DML 문의 FROM 절에서 지정하며 해당 절에서 참조되는 테이블이나 뷰에만 영향을 줍니다.  
  
> [!CAUTION]  
>  일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 쿼리에 대해 최상의 실행 계획을 선택하므로 숙련된 개발자 및 데이터베이스 관리자가 마지막 방법으로만 힌트를 사용하는 것이 좋습니다.  
  
 **적용 대상:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
WITH  ( <table_hint> [ [, ]...n ] )  
  
<table_hint> ::=   
[ NOEXPAND ] {   
    INDEX  ( index_value [ ,...n ] )   
  | INDEX =  ( index_value )      
  | FORCESEEK [( index_value ( index_column_name  [ ,... ] ) ) ]  
  | FORCESCAN  
  | FORCESEEK  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT   
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK   
}   
  
<table_hint_limited> ::=  
{  
    KEEPIDENTITY   
  | KEEPDEFAULTS   
  | HOLDLOCK   
  | IGNORE_CONSTRAINTS   
  | IGNORE_TRIGGERS   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT   
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK   
}   
```  
  
## <a name="arguments"></a>인수  
WITH **(** \<table_hint> **)** [ [ **,** ]...*n* ]  
몇 가지 예외가 있지만 테이블 힌트는 WITH 키워드를 사용하여 힌트를 지정할 때만 FROM 절에서 지원됩니다. 또한 테이블 힌트는 괄호로 묶어 지정해야 합니다.  
  
> [!IMPORTANT]  
> WITH 키워드 생략은 더 이상 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
NOLOCK, READUNCOMMITTED, UPDLOCK, REPEATABLEREAD, SERIALIZABLE, READCOMMITTED, TABLOCK, TABLOCKX, PAGLOCK, ROWLOCK, NOWAIT, READPAST, XLOCK, SNAPSHOT 및 NOEXPAND 테이블 힌트를 WITH 키워드와 함께 또는 WITH 키워드 없이 사용할 수 있습니다. 이러한 테이블 힌트를 WITH 키워드 없이 지정하는 경우 힌트를 단독으로 지정해야 합니다. 예를 들어  
  
```sql  
FROM t (TABLOCK)  
```  
  
힌트를 다른 옵션과 함께 지정하는 경우 다음과 같이 힌트를 WITH 키워드로 지정해야 합니다.  
  
```sql  
FROM t WITH (TABLOCK, INDEX(myindex))  
```  
  
테이블 힌트 사이에는 쉼표를 사용하는 것이 좋습니다.  
  
> [!IMPORTANT]  
>  힌트를 구분할 때 쉼표 대신 공백은 더 이상 사용할 수 없습니다. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
NOEXPAND  
쿼리 최적화 프로그램에서 쿼리를 처리할 때 기본 테이블에 액세스하기 위해 인덱싱된 뷰를 확장하지 않도록 지정합니다. 쿼리 최적화 프로그램은 뷰를 클러스터형 인덱스가 있는 테이블처럼 처리합니다. NOEXPAND는 인덱싱된 뷰에만 적용됩니다. 자세한 내용은 [NOEXPAND 사용](#using-noexpand)을 참조하세요.  
  
INDEX  **(** _index\_value_ [ **,** ... _n_ ] ) | INDEX =  ( _index\_value_ **)**  
INDEX() 구문은 쿼리 최적화 프로그램이 문을 처리할 때 사용할 인덱스 하나 이상의 이름이나 ID를 지정합니다. 대체 INDEX = 구문은 단일 인덱스 값을 지정하며 테이블당 하나의 인덱스 힌트만 지정할 수 있습니다.  
  
클러스터형 인덱스가 있는 경우에는 INDEX(0)이 클러스터형 인덱스 검색을 강제 실행하고 INDEX(1)이 클러스터형 인덱스 검색 또는 찾기를 강제 실행합니다. 클러스터형 인덱스가 없는 경우 INDEX(0)은 테이블 검색을 강제 실행하고 INDEX(1)은 오류로 해석됩니다.  
  
 단일 힌트 목록에서 여러 인덱스가 사용되는 경우에는 중복이 무시되고 나열된 인덱스 중 나머지를 사용하여 테이블의 행을 검색합니다. 이때 인덱스 힌트에 있는 인덱스의 순서가 중요합니다. 여러 인덱스 힌트는 또한 인덱스 AND 연산을 강제 실행하고 쿼리 최적화 프로그램은 액세스되는 각 인덱스에 대해 가능한 한 많은 조건을 적용합니다. 인덱스 힌트 컬렉션에 쿼리에서 참조하는 모든 열이 포함되지 않은 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]이 모든 인덱싱된 열을 검색한 후 인출을 수행하여 남은 열을 검색합니다.  
  
> [!NOTE]  
> 여러 인덱스를 참조하는 인덱스 힌트가 스타 조인의 팩트 테이블에 사용되는 경우 최적화 프로그램은 인덱스 힌트를 무시하고 경고 메시지를 반환합니다. 또한 인덱스 힌트가 지정된 테이블에 대해서는 인덱스 OR 연산을 사용할 수 없습니다.  
  
 테이블 힌트의 최대 인덱스 수는 비클러스터형 인덱스 250개입니다.  
  
KEEPIDENTITY  
BULK 옵션이 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)와 함께 사용되는 경우 INSERT 문에만 적용됩니다.  
  
 가져온 데이터 파일의 ID 값이 ID 열에 사용되도록 지정합니다. KEEPIDENTITY를 지정하지 않는 경우 이 열의 ID 값을 확인하지만 가져오지는 않으며 쿼리 최적화 프로그램은 테이블 생성 중에 지정된 초기값 및 증가값에 따라 고유 값을 자동으로 할당합니다.  
  
> [!IMPORTANT]  
> 데이터 파일의 테이블 또는 뷰에서 ID 열에 값이 없고 ID 열이 테이블의 마지막 열이 아닌 경우 ID 열을 건너뛰어야 합니다. 자세한 내용은 [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)를 참조하세요. ID 열을 성공적으로 건너뛰면 쿼리 최적화 프로그램은 가져온 테이블 행에 ID 열의 고유 값을 자동으로 할당합니다.  
  
`INSERT ... SELECT * FROM OPENROWSET(BULK...)` 문에서 이 힌트를 사용하는 예제는 [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)를 참조하세요.  
  
테이블에 대한 ID 값을 확인하는 방법에 대한 내용은 [DBCC CHECKIDENT&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)를 참조하세요.  
  
KEEPDEFAULTS  
BULK 옵션이 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)와 함께 사용되는 경우 INSERT 문에만 적용됩니다.  
  
데이터 레코드에 열의 값이 없는 경우 NULL 대신 테이블 열의 기본값(있는 경우)을 삽입하도록 지정합니다.  
  
INSERT ... SELECT * FROM OPENROWSET (BULK ...) 문에서 이 힌트를 사용하는 예제는 [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)을 참조하세요.  
  
FORCESEEK [ **(** _index\_value_ **(** _index\_column\_name_ [ **,** ... _n_ ] **))** ]  
쿼리 최적화 프로그램이 테이블 또는 뷰의 데이터에 대한 액세스 경로로 Index Seek 연산만 사용하도록 지정합니다. 

> [!NOTE]
> [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP1부터는 인덱스 매개 변수도 지정할 수 있습니다. 이 경우 쿼리 최적화 프로그램이 최소 지정된 인덱스 열을 사용하여 지정된 인덱스 전체에서 Index Seek 연산만 고려합니다.  
  
 *index_value*  
 인덱스 이름 또는 인덱스 ID 값입니다. 인덱스 ID 0(힙)은 지정할 수 없습니다. 인덱스 이름 또는 ID를 반환하려면 **sys.indexes** 카탈로그 뷰를 쿼리합니다.  
  
 *index_column_name*  
 Seek 연산에 포함하려는 인덱스 열의 이름입니다. 인덱스 매개 변수와 함께 FORCESEEK를 지정하는 것은 INDEX 힌트와 함께 FORCESEEK를 사용하는 것과 유사합니다. 그러나 검색할 인덱스와 Seek 연산에서 고려하는 인덱스 열을 모두 지정하여 쿼리 최적화 프로그램에 사용되는 액세스 경로를 더 많이 제어할 수 있습니다. 최적화 프로그램은 필요할 경우 추가 열을 고려할 수도 있습니다. 예를 들어, 비클러스터형 인덱스가 지정될 경우 최적화 프로그램은 지정된 열과 함께 클러스터형 인덱스 키 열을 사용하도록 선택할 수도 있습니다.  
  
FORCESEEK 힌트는 다음과 같은 방법으로 지정할 수 있습니다.  
  
|구문|예제|설명|  
|------------|-------------|-----------------|  
|인덱스 또는 INDEX 힌트 없이 사용|`FROM dbo.MyTable WITH (FORCESEEK)`|쿼리 최적화 프로그램이 Index Seek 연산만 고려하여 모든 관련 인덱스 전체에서 테이블 또는 뷰에 액세스합니다.|  
|INDEX 힌트와 함께 사용|`FROM dbo.MyTable WITH (FORCESEEK, INDEX (MyIndex))`|쿼리 최적화 프로그램이 Index Seek 연산만 고려하여 지정된 인덱스 전체에서 테이블 또는 뷰에 액세스합니다.|  
|인덱스 및 인덱스 열을 지정하여 매개 변수 있음|`FROM dbo.MyTable WITH (FORCESEEK (MyIndex (col1, col2, col3)))`|쿼리 최적화 프로그램이 최소 지정된 인덱스 열을 사용하여 지정된 인덱스 전체에서 Index Seek 연산만 고려하여 테이블 또는 뷰에 액세스합니다.|  
  
FORCESEEK 힌트(인덱스 매개 변수와 함께 또는 없이)를 사용할 경우 다음 지침을 고려합니다.  
-   힌트는 테이블 힌트 또는 쿼리 힌트로 지정될 수 있습니다. 쿼리 힌트에 대한 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
-   FORCESEEK를 인덱싱된 뷰로 적용하려면 NOEXPAND 힌트도 지정해야 합니다.  
-   힌트는 테이블 또는 뷰마다 최대 한 번 적용될 수 있습니다.  
-   원격 데이터 원본에 대해서는 힌트를 지정할 수 없습니다. 오류 7377은 FORCESEEK가 인덱스 힌트와 함께 지정될 때 반환되고 오류 8180은 FORCESEEK가 인덱스 힌트 없이 사용될 때 반환됩니다.  
-   FORCESEEK로 계획이 검색되지 않으면 오류 8622가 반환됩니다.  
  
FORCESEEK가 인덱스 매개 변수와 함께 지정된 경우 다음 지침과 제한이 적용됩니다.  
-   INSERT, UPDATE 또는 DELETE 문의 대상인 테이블에는 힌트를 지정할 수 없습니다.  
-   힌트는 INDEX 힌트 또는 기타 FORCESEEK 힌트와 함께 지정할 수 없습니다.  
-   최소 하나의 열이 지정되어야 하고 선행 키 열이어야 합니다.  
-   추가 인덱스 열을 지정할 수 있지만 키 열은 건너뛸 수 없습니다. 예를 들어 지정된 인덱스가 키 열을 포함할 경우 `a`, `b`, `c` 및 유효한 구문은 `FORCESEEK (MyIndex (a))` 및 `FORCESEEK (MyIndex (a, b)`를 포함합니다. 유효하지 않은 구문은 `FORCESEEK (MyIndex (c))` 및 `FORCESEEK (MyIndex (a, c)`를 포함합니다.  
-   힌트에서 지정한 열 이름 순서는 반드시 참조된 인덱스에 있는 열 순서와 일치해야 합니다.  
-   인덱스 키 정의에 없는 열은 지정할 수 없습니다. 예를 들어 비클러스터형 인덱스에서는 정의된 인덱스 키 열만 지정할 수 있습니다. 인덱스에 자동으로 포함된 클러스터형 키 열은 지정될 수 없지만 최적화 프로그램에서 사용될 수 있습니다.  
-   xVelocity 메모리 액세스에 최적화된 columnstore 인덱스는 인덱스 매개 변수로 지정할 수 없습니다. 오류 366이 반환됩니다.  
-   열을 추가하거나 제거하여 인덱스 정의를 수정하려면 해당 인덱스를 참조하는 쿼리를 수정해야 할 수도 있습니다.  
-   힌트는 최적화 프로그램이 테이블의 모든 공간 또는 XML 인덱스를 고려하지 않도록 합니다.  
-   힌트는 FORCESCAN 힌트와 함께 지정할 수 없습니다.  
-   분할된 인덱스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 암시적으로 추가된 분할 열은 FORCESEEK 힌트에 지정할 수 없습니다.  
  
> [!CAUTION]  
> 매개 변수와 함께 FORCESEEK를 지정할 경우 매개 변수 없이 FORCESEEK를 지정할 때보다 최적화 프로그램에서 고려할 수 있는 계획 수가 더 제한됩니다. 이로 인해 더 많은 사례에서 `Plan cannot be generated` 오류가 발생할 수 있습니다. 후속 릴리스에서는 더 많은 계획을 고려할 수 있도록 쿼리 최적화 프로그램이 수정될 것입니다.  
  
FORCESCAN **적용 대상**: [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP1 ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
쿼리 최적화 프로그램이 참조된 테이블 또는 뷰의 액세스 경로로 인덱스 검색 작업만 사용하도록 지정합니다. FORCESCAN 힌트는 최적화 프로그램이 영향을 받는 행의 수를 과소평가하고 검색 작업 대신 Seek 연산을 선택하는 경우 쿼리에 유용할 수 있습니다. 이러한 경우 작업에 할당되는 메모리 양이 적으며 쿼리 성능에도 영향을 줍니다.  
  
FORCESCAN은 인덱스 힌트와 함께 또는 인덱스 힌트 없이 지정할 수 있습니다. 인덱스 힌트와 함께 사용할 경우(`INDEX = index_name, FORCESCAN`) 쿼리 최적화 프로그램은 참조 테이블에 액세스할 때 지정된 인덱스 전체에서 검색 액세스 경로만 고려합니다. 기본 테이블에 대해 테이블 검색 작업이 강제로 수행되도록 하기 위해 FORCESCAN을 인덱스 힌트 INDEX(0)와 함께 지정할 수 없습니다.  
  
분할된 테이블과 인덱스의 경우 FORCESCAN은 파티션이 쿼리 조건자 평가를 통해 제거된 이후에 적용됩니다. 즉, 검색은 전체 테이블이 아니라 나머지 파티션에만 적용됩니다.  
  
FORCESCAN 힌트는 다음과 같은 제한 사항이 있습니다.  
-   INSERT, UPDATE 또는 DELETE 문의 대상인 테이블에는 힌트를 지정할 수 없습니다.  
-   힌트를 두 개 이상의 인덱스 힌트와 함께 사용할 수 없습니다.  
-   힌트는 최적화 프로그램이 테이블의 모든 공간 또는 XML 인덱스를 고려하지 않도록 합니다.  
-   원격 데이터 원본에 대해서는 힌트를 지정할 수 없습니다.  
-   힌트는 FORCESEEK 힌트와 함께 지정할 수 없습니다.  
  
HOLDLOCK  
SERIALIZABLE과 동일합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 SERIALIZABLE을 참조하세요. HOLDLOCK은 이 옵션이 지정된 테이블 또는 뷰에 대해 이 옵션이 사용된 문이 정의한 트랜잭션이 완료될 때까지만 적용됩니다. HOLDLOCK은 FOR BROWSE 옵션이 포함된 SELECT 문에 사용할 수 없습니다.  
  
IGNORE_CONSTRAINTS  
BULK 옵션이 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)와 함께 사용되는 경우 INSERT 문에만 적용됩니다.  
  
대량 가져오기 작업에서 테이블의 모든 제약 조건을 무시하도록 지정합니다. 기본적으로 INSERT는 [Unique 제약 조건 및 Check 제약 조건](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 및 [Primary Key 및 Foreign Key 제약 조건](../../relational-databases/tables/primary-and-foreign-key-constraints.md)을 검사합니다. 대량 가져오기 작업에 IGNORE_CONSTRAINTS가 지정된 경우 INSERT는 대상 테이블의 이러한 제약 조건을 무시해야 합니다. UNIQUE, PRIMARY KEY 또는 NOT NULL 제약 조건은 비활성화할 수 없습니다.  
  
입력 데이터에 제약 조건을 위반하는 행이 포함된 경우에는 CHECK 및 FOREIGN KEY 제약 조건을 비활성화할 수 있습니다. CHECK 및 FOREIGN KEY 제약 조건을 비활성화하여 데이터를 가져온 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 데이터를 정리할 수 있습니다.  
  
그러나 CHECK 및 FOREIGN KEY 제약 조건이 무시되는 경우, 테이블에서 무시된 각 제약 조건은 작업 후에 [sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) 또는 [sys.foreign_keys](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md) 카탈로그 뷰에서 **is_not_trusted**로 표시됩니다. 어느 시점에서는 전체 테이블의 제약 조건을 확인해야 합니다. 대량 가져오기 작업을 수행하기 전에 테이블이 비어 있지 않으면 제약 조건의 유효성을 다시 검사하는 비용이 증분 데이터에 CHECK 및 FOREIGN KEY 제약 조건을 적용하는 비용을 초과할 수 있습니다.  
  
IGNORE_TRIGGERS  
BULK 옵션이 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)와 함께 사용되는 경우 INSERT 문에만 적용됩니다.  
  
대량 가져오기 작업에서 테이블에 정의된 모든 트리거를 무시하도록 지정합니다. 기본적으로 INSERT는 트리거를 적용합니다.  
  
응용 프로그램이 트리거에 의존하지 않으며 성능을 최대화해야 하는 경우에만 IGNORE_TRIGGERS를 사용하세요.  
  
NOLOCK  
READUNCOMMITTED와 동일합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 READUNCOMMITTED를 참조하세요.  
  
> [!NOTE]  
> UPDATE 또는 DELETE 문의 경우: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
NOWAIT  
테이블에 잠금이 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 바로 메시지를 반환하도록 지정합니다. NOWAIT는 특정 테이블에 SET LOCK_TIMEOUT 0을 지정하는 것과 동일합니다. TABLOCK 힌트도 포함되어 있는 경우 NOWAIT 힌트가 작동하지 않습니다. TABLOCK 힌트를 사용할 때 기다리지 않고 쿼리를 종료하려면 쿼리 앞에 `SETLOCK_TIMEOUT 0;`을 대신 추가하세요.  
  
PAGLOCK  
일반적으로 행 또는 키에 개별 잠금이 사용되거나 일반적으로 단일 테이블 잠금이 사용되는 곳에서 페이지 잠금을 사용합니다. 기본적으로 작업에 적합한 잠금 모드를 사용합니다. SNAPSHOT 격리 수준에서 작동하는 트랜잭션에 지정하는 경우 UPDLOCK 및 HOLDLOCK과 같은 잠금이 필요한 다른 테이블 힌트와 함께 PAGLOCK을 사용하지 않으면 페이지 잠금이 수행되지 않습니다.  
  
READCOMMITTED  
읽기 작업이 잠금 또는 행 버전 관리를 사용하여 READ COMMITTED 격리 수준에 대한 규칙을 따르도록 지정합니다. READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 OFF인 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 데이터를 읽을 때 공유 잠금을 획득하고 읽기 작업이 완료되면 잠금을 해제합니다. READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON인 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 잠금을 획득하지 않고 행 버전 관리를 사용합니다. 격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
> UPDATE 또는 DELETE 문의 경우: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
READCOMMITTEDLOCK  
읽기 작업이 잠금을 사용하여 READ COMMITTED 격리 수준에 대한 규칙을 따르도록 지정합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 READ_COMMITTED_SNAPSHOT 데이터베이스 옵션의 설정에 관계없이 데이터를 읽을 때 공유 잠금을 획득하고 읽기 작업이 완료되면 잠금을 해제합니다. 격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요. INSERT 문의 대상 테이블에는 힌트를 지정할 수 없습니다. 지정할 경우 4140 오류가 반환됩니다.  
  
READPAST  
[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 다른 트랜잭션에 의해 잠긴 행을 읽지 않도록 지정합니다. READPAST가 지정되면 행 수준 잠금은 건너뛰지만, 페이지 수준 잠금은 건너뛰지 않습니다. 즉, [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 잠금이 해제될 때까지 현재 트랜잭션을 차단하는 대신 행을 건너뜁니다. 예를 들어 `T1` 테이블에 값이 1, 2, 3, 4, 5인 단일 정수 열이 있다고 가정합니다. 트랜잭션 A가 값 3을 8로 변경했으나 아직 커밋하지 않은 경우 SELECT * FROM T1 (READPAST)는 1, 2, 4, 5 값을 생성합니다. READPAST는 주로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 사용하는 작업 큐를 구현할 때 잠금 경합을 줄이는 데 사용됩니다. READPAST를 사용하는 큐 판독기는 다른 트랜잭션에 의해 잠긴 큐 항목이 있으면 다른 트랜잭션이 잠금을 해제할 때까지 기다리지 않고 사용 가능한 다음 큐 항목으로 건너뜁니다.  
  
READPAST는 UPDATE 또는 DELETE 문에서 참조되는 테이블과 FROM 절에서 참조되는 테이블에 지정할 수 있습니다. UPDATE 문에 지정되는 경우 READPAST는 문에서 지정된 위치와 관계없이 데이터를 읽어 업데이트할 레코드를 식별하는 경우에만 적용됩니다. READPAST는 INSERT 문의 INTO 절에서 테이블에 대해 지정할 수 없습니다. READPAST를 사용하는 업데이트 또는 삭제 작업은 외래 키 또는 인덱싱된 뷰를 읽거나 보조 인덱스를 수정할 때 차단될 수 있습니다.  
  
READPAST는 READ COMMITTED 또는 REPEATABLE READ 격리 수준에서 작동하는 트랜잭션에만 지정할 수 있습니다. SNAPSHOT 격리 수준에서 작동하는 트랜잭션에 지정하는 경우 UPDLOCK 및 HOLDLOCK과 같은 잠금이 필요한 다른 테이블 힌트와 함께 READPAST를 사용해야 합니다.  
  
READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON으로 설정되어 있고 다음 조건 중 하나에 해당하는 경우에는 READPAST 테이블 힌트를 지정할 수 없습니다.  
-   세션의 트랜잭션 격리 수준이 READ COMMITTED입니다.  
-   READCOMMITTED 테이블 힌트가 쿼리에도 지정되어 있습니다.  
  
이러한 경우 READPAST 힌트를 지정하려면 READCOMMITTED 테이블 힌트가 있으면 이를 제거하고 쿼리에 READCOMMITTEDLOCK 테이블 힌트를 포함합니다.  
  
READUNCOMMITTED  
더티 읽기를 허용하도록 지정합니다. 다른 트랜잭션이 현재 트랜잭션의 데이터 읽기를 수정하지 못하도록 하는 공유 잠금이 실행되지 않으며 다른 트랜잭션에 의해 설정된 배타적 잠금은 현재 트랜잭션의 잠긴 데이터 읽기를 차단하지 않습니다. 더티 읽기를 허용하면 동시성이 높아질 수 있지만 다른 트랜잭션이 데이터 수정 내용을 읽고 롤백할 가능성이 있습니다. 이 경우 트랜잭션에 대한 오류가 생성되거나 사용자에게 커밋되지 않은 데이터가 제공될 수 있습니다. 또한 사용자에게 레코드가 두 번 표시되거나 전혀 표시되지 않을 수도 있습니다.  
  
READUNCOMMITTED 및 NOLOCK 힌트는 데이터 잠금에만 적용됩니다. READUNCOMMITTED 및 NOLOCK 힌트가 있는 쿼리를 포함하여 모든 쿼리는 컴파일 및 실행 중에 Sch-S(스키마 안정성) 잠금을 획득합니다. 이 때문에 동시 트랜잭션이 테이블에 대해 Sch-M(스키마 수정) 잠금을 유지하면 쿼리가 차단됩니다. 예를 들어 DDL(데이터 정의 언어) 작업은 테이블의 스키마 정보를 수정하기 전에 Sch-M 잠금을 획득합니다. READUNCOMMITTED 또는 NOLOCK 힌트를 사용하여 실행되는 쿼리를 포함하여 Sch-S 잠금을 획득하려고 시도하는 동시 쿼리는 모두 차단됩니다. 반대로 Sch-S 잠금을 유지하는 쿼리는 Sch-M 잠금을 획득하려고 시도하는 동시 트랜잭션을 차단합니다.  
  
삽입, 업데이트 또는 삭제 작업으로 수정된 테이블에 대해서는 READUNCOMMITTED와 NOLOCK을 지정할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 UPDATE 또는 DELETE 문의 대상 테이블에 적용되는 FROM 절의 READUNCOMMITTED 및 NOLOCK 힌트를 무시합니다.  
  
> [!NOTE]  
> UPDATE 또는 DELETE 문의 대상 테이블에 적용되는 FROM 절의 READUNCOMMITTED 및 NOLOCK 힌트 사용 지원은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서 제거될 예정입니다. 새 개발 작업에서는 이 컨텍스트에서 이러한 힌트를 사용하지 않도록 하고 현재 이 힌트를 사용하는 응용 프로그램은 수정하세요.  
  
다음 중 하나를 사용하여 트랜잭션에서 커밋되지 않은 데이터 수정 내용에 대해 더티 읽기를 수행할 수 없도록 하여 잠금 경합을 최소화할 수도 있습니다.  
-   READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 ON으로 설정된 READ COMMITTED 격리 수준  
-   SNAPSHOT 격리 수준  
  
격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
> READUNCOMMITTED를 지정할 때 오류 메시지 601이 표시되면 교착 상태 오류(1205)를 해결하는 방법으로 오류를 해결하고 문을 다시 시도하세요.  
  
REPEATABLEREAD  
REPEATABLE READ 격리 수준에서 실행되는 트랜잭션과 동일한 잠금 기능으로 검색이 수행되도록 지정합니다. 격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.  
  
ROWLOCK  
페이지 또는 테이블 잠금이 일반적으로 사용될 때 행 잠금을 사용하도록 지정합니다. SNAPSHOT 격리 수준에서 작동하는 트랜잭션에 지정하는 경우 UPDLOCK 및 HOLDLOCK과 같은 잠금이 필요한 다른 테이블 힌트와 함께 ROWLOCK을 사용하지 않으면 행 잠금이 수행되지 않습니다.  
  
SERIALIZABLE  
HOLDLOCK과 동일합니다. 필요한 테이블 또는 데이터 페이지가 더 이상 필요 없을 때 트랜잭션의 완료 여부와 관계없이 즉시 공유 잠금을 해제하지 않고 트랜잭션 완료 시까지 유지함으로써 공유 잠금을 더욱 제한적으로 만듭니다. SERIALIZABLE 격리 수준에서 실행되는 트랜잭션과 동일한 잠금 기능으로 검색이 수행됩니다. 격리 수준에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.  
  
SNAPSHOT  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
메모리 최적화 테이블은 SNAPSHOT 격리로 액세스됩니다. SNAPSHOT은 메모리 최적화 테이블에서만 사용할 수 있습니다(디스크 기반 테이블에서 사용할 수 없음). 자세한 내용은 [메모리 액세스에 최적화된 테이블 소개](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)를 참조하세요.  
  
```sql 
SELECT * FROM dbo.Customers AS c   
WITH (SNAPSHOT)   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id=oh.customer_id;  
```  
  
SPATIAL_WINDOW_MAX_CELLS = *integer*  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
geometry 또는 geography 개체의 공간 분할(tessellation)에 사용할 최대 셀 개수를 지정합니다. *number*는 1과 8192 사이의 값입니다.  
  
이 옵션을 사용하면 기본 및 보조 필터 실행 시간을 서로 조정하여 쿼리 실행 시간을 미세 조정할 수 있습니다. 숫자가 클수록 보조 필터 실행 시간은 줄어들고 기본 실행 필터 시간은 늘어나며 숫자가 작을수록 기본 필터 실행 시간은 줄어들고 보조 필터 실행은 늘어납니다. 밀도가 높은 공간 데이터의 경우 숫자가 높을수록 기본 필터로 더 정확한 근사값을 제공하여 실행 시간이 빨라지고 보조 필터 실행 시간이 줄어듭니다. 스파스 데이터의 경우 숫자가 낮을수록 기본 필터 실행 시간이 줄어듭니다.  
  
 수동 및 자동 표 공간 분할에 모두 이 옵션을 사용할 수 있습니다.  
  
TABLOCK  
획득한 잠금이 테이블 수준에 적용되도록 지정합니다. 획득한 잠금 유형은 실행 중인 문에 따라 달라집니다. 예를 들어 SELECT 문에서는 공유 잠금을 획득할 수 있습니다. TABLOCK을 지정하여 공유 잠금을 행 또는 페이지 수준 대신 전체 테이블에 적용할 수 있습니다. HOLDLOCK도 함께 지정한 경우에는 트랜잭션이 끝날 때까지 테이블 잠금이 유지됩니다.  
  
INSERT INTO \<target_table> SELECT \<columns> FROM \<source_table> 문을 사용하여 힙으로 데이터를 가져오는 경우, 대상 테이블에 대해 TABLOCK 힌트를 지정하여 명령문에 최적화된 잠금과 로깅을 사용하도록 설정할 수 있습니다. 또한 데이터베이스의 복구 모델은 단순 또는 대량으로 지정해야 합니다. 자세한 내용은 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)를 참조하세요.  
  
[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 대량 행 집합 공급자와 함께 TABLOCK을 사용하여 테이블로 데이터를 가져오는 경우, 여러 클라이언트에서 로깅 및 잠금이 최적화된 상태에서 대상 테이블로 데이터를 동시에 로드할 수 있습니다. 자세한 내용은 [대량 가져오기의 최소 로깅을 위한 필수 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요.  
  
TABLOCKX  
테이블을 배타적으로 잠그도록 지정합니다.  
  
UPDLOCK  
업데이트 잠금을 사용하고 트랜잭션이 완료될 때까지 유지하도록 지정합니다. UPDLOCK은 읽기 작업을 위해 행 수준 또는 페이지 수준에서만 업데이트 잠금을 사용합니다. UPDLOCK이 TABLOCK과 함께 사용되는 경우 또는 테이블 수준 잠금이 여러 이유로 인해 사용되는 경우, 배타(X) 잠금이 대신 사용됩니다.  
  
UPDLOCK이 지정된 경우 READCOMMITTED 및 READCOMMITTEDLOCK 격리 수준 힌트는 무시됩니다. 예를 들어 세션의 격리 수준이 SERIALIZABLE로 설정되고 쿼리가 (UPDLOCK, READCOMMITTED)를 지정할 경우 READCOMMITTED 힌트는 무시되고 트랜잭션은 SERIALIZABLE 격리 수준을 사용하여 실행됩니다.  
  
XLOCK  
배타적 잠금을 사용하고 트랜잭션이 완료될 때까지 유지하도록 지정합니다. ROWLOCK, PAGLOCK 또는 TABLOCK과 함께 지정한 경우에는 배타적 잠금이 적절한 세분성 수준에 적용됩니다.  
  
## <a name="remarks"></a>Remarks  
테이블을 쿼리 계획으로 액세스하지 않는 경우에는 테이블 힌트가 무시됩니다. 최적화 프로그램의 선택에 의해 테이블 자체를 액세스하지 않거나 테이블 대신 인덱싱된 뷰를 액세스하기로 하는 경우 등이 해당됩니다. 후자의 경우에 OPTION(EXPAND VIEWS) 쿼리 힌트를 사용하여 인덱싱된 뷰 액세스를 금지할 수도 있습니다.  
  
모든 잠금 힌트는 뷰에서 참조되는 테이블과 뷰를 포함하여 쿼리 계획에서 액세스하는 모든 테이블과 뷰로 전달됩니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 해당되는 잠금 일관성 검사를 수행합니다.  
  
행 수준의 잠금을 획득하는 잠금 힌트 ROWLOCK, UPDLOCK 및 XLOCK은 실제 데이터 행이 아닌 인덱스 키에 잠금을 설정합니다. 예를 들어 테이블에 비클러스터형 인덱스가 있고 잠금 힌트를 사용하는 SELECT 문이 포함 인덱스에 의해 처리되는 경우 잠금은 기본 테이블의 데이터 행이 아닌 포함 인덱스의 인덱스 키에서 획득됩니다.  
  
다른 테이블에 있는 열에 액세스하는 식 또는 함수에 의해 계산되는 계산 열이 테이블에 있는 경우 테이블 힌트는 해당 테이블에서 사용되지 않으며 전파되지 않습니다. 예를 들어 NOLOCK 테이블 힌트는 쿼리의 테이블에 지정됩니다. 이 테이블에는 다른 테이블에 있는 열에 액세스하는 식과 함수의 조합에 의해 계산되는 계산 열이 있습니다. 이러한 식과 함수에 의해 참조되는 테이블은 액세스될 때 NOLOCK 테이블 힌트를 사용하지 않습니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FROM 절의 각 테이블에 대해 다음 각 그룹에서 두 개 이상의 테이블 힌트를 허용하지 않습니다.  
-   세분성 힌트: PAGLOCK, NOLOCK, READCOMMITTEDLOCK, ROWLOCK, TABLOCK 또는 TABLOCKX  
-   격리 수준 힌트: HOLDLOCK, NOLOCK, READCOMMITTED, REPEATABLEREAD, SERIALIZABLE  
  
## <a name="filtered-index-hints"></a>필터링된 인덱스 힌트  
 필터링된 인덱스는 테이블 힌트로 사용될 수 있지만 쿼리가 선택한 모든 행을 포함하지 않을 경우 쿼리 최적화 프로그램에서 오류 8622가 발생합니다. 다음은 잘못된 필터링된 인덱스 힌트에 대한 예입니다. 이 예에서는 필터링된 인덱스 `FIBillOfMaterialsWithComponentID`를 만든 다음 이를 SELECT 문에 대한 인덱스 힌트로 사용합니다. 필터링된 인덱스 조건자에는 ComponentID 533, 324 및 753의 데이터 행이 포함됩니다. 쿼리 조건자에도 ComponentID 533, 324 및 753의 데이터 행이 포함되지만 필터링된 인덱스에 없는 ComponentID 855 및 924도 포함하도록 결과 집합이 확장되어 있습니다. 따라서 쿼리 최적화 프로그램에서는 필터링된 인덱스 힌트를 사용할 수 없으며 오류 8622가 발생합니다. 자세한 내용은 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)을(를) 참조하세요.  
  
```sql  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithComponentID'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithComponentID  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithComponentID"  
    ON Production.BillOfMaterials (ComponentID, StartDate, EndDate)  
    WHERE ComponentID IN (533, 324, 753);  
GO  
SELECT StartDate, ComponentID FROM Production.BillOfMaterials  
    WITH( INDEX (FIBillOfMaterialsWithComponentID) )  
    WHERE ComponentID in (533, 324, 753, 855, 924);  
GO  
```  
  
쿼리 최적화 프로그램은 SET 옵션에 필터링된 인덱스에 대한 필수 값이 없으면 인덱스 힌트를 인식하지 않습니다. 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
## <a name="using-noexpand"></a>NOEXPAND 사용  
NOEXPAND는 *인덱싱된 뷰*에만 적용됩니다. 인덱싱된 뷰란 고유한 클러스터형 인덱스가 만들어져 있는 뷰를 의미합니다. 인덱싱된 뷰와 기본 테이블 모두에 있는 열에 대한 참조가 포함된 쿼리의 경우 쿼리 최적화 프로그램이 쿼리를 실행하는 데 인덱싱된 뷰를 사용하는 것이 최상의 방법이라고 결정하면 뷰의 인덱스를 사용합니다. 이 기능은 *인덱싱된 뷰 일치*라고 합니다. [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 이전에는 쿼리 최적화 프로그램에서 인덱싱된 뷰를 자동으로 사용하는 것은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 버전에서만 지원됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
단, 최적화 프로그램에서 일치시킬 인덱싱된 뷰를 고려하거나 NOEXPAND 힌트로 참조된 인덱싱된 뷰를 사용하려면 다음 SET 옵션을 ON으로 설정해야 합니다.  
 
> [!NOTE]  
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 NOEXPAND 힌트를 지정하지 않고도 인덱싱된 뷰를 자동으로 사용할 수 있도록 지원합니다.
  
||||  
|-|-|-|  
|ANSI_NULLS|ANSI_WARNINGS|CONCAT_NULL_YIELDS_NULL|  
|ANSI_PADDING|ARITHABORT<sup>1</sup>|QUOTED_IDENTIFIER|  
  
 <sup>1</sup> ANSI_WARNINGS가 ON으로 설정되면 ARITHABORT가 암시적으로 ON으로 설정됩니다. 따라서 이 설정을 수동으로 조정할 필요가 없습니다.  
  
 또한 NUMERIC_ROUNDABORT 옵션은 OFF로 설정해야 합니다.  
  
 최적화 프로그램이 인덱싱된 뷰에 대한 인덱스를 강제로 사용하게 하려면 NOEXPAND 옵션을 지정합니다. 이 힌트는 뷰가 쿼리에서도 명명되어 있는 경우에만 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FROM 절에서 직접 뷰를 명명하지 않는 쿼리에서 특정 인덱싱된 뷰를 강제로 사용하도록 힌트를 제공하지 않지만 쿼리 최적화 프로그램은 쿼리에서 직접 참조되지 않은 경우에도 인덱싱된 뷰의 사용을 고려합니다. NOEXPAND 테이블 힌트를 사용하는 경우 SQL Server는 인덱싱된 보기의 통계만 자동으로 만듭니다. 이 힌트를 생략하면 수동으로 통계를 생성하여 확인할 수 없는 누락된 통계에 대한 실행 계획 경고가 발생할 수 있습니다. 쿼리 최적화 중 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 쿼리가 보기를 직접 참조하고 NOEXPAND 힌트를 사용할 때 자동 또는 수동으로 생성된 보기 통계를 사용합니다.    
  
## <a name="using-a-table-hint-as-a-query-hint"></a>테이블 힌트를 쿼리 힌트로 사용  
 *테이블 힌트*는 OPTION (TABLE HINT) 절을 사용하여 쿼리 힌트로 지정할 수도 있습니다. 테이블 힌트는 [계획 지침](../../relational-databases/performance/plan-guides.md)의 컨텍스트에서 쿼리 힌트로만 사용하는 것이 좋습니다. 다른 임시 쿼리의 경우에는 이러한 힌트를 테이블 힌트로만 지정합니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 KEEPIDENTITY, IGNORE_CONSTRAINTS 및 IGNORE_TRIGGERS 힌트를 사용하려면 테이블에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-tablock-hint-to-specify-a-locking-method"></a>1\. TABLOCK 힌트를 사용하여 잠금 방법 지정  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Production.Product` 테이블에 공유 잠금을 사용하고 UPDATE 문이 끝날 때까지 유지하도록 지정합니다.  
  
```sql  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
### <a name="b-using-the-forceseek-hint-to-specify-an-index-seek-operation"></a>2\. FORCESEEK 힌트를 사용하여 Index Seek 연산 지정  
 다음 예에서는 인덱스를 지정하지 않고 FORCESEEK 힌트를 사용하여 쿼리 최적화 프로그램이 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Sales.SalesOrderDetail` 테이블에서 Index Seek 연산을 수행하도록 지정합니다.  
  
```sql
SELECT *  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d WITH (FORCESEEK)  
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
GO  
  
```  
  
 다음 예에서는 인덱스와 함께 FORCESEEK 힌트를 사용하여 쿼리 최적화 프로그램이 지정된 인덱스 및 인덱스 열에서 Index Seek 연산을 수행하도록 지정합니다.  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESEEK (PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID (SalesOrderID)))   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);   
GO  
  
```  
  
### <a name="c-using-the-forcescan-hint-to-specify-an-index-scan-operation"></a>C. FORCESCAN 힌트를 사용하여 Index Scan 연산 지정  
 다음 예에서는 FORCESCAN 힌트를 사용하여 쿼리 최적화 프로그램이 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Sales.SalesOrderDetail` 테이블에서 검색 작업을 수행하도록 지정합니다.  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESCAN)   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
```  
  
## <a name="see-also"></a>참고 항목  
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [힌트&#40;Transact SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)  
  
  
