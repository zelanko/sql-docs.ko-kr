---
title: "다음 (Transact SQL)에 대 한 값 | Microsoft Docs"
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NEXT_VALUE_TSQL
- NEXT
- NEXT VALUE
- NEXT VALUE FOR
- NEXT_TSQL
- NEXT_VALUE_FOR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEXT VALUE FOR function
- sequence number object, NEXT VALUE FOR function
ms.assetid: 92632ed5-9f32-48eb-be28-a5e477ef9076
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aab8020fa04b978d7ec1b657fe0a1084123dfb48
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="next-value-for-transact-sql"></a>NEXT VALUE FOR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  지정한 시퀀스 개체에서 시퀀스 번호를 생성합니다.  
  
 만들고 시퀀스를 사용 하 여 전체 논의 알려면 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)합니다. 사용 하 여 [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) 생성 하려면 시퀀스 번호의 범위를 예약 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
NEXT VALUE FOR [ database_name . ] [ schema_name . ]  sequence_name  
   [ OVER (<over_order_by_clause>) ]  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 시퀀스 개체가 있는 데이터베이스의 이름입니다.  
  
 *schema_name*  
 시퀀스 개체가 있는 스키마의 이름입니다.  
  
 *sequence_name*  
 번호를 생성하는 시퀀스 개체의 이름입니다.  
  
 *over_order_by_clause*  
 파티션에서 시퀀스 값이 행에 할당되는 순서를 결정합니다. 자세한 내용은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>반환 형식  
 시퀀스 형식을 사용하여 숫자를 반환합니다.  
  
## <a name="remarks"></a>주의  
 **NEXT VALUE FOR** 함수는 저장된 프로시저 및 트리거에 사용할 수 있습니다.  
  
 경우는 **NEXT VALUE FOR** 같은 시퀀스 개체가 두 번 이상 사용 하는 경우 또는 같은 시퀀스 개체가 값을 제공 하는 문과 기본 제약 조건에서 사용 하는 경우 함수는 쿼리 또는 기본 제약 조건에 사용 됩니다 실행 중인 결과 집합의 행 내에서 같은 시퀀스를 참조 하는 모든 열에 대해 동일한 값이 반환 됩니다.  
  
 **NEXT VALUE FOR** 함수는 비결 정적 이므로 생성 되는 시퀀스 값의 개수는 잘 정의 된 컨텍스트에서만에서 허용 됩니다. 다음은 지정된 문에서 참조되는 각 시퀀스 개체에 사용할 값 수를 정의합니다.  
  
-   **선택** -각 참조 된 시퀀스 개체에 대 한 새 값은 행당 한 번 생성 문의 결과입니다.  
  
-   **삽입** 중... **값** -각 참조 된 시퀀스 개체에 대 한 새 값은 한 번 생성 문에 삽입 된 각 행에 대 한 합니다.  
  
-   **업데이트** -각 참조 된 시퀀스 개체에 대 한 새 값이 문에서 업데이트 중인 각 행에 대해 생성 됩니다.  
  
-   절차 문 (예: **DECLARE**, **설정**등)-각 참조 된 시퀀스 개체에 대 한 새 값이 각 문에 대해 생성 됩니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 **NEXT VALUE FOR** 함수는 다음과 같은 상황에서 사용할 수 없습니다.  
  
-   데이터베이스가 읽기 전용 모드인 경우  
  
-   테이블 반환 함수의 인수로 사용할 경우  
  
-   집계 함수의 인수로 사용할 경우  
  
-   공통 테이블 식 및 파생 테이블을 포함하는 하위 쿼리에 사용할 경우  
  
-   뷰, 사용자 정의 함수 또는 계산 열에 사용할 경우  
  
-   사용 하는 문에 **DISTINCT**, **UNION**, **UNION ALL**, **EXCEPT** 또는 **INTERSECT** 연산자입니다.  
  
-   사용 하는 문에 **ORDER BY** 절 하지 않는 한 **NEXT VALUE FOR** ... **통해** (**ORDER BY** ...) 사용 됩니다.  
  
