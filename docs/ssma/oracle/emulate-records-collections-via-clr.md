---
title: CLR UDT를 통해 레코드 및 컬렉션 에뮬레이트
description: Oracle 용 SSMA (SQL Server Migration Assistant)에서 SQL Server CLR (공용 언어 런타임) UDT (사용자 정의 데이터 형식)를 사용 하 여 Oracle 레코드 및 컬렉션을 에뮬레이트하는 방법에 대해 설명 합니다.
author: nahk-ivanov
ms.prod: sql
ms.technology: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 73991999cf0a6e7bd2c8cd541ec58a37d1f18f09
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84779383"
---
# <a name="emulating-records-and-collections-via-clr-udt"></a>CLR UDT를 통해 레코드 및 컬렉션 에뮬레이트

이 문서에서는 Oracle 용 SSMA (SQL Server Migration Assistant)에서 SQL Server CLR (공용 언어 런타임) UDT (사용자 정의 데이터 형식)를 사용 하 여 Oracle 레코드 및 컬렉션을 에뮬레이트하는 방법에 대해 설명 합니다.

## <a name="declaring-record-or-collection-types-and-variables"></a>레코드 또는 컬렉션 형식 및 변수 선언

SSMA는 세 가지 CLR 기반 Udt를 만듭니다.

* `CollectionIndexInt`
* `CollectionIndexString`
* `Record`

`CollectionIndexInt`형식은 정수 (예: `VARRAY` s, 중첩 테이블 및 정수 키 기반 결합형 배열)로 인덱싱된 컬렉션을 에뮬레이트 하기 위한 것입니다. `CollectionIndexString`형식은 문자 키로 인덱싱된 결합형 배열에 사용 됩니다. Oracle 레코드 기능은 형식에 의해 에뮬레이션 됩니다 `Record` .

레코드 또는 컬렉션 형식의 모든 선언은 다음 Transact-sql 선언으로 변환 됩니다.

```sql
declare @Collection$TYPE varchar(max) = '<type definition>'
```

다음 `<type definition>` 은 원본 PL/SQL 유형을 고유 하 게 식별 하는 설명 텍스트입니다.

다음 예제를 참조하세요.

```sql
DECLARE
    TYPE Manager IS RECORD
    (
        mgrid integer,
        mgrname varchar2(40),
        hiredate date
    );

    TYPE Manager_table is TABLE OF Manager INDEX BY PLS_INTEGER;

    Mgr_rec Manager;
    Mgr_table_rec Manager_table;
BEGIN
    mgr_rec.mgrid := 1;
    mgr_rec.mgrname := 'Mike';
    mgr_rec.hiredate := sysdate;

    select
        empno,
        ename,
        hiredate
    BULK COLLECT INTO
        mgr_table_rec
    FROM
        emp;
END;
```

SSMA를 사용 하 여 변환 하면 다음 Transact-sql 코드가 됩니다.

```sql
BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) =
            ' TABLE INDEX BY INT OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'

    DECLARE
        @Mgr_rec$mgrid int,
        @Mgr_rec$mgrname varchar(40),
        @Mgr_rec$hiredate datetime2(0),
        @Mgr_table_rec dbo.CollectionIndexInt =
            dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

    SET @mgr_rec$mgrid = 1
    SET @mgr_rec$mgrname = 'Mike'
    SET @mgr_rec$hiredate = sysdatetime()

    SET @mgr_table_rec = @mgr_table_rec.RemoveAll()
    SET @mgr_table_rec =
        @mgr_table_rec.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionComplex((
                SELECT
                    CAST(EMP.EMPNO AS int) AS mgrid,
                    EMP.ENAME AS mgrname,
                    EMP.HIREDATE AS hiredate
                FROM dbo.EMP
                FOR XML PATH
            ))
        )
END
```

여기서 `Manager` 는 테이블이 숫자 인덱스 ()와 연결 되어 있기 때문에 `INDEX BY PLS_INTEGER` 사용 되는 해당 t-sql 선언은 형식입니다 `@CollectionIndexInt$TYPE` . 테이블이 문자 집합 인덱스와 연결 된 경우 `VARCHAR2` 해당 t-sql 선언은 다음과 같은 형식입니다 `@CollectionIndexString$TYPE` .

```sql
-- Oracle
TYPE Manager_table is TABLE OF Manager INDEX BY VARCHAR2(40);

-- SQL Server
@CollectionIndexString$TYPE varchar(max) =
    ' TABLE INDEX BY STRING OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'
```

Oracle 레코드 기능은 형식에 의해서만 에뮬레이션 됩니다 `Record` .

각 형식,, 및에는 `CollectionIndexInt` `CollectionIndexString` `Record` 빈 인스턴스를 반환 하는 정적 속성이 있습니다 `[Null]` . `SetType`메서드는 위의 예제에서 볼 수 있듯이 특정 형식의 빈 개체를 수신 하기 위해 호출 됩니다.

