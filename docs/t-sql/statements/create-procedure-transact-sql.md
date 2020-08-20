---
description: CREATE PROCEDURE(Transact-SQL)
title: CREATE PROCEDURE(Transact-SQL)
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PROC
- PROCEDURE
- CREATE PROCEDURE
- CREATE_PROC_TSQL
- PROCEDURE_TSQL
- CREATE PROC
- PROC_TSQL
- CREATE_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- table-valued parameters
- SET statement, stored procedures
- stored procedures [SQL Server], creating
- wildcard parameters [SQL Server]
- maximum size of stored procedures
- WITH RECOMPILE clause
- common language runtime [SQL Server], stored procedures
- CREATE PROCEDURE statement
- local temporary procedures [SQL Server]
- WITH ENCRYPTION clause
- output parameters [SQL Server]
- nesting stored procedures
- user-defined stored procedures [SQL Server]
- system stored procedures [SQL Server], creating
- deferred name resolution, stored procedures
- referenced tables [SQL Server]
- global temporary procedures [SQL Server]
- cursor data type
- temporary stored procedures [SQL Server]
- size [SQL Server], stored procedures
- automatic stored procedure execution
- creating stored procedures
ms.assetid: afe3d86d-c9ab-44e4-b74d-4e3dbd9cc58c
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 368c73b776b3aa9a8088ccd7d19fe1b28a56c1eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488146"
---
# <a name="create-procedure-transact-sql"></a>CREATE PROCEDURE(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Data Warehouse 및 병렬 데이터 웨어하우스에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CLR(공용 언어 런타임) 저장 프로시저를 만듭니다. 저장 프로시저는 다음과 같은 점에서 다른 프로그래밍 언어의 프로시저와 유사합니다.

- 입력 매개 변수를 받아 여러 값을 출력 매개 변수의 형태로 호출하는 프로시저 또는 일괄 처리에 반환합니다.
- 다른 프로시저 호출을 비롯하여 데이터베이스에서 작업을 수행하는 프로그래밍 문이 포함되어 있습니다.
- 호출하는 프로시저 또는 일괄 처리에 상태 값을 반환하여 성공 또는 실패 및 실패 원인을 나타냅니다.

이 명령문을 사용하여 현재 데이터베이스에 영구 프로시저를 만들거나 **tempdb** 데이터베이스에 임시 프로시저를 만들 수 있습니다.

> [!NOTE]
> 이 항목에서는 .NET Framework CLR을 SQL Server에 통합하는 방법에 대해 설명합니다. Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에는 CLR 통합이 적용되지 않습니다.

구문의 세부 사항을 건너 뛰고 기본 저장 프로시저에 대한 빠른 예제를 보려면 [간단한 예](#Simple)로 이동하세요.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql
-- Transact-SQL Syntax for Stored Procedures in SQL Server and Azure SQL Database

CREATE [ OR ALTER ] { PROC | PROCEDURE }
    [schema_name.] procedure_name [ ; number ]
    [ { @parameter [ type_schema_name. ] data_type }
        [ VARYING ] [ = default ] [ OUT | OUTPUT | [READONLY]
    ] [ ,...n ]
[ WITH <procedure_option> [ ,...n ] ]
[ FOR REPLICATION ]
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }
[;]

<procedure_option> ::=
    [ ENCRYPTION ]
    [ RECOMPILE ]
    [ EXECUTE AS Clause ]
```

```syntaxsql
-- Transact-SQL Syntax for CLR Stored Procedures

CREATE [ OR ALTER ] { PROC | PROCEDURE }
    [schema_name.] procedure_name [ ; number ]
    [ { @parameter [ type_schema_name. ] data_type }
        [ = default ] [ OUT | OUTPUT ] [READONLY]
    ] [ ,...n ]
[ WITH EXECUTE AS Clause ]
AS { EXTERNAL NAME assembly_name.class_name.method_name }
[;]
```

```syntaxsql
-- Transact-SQL Syntax for Natively Compiled Stored Procedures

CREATE [ OR ALTER ] { PROC | PROCEDURE } [schema_name.] procedure_name
    [ { @parameter data_type } [ NULL | NOT NULL ] [ = default ]
        [ OUT | OUTPUT ] [READONLY]
    ] [ ,... n ]
  WITH NATIVE_COMPILATION, SCHEMABINDING [ , EXECUTE AS clause ]
AS
{
  BEGIN ATOMIC WITH (set_option [ ,... n ] )
sql_statement [;] [ ... n ]
 [ END ]
}
 [;]

<set_option> ::=
    LANGUAGE = [ N ] 'language'
  | TRANSACTION ISOLATION LEVEL = { SNAPSHOT | REPEATABLE READ | SERIALIZABLE }
  | [ DATEFIRST = number ]
  | [ DATEFORMAT = format ]
  | [ DELAYED_DURABILITY = { OFF | ON } ]
```

```syntaxsql
-- Transact-SQL Syntax for Stored Procedures in Azure SQL Data Warehouse
-- and Parallel Data Warehouse

-- Create a stored procedure
CREATE { PROC | PROCEDURE } [ schema_name.] procedure_name
    [ { @parameterdata_type } [ OUT | OUTPUT ] ] [ ,...n ]
AS { [ BEGIN ] sql_statement [;][ ,...n ] [ END ] }
[;]
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

OR ALTER

**적용 대상**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1부터 시작)

프로시저가 이미 존재하는 경우 변경합니다.

*schema_name* 프로시저가 속한 스키마의 이름입니다. 프로시저는 스키마 바운드 개체입니다. 프로시저를 만들 때 스키마 이름을 지정하지 않으면 프로시저를 만드는 사용자의 기본 스키마가 자동으로 할당됩니다.

*procedure_name* 프로시저의 이름입니다. 프로시저 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 준수해야 하며 스키마 내에서 고유해야 합니다.

프로시저 이름을 지정할 때 **sp_** 접두사를 사용하지 않도록 합니다. 이 접두사는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 시스템 프로시저를 지정하는 데 사용됩니다. 이 접두사를 사용하면 같은 이름의 시스템 프로시저가 있을 경우 애플리케이션 코드가 손상될 수 있습니다.

로컬 임시 프로시저의 경우 *procedure_name* 앞에 숫자 기호(#)를 하나 사용하고( *#procedure_name*) 전역 임시 프로시저의 경우 숫자 기호를 두 개 사용하여( *##procedure_name*) 로컬 또는 전역 임시 프로시저를 각각 만들 수 있습니다. 로컬 임시 프로시저는 해당 프로시저를 만든 연결에만 표시되고 해당 연결을 닫을 때 삭제됩니다. 전역 임시 프로시저는 모든 연결에서 사용할 수 있고 해당 프로시저를 사용하는 마지막 세션이 종료될 때 삭제됩니다. CLR 프로시저에는 임시 이름을 지정할 수 없습니다.

프로시저 또는 전역 임시 프로시저의 전체 이름은 ##을 포함하여 128자를 초과할 수 없습니다. 로컬 임시 프로시저의 전체 이름은 #을 포함하여 116자를 초과할 수 없습니다.

**;** *number*

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

같은 이름의 프로시저를 그룹화하는 데 사용하는 정수입니다(선택 사항). 이렇게 그룹화된 프로시저는 DROP PROCEDURE 문 하나를 사용하여 한꺼번에 삭제할 수 있습니다.

> [!NOTE]
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]

번호가 매겨진 프로시저는 **xml** 또는 CLR 사용자 정의 형식을 사용할 수 없으며 계획 지침에 사용될 수 없습니다.

**@** *parameter* 프로시저에 선언된 매개 변수입니다. at 기호( **@** )를 첫 번째 문자로 사용하여 매개 변수 이름을 지정합니다. 매개 변수 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다. 매개 변수는 프로시저에서 로컬로 사용되므로 다른 프로시저에서 동일한 매개 변수 이름을 사용할 수 있습니다.