-   절에서: **인출**, **통해**, **출력**, **ON**, **피벗**,  **피벗 해제**, **그룹화**, **HAVING**, **계산**, **여 계산**, 또는 **FORXML**.  
  
-   사용 하 여 조건식 **대/소문자**, **선택**, **COALESCE**, **IIF**, **ISNULL**, 또는  **NULLIF**합니다.  
  
-   에 **값** 하지 않은 절의 일부가 **삽입** 문.  
  
-   CHECK 제약 조건을 정의하는 데 사용할 경우  
  
-   규칙 또는 기본 개체를 정의하는 데 사용할 경우(기본 제약 조건에는 사용할 수 있음)  
  
-   사용자 정의 테이블 형식에서 기본값으로 사용할 경우  
  
-   사용 하는 문을 **TOP**, **오프셋**, 되거나는 **행 개수** 옵션을 설정 합니다.  
  
-   에 **여기서** 문의 절.  
  
-   에 **병합** 문. (경우는 제외의 **NEXT VALUE FOR** 함수를 사용 하는 대상 테이블의 기본 제약 조건에서 및 기본값에 사용 되는 **만들기** 의 문은 **병합** 문.)  
  
## <a name="using-a-sequence-object-in-a-default-constraint"></a>기본 제약 조건에 시퀀스 개체 사용  
 사용 하는 경우는 **NEXT VALUE FOR** 함수는 기본 제약 조건에는 다음 규칙이 적용:  
  
-   여러 테이블의 기본 제약 조건에서 단일 시퀀스 개체를 참조할 수 있습니다.  
  
-   테이블과 시퀀스 개체가 동일한 데이터베이스에 있어야 합니다.  
  
-   기본 제약 조건을 추가하는 사용자에게 시퀀스 개체에 대한 REFERENCES 권한이 있어야 합니다.  
  
-   기본 제약 조건에서 참조하는 시퀀스 개체를 삭제하려면 먼저 기본 제약 조건을 삭제해야 합니다.  
  
-   여러 기본 제약 조건에서 같은 시퀀스 개체를 사용하거나 값을 제공하는 문과 현재 실행 중인 기본 제약 조건 둘 다에서 같은 시퀀스 개체를 사용하는 경우 행의 모든 열에 대해 동일한 시퀀스 번호가 반환됩니다.  
  
-   에 대 한 참조는 **NEXT VALUE FOR** 기본 제약 조건에서 함수를 지정할 수 없습니다는 **통해** 절.  
  
-   기본 제약 조건에서 참조하는 시퀀스 개체를 변경할 수 있습니다.  
  
-   경우에 `INSERT … SELECT` 또는 `INSERT … EXEC` 문을 삽입할 데이터를 사용 하는 쿼리에서 가져오는 위치는 **ORDER BY** 절에서 반환 되는 값은 **NEXT VALUE FOR** 함수는 수 로 지정 된 순서 대로 생성의 **ORDER BY** 절.  
  
## <a name="using-a-sequence-object-with-an-over-order-by-clause"></a>OVER ORDER BY 절에서 시퀀스 개체 사용  
 **NEXT VALUE FOR** 함수를 적용 하 여 정렬 된 시퀀스 값의 생성을 지원는 **통해** 절을는 **NEXT VALUE FOR** 호출 합니다. 사용 하 여는 **통해** 절, 사용자는 보장 반환 되는 값의 순서 대로 생성 됩니다는 **통해** 절의 **순서 B**Y 하위 절. 사용 하는 경우 다음 추가 규칙이 적용 된 **NEXT VALUE FOR** 작동는 **통해** 절:  
  
-   여러 번 호출 된 **NEXT VALUE FOR** 단일 문의 동일한 시퀀스 생성기 해야 모두 사용 하 여 동일한 함수 **통해** 절 정의 합니다.  
  