## <a name="constructor-call-conversions"></a>생성자 호출 변환

생성자 표기법은 중첩 테이블 및에만 사용할 수 `VARRAY` 있으므로 모든 명시적 생성자 호출은 형식을 사용 하 여 변환 됩니다 `CollectionIndexInt` . 빈 생성자 호출은 `SetType` 의 null 인스턴스에 대해 호출 된 호출을 통해 변환 됩니다 `CollectionIndexInt` . `[Null]`속성은 null 인스턴스를 반환 합니다. 생성자에 요소 목록이 포함 되어 있으면 특수 메서드 호출이 순차적으로 적용 되어 컬렉션에 값을 추가 합니다.

다음은 그 예입니다.

```sql
-- Oracle

DECLARE
    TYPE nested_type IS TABLE OF VARCHAR2(20);
    TYPE varray_type IS VARRAY(5) OF INTEGER;

    v1 nested_type;
    v2 varray_type;
BEGIN
   v1 := nested_type('Arbitrary','number','of','strings');
   v2 := varray_type(10, 20, 40, 80, 160);
END;

-- SQL Server

BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) = ' VARRAY OF INT',
        @CollectionIndexInt$TYPE$2 varchar(max) = ' TABLE OF STRING',
        @v1 dbo.CollectionIndexInt,
        @v2 dbo.CollectionIndexInt

    SET @v1 =
        dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE$2)
            .AddString('Arbitrary')
            .AddString('number')
            .AddString('of')
            .AddString('strings')

   SET @v2 =
       dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE)
            .AddInt(10)
            .AddInt(20)
            .AddInt(40)
            .AddInt(80)
            .AddInt(160)
END
```

## <a name="referencing-and-assigning-record-and-collection-elements"></a>레코드 및 컬렉션 요소 참조 및 할당

각 Udt에는 다양 한 데이터 형식의 요소를 사용 하는 일련의 메서드가 있습니다. 예를 들어 `SetDouble` 메서드는 `float(53)` 레코드 또는 컬렉션에 값을 할당 하 고 `GetDouble` 이 값을 읽을 수 있습니다. 다음은 전체 메서드 목록입니다.

```sql
GetCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
SetCollectionIndexInt(@key <KeyType>, @value CollectionIndexInt) returns <UDT_type>;
GetCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
SetCollectionIndexString(@key <KeyType>, @value CollectionIndexString) returns <UDT_type>;
Record GetRecord(@key <KeyType>) returns Record;
SetRecord(@key <KeyType>, @value Record) returns <UDT_type>;
GetString(@key <KeyType>) returns nvarchar(max);
SetString(@key <KeyType>, @value nvarchar(max)) returns nvarchar(max);
GetDouble(@key <KeyType>) returns float(53);
SetDouble(@key <KeyType>, @value float(53)) returns <UDT_type>;
GetDatetime(@key <KeyType>) returns datetime;
SetDatetime(@key <KeyType>, @value datetime) returns <UDT_type>;
GetVarbinary(@key <KeyType>) returns varbinary(max);
SetVarbinary(@key <KeyType>, @value varbinary(max)) returns <UDT_type>;
SqlDecimal GetDecimal(@key <KeyType>);
SetDecimal(@key <KeyType>, @value numeric) returns <UDT_type>;
GetXml(@key <KeyType>) returns xml;
SetXml(@key <KeyType>, @value xml) returns <UDT_type>;
GetInt(@key <KeyType>) returns bigint;
SetInt(@key <KeyType>, @value bigint) returns <UDT_type>;
```

이러한 메서드는 컬렉션/레코드의 요소에 값을 참조 하거나 할당할 때 사용 됩니다.

```sql
-- Oracle
a_collection(i) := 'VALUE';

-- SQL Server
SET @a_collection = @a_collection.SetString(@i, 'VALUE');
```

다차원 컬렉션 또는 record 요소를 사용 하는 컬렉션에 대 한 대입문을 변환할 때 SSMA는 set 메서드 내의 부모 요소를 참조 하는 다음 메서드를 추가 합니다.

```sql
GetOrCreateCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
GetOrCreateCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
GetOrCreateRecord(@key <KeyType>) returns Record;
```

예를 들어 record 요소의 컬렉션은 다음과 같은 방식으로 만들어집니다.

```sql
-- Oracle
DECLARE
    TYPE rec_details IS RECORD (id int, name varchar2(20));
    TYPE ntb1 IS TABLE of rec_details index BY binary_integer;
    c ntb1;
BEGIN
    c(1).id := 1;
END;

-- SQL Server
DECLARE
   @CollectionIndexInt$TYPE varchar(max) =
       ' TABLE INDEX BY INT OF ( RECORD ( ID INT , NAME STRING ) )',
   @c dbo.CollectionIndexInt =
       dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

SET @c = @c.SetRecord(1, @c.GetOrCreateRecord(1).SetInt(N'ID', 1))
```