하나 이상의 매개 변수를 선언할 수 있으며 최대 2,100개까지 선언할 수 있습니다. 선언된 각 매개 변수의 값은 기본값이 정의된 경우나 다른 매개 변수와 값이 같도록 설정된 경우를 제외하면 프로시저가 호출될 때 사용자가 지정해야 합니다. 프로시저에 [테이블 반환 매개 변수](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)가 포함되어 있고 호출에 매개 변수가 없는 경우 빈 테이블이 전달됩니다. 매개 변수는 상수 식 대신 사용할 수 있지만 테이블 이름, 열 이름 또는 다른 데이터베이스 개체의 이름 대신 사용할 수는 없습니다. 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)을 참조하세요.

FOR REPLICATION을 지정하면 매개 변수를 선언할 수 없습니다.

[ _type\_schema\_name_ **.** ] *data_type* 매개 변수의 데이터 형식 및 해당 데이터 형식이 속하는 스키마입니다.

**[!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저에 대한 지침**:

- 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터 형식을 매개 변수로 사용할 수 있습니다.
- 사용자 정의 테이블 형식을 사용하여 테이블 반환 매개 변수를 만들 수 있습니다. 테이블 반환 매개 변수는 INPUT 매개 변수로만 지정할 수 있으며 READONLY 키워드와 함께 사용해야 합니다. 자세한 내용은 [테이블 반환 매개 변수 사용&#40;데이터베이스 엔진&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)을 참조하세요.
- **cursor** 데이터 형식은 OUTPUT 매개 변수로만 지정할 수 있으며 VARYING 키워드와 함께 사용해야 합니다.

**CLR 프로시저에 대한 지침**:

- 관리 코드에 해당 형식이 있는 모든 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 매개 변수로 사용할 수 있습니다. CLR 형식과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식 간의 관계에 대한 자세한 내용은 [CLR 매개 변수 데이터 매핑](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)을 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식과 해당 구문에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.

- 테이블 반환 데이터 형식이나 **cursor** 데이터 형식은 매개 변수로 사용할 수 없습니다.
- 매개 변수의 데이터 형식이 CLR 사용자 정의 형식인 경우 해당 형식에 대해 EXECUTE 권한이 있어야 합니다.

VARYING 결과 집합이 출력 매개 변수로 사용되도록 지정합니다. 이 매개 변수는 프로시저에 의해 동적으로 생성될 수 있으며 해당 내용은 여러 가지가 될 수 있습니다. **cursor** 매개 변수에만 적용됩니다. CLR 프로시저에는 이 옵션이 유효하지 않습니다.

*default* 매개 변수의 기본값을 지정합니다. 매개 변수에 대해 기본값이 정의되어 있으면 해당 매개 변수 값을 지정하지 않아도 프로시저를 실행할 수 있습니다. 기본값은 상수이거나 NULL입니다. 상수 값을 와일드카드 형태로 지정할 수 있으므로 프로시저에 매개 변수를 전달할 때 LIKE 키워드를 사용할 수 있습니다.

기본값은 CLR 프로시저의 경우에만 **sys.parameters.default** 열에 기록됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저 매개 변수의 경우 이 열은 NULL입니다.

OUT | OUTPUT 매개 변수가 출력 매개 변수임을 나타냅니다. OUTPUT 매개 변수를 사용하여 프로시저의 호출자에 값을 반환할 수 있습니다. 프로시저가 CLR 프로시저가 아니면 **text**, **ntext** 및 **image** 매개 변수를 OUTPUT 매개 변수로 사용할 수 없습니다. 프로시저가 CLR 프로시저가 아닐 경우 출력 매개 변수는 커서 자리 표시자일 수 있습니다. 테이블 반환 데이터 형식은 프로시저의 OUTPUT 매개 변수로 지정할 수 없습니다.

READONLY 프로시저 본문 내에서 매개 변수를 업데이트하거나 수정할 수 없음을 나타냅니다. 매개 변수 형식이 테이블 반환 형식인 경우 READONLY를 지정해야 합니다.

RECOMPILE [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 현재 프로시저의 쿼리 계획을 캐시하지 않고 프로시저가 실행될 때마다 컴파일한다는 것을 나타냅니다. 다시 컴파일을 적용하는 이유에 대한 자세한 내용은 [저장 프로시저 다시 컴파일](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)을 참조하세요. CLR 프로시저에 대해 FOR REPLICATION을 지정한 경우에는 이 옵션을 사용할 수 없습니다.

[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 프로시저 안에 있는 개별 쿼리에 대한 쿼리 계획을 삭제하도록 하려면 쿼리 정의에서 RECOMPILE 쿼리 힌트를 사용합니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.

ENCRYPTION

**적용 대상**: SQL Server([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 CREATE PROCEDURE 문의 원본 텍스트를 난독 처리된 형식으로 변환하는 것을 나타냅니다. 난독 처리된 출력은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 카탈로그 뷰 어디에서도 직접 표시되지 않습니다. 시스템 테이블 또는 데이터베이스 파일에 대한 액세스 권한이 없는 사용자는 변조된 텍스트를 검색할 수 없습니다. 하지만 [DAC 포트](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)를 통해 시스템 테이블에 액세스하거나 데이터베이스 파일에 직접 액세스할 수 있는 권한이 있는 사용자는 난독 처리된 텍스트를 사용할 수 있습니다. 또한 디버거를 서버 프로세스에 연결할 수 있는 사용자는 런타임에 메모리에서 해독된 프로시저를 검색할 수 있습니다. 시스템 메타데이터에 액세스하는 방법에 대한 자세한 내용은 [메타데이터 표시 유형 구성](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.

CLR 프로시저에는 이 옵션이 유효하지 않습니다.

이 옵션을 사용하여 만든 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제의 일부로 게시할 수 없습니다.

EXECUTE AS *clause* 프로시저를 실행할 보안 컨텍스트를 지정합니다.

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 고유하게 컴파일된 저장 프로시저의 경우 EXECUTE AS 절에 대한 제한이 없습니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]의 경우 SELF, OWNER 및 *‘user_name’* 절이 고유하게 컴파일된 저장 프로시저에서 지원됩니다.

자세한 내용은 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)을 참조하세요.

FOR REPLICATION

**적용 대상**: SQL Server([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

프로시저가 복제용으로 생성되도록 지정합니다. 따라서 구독자에서는 프로시저를 실행할 수 없습니다. FOR REPLICATION 옵션을 사용하여 만든 프로시저는 프로시저 필터로 사용되며 복제하는 동안에만 실행됩니다. FOR REPLICATION을 지정하면 매개 변수를 선언할 수 없습니다. CLR 프로시저에는 FOR REPLICATION을 지정할 수 없습니다. FOR REPLICATION으로 만든 프로시저의 경우 RECOMPILE 옵션이 무시됩니다.

`FOR REPLICATION` 프로시저는 **sys.objects** 및 **sys.procedures**에 개체 형식 **RF**가 있습니다.

{ [ BEGIN ] *sql_statement* [;] [ ...*n* ] [ END ] } 프로시저의 본문을 구성하는 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. 선택적 키워드인 BEGIN과 END를 사용하여 문을 묶을 수 있습니다. 자세한 내용은 다음에 나오는 최선의 구현 방법, 일반적인 주의 사항 및 제한 사항 섹션을 참조하세요.

EXTERNAL NAME _assembly\_name_ **.** _class\_name_ **.** _method\_name_

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

CLR 저장 프로시저가 참조할 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 어셈블리의 메서드를 지정합니다. *class_name*은 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자여야 하며 어셈블리에서 클래스로 존재해야 합니다. 클래스가 마침표( **.** )를 사용하여 네임스페이스 부분을 구분하는 네임스페이스로 한정된 이름을 가질 경우 클래스 이름은 대괄호( **[]** ) 또는 큰따옴표( **""** )를 사용하여 구분되어야 합니다. 지정한 메서드는 해당 클래스의 정적 메서드여야 합니다.

기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CLR 코드를 실행할 수 없습니다. 공용 언어 런타임 모듈을 참조하는 데이터베이스 개체를 생성, 수정 및 삭제할 수 있지만 [clr enabled 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)을 설정할 때까지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이러한 참조를 실행할 수 없습니다. 이 옵션을 설정하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용합니다.

> [!NOTE]
> CLR 프로시저는 포함된 데이터베이스에서 지원되지 않습니다.

ATOMIC WITH

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

원자성 저장 프로시저 실행을 나타냅니다. 변경 내용이 커밋되거나 모든 변경 내용이 예외를 발생하고 롤백됩니다. ATOMIC WITH 블록은 고유하게 컴파일된 저장 프로시저에 필요합니다.

명시적으로 RETRUN 문을 사용하거나 암시적으로 실행을 완료해서 프로시저가 RETURN되면 프로시저로 수행된 작업이 커밋됩니다. 프로시저가 THROW하면 프로시저로 수행된 작업이 롤백됩니다.

XACT_ABORT는 기본적으로 원자성 블록 내에서 ON이며 변경할 수 없습니다. XACT_ABORT는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문이 런타임 오류를 일으킬 때 [!INCLUDE[tsql](../../includes/tsql-md.md)]가 현재 트랜잭션을 자동으로 롤백할지 여부를 지정합니다.

 다음 SET 옵션은 ATOMIC 블록에서 항상 ON이며 이 옵션은 변경할 수 없습니다.

- CONCAT_NULL_YIELDS_NULL
- QUOTED_IDENTIFIER, ARITHABORT
- NOCOUNT
- ANSI_NULLS
- ANSI_WARNINGS

SET 옵션은 ATOMIC 블록 내에서 변경할 수 없습니다. 사용자 세션에서 SET 옵션은 고유하게 컴파일된 저장 프로시저의 범위에 사용되지 않습니다. 이러한 옵션은 컴파일 시에 고정됩니다.

BEGIN, ROLLBACK 및 COMMIT 작업은 원자성 블록 내에서 사용할 수 없습니다.

프로시저 외부 범위에 고유하게 컴파일된 저장 프로시저당 한 개의 ATOMIC 블록이 있습니다. 블록은 중첩될 수 없습니다. Atomic 블록에 대한 자세한 내용은 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)를 참조하세요.

**NULL** | NOT NULL 매개 변수의 Null 값 허용 여부를 결정합니다. NULL이 기본값입니다.

NATIVE_COMPILATION

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

프로시저가 고유하게 컴파일되었음을 나타냅니다. NATIVE_COMPILATION, SCHEMABINDING 및 EXECUTE AS는 임의 순서로 지정할 수 있습니다. 자세한 내용은 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)를 참조하세요.

SCHEMABINDING

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

프로시저에서 참조되는 테이블을 삭제 또는 변경할 수 없도록 보장합니다. SCHEMABINDING은 고유하게 컴파일된 저장 프로시저에 필요합니다. (자세한 내용은 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)를 참조하세요.) SCHEMABINDING 제한은 사용자 정의 함수의 경우와 동일합니다. 자세한 내용은 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)에서 SCHEMABINDING 섹션을 참조하세요.

LANGUAGE = [N] '언어'

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

[SET LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md) 세션 옵션에 해당합니다. LANGUAGE = [N] '언어'는 필수입니다.

TRANSACTION ISOLATION LEVEL

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

고유하게 컴파일된 저장 프로시저에 필요합니다. 저장 프로시저의 트랜잭션 격리 수준을 지정합니다. 옵션은 다음과 같습니다.

이러한 옵션에 대한 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.

REPEATABLE READ 다른 트랜잭션에 의해 수정되었지만 커밋되지 않은 데이터를 문에서 읽을 수 없도록 지정합니다. 현재 트랜잭션에서 읽은 데이터를 다른 트랜잭션이 수정할 경우 현재 트랜잭션이 실패합니다.

SERIALIZABLE 다음을 지정합니다.

- 문은 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 데이터를 읽을 수 없습니다.
- 현재 트랜잭션에서 읽은 데이터를 다른 트랜잭션이 수정할 경우 현재 트랜잭션이 실패합니다.
- 현재 트랜잭션의 명령문에서 읽은 키의 범위에 속하는 키 값이 포함된 새 행을 다른 트랜잭션이 삽입하면 현재 트랜잭션이 실패합니다.

SNAPSHOT 트랜잭션의 문에서 읽은 데이터가 트랜잭션 시작 부분에 존재하는 데이터의 트랜잭션이 일치되는 버전이 되도록 지정합니다.

DATEFIRST = *number*

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

일주일의 시작 요일을 1부터 7까지의 숫자로 지정합니다. DATEFIRST는 선택 사항입니다. 지정하지 않으면 지정된 언어로부터 설정이 유추됩니다.

자세한 내용은 [SET DATEFIRST&#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md)를 참조하세요.

DATEFORMAT = *format*

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

date, smalldatetime, datetime, datetime2 및 datetimeoffset 문자열 해석을 위한 월, 일 및 연도 날짜 부분의 순서를 지정합니다. DATEFORMAT은 선택 사항입니다. 지정하지 않으면 지정된 언어로부터 설정이 유추됩니다.

자세한 내용은 [SET DATEFORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md)을 참조하세요.

DELAYED_DURABILITY = { OFF | ON }

**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션은 완전 내구성이 있는(기본값) 커밋 또는 지연된 내구성이 있는 커밋을 수행할 수 있습니다.

자세한 내용은 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md)를 참조하세요.

## <a name="simple-examples"></a><a name="Simple"></a> 간단한 예

다음은 시작하는 데 도움이 되는 두 가지 간단한 예제입니다. `SELECT DB_NAME() AS ThisDB;`는 현재 데이터베이스의 이름을 반환합니다.
저장 프로시저에서 이 명령문을 다음과 같이 래핑할 수 있습니다.

```sql
CREATE PROC What_DB_is_this
AS
SELECT DB_NAME() AS ThisDB;
```

`EXEC What_DB_is_this;` 문으로 저장 프로시저 호출

좀더 복잡한 방법은 입력 매개 변수를 제공하여 프로시저의 유연성을 높이는 것입니다. 예를 들면 다음과 같습니다.

```sql
CREATE PROC What_DB_is_that @ID INT
AS
SELECT DB_NAME(@ID) AS ThatDB;
```

프로시저를 호출할 때 데이터베이스 ID 번호를 제공합니다. 예를 들어 `EXEC What_DB_is_that 2;`는 `tempdb`를 반환합니다.

더 많은 예제를 보려면 이 토픽 끝에 있는 [예제](#Examples)를 참조하세요.

## <a name="best-practices"></a>모범 사례

여기에 제시된 최선의 구현 방법은 일부에 불과하지만 이를 적절히 참고하면 프로시저 성능을 개선하는 데 도움이 됩니다.

- 프로시저 본문에서 SET NOCOUNT ON 문을 첫 번째 문으로 사용합니다. 즉, 이 문을 AS 키워드 바로 다음에 배치합니다. 이렇게 하면 SELECT, INSERT, UPDATE, MERGE 및 DELETE 문이 실행된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 클라이언트로 보내는 메시지가 해제됩니다. 그러면 투명도를 위해 생성된 출력이 최소 수준으로 유지됩니다. 그러나 현재의 하드웨어에서는 측정 가능한 성능 혜택이 없습니다. 자세한 내용은 [SET NOCOUNT&#40;Transact-SQL&#41;](../../t-sql/statements/set-nocount-transact-sql.md)를 참조하세요.
- 프로시저에서 데이터베이스 개체를 만들거나 참조할 때 스키마 이름을 사용합니다. 여러 스키마를 검색할 필요가 없는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 개체 이름을 확인하기 위한 처리 시간이 줄어듭니다. 또한 스키마를 지정하지 않고 개체를 만들 경우 사용자의 기본 스키마 할당으로 인해 발생하는 권한 및 액세스 문제도 방지됩니다.
- WHERE 및 JOIN 절에서 지정한 열을 함수로 묶지 않도록 합니다. 함수로 묶을 경우 열이 비결정적 열이 되어 쿼리 프로세서에서 인덱스를 사용할 수 없습니다.
- 대량의 데이터 행을 반환하는 SELECT 문에서는 스칼라 함수를 사용하지 않도록 합니다. 스칼라 함수는 모든 행에 적용되어야 하므로 행 기반 처리와 비슷한 동작이 발생하여 성능이 저하됩니다.
- `SELECT *`를 사용을 피합니다. 대신 필요한 열 이름을 지정합니다. 이렇게 하면 프로시저 실행을 중지하는 몇몇 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 오류를 방지할 수 있습니다. 예를 들어, 12 열 테이블에서 데이터를 반환하고 이 데이터를 12 열 임시 테이블에 삽입하는 `SELECT *` 문은 두 테이블 중 하나에서 열의 개수나 순서가 변경되기 전까지 계속 실행됩니다.
- 너무 많은 데이터를 처리하거나 반환하지 않도록 합니다. 되도록 프로시저 코드의 앞 부분에서 결과를 좁혀 해당 프로시저에서 수행하는 이후의 작업은 가능하면 가장 적은 데이터 집합을 사용하여 완료되도록 합니다. 꼭 필요한 데이터를 클라이언트 애플리케이션에 보낼 수 있습니다. 이렇게 하면 네트워크를 통해 불필요한 데이터를 보내 클라이언트 애플리케이션에서 필요 없이 많은 결과 집합을 처리하지 않아도 되므로 효율적입니다.
- BEGIN/COMMIT TRANSACTION을 사용하여 명시적 트랜잭션을 사용하고 트랜잭션을 되도록 짧게 유지합니다. 트랜잭션이 길면 레코드 잠금 시간이 길어지고 교착 상태가 발생할 확률이 높아집니다.
- 프로시저 내의 오류 처리에 [!INCLUDE[tsql](../../includes/tsql-md.md)] TRY...CATCH 기능을 사용합니다. TRY...CATCH는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 전체 블록을 캡슐화할 수 있습니다. 따라서 성능 오버헤드가 줄어들 뿐만 아니라 대폭 줄어든 프로그래밍과 함께 오류 보고가 더욱 정확해집니다.
- 프로시저 본문에서 CREATE TABLE 또는 ALTER TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 참조하는 모든 테이블 열에 DEFAULT 키워드를 사용합니다. 이렇게 하면 Null 값을 허용하지 않는 열에 NULL이 전달되지 않습니다.
- 임시 테이블의 각 열에 NULL 또는 NOT NULL을 사용합니다. ANSI_DFLT_ON과 ANSI_DFLT_OFF 옵션은 CREATE TABLE 또는 ALTER TABLE 문에 NULL 또는 NOT NULL 특성이 지정되지 않은 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 열에 이러한 특성을 할당하는 방식을 제어합니다. 프로시저를 만든 연결과는 이 옵션 설정이 다른 프로시저를 연결이 실행하면 두 번째 연결에 만들어진 테이블의 열은 Null 허용 여부가 달라질 수 있으며 다른 동작을 나타낼 수 있습니다. 각 열에 NULL 또는 NOT NULL을 명시적으로 지정하면 프로시저를 실행하는 모든 연결에 대해 Null 허용 여부가 동일한 임시 테이블이 만들어집니다.
- Null 값을 변환하는 수정 문을 사용하고 Null 값을 포함하는 행을 쿼리에서 제거하는 논리를 포함합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 NULL은 비어 있거나 "없음"을 의미하는 것이 아니라 알 수 없는 값에 대한 자리 표시자를 나타냅니다. 이 NULL은 특히 결과 집합을 쿼리하거나 AGGREGATE 함수를 사용할 때 예기치 않은 동작을 야기할 수 있습니다.
- 고유 값에 대한 특별한 요구 사항이 있지 않으면 UNION 또는 OR 연산자 대신 UNION ALL 연산자를 사용합니다. UNION ALL 연산자를 사용할 경우 중복되는 항목이 결과 집합에서 필터링되지 않으므로 처리 오버헤드가 줄어듭니다.

## <a name="general-remarks"></a>일반적인 주의 사항

프로시저에는 미리 정의된 최대 크기가 없습니다.

프로시저 내에 지정한 변수는 @@SPID와 같은 시스템 변수이거나 사용자 정의 변수일 수 있습니다.

프로시저를 처음 실행하면 데이터 검색을 위한 최적 액세스 계획을 결정하기 위해 프로시저가 컴파일됩니다. 이후에 프로시저를 실행할 때는 이미 생성된 계획이 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 계획 캐시에 남아 있을 경우 해당 계획을 다시 사용할 수 있습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 시 하나 이상의 프로시저를 자동으로 실행할 수 있습니다. 이러한 프로시저는 시스템 관리자가 **master** 데이터베이스에 만들어야 하며 **sysadmin** 고정 서버 역할에서 백그라운드 프로세스로 실행되어야 합니다. 프로시저에 입력 또는 출력 매개 변수는 사용할 수 없습니다. 자세한 내용은 [저장 프로시저 실행](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)을 참조하세요.

프로시저가 다른 프로시저를 호출하거나 CRL 루틴, 형식 또는 집계를 참조하여 관리 코드를 실행하는 경우에 프로시저가 중첩됩니다. 프로시저와 관리 코드 참조는 최대 32 수준까지 중첩될 수 있습니다. 호출된 프로시저나 관리 코드 참조의 실행이 시작되면 중첩 수준이 하나 증가하고 호출된 프로시저나 관리 참조 코드의 실행이 끝나면 중첩 수준이 하나 감소합니다. 관리 코드 내에서 호출된 메서드는 중첩 수준 제한에 따라 계산되지 않습니다. 그러나 CLR 저장 프로시저가 SQL Server 관리 공급자를 통해 데이터 액세스 작업을 수행하면 관리 코드에서 SQL로의 전환에 추가적인 중첩 수준이 더해집니다.

최대 중첩 수준을 초과하려고 시도하면 전체 호출 체인이 끊어집니다. @@NESTLEVEL 함수를 사용하여 현재 저장 프로시저 실행에 대한 중첩 수준을 반환할 수 있습니다.

## <a name="interoperability"></a>상호 운용성

[!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저를 만들거나 수정할 때 SET QUOTED_IDENTIFIER와 SET ANSI_NULLS의 설정을 저장합니다. 프로시저를 실행할 때는 이러한 원래 설정이 사용됩니다. 따라서 프로시저 실행 시 SET QUOTED_IDENTIFIER와 SET ANSI_NULLS에 대한 클라이언트 세션 설정은 모두 무시됩니다.

SET ARITHABORT, SET ANSI_WARNINGS, SET ANSI_PADDINGS 등의 기타 SET 옵션은 프로시저를 만들거나 수정할 때 저장되지 않습니다. 프로시저의 논리가 특정 설정에 따라 좌우될 경우 적합한 설정을 위해 프로시저 시작 부분에 SET 문을 포함합니다. 프로시저에서 SET 문을 실행할 경우 해당 설정은 프로시저의 실행이 완료될 때까지만 유지됩니다. 그런 다음 프로시저가 호출되었을 때의 값으로 설정이 복원됩니다. 따라서 각 클라이언트는 프로시저의 논리에 영향을 주지 않고 원하는 옵션을 설정할 수 있습니다.

SET SHOWPLAN_TEXT와 SET SHOWPLAN_ALL을 제외한 모든 SET 문을 프로시저 내에 지정할 수 있습니다. 이러한 문은 일괄 처리에서 유일한 문이어야 합니다. 선택된 SET 옵션은 프로시저가 실행되는 동안만 유지되고 다시 원래 설정으로 돌아갑니다.

> [!NOTE]
> 프로시저 또는 사용자 정의 함수에 매개 변수를 전달할 때 또는 일괄 처리 문에서 변수를 선언하고 설정할 때 SET ANSI_WARNINGS는 인식되지 않습니다. 예를 들어 변수가 **char**(3)으로 정의된 경우 3자보다 큰 값으로 설정하면 해당 데이터가 정의된 크기로 잘리고 INSERT 또는 UPDATE 문은 성공합니다.

## <a name="limitations-and-restrictions"></a>제한 사항

CREATE PROCEDURE 문은 단일 일괄 처리에서 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 함께 사용할 수 없습니다.

다음 문은 저장 프로시저의 본문 어디에서도 사용할 수 없습니다.

| CREATE | SET | USE |
|--------|-----|-----|
| CREATE AGGREGATE | SET SHOWPLAN_TEXT | USE *database_name*|
| CREATE DEFAULT | SET SHOWPLAN_XML
| CREATE RULE | SET PARSEONLY |
| CREATE SCHEMA | SET SHOWPLAN_ALL |
| CREATE 또는 ALTER TRIGGER |
| CREATE 또는 ALTER FUNCTION |
| CREATE 또는 ALTER PROCEDURE |
| CREATE 또는 ALTER VIEW |

 프로시저는 아직 존재하지 않는 테이블을 참조할 수 있습니다. 프로시저를 만들 때는 구문 검사만 수행되며 처음 실행할 때까지는 프로시저가 컴파일되지 않습니다. 컴파일 중에만 프로시저에서 참조되는 모든 개체가 확인됩니다. 따라서 구문이 정확하면서 존재하지 않는 테이블을 참조하는 프로시저를 만들 수는 있지만 참조되는 테이블이 없을 경우 실행 시간에 오류가 발생합니다.

 프로시저 실행 시 매개 변수의 기본값이나 매개 변수로 전달되는 값으로 함수 이름을 지정할 수 없습니다. 그러나 다음 예와 같이 함수를 변수로 전달할 수 있습니다.

```sql
-- Passing the function value as a variable.
DECLARE @CheckDate DATETIME = GETDATE();
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;
GO
```

프로시저가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 원격 인스턴스에서 변경 작업을 수행하면 이러한 변경 내용은 롤백될 수 없습니다. 원격 프로시저는 트랜잭션에 포함되지 않습니다.

[!INCLUDE[ssDE](../../includes/ssde-md.md)]이 .NET Framework에서 오버로드될 때 올바른 메서드를 참조하려면 EXTERNAL NAME 절에 지정된 메서드에 다음과 같은 특징이 있어야 합니다.

- 정적 메서드로 선언되었습니다.
- 프로시저의 매개 변수 개수와 동일한 개수의 매개 변수를 받습니다.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로시저에 있는 해당 매개 변수의 데이터 형식과 호환되는 매개 변수 형식을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 일치하는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 형식에 대한 자세한 내용은 [CLR 매개 변수 데이터 매핑](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)을 참조하세요.

## <a name="metadata"></a>메타데이터

다음 테이블에서는 저장 프로시저에 대한 정보를 반환하는 데 사용할 수 있는 카탈로그 뷰 및 동적 관리 뷰를 나열합니다.

|보기|Description|
|----------|-----------------|
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저의 정의를 반환합니다. ENCRYPTION 옵션으로 만든 프로시저의 텍스트는 **sys.sql_modules** 카탈로그 뷰를 사용하여 볼 수 없습니다.|
|[sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|CLR 프로시저 정보를 반환합니다.|
|[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|프로시저에서 정의된 매개 변수 정보를 반환합니다.|
|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)|프로시저에서 참조하는 개체를 반환합니다.|

컴파일된 프로시저의 크기를 예측하려면 다음과 같은 성능 모니터 카운터를 사용합니다.

|성능 모니터 개체 이름|성능 모니터 카운터 이름|
|-------------------------------------|--------------------------------------|
|SQLServer: 플랜 캐시 개체|캐시 적중률|
||Cache Pages|
||Cache Object Counts*|

\* 이 카운터는 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)], 준비된 [!INCLUDE[tsql](../../includes/tsql-md.md)], 프로시저, 트리거 등 여러 종류의 캐시 개체에서 사용할 수 있습니다. 자세한 내용은 [SQL Server, Plan Cache 개체](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)를 참조하세요.

## <a name="security"></a>보안

### <a name="permissions"></a>사용 권한

데이터베이스에 대한 **CREATE PROCEDURE** 권한과 프로시저를 만들고 있는 스키마에 대한 **ALTER** 권한이 필요하거나 **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격이 필요합니다.

CLR 저장 프로시저의 경우 EXTERNAL NAME 절에서 참조되는 어셈블리에 대한 소유권 또는 해당 어셈블리에 대한 **REFERENCES** 권한이 필요합니다.

## <a name="create-procedure-and-memory-optimized-tables"></a><a name="mot"></a> CREATE PROCEDURE 및 메모리 최적화 테이블

메모리 최적화 테이블은 기존 및 고유하게 컴파일된 저장 프로시저를 통해 액세스할 수 있습니다. 네이티브 프로시저는 대부분의 경우에 효율적인 방법입니다. 자세한 내용은 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)를 참조하세요.

다음 샘플은 메모리 최적화 테이블 `dbo.Departments`에 액세스하는 고유하게 컴파일된 저장 프로시저를 만드는 방법을 보여줍니다.

```sql
CREATE PROCEDURE dbo.usp_add_kitchen @dept_id INT, @kitchen_count INT NOT NULL
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION
AS
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')

UPDATE dbo.Departments
SET kitchen_count = ISNULL(kitchen_count, 0) + @kitchen_count
WHERE ID = @dept_id
END;
GO
```

 NATIVE_COMPILATION 없이 만든 프로시저는 고유하게 컴파일된 저장 프로시저로 변경할 수 없습니다.

 고유하게 컴파일된 저장 프로시저, 지원되는 쿼리 노출 영역 및 연산자의 프로그래밍 기능에 대한 자세한 내용은 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)을 참조하세요.

## <a name="examples"></a><a name="Examples"></a> 예

|범주|중요한 구문 요소|
|--------------|------------------------------|
|[기본 구문](#BasicSyntax)|CREATE PROCEDURE|
|[매개 변수 전달](#Parameters)|@parameter <br> &nbsp;&nbsp;• = default <br> &nbsp;&nbsp; • OUTPUT <br> &nbsp;&nbsp; • 테이블 반환 매개 변수 <br> &nbsp;&nbsp; • CURSOR VARYING|
|[저장 프로시저를 사용하여 데이터 수정](#Modify)|UPDATE|
|[오류 처리](#Error)|TRY...CATCH|
|[프로시저 정의 난독 처리](#Encrypt)|WITH ENCRYPTION|
|[프로시저의 다시 컴파일 강제 수행](#Recompile)|WITH RECOMPILE|
|[보안 컨텍스트 설정](#Security)|EXECUTE AS|

### <a name="basic-syntax"></a><a name="BasicSyntax"></a> 기본 구문

이 섹션의 예에서는 최소 필수 구문을 사용하여 CREATE PROCEDURE 문의 기본 기능을 보여 줍니다.

#### <a name="a-creating-a-simple-transact-sql-procedure"></a>A. 단순 Transact-SQL 프로시저 만들기

다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 뷰에서 모든 직원(성과 이름 제공), 직함 및 부서 이름을 반환하는 저장 프로시저를 만듭니다. 이 프로시저는 매개 변수를 사용하지 않습니다. 다음 예에서는 세 가지의 프로시저 실행 방법에 대해 설명합니다.

```sql
CREATE PROCEDURE HumanResources.uspGetAllEmployees
AS
    SET NOCOUNT ON;
    SELECT LastName, FirstName, JobTitle, Department
    FROM HumanResources.vEmployeeDepartment;
GO

SELECT * FROM HumanResources.vEmployeeDepartment;
```

`uspGetEmployees` 프로시저는 다음과 같은 방법으로 실행할 수 있습니다.

```sql
EXECUTE HumanResources.uspGetAllEmployees;
GO
-- Or
EXEC HumanResources.uspGetAllEmployees;
GO
-- Or, if this procedure is the first statement within a batch:
HumanResources.uspGetAllEmployees;
```

#### <a name="b-returning-more-than-one-result-set"></a>B. 둘 이상의 결과 집합 반환

다음 프로시저는 두 개의 결과 집합을 반환합니다.

```sql
CREATE PROCEDURE dbo.uspMultipleResults
AS
SELECT TOP(10) BusinessEntityID, Lastname, FirstName FROM Person.Person;
SELECT TOP(10) CustomerID, AccountNumber FROM Sales.Customer;
GO
```

#### <a name="c-creating-a-clr-stored-procedure"></a>C. CLR 저장 프로시저 만들기

다음 예에서는 `HandlingLOBUsingCLR`어셈블리에 있는 `LargeObjectBinary` 클래스의 `GetPhotoFromDB` 메서드를 참조하는 `GetPhotoFromDB` 프로시저를 만듭니다. 프로시저를 만들기 전에 `HandlingLOBUsingCLR` 어셈블리가 로컬 데이터베이스에 등록됩니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)](*assembly_bits*에서 생성된 어셈블리를 사용하는 경우)

```sql
CREATE ASSEMBLY HandlingLOBUsingCLR
FROM '\\MachineName\HandlingLOBUsingCLR\bin\Debug\HandlingLOBUsingCLR.dll';
GO
CREATE PROCEDURE dbo.GetPhotoFromDB
(
    @ProductPhotoID INT
    , @CurrentDirectory NVARCHAR(1024)
    , @FileName NVARCHAR(1024)
)
AS EXTERNAL NAME HandlingLOBUsingCLR.LargeObjectBinary.GetPhotoFromDB;
GO
```

### <a name="passing-parameters"></a><a name="Parameters"></a> 매개 변수 전달

이 섹션의 예에서는 입력 및 출력 매개 변수를 통해 값을 저장 프로시저로 전달 및 저장 프로시저에서 값을 전달하는 방법을 보여 줍니다.

#### <a name="d-creating-a-procedure-with-input-parameters"></a>D. 입력 매개 변수가 있는 프로시저 만들기

다음 예에서는 직원의 성과 이름에 대한 값을 전달하여 특정 직원 정보를 반환하는 저장 프로시저를 만듭니다. 이 프로시저는 전달된 매개 변수와 정확히 일치하는 항목만 받습니다.

```sql
IF OBJECT_ID ( 'HumanResources.uspGetEmployees', 'P' ) IS NOT NULL
    DROP PROCEDURE HumanResources.uspGetEmployees;
GO
CREATE PROCEDURE HumanResources.uspGetEmployees
    @LastName NVARCHAR(50),
    @FirstName NVARCHAR(50)
AS

    SET NOCOUNT ON;
    SELECT FirstName, LastName, JobTitle, Department
    FROM HumanResources.vEmployeeDepartment
    WHERE FirstName = @FirstName AND LastName = @LastName;
GO

```

`uspGetEmployees` 프로시저는 다음과 같은 방법으로 실행할 수 있습니다.

```sql
EXECUTE HumanResources.uspGetEmployees N'Ackerman', N'Pilar';
-- Or
EXEC HumanResources.uspGetEmployees @LastName = N'Ackerman', @FirstName = N'Pilar';
GO
-- Or
EXECUTE HumanResources.uspGetEmployees @FirstName = N'Pilar', @LastName = N'Ackerman';
GO
-- Or, if this procedure is the first statement within a batch:
HumanResources.uspGetEmployees N'Ackerman', N'Pilar';

```

#### <a name="e-using-a-procedure-with-wildcard-parameters"></a>E. 프로시저에 와일드카드 매개 변수 사용

다음 예에서는 직원의 성과 이름에 대한 전체 또는 일부 값을 전달하여 직원 정보를 반환하는 저장 프로시저를 만듭니다. 이 프로시저는 전달된 매개 변수에 패턴 일치를 사용하고 매개 변수가 없으면 미리 설정된 기본값(`D`로 시작되는 성)을 사용합니다.

```sql
IF OBJECT_ID ( 'HumanResources.uspGetEmployees2', 'P' ) IS NOT NULL
    DROP PROCEDURE HumanResources.uspGetEmployees2;
GO
CREATE PROCEDURE HumanResources.uspGetEmployees2
    @LastName NVARCHAR(50) = N'D%',
    @FirstName NVARCHAR(50) = N'%'
AS
    SET NOCOUNT ON;
    SELECT FirstName, LastName, JobTitle, Department
    FROM HumanResources.vEmployeeDepartment
    WHERE FirstName LIKE @FirstName AND LastName LIKE @LastName;
```

`uspGetEmployees2` 프로시저는 여러 가지 조합으로 실행할 수 있습니다. 다음에 표시된 것은 이 중 일부입니다.

```sql
EXECUTE HumanResources.uspGetEmployees2;
-- Or
EXECUTE HumanResources.uspGetEmployees2 N'Wi%';
-- Or
EXECUTE HumanResources.uspGetEmployees2 @FirstName = N'%';
-- Or
EXECUTE HumanResources.uspGetEmployees2 N'[CK]ars[OE]n';
-- Or
EXECUTE HumanResources.uspGetEmployees2 N'Hesse', N'Stefen';
-- Or
EXECUTE HumanResources.uspGetEmployees2 N'H%', N'S%';
```

#### <a name="f-using-output-parameters"></a>F. OUTPUT 매개 변수 사용

다음 예에서는 `uspGetList` 프로시저를 만듭니다. 이 프로시저에서는 가격이 지정한 금액을 초과하지 않는 제품 목록을 반환합니다. 다음 예에서는 여러 `SELECT` 문과 여러 `OUTPUT` 매개 변수의 사용 방법을 보여 줍니다. OUTPUT 매개 변수는 프로시저를 실행하는 동안 외부 프로시저, 일괄 처리 또는 둘 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 값 집합을 액세스하도록 허용합니다.

```sql
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL
    DROP PROCEDURE Production.uspGetList;
GO  
CREATE PROCEDURE Production.uspGetList @Product VARCHAR(40)
    , @MaxPrice MONEY
    , @ComparePrice MONEY OUTPUT
    , @ListPrice MONEY OUT
AS  
    SET NOCOUNT ON;
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'
    FROM Production.Product AS p
    JOIN Production.ProductSubcategory AS s
      ON p.ProductSubcategoryID = s.ProductSubcategoryID
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;
-- Populate the output variable @ListPprice.
SET @ListPrice = (SELECT MAX(p.ListPrice)
    FROM Production.Product AS p
    JOIN Production.ProductSubcategory AS s
      ON p.ProductSubcategoryID = s.ProductSubcategoryID
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);
-- Populate the output variable @compareprice.
SET @ComparePrice = @MaxPrice;
GO
```

`uspGetList`를 실행하여 가격이 `$700` 미만인 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 제품(자전거) 목록을 반환합니다. `OUTPUT` 매개 변수인 `@Cost`와 `@ComparePrices`는 **메시지** 창의 메시지를 반환하기 위해 흐름 제어 언어와 함께 사용됩니다.

> [!NOTE]
> 프로시저가 만들어질 때뿐 아니라 변수가 사용될 때도 OUTPUT 변수를 정의해야 합니다. 매개 변수 이름과 변수 이름은 일치하지 않아도 되지만 `@ListPrice` = *variable*을 사용하지 않는 한 데이터 형식과 매개 변수 위치가 일치해야 합니다.

```sql
DECLARE @ComparePrice MONEY, @Cost MONEY;
EXECUTE Production.uspGetList '%Bikes%', 700,
    @ComparePrice OUT,
    @Cost OUTPUT
IF @Cost <= @ComparePrice
BEGIN
    PRINT 'These products can be purchased for less than
    $'+RTRIM(CAST(@ComparePrice AS VARCHAR(20)))+'.'
END
ELSE
    PRINT 'The prices for all products in this category exceed
    $'+ RTRIM(CAST(@ComparePrice AS VARCHAR(20)))+'.';
```

다음은 결과 집합의 일부입니다.

```
Product                     List Price
--------------------------  ----------
Road-750 Black, 58          539.99
Mountain-500 Silver, 40     564.99
Mountain-500 Silver, 42     564.99
...
Road-750 Black, 48          539.99
Road-750 Black, 52          539.99

(14 row(s) affected)

These items can be purchased for less than $700.00.
```

#### <a name="g-using-a-table-valued-parameter"></a>G. 테이블 반환 매개 변수 사용

다음 예에서는 테이블 반환 매개 변수 유형을 사용하여 테이블에 여러 행을 삽입합니다. 다음 예에서는 매개 변수 유형을 만들고, 해당 형식을 참조하는 테이블 변수를 선언하며, 매개 변수 목록을 채운 다음 저장 프로시저에 값을 전달하는 방법을 보여 줍니다. 저장 프로시저는 해당 값을 사용하여 테이블에 여러 행을 삽입합니다.

```sql
/* Create a table type. */
CREATE TYPE LocationTableType AS TABLE
( LocationName VARCHAR(50)
, CostRate INT );
GO

/* Create a procedure to receive data for the table-valued parameter. */
CREATE PROCEDURE usp_InsertProductionLocation
    @TVP LocationTableType READONLY
    AS
    SET NOCOUNT ON
    INSERT INTO [AdventureWorks2012].[Production].[Location]
       ([Name]
       , [CostRate]
       , [Availability]
       , [ModifiedDate])
    SELECT *, 0, GETDATE()
    FROM @TVP;
GO

/* Declare a variable that references the type. */
DECLARE @LocationTVP
AS LocationTableType;

/* Add data to the table variable. */
INSERT INTO @LocationTVP (LocationName, CostRate)
    SELECT [Name], 0.00
    FROM
    [AdventureWorks2012].[Person].[StateProvince];

/* Pass the table variable data to a stored procedure. */
EXEC usp_InsertProductionLocation @LocationTVP;
GO
```

##### <a name="h-using-an-output-cursor-parameter"></a>H. OUTPUT 커서 매개 변수 사용

다음 예에서는 프로시저에서 로컬로 사용되는 커서를 호출한 일괄 처리, 프로시저 또는 트리거에 다시 전달하는 OUTPUT 커서 매개 변수를 사용합니다.

먼저 커서를 선언하여 `Currency` 테이블에서 여는 프로시저를 만듭니다.

```sql
CREATE PROCEDURE dbo.uspCurrencyCursor
    @CurrencyCursor CURSOR VARYING OUTPUT
AS
    SET NOCOUNT ON;
    SET @CurrencyCursor = CURSOR
    FORWARD_ONLY STATIC FOR
      SELECT CurrencyCode, Name
      FROM Sales.Currency;
    OPEN @CurrencyCursor;
GO
```

다음으로 로컬 커서 변수를 선언하는 일괄 처리를 실행하고 지역 변수에 커서를 할당하는 프로시저를 실행한 다음 커서에서 행을 인출합니다.

```sql
DECLARE @MyCursor CURSOR;
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;
WHILE (@@FETCH_STATUS = 0)
BEGIN;
    FETCH NEXT FROM @MyCursor;
END;
CLOSE @MyCursor;
DEALLOCATE @MyCursor;
GO
```

### <a name="modifying-data-by-using-a-stored-procedure"></a><a name="Modify"></a> 저장 프로시저를 사용하여 데이터 수정

이 섹션의 예에서는 프로시저 정의에 DML(데이터 조작 언어) 문을 포함해 테이블 또는 뷰에 있는 데이터를 삽입하거나 수정하는 방법을 보여 줍니다.

#### <a name="i-using-update-in-a-stored-procedure"></a>9\. 저장 프로시저에 UPDATE 사용

다음 예에서는 저장 프로시저에 UPDATE 문을 사용합니다. 이 프로시저에서는 `@NewHours`라는 입력 매개 변수 하나와 `@RowCount`라는 출력 매개 변수 하나를 사용합니다. UPDATE 문에 사용된 `@NewHours` 매개 변수 값은 `HumanResources.Employee` 테이블의 `VacationHours` 열을 업데이트합니다. `@RowCount` 출력 매개 변수는 영향을 받는 행 수를 지역 변수에 반환하는 데 사용됩니다. CASE 식은 SET 절에서 `VacationHours`에 설정되는 값을 조건에 따라 결정하는 데 사용됩니다. 시간당 급여를 받는 직원(`SalariedFlag` = 0)의 경우 현재 시간 수에 `VacationHours`에 지정된 값을 더한 값으로 `@NewHours`가 설정되고, 그 외의 경우에는 `VacationHours`에 지정된 값으로 `@NewHours`가 설정됩니다.

```sql
CREATE PROCEDURE HumanResources.Update_VacationHours
@NewHours SMALLINT, @Rowcount INT OUTPUT
AS
SET NOCOUNT ON;
UPDATE HumanResources.Employee
SET VacationHours =
    ( CASE
        WHEN SalariedFlag = 0 THEN VacationHours + @NewHours
        ELSE @NewHours
        END
    )
WHERE CurrentFlag = 1;
SET @Rowcount = @@rowcount;

GO
DECLARE @Rowcount INT
EXEC HumanResources.Update_VacationHours 40, @Rowcount OUTPUT
PRINT @Rowcount;
```

### <a name="error-handling"></a><a name="Error"></a> 오류 처리

이 섹션의 예에서는 저장 프로시저가 실행될 때 발생할 수 있는 오류를 처리하는 방법을 보여 줍니다.

#### <a name="j-using-trycatch"></a>J. TRY...CATCH 사용

다음 예에서는 TRY...CATCH 구문을 사용하여 저장 프로시저를 실행하는 동안 발생한 오류 정보를 반환합니다.

```sql
CREATE PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID INT )
AS
SET NOCOUNT ON;
BEGIN TRY
  BEGIN TRANSACTION
  -- Delete rows from the child table, WorkOrderRouting, for the specified work order.
    DELETE FROM Production.WorkOrderRouting
    WHERE WorkOrderID = @WorkOrderID;
  -- Delete the rows from the parent table, WorkOrder, for the specified work order.
    DELETE FROM Production.WorkOrder
    WHERE WorkOrderID = @WorkOrderID;
  COMMIT
END TRY

BEGIN CATCH
  -- Determine if an error occurred.
  IF @@TRANCOUNT > 0
    ROLLBACK

  -- Return the error information.
  DECLARE @ErrorMessage NVARCHAR(4000), @ErrorSeverity INT;
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);
END CATCH;

GO
EXEC Production.uspDeleteWorkOrder 13;

/* Intentionally generate an error by reversing the order in which rows
   are deleted from the parent and child tables. This change does not
   cause an error when the procedure definition is altered, but produces
   an error when the procedure is executed.
*/
ALTER PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID INT )
AS

BEGIN TRY
  BEGIN TRANSACTION
  -- Delete the rows from the parent table, WorkOrder, for the specified work order.
    DELETE FROM Production.WorkOrder
    WHERE WorkOrderID = @WorkOrderID;

  -- Delete rows from the child table, WorkOrderRouting, for the specified work order.
    DELETE FROM Production.WorkOrderRouting
    WHERE WorkOrderID = @WorkOrderID;
  COMMIT TRANSACTION
END TRY

BEGIN CATCH
  -- Determine if an error occurred.
  IF @@TRANCOUNT > 0
    ROLLBACK TRANSACTION

  -- Return the error information.
  DECLARE @ErrorMessage NVARCHAR(4000), @ErrorSeverity INT;
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);
END CATCH;
GO
-- Execute the altered procedure.
EXEC Production.uspDeleteWorkOrder 15;

DROP PROCEDURE Production.uspDeleteWorkOrder;
```

### <a name="obfuscating-the-procedure-definition"></a><a name="Encrypt"></a> 프로시저 정의 난독 처리

이 섹션의 예에서는 저장 프로시저 정의를 난독 처리하는 방법을 보여 줍니다.

#### <a name="k-using-the-with-encryption-option"></a>11. WITH ENCRYPTION 옵션 사용

다음 예에서는 `HumanResources.uspEncryptThis` 프로시저를 만듭니다.

**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상, SQL Database.

```sql
CREATE PROCEDURE HumanResources.uspEncryptThis
WITH ENCRYPTION
AS
    SET NOCOUNT ON;
    SELECT BusinessEntityID, JobTitle, NationalIDNumber,
        VacationHours, SickLeaveHours
    FROM HumanResources.Employee;
GO
```

`WITH ENCRYPTION` 옵션은 다음 예에서 나타난 바와 같이 시스템 카탈로그를 쿼리하거나 메타데이터 함수를 사용할 때 프로시저 정의를 난독 처리합니다.

`sp_helptext`를 실행합니다.

```sql
EXEC sp_helptext 'HumanResources.uspEncryptThis';
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

`The text for object 'HumanResources.uspEncryptThis' is encrypted.`

`sys.sql_modules` 카탈로그 뷰를 직접 쿼리합니다.

```sql
SELECT definition FROM sys.sql_modules
WHERE object_id = OBJECT_ID('HumanResources.uspEncryptThis');
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
definition
--------------------------------
NULL
```

### <a name="forcing-the-procedure-to-recompile"></a><a name="Recompile"></a> 프로시저의 다시 컴파일 강제 수행

이 섹션의 예에서는 WITH RECOMPILE 절을 사용하여 프로시저를 실행할 때마다 강제로 다시 컴파일되도록 합니다.

#### <a name="l-using-the-with-recompile-option"></a>12. WITH RECOMPILE 옵션 사용

`WITH RECOMPILE` 절은 프로시저에 제공되는 매개 변수가 일반적이지 않으며 새 실행 계획이 메모리에 캐시되거나 저장되지 않을 때 유용합니다.

```sql
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL
    DROP PROCEDURE dbo.uspProductByVendor;
GO
CREATE PROCEDURE dbo.uspProductByVendor @Name VARCHAR(30) = '%'
WITH RECOMPILE
AS
    SET NOCOUNT ON;
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'
    FROM Purchasing.Vendor AS v
    JOIN Purchasing.ProductVendor AS pv
      ON v.BusinessEntityID = pv.BusinessEntityID
    JOIN Production.Product AS p
      ON pv.ProductID = p.ProductID
    WHERE v.Name LIKE @Name;
```

### <a name="setting-the-security-context"></a><a name="Security"></a> 보안 컨텍스트 설정

이 섹션의 예에서는 EXECUTE AS 절을 사용하여 저장 프로시저가 실행되는 보안 컨텍스트를 설정합니다.

#### <a name="m-using-the-execute-as-clause"></a>13. EXECUTE AS 절 사용

다음 예에서는 [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) 절을 사용하여 프로시저가 실행될 수 있는 보안 컨텍스트를 지정하는 방법을 보여줍니다. 이 예에서 `CALLER` 옵션은 프로시저를 호출하는 사용자 컨텍스트에서 프로시저가 실행될 수 있도록 지정합니다.

```sql
CREATE PROCEDURE Purchasing.uspVendorAllInfo
WITH EXECUTE AS CALLER
AS
    SET NOCOUNT ON;
    SELECT v.Name AS Vendor, p.Name AS 'Product name',
      v.CreditRating AS 'Rating',
      v.ActiveFlag AS Availability
    FROM Purchasing.Vendor v
    INNER JOIN Purchasing.ProductVendor pv
      ON v.BusinessEntityID = pv.BusinessEntityID
    INNER JOIN Production.Product p
      ON pv.ProductID = p.ProductID
    ORDER BY v.Name ASC;
GO
```

#### <a name="n-creating-custom-permission-sets"></a>14. 사용자 지정 권한 집합 만들기

다음 예에서는 EXECUTE AS를 사용하여 데이터베이스 작업에 대한 사용자 지정 권한을 만듭니다. TRUNCATE TABLE과 같은 일부 작업에는 부여할 수 있는 사용 권한이 없습니다. TRUNCATE TABLE 문을 저장 프로시저에 통합하고 테이블 수정 권한을 가진 사용자로 프로시저가 실행되도록 지정하면 테이블 자르기 권한을 프로시저에 대해 EXECUTE 권한을 부여한 사용자에게로 확장할 수 있습니다.

```sql
CREATE PROCEDURE dbo.TruncateMyTable
WITH EXECUTE AS SELF
AS TRUNCATE TABLE MyDB..MyTable;
```

## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

### <a name="o-create-a-stored-procedure-that-runs-a-select-statement"></a>15. SELECT 문을 실행하는 저장 프로시저 만들기

이 예제는 프로시저를 만들고 실행하기 위한 기본 구문을 보여줍니다. 일괄 처리를 실행할 때 CREATE PROCEDURE가 첫 번째 명령문이어야 합니다. 예를 들어 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]에서 다음 저장 프로시저를 만들려면 먼저 데이터베이스 컨텍스트를 설정 한 다음, CREATE PROCEDURE 문을 실행합니다.

```sql
-- Uses AdventureWorksDW database

--Run CREATE PROCEDURE as the first statement in a batch.
CREATE PROCEDURE Get10TopResellers
AS
BEGIN
    SELECT TOP (10) r.ResellerName, r.AnnualSales
    FROM DimReseller AS r
    ORDER BY AnnualSales DESC, ResellerName ASC;
END
;
GO

--Show 10 Top Resellers
EXEC Get10TopResellers;
```

## <a name="see-also"></a>참고 항목

- [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)
- [흐름 제어 언어&#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)
- [커서](../../relational-databases/cursors.md)
- [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
- [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [DROP PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)
- [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)
- [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)
- [저장 프로시저&#40;데이터베이스 엔진&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)
- [sp_procoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md)
- [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)
- [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)
- [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)
- [sys.procedures&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)
- [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)
- [sys.assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)
- [sys.numbered_procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)
- [sys.numbered_procedure_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedure-parameters-transact-sql.md)
- [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)
- [저장 프로시저 만들기](../../relational-databases/stored-procedures/create-a-stored-procedure.md)
- [테이블 반환 매개 변수 사용&#40;Database Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)
- [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)
- [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