-   여러 번 호출는 **NEXT VALUE FOR** 단일 문의 서로 다른 시퀀스 생성기 참조 다른는 작동 **통해** 절 정의 합니다.  
  
-   **통해** 절에 적용 된 **NEXT VALUE FOR** 함수 지원 하지 않습니다는 **PARTITION BY** 하위 절.  
  
-   모든 호출 하는 경우는 **NEXT VALUE FOR** 함수는 **선택** 문에서 지정는 **통해** 절은 **ORDER BY** 절에 사용할 수 있습니다 **선택** 문.  
  
-   **통해** 절을 사용할 수는 **NEXT VALUE FOR** 에 사용 된 경우 작동 하지는 **선택** 문 또는 `INSERT … SELECT …` 문. 사용는 **통해** 절과 함께 **NEXT VALUE FOR** 함수에서 허용 되지 않는 **업데이트** 또는 **병합** 문.  
  
-   다른 프로세스에서 시퀀스 개체에 동시에 액세스할 경우 반환되는 번호에 간격이 생길 수 있습니다.  
  
## <a name="metadata"></a>메타데이터  
 시퀀스에 대 한 정보, 쿼리는 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 필요한 **업데이트** 시퀀스 개체 또는 시퀀스의 스키마에 대 한 권한이 있습니다. 사용 권한을 부여하는 방법에 대한 예는 이 항목의 뒷부분에 나오는 예 7을 참조하십시오.  
  
### <a name="ownership-chaining"></a>소유권 체인  
 시퀀스 개체는 소유권 체인을 지원합니다. 시퀀스 개체의 소유자가 호출하는 저장 프로시저, 트리거 또는 테이블(기본 제약 조건으로 시퀀스 개체 사용)의 소유자와 같은 경우에는 시퀀스 개체에 대한 권한 확인이 필요 없습니다. 호출하는 저장 프로시저, 트리거 또는 테이블의 소유자가 시퀀스 개체를 소유하지 않은 경우에는 시퀀스 개체에 대한 권한 확인이 필요합니다.  
  
 때는 **NEXT VALUE FOR** 함수를 사용 하는 테이블의 기본 값으로, 둘 다 요구 하는 사용자가 **삽입** 테이블에 대 한 권한 및 **업데이트** 시퀀스 개체에 대 한 권한 기본값을 사용 하 여 데이터를 삽입 합니다.  
  
-   기본 제약 조건의 소유자가 시퀀스 개체의 소유자와 같은 경우에는 기본 제약 조건을 호출할 때 시퀀스 개체에 대한 권한이 필요 없습니다.  
  
-   기본 제약 조건과 시퀀스 개체의 소유자가 다른 경우에는 기본 제약 조건을 통해 호출하는 경우에도 시퀀스 개체에 대한 권한이 필요합니다.  
  
### <a name="audit"></a>감사  
 감사는 **NEXT VALUE FOR** 함수, 하려면 SCHEMA_OBJECT_ACCESS_GROUP을 모니터링 합니다.  
  
## <a name="examples"></a>예  
 시퀀스를 생성 및 사용에 대 한 예제는 **NEXT VALUE FOR** 함수 시퀀스 번호를 생성, 참조를 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)합니다.  
  
 다음 예에서는 `CountBy1`라는 스키마의 `Test`이라는 시퀀스를 사용합니다. `Test.CountBy1` 시퀀스를 만들려면 다음 문을 실행합니다. 예 3과 4에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용하여 `CountBy1` 시퀀스를 만듭니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Test;  
GO  
  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="a-using-a-sequence-in-a-select-statement"></a>1. SELECT 문에 시퀀스 사용  
 다음 예에서는 사용할 때마다 1씩 증가하는 `CountBy1`이라는 시퀀스를 만듭니다.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1 AS FirstUse;  
SELECT NEXT VALUE FOR Test.CountBy1 AS SecondUse;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstUse  
1  
  