## <a name="collection-built-in-methods"></a>컬렉션 기본 제공 메서드

SSMA는 다음 UDT 메서드를 사용 하 여 PL/SQL 컬렉션의 기본 제공 메서드를 에뮬레이트합니다.

Oracle 컬렉션 메서드 | `CollectionIndexInt`및 `CollectionIndexString` 동급
--- | ---
개수 | `Count returns int`
Delete | `RemoveAll() returns <UDT_type>`
삭제 (n) | `Remove(@index int) returns <UDT_type>`
삭제 (m, n) | `RemoveRange(@indexFrom int, @indexTo int) returns <UDT_type>`
EXISTS | `ContainsElement(@index int) returns bit`
넘으면 | `Extend() returns <UDT_type>`
확장 (n) | `Extend() returns <UDT_type>`
확장 (n, i) | `ExtendDefault(@count int, @def int) returns <UDT_type>`
FIRST | `First() returns int`
LAST | `Last() returns int`
LIMIT | 해당 없음
PRIOR | `Prior(@current int) returns int`
NEXT | `Next(@current int) returns int`
TRIM | `Trim() returns <UDT_type>`
TRIM (n) | `TrimN(@count int) returns <UDT_type>`

## <a name="bulk-collect-operation"></a>대량 수집 작업

SSMA `BULK COLLECT INTO` 는 문을 SQL Server 문으로 변환 합니다 `SELECT ... FOR XML PATH` . 그 결과는 다음 함수 중 하나로 래핑됩니다.

* `ssma_oracle.fn_bulk_collect2CollectionSimple`
* `ssma_oracle.fn_bulk_collect2CollectionComplex`

선택은 대상 개체의 형식에 따라 달라 집니다. 이러한 함수는, 및 형식으로 구문 분석할 수 있는 XML 값을 반환 `CollectionIndexInt` `CollectionIndexString` `Record` 합니다. 특수 `AssignData` 함수는 XML 기반 컬렉션을 UDT에 할당 합니다.

SSMA는 세 가지 종류의 `BULK COLLECT INTO` 문을 인식 합니다.

### <a name="the-collection-contains-elements-with-scalar-types-and-the-select-list-contains-one-column"></a>컬렉션에 스칼라 형식의 요소가 포함 되어 있고 목록에 `SELECT` 열이 하나 포함 되어 있습니다.

```sql
-- Oracle
SELECT column_name_1
BULK COLLECT INTO <collection_name_1>
FROM <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionSimple(
            (SELECT column_name_1 FROM <data_source> FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-record-types-and-the-select-list-contains-one-column"></a>컬렉션에는 레코드 형식이 포함 된 요소가 포함 되 고 목록에는 `SELECT` 하나의 열이 포함 됩니다.

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2...]
BULK COLLECT INTO
    <collection_name_1>
FROM
    <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionComplex(
            (SELECT
                column_name_1 as [collection_name_1_element_field_name_1],
                column_name_2 as [collection_name_1_element_field_name_2]
            FROM <data_source>
            FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-scalar-type-and-the-select-list-contains-multiple-columns"></a>컬렉션에 스칼라 형식의 요소가 포함 되어 있고 목록에 `SELECT` 여러 열이 포함 되어 있습니다.

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2 ...]
BULK COLLECT INTO
    <collection_name_1>[, <collection_name_2> ...]
FROM
    <data_source>

-- SQL Server
;WITH bulkC AS (
    SELECT
        column_name_1 [collection_name_1_element_field_name_1],
        column_name_2 [collection_name_1_element_field_name_2]
    FROM
        <data_source>
)
SELECT
    @<collection_name_1> =
        @<collection_name_1>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_1]
                FROM
                    bulkC
                FOR XML PATH))),
    @<collection_name_2> =
        @<collection_name_2>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_2]
                FROM bulkC
                FOR XML PATH)))
```

## <a name="select-into-record"></a>SELECT INTO 레코드

Oracle 쿼리 결과가 PL/SQL record 변수에 저장 되 면 레코드 변환의 ssma 설정에 따라 **구분 된 변수 목록** ( **도구** 메뉴에서 사용 가능, **프로젝트 설정**, **일반**  ->  **변환**)에 따라 두 가지 옵션이 제공 됩니다. 이 설정의 값이 **예** (기본값) 이면 Ssma는 레코드 형식의 인스턴스를 만들지 않습니다. 대신 각 레코드 필드 마다 별도의 Transact-sql 변수를 만들어 레코드를 백업을 위해 필드로 분할 합니다. 설정이 **아니요**인 경우 레코드는 인스턴스화되고 메서드를 사용 하 여 각 필드에 값이 할당 됩니다 `Set` .
