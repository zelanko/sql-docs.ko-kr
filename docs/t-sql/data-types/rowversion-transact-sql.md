---
title: rowversion(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- timestamp_TSQL
- timestamp
dev_langs:
- TSQL
helpviewer_keywords:
- rowversion data type
- size [SQL Server], rowversion
- row version-stamping [SQL Server]
- rowversion columns
- version-stamping table rows
- unique rowversion numbers
- unique timestamp numbers
- timestamp data type
- timestamp columns
- size [SQL Server], timestamp
ms.assetid: 65c9cf0e-3e8a-45f8-87b3-3460d96afb0b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f2962d457ce079bd0ec2164f9fdd2a982b983f14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85638134"
---
# <a name="rowversion-transact-sql"></a>rowversion(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

데이터베이스 내에서 자동으로 생성된 고유 이진 숫자를 표시하는 데이터 형식입니다. 일반적으로 **rowversion**은 버전이 표시되는 테이블 행에 대한 메커니즘으로 사용됩니다. 스토리지 크기는 8바이트입니다. **rowversion** 데이터 형식은 증가하는 숫자일 뿐이며 날짜 또는 시간을 보존하지 않습니다. 날짜 또는 시간을 기록하려면 **datetime2** 데이터 형식을 사용합니다.
  
## <a name="remarks"></a>설명  
각 데이터베이스에는 데이터베이스 내에 **rowversion** 열을 포함하는 테이블에서 수행되는 각 삽입 또는 업데이트 작업에 따라 증가되는 카운터가 있습니다. 이 카운터는 데이터베이스 rowversion이며 시계와 연동되는 실제 시간이 아닌 데이터베이스 내의 상대적 시간을 추적합니다. 한 테이블은 하나의 **rowversion** 열만 가질 수 있습니다. **rowversion** 열이 있는 행이 수정되거나 삽입될 때마다 증가된 데이터베이스 rowversion 값이 **rowversion** 열에 삽입됩니다. 이런 속성 때문에 **rowversion** 열은 키, 특히 기본 키가 되기 어렵습니다. 행이 업데이트되면 rowversion 값이 변경되고 그렇게 되면 키 값도 변경됩니다. 열이 기본 키에 있는 경우 이전 키 값은 더 이상 유효하지 않으며 이전 값을 참조하는 외래 키도 더 이상 유효하지 않습니다. 테이블이 동적 커서에서 참조되면 업데이트를 할 때마다 커서 안의 행 위치가 변경됩니다. 열이 인덱스 키에 있는 경우 데이터 행을 업데이트할 때마다 인덱스도 업데이트됩니다.  행 값이 변경되지 않더라도 **rowversion** 값은 모든 업데이트 문으로 증가됩니다. (예를 들어 열 값이 5이고 업데이트 문이 값을 5로 설정하면, 변경 사항이 없어도 이 동작이 업데이트로 간주되어 **rowversion**이 증가됩니다.)
  
**timestamp**는 **rowversion** 데이터 형식의 동의어이며 데이터 형식 동의어의 동작에 따라 달라집니다. DDL 문에서 가능하면 **timestamp** 대신 **rowversion**을 사용하세요. 자세한 내용은 [데이터 형식 동의어&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md)를 참조하세요.
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] **timestamp** 데이터 형식은 ISO 표준에 정의된 **timestamp** 데이터 형식과 다릅니다.
  
> [!NOTE]  
>  **timestamp** 구문은 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
CREATE TABLE 또는 ALTER TABLE 문에서 **timestamp** 데이터 형식에 대한 열 이름을 입력하지 않아도 됩니다. 예를 들면 다음과 같습니다.
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
열 이름을 지정하지 않을 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 **timestamp** 열 이름을 생성하지만 **rowversion** 동의어는 이 동작을 따르지 않습니다. **rowversion**을 사용할 때는 열 이름을 지정해야 합니다. 예를 들면 다음과 같습니다.
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  SELECT 목록에 **rowversion** 열이 있는 SELECT INTO 문을 사용하면 중복된 **rowversion** 값이 생성됩니다. 이와 같은 방법으로 **rowversion**을 사용하지 않는 것이 좋습니다.  
  
null이 아닌 **rowversion** 열은 기능적으로 **binary(8)** 열과 같습니다. null이 아닌 **rowversion** 열은 기능적으로 **varbinary(8)** 열과 같습니다.
  
행의 **rowversion** 열을 사용하여 마지막으로 행을 읽은 이후 행에 대해 업데이트 문이 실행되었는지 여부를 쉽게 확인할 수 있습니다. 행에 대해 업데이트 문이 실행되면 rowversion 값이 업데이트됩니다. 행에 대해 업데이트 문이 실행되지 않으면 rowversion 값이 이전에 읽은 값과 같습니다. 데이터베이스의 현재 rowversion 값을 반환하려면 [@@DBTS](../../t-sql/functions/dbts-transact-sql.md)를 사용합니다.
  
여러 명의 사용자가 동시에 행을 업데이트할 때 데이터베이스의 무결성을 유지하기 위해 테이블에 **rowversion** 열을 추가할 수 있습니다. 또한 테이블을 다시 쿼리하지 않고도 얼마나 많은 행이 업데이트되었고 어떤 행이 업데이트되었는지 확인할 수 있습니다.
  
예를 들어 `MyTest`라는 테이블을 만드는 경우 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 테이블에 특정 데이터를 채웁니다.
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
그런 후 다음 예제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 업데이트 중에 `MyTest` 테이블에 대한 낙관적 동시성 제어를 구현할 수 있습니다. 이 스크립트는 행을 마지막으로 읽을 때의 **rowversion** 값을 나타내기 위해 `<myRv>`를 사용합니다. 값을 실제 **rowversion** 값으로 바꿉니다. 실제 **rowversion** 값의 예는 `0x00000000000007D3`입니다.
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = <myRv>;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  


또한 예제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 트랜잭션에 삽입할 수도 있습니다. 트랜잭션 범위 내에서 `@t` 변수를 쿼리하면 `myKey` 테이블을 다시 쿼리하지 않고도 테이블의 업데이트된 `MyTest` 열을 검색할 수 있습니다.

다음은 **timestamp** 구문을 사용하는 동일한 예입니다. `<myTS>`를 실제 **timestamp**로 바꿉니다.

```sql
CREATE TABLE MyTest2 (myKey int PRIMARY KEY  
    ,myValue int, TS timestamp);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (2, 0);  
GO  
DECLARE @t TABLE (myKey int);  
UPDATE MyTest2  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND TS = <myTS>;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
## <a name="see-also"></a>참고 항목
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
[INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION&#40;Transact-SQL&#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
  
  