SecondUse  
2
```  
  
### <a name="b-setting-a-variable-to-the-next-sequence-value"></a>2. 변수를 다음 시퀀스 값으로 설정  
 다음 예에서는 변수를 시퀀스 번호의 다음 값으로 설정하는 세 가지 방법을 보여 줍니다.  
  
```  
DECLARE @myvar1 bigint = NEXT VALUE FOR Test.CountBy1  
DECLARE @myvar2 bigint ;  
DECLARE @myvar3 bigint ;  
SET @myvar2 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar3 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar1 AS myvar1, @myvar2 AS myvar2, @myvar3 AS myvar3 ;  
GO  
```  
  
### <a name="c-using-a-sequence-with-a-ranking-window-function"></a>3. 순위 창 함수에 시퀀스 사용  
  
```  
USE AdventureWorks2012 ;  
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 OVER (ORDER BY LastName) AS ListNumber,  
    FirstName, LastName  
FROM Person.Contact ;  
GO  
```  
  
### <a name="d-using-the-next-value-for-function-in-the-definition-of-a-default-constraint"></a>4. 기본 제약 조건 정의에 NEXT VALUE FOR 함수 사용  
 사용 하는 **NEXT VALUE FOR** 기본 제약 조건 정의에 함수는 지원 합니다. 사용 하는 예제에 대 한 **NEXT VALUE FOR** 에 **CREATE TABLE** 문의 예 3 참조[시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)합니다. 다음 예에서는 `ALTER TABLE`을 사용하여 현재 테이블에 기본값으로 시퀀스를 추가합니다.  
  
```  
CREATE TABLE Test.MyTable  
(  
    IDColumn nvarchar(25) PRIMARY KEY,  
    name varchar(25) NOT NULL  
) ;  
GO  
  
CREATE SEQUENCE Test.CounterSeq  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
ALTER TABLE Test.MyTable  
    ADD   
        DEFAULT N'AdvWorks_' +   
        CAST(NEXT VALUE FOR Test.CounterSeq AS NVARCHAR(20))   
        FOR IDColumn;  
GO  
  
INSERT Test.MyTable (name)  
VALUES ('Larry') ;  
GO  
  
SELECT * FROM Test.MyTable;  
GO  
```  
  
### <a name="e-using-the-next-value-for-function-in-an-insert-statement"></a>5. INSERT 문에 NEXT VALUE FOR 함수 사용  
 다음 예에서는 `TestTable`이라는 테이블을 만든 다음 `NEXT VALUE FOR` 함수를 사용하여 행을 삽입합니다.  
  
```  
CREATE TABLE Test.TestTable  
     (CounterColumn int PRIMARY KEY,  
    Name nvarchar(25) NOT NULL) ;   
GO  
  
INSERT Test.TestTable (CounterColumn,Name)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Syed') ;  
GO  
  
SELECT * FROM Test.TestTable;   
GO  
  
```  
  
### <a name="e-using-the-next-value-for-function-with-select--into"></a>5. SELECT … INTO에 NEXT VALUE FOR 함수 사용 INTO  
 다음 예제에서는 `SELECT … INTO` 라는 테이블을 만드는 문을 `Production.NewLocation` 사용 하 여는 `NEXT VALUE FOR` 함수 각 행의 번호입니다.  
  
```  
USE AdventureWorks2012 ;   
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 AS LocNumber, Name   
    INTO Production.NewLocation  
    FROM Production.Location ;  
GO  
  
SELECT * FROM Production.NewLocation ;  
GO  
```  
  
### <a name="f-granting-permission-to-execute-next-value-for"></a>6. NEXT VALUE FOR 실행 권한 부여  
 다음 예에서는 권한을 부여 **업데이트** 라는 사용자에 대 한 사용 권한을 `AdventureWorks\Larry` 실행할 수 있는 권한이 `NEXT VALUE FOR` 를 사용 하는 `Test.CounterSeq` 시퀀스입니다.  
  
```  
GRANT UPDATE ON OBJECT::Test.CounterSeq TO [AdventureWorks\Larry] ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Sequence&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER sequence&#40; Transact SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  

