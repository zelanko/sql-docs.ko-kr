---
title: rowversion (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4a8a9c6a9ea076ec1727bfa5422a3dfbda58386c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="rowversion-transact-sql"></a>rowversion(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

데이터베이스 내에서 자동으로 생성된 고유 이진 숫자를 표시하는 데이터 형식입니다. **rowversion** 버전 표시 테이블 행에 대 한 메커니즘으로 일반적으로 사용 됩니다. 저장소 크기는 8바이트입니다. **rowversion** 데이터 형식은 숫자일 뿐 이며 날짜 또는 시간을 유지 하지 않습니다. 날짜 또는 시간을 기록 하려면 사용 하 여 한 **datetime2** 데이터 형식입니다.
  
## <a name="remarks"></a>주의  
각 데이터베이스는 각 삽입 작업 마다 증가 하는 카운터 또는 포함 된 테이블에서 수행 되는 업데이트 작업에는 **rowversion** 데이터베이스 내의 열입니다. 이 카운터는 데이터베이스 rowversion이며 시계와 연동되는 실제 시간이 아닌 데이터베이스 내의 상대적 시간을 추적합니다. 테이블이 하나만 포함할 수 **rowversion** 열입니다. 때마다를 사용 하 여 행은 **rowversion** 열이 수정 되거나 삽입, 증가 된 데이터베이스 rowversion 값에 삽입 됩니다는 **rowversion** 열입니다. 이 속성을 사용 하면 한 **rowversion** 저하 될 수 있는 키, 특히 기본 키 열입니다. 행이 업데이트되면 rowversion 값이 변경되고 그렇게 되면 키 값도 변경됩니다. 열이 기본 키에 있는 경우 이전 키 값은 더 이상 유효하지 않으며 이전 값을 참조하는 외래 키도 더 이상 유효하지 않습니다. 테이블이 동적 커서에서 참조되면 업데이트를 할 때마다 커서 안의 행 위치가 변경됩니다. 열이 인덱스 키에 있는 경우 데이터 행을 업데이트할 때마다 인덱스도 업데이트됩니다.  **rowversion** 없는 행 값이 변경 되는 경우에 모든 update 문을 사용 하 여 값이 증가 합니다. (예를 들어 열 값이 5, 5로 값을 설정 하는 update 문이,이 작업 것으로 간주 됩니다 업데이트가 변경 되지 않은 경우에 및 **rowversion** 증가 됩니다.)
  
**타임 스탬프** 에 대 한 동의어는 **rowversion** 데이터 형식 및 형식 동의어 데이터의 동작이 적용 됩니다. DDL 문을 사용 하 여 **rowversion** 대신 **타임 스탬프** 가능 합니다. 자세한 내용은 참조 [데이터 형식 동의어 &#40; Transact SQL &#41; ](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] **타임 스탬프** 된 데이터 형식이 다른는 **타임 스탬프** ISO 표준에 정의 된 데이터 형식입니다.
  
> [!NOTE]  
>  **타임 스탬프** 구문을 사용 하는 사용 되지 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
CREATE TABLE 또는 ALTER TABLE 문에서 않아도 대 한 열 이름을 지정 하는 **타임 스탬프** 데이터 형식:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
열 이름을 지정 하지 않으면는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 생성는 **타임 스탬프** 열 이름 이지만 **rowversion** 동의어가이 동작을 따르지 않습니다. 사용 하는 경우 **rowversion**, 예를 들어 열 이름을 지정 해야 합니다.
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  중복 **rowversion** 는 SELECT INTO 문을 사용 하 여 값을 생성할 수 있습니다는 **rowversion** SELECT 목록에 열이 있습니다. 사용 하지 않는 것이 좋습니다 **rowversion** 이런이 방식으로 합니다.  
  
null이 아닌 **rowversion** 열은 기능적으로 동일는 **binary (8)** 열입니다. Null 허용 **rowversion** 열은 기능적으로 동일는 **varbinary (8)** 열입니다.
  
사용할 수는 **rowversion** 쉽게 행을 update 문을 가진 여부를 결정 하는 행의 열에 대해 마지막으로 읽은 후 실행 합니다. Update 문에 행에 대해를 실행 하는 경우에 rowversion 값이 업데이트 됩니다. 문은 업데이트가 없는 행에 대해 실행 rowversion 기간은 이전에 읽은 경우와 동일입니다. 사용 하 여 데이터베이스에 대 한 현재 rowversion 값을 반환 하려면 [@@DBTS](../../t-sql/functions/dbts-transact-sql.md)합니다.
  
추가할 수는 **rowversion** 여러 사용자가 동시에 행을 업데이트 하는 경우 데이터베이스의 무결성을 유지 하기 위해 테이블에는 열입니다. 또한 테이블을 다시 쿼리하지 않고도 얼마나 많은 행이 업데이트되었고 어떤 행이 업데이트되었는지 확인할 수 있습니다.
  
예를 들어 `MyTest`라는 테이블을 만드는 경우 다음을 실행 하 여 테이블의 일부 데이터를 채우는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
그런 후 다음 예제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 업데이트 중에 `MyTest` 테이블에 대한 낙관적 동시성 제어를 구현할 수 있습니다.
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
`myValue`이 **rowversion** 행을 읽은 마지막으로 표시 하는 행에 대 한 열 값입니다. 이 값을 실제 클래스로 바꿔야 **rowversion** 값입니다. 실제 예 **rowversion** 값은 0x00000000000007D3 합니다.
  
또한 예제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 트랜잭션에 삽입할 수도 있습니다. 트랜잭션 범위 내에서 `@t` 변수를 쿼리하면 `myKey` 테이블을 다시 쿼리하지 않고도 테이블의 업데이트된 `MyTes` 열을 검색할 수 있습니다.
  
다음은 동일한 예제를 사용 하 여 **타임 스탬프** 구문:
  
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
    AND TS = myValue;  
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
[MIN_ACTIVE_ROWVERSION &#40; Transact SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
  
  
