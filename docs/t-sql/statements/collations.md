---
title: COLLATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COLLATE
- COLLATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], COLLATE clause
- COLLATE clause
ms.assetid: 76763ac8-3e0d-4bbb-aa53-f5e7da021daa
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a706193058256747ba1ec2fa71c7641cdecc4e8
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011326"
---
# <a name="collate-transact-sql"></a>COLLATE(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

문자열 식에 적용될 때 데이터베이스 또는 테이블 열의 데이터 정렬 또는 데이터 정렬 캐스트 작업을 정의합니다. 데이터 정렬 이름으로는 Windows 데이터 정렬 이름 또는 SQL 데이터 정렬 이름을 사용할 수 있습니다. 데이터베이스를 만들 때 지정하지 않으면 데이터베이스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 데이터 정렬이 할당됩니다. 테이블 열을 만들 때 지정하지 않으면 열에 데이터베이스의 기본 데이터 정렬이 할당됩니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql
COLLATE { <collation_name> | database_default }
<collation_name> :: =
    { Windows_collation_name } | { SQL_collation_name }
```

## <a name="arguments"></a>인수

*collation_name* 식, 열 정의 또는 데이터베이스 정의에 적용할 데이터 정렬의 이름입니다. *collation_name*에는 지정된 *Windows_collation_name* 또는 *SQL_collation_name*만 사용할 수 있습니다. *collation_name*은 리터럴 값이어야 합니다. 변수나 식으로 *collation_name*을 나타낼 수 없습니다.

*Windows_collation_name*은 [Windows 데이터 정렬 이름](../../t-sql/statements/windows-collation-name-transact-sql.md)의 데이터 정렬 이름입니다.

*SQL_collation_name*은 [SQL Server 데이터 정렬 이름](../../t-sql/statements/sql-server-collation-name-transact-sql.md)의 데이터 정렬 이름입니다.

**database_default** COLLATE 절이 현재 데이터베이스의 데이터 정렬을 상속하도록 합니다.

## <a name="remarks"></a>설명

COLLATE 절은 여러 수준에서 지정할 수 있습니다. 여기에는 다음과 같은 옵션이 포함됩니다.

1. 데이터베이스 만들기 또는 변경

    `CREATE DATABASE` 또는 `ALTER DATABASE` 문의 COLLATE 절을 사용하여 데이터베이스의 기본 데이터 정렬을 지정할 수 있습니다. 또한 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 데이터베이스를 만들 때 데이터 정렬을 지정할 수 있습니다. 데이터 정렬을 지정하지 않은 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 데이터 정렬이 데이터베이스에 할당됩니다.

    > [!NOTE]
    > Windows 유니코드 전용 데이터 정렬은 COLLATE 절에서 열 수준 및 식 수준 데이터의 **nchar**, **nvarchar** 및 **ntext** 데이터 형식에 데이터 정렬을 적용하기 위해서만 사용할 수 있고 COLLATE 절에서 데이터베이스 또는 서버 인스턴스의 데이터 정렬을 정의하거나 변경하기 위해 사용할 수는 없습니다.

2. 테이블 열 만들기 또는 변경

    `CREATE TABLE` 또는 `ALTER TABLE` 문의 COLLATE 절을 사용하여 각 문자열 열에 대한 데이터 정렬을 지정할 수 있습니다. 또한 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 테이블을 만들 때 데이터 정렬을 지정할 수 있습니다. 데이터 정렬을 지정하지 않은 경우에는 데이터베이스의 기본 데이터 정렬이 열에 할당됩니다.

    또한 COLLATE 절에서 `database_default` 옵션을 사용하여 임시 테이블의 열이 연결에 대해 **tempdb** 대신 현재 사용자 데이터베이스의 기본 데이터 정렬을 사용하도록 지정할 수 있습니다.

3. 식의 데이터 정렬 캐스팅

    COLLATE 절을 사용하여 문자 식을 특정 데이터 정렬에 적용할 수 있습니다. 문자 리터럴과 변수에는 현재 데이터베이스의 기본 데이터 정렬이 할당됩니다. 열 참조에는 열의 기본 데이터 정렬이 할당됩니다.

식별자의 데이터 정렬은 식별자가 정의된 수준에 따라 달라집니다. 로그인과 데이터베이스 이름 등 인스턴스 수준 개체의 식별자에는 인스턴스의 기본 데이터 정렬이 할당됩니다. 테이블, 뷰, 열 이름 등 데이터베이스에 있는 개체의 식별자에는 데이터베이스의 기본 데이터 정렬이 할당됩니다. 예를 들어 대/소문자만 다르고 동일한 이름인 두 테이블은 데이터 정렬이 대/소문자를 구분하는 데이터베이스에서는 만들 수 있지만 대/소문자를 구분하지 않는 데이터베이스에서는 만들 수 없습니다. 자세한 내용은 [Database Identifiers](../../relational-databases/databases/database-identifiers.md)을 참조하세요.

변수, GOTO 레이블, 임시 저장 프로시저 및 임시 테이블은 연결 컨텍스트를 한 데이터베이스와 연결한 경우에 만들 수 있으며 컨텍스트를 다른 데이터베이스로 전환한 경우에 참조할 수 있습니다. 변수, GOTO 레이블, 임시 저장 프로시저 및 임시 테이블의 식별자는 서버 인스턴스의 기본 데이터 정렬에 있습니다.

COLLATE 절은 **char**, **varchar**, **text**, **nchar**, **nvarchar** 및 **ntext** 데이터 형식에만 적용할 수 있습니다.

COLLATE는 *collate_name*을 사용하여 식, 열 정의 또는 데이터베이스 정의에 적용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬 또는 Windows 데이터 정렬의 이름을 참조하세요. *collation_name*에는 지정된 *Windows_collation_name* 또는 *SQL_collation_name*만 사용할 수 있으며 매개 변수에는 리터럴 값이 포함되어야 합니다. 변수나 식으로 *collation_name*을 나타낼 수 없습니다.

데이터 정렬은 설치할 때를 제외하고 일반적으로 데이터 정렬 이름으로 식별됩니다. 설치할 때는 Windows 데이터 정렬에 대해 루트 데이터 정렬 지정자(데이터 정렬 로캘)를 지정한 다음, 대소문자와 악센트를 구분하거나 구분하지 않는 정렬 옵션을 지정합니다.

시스템 함수인 [fn_helpcollations](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)를 실행하여 Windows 데이터 정렬과 SQL Server 데이터 정렬에 대해 유효한 모든 데이터 정렬 이름의 목록을 검색할 수 있습니다.

```sql
SELECT name, description
FROM fn_helpcollations();
```

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 해당 운영 체제에서 지원되는 코드 페이지만 지원할 수 있습니다. 데이터 정렬을 기반으로 하는 동작을 수행할 때마다 참조된 개체가 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬은 시스템에서 실행 중인 운영 체제가 지원하는 코드 페이지를 사용해야 합니다. 여기에는 다음과 같은 동작이 포함됩니다.

- 데이터베이스를 만들거나 변경할 때 데이터베이스에 대한 기본 데이터 정렬 지정
- 테이블을 만들거나 변경할 때 열에 대한 데이터 정렬 지정
- 데이터베이스를 복원하거나 연결할 때 데이터베이스의 기본 데이터 정렬과 데이터베이스 내의 모든 **char**, **varchar** 및 **text** 열 또는 매개 변수의 데이터 정렬은 반드시 운영 체제에서 지원되는 것이어야 합니다.

> [!NOTE]
> **char** 및 **varchar** 데이터 형식에 대해서는 코드 페이지 변환이 지원되지만 **text** 데이터 형식에 대해서는 지원되지 않습니다. 코드 페이지 변환 중 데이터가 손실되어도 보고되지 않습니다.
>
> 지정된 데이터 정렬 또는 참조된 개체가 사용하는 데이터 정렬에서 Windows가 지원하지 않는 코드 페이지를 사용하는 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 나타납니다.

## <a name="examples"></a>예

### <a name="a-specifying-collation-during-a-select"></a>A. SELECT 중 데이터 정렬 지정

다음 예에서는 간단한 테이블을 만든 후 행 4개를 삽입합니다. 그런 다음 테이블에서 데이터를 선택할 때 두 데이터 정렬을 적용하여 `Chiapas`가 서로 다르게 정렬되는 방식을 보여 줍니다.

```sql
CREATE TABLE Locations
(Place varchar(15) NOT NULL);
GO
INSERT Locations(Place) VALUES ('Chiapas'),('Colima')
                             , ('Cinco Rios'), ('California');
GO
--Apply an typical collation
SELECT Place FROM Locations
ORDER BY Place
COLLATE Latin1_General_CS_AS_KS_WS ASC;
GO
-- Apply a Spanish collation
SELECT Place FROM Locations
ORDER BY Place
COLLATE Traditional_Spanish_ci_ai ASC;
GO
```

다음은 첫 번째 쿼리의 결과입니다.

```output
Place
-------------
California
Chiapas
Cinco Rios
Colima
```

다음은 두 번째 쿼리의 결과입니다.

```output
Place
-------------
California
Cinco Rios
Colima
Chiapas
```

### <a name="b-additional-examples"></a>B. 추가 예

**COLLATE**를 사용하는 추가 예는 [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017#examples) 예제 **G. 데이터베이스 만들기 및 데이터 정렬 이름과 옵션 지정** 및 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md#alter_column) 예제 **V. 열 데이터 정렬 변경**을 참조하세요.

## <a name="see-also"></a>참고 항목

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)
- [데이터 정렬 선행 규칙](../../t-sql/statements/collation-precedence-transact-sql.md)
- [상수](../../t-sql/data-types/constants-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [선언 @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [테이블 데이터 형식](../../t-sql/data-types/table-transact-sql.md)
