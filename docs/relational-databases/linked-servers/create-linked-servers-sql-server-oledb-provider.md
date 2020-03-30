---
title: 연결된 서버 공급자 만들기
ms.date: 07/01/2019
ms.prod: sql
ms.technology: ''
ms.prod_service: database-engine
ms.reviewer: MikeRayMSFT
ms.topic: conceptual
author: pmasl
ms.author: pelopes
manager: rothj
ms.custom: seo-dt-2019
ms.openlocfilehash: 933a37dd4ef627796b7688510bd235c80db417be
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74095998"
---
# <a name="microsoft-sql-server-distributed-queries-ole-db-connectivity"></a>Microsoft SQL Server 분산 쿼리: OLE DB 연결

이 문서에서는 Microsoft SQL Server 쿼리 프로세서가 OLE DB 공급자와 상호 작용하여 다른 유형의 분산 쿼리를 사용하도록 설정하는 방법을 설명합니다. 이 문서는 주로 OLE DB 공급자 개발자를 위해 작성되었으며 OLE DB 사양을 잘 알고 있다고 가정합니다. 또한 분산 쿼리 기능 자체가 아니라 SQL Server 쿼리 프로세서와 OLE DB 공급자 간의 OLE DB 인터페이스에 중점을 둡니다. 분산 쿼리 기능에 대한 자세한 내용은 [연결된 서버](../../relational-databases/linked-servers/linked-servers-database-engine.md)를 참조하세요.

## <a name="overview-and-terminology"></a>개요 및 용어

 Microsoft SQL Server 분산 쿼리를 사용하면 SQL Server 사용자가 SQL Server를 실행하는 다른 서버 또는 OLE DB 인터페이스를 공개하는 다른 데이터 원본 내에 있는 SQL Server 기반 서버 외부의 데이터에 액세스할 수 있습니다. OLE DB를 사용하면 다른 유형의 데이터 원본에 있는 표 형식 데이터에 일관되게 액세스할 수 있습니다.

이 문서에서 분산 쿼리는 하나 이상의 외부 OLE DB 데이터 원본에 있는 테이블 및 행 집합을 참조하는 `SELECT`, `INSERT`, `UPDATE` 또는 `DELETE` 문입니다.

원격 테이블은 OLE DB 데이터 원본에 저장되어 있고, 쿼리를 실행하는 SQL Server 기반 서버 외부에 있는 테이블입니다. 분산 쿼리는 하나 이상의 원격 테이블에 액세스합니다.

### <a name="ole-db-provider-categories"></a>OLE DB 공급자 범주

다음은 SQL Server 분산 쿼리 관점의 기능을 기반으로 한 OLE DB 공급자 분류입니다. 정의된 대로, 이러한 분류는 함께 사용할 수 있으므로 지정된 공급자가 다음 범주 중 두 개 이상에 속할 수 있습니다.

- SQL 명령 공급자

- 인덱스 공급자

- 단순 테이블 공급자

- 비 SQL 명령 공급자

#### <a name="sql-command-providers"></a>SQL 명령 공급자

SQL Server에서 인식하는 SQL 표준 언어를 사용하는 `Command` 개체를 지원하는 공급자가 이 범주에 속합니다. 지정된 OLE DB 공급자가 SQL Server에서 SQL 명령 공급자로 간주되기 위한 특정 요구 사항은 다음과 같습니다.

- 공급자가 `Command` 개체와 모든 필수 OLE DB 인터페이스(`ICommand`, `ICommandText`, `IColumnsInfo`, `ICommandProperties`, `IAccessor`)를 지원해야 합니다.

- 공급자가 지원하는 SQL 언어가 최소한 SQL Subminimum이어야 합니다. 공급자가 `DBPROP_SQLSUPPORT` 속성을 통해 언어를 보고해야 합니다.

SQL 명령 공급자의 예로 Microsoft OLE DB Provider for SQL Server와 Microsoft OLE DB Provider for ODBC가 있습니다.

#### <a name="index-providers"></a>인덱스 공급자

인덱스 공급자는 OLE DB에 따라 인덱스를 지원 및 공개하고 기본 테이블의 인덱스 기반 조회를 허용하는 공급자입니다. 지정된 OLE DB 공급자가 SQL Server에서 인덱스 공급자로 간주되기 위한 특정 요구 사항은 다음과 같습니다.

- 공급자가 TABLES, COLUMNS, INDEXES 스키마 행 집합이 있는 `IDBSchemaRowset` 인터페이스를 지원해야 합니다.

- 공급자가 인덱스 이름과 해당 기본 테이블 이름을 지정하여 `IOpenRowset`를 통해 인덱스의 행 집합 열기를 지원해야 합니다.

- `Index` 개체가 모든 필수 인터페이스(`IRowset`, `IRowsetIndex`, `IAccessor`, `IColumnsInfo`, `IRowsetInfo`, `IConvertTypes`)를 지원해야 합니다.

- `IOpenRowset`를 통해 인덱싱된 기본 테이블에 대해 열린 행 집합이 책갈피를 기준으로 행에 배치되려면 `IRowsetLocate` 인터페이스를 지원해야 합니다.

OLE DB 공급자가 위의 요구 사항을 충족하는 경우 SQL Server에서 공급자의 인덱스를 사용하여 쿼리를 평가할 수 있도록 사용자가 `Index As Access Path` 공급자 옵션을 설정할 수 있습니다. 이 옵션을 설정하지 않으면 기본적으로 SQL Server는 공급자의 인덱스를 사용하지 않습니다.

>[!NOTE]
>SQL Server는 SQL Server에서 OLE DB 공급자에 액세스하는 방법에 영향을 주는 다양한 옵션을 지원합니다. SQL Server Enterprise Manager의 `Linked Server Properties` 대화 상자를 사용하여 이러한 옵션을 설정할 수 있습니다.

#### <a name="simple-table-providers"></a>단순 테이블 공급자

`IOpenRowset` 인터페이스를 통해 기본 테이블에 대해 행 집합을 여는 옵션을 공개하는 공급자입니다. 이러한 공급자는 SQL 명령 공급자나 인덱스 공급자가 아니라, SQL Server 분산 쿼리에서 사용할 수 있는 가장 간단한 공급자 클래스입니다.

이러한 공급자에 대해 SQL Server는 분산 쿼리 평가 중에만 테이블 검색을 수행할 수 있습니다.

#### <a name="non-sql-command-providers"></a>비 SQL 명령 공급자

`Command` 개체와 필수 인터페이스를 지원하지만 SQL Server에서 인식하는 SQL 표준 언어를 지원하지 않는 공급자가 이 범주에 속합니다.

비 SQL 명령 공급자의 두 가지 예는 Microsoft OLE DB Provider for Indexing Service와 [Microsoft OLE DB Provider for Microsoft Active Directory Service](../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)입니다.

### <a name="transact-sql-subset"></a>Transact-SQL 하위 집합

공급자가 필요한 OLE DB 인터페이스를 지원하는 경우 다음과 같은 Transact-SQL 문 클래스가 분산 쿼리에 대해 지원됩니다.

- 원격 테이블을 대상 테이블로 사용하는 `SELECT` INTO 문을 제외하고 모든 `SELECT` 문이 허용됩니다.

- 공급자가 삽입에 필요한 인터페이스를 지원하는 경우 원격 테이블에 대한 `INSERT` 문이 허용됩니다. INSERT의 OLE DB 요구 사항에 대한 자세한 내용은 이 문서의 뒷부분에 있는 \"INSERT 문\"을 참조하세요.

- 공급자가 지정된 테이블의 OLE DB 인터페이스 요구 사항을 충족하는 경우 원격 테이블에 대한 `UPDATE` 및 DELETE 문이 허용됩니다. 원격 테이블을 업데이트하거나 삭제할 수 있는 OLE DB 인터페이스 요구 사항 및 조건에 대한 자세한 내용은 이 문서의 뒷부분에 있는 \"UPDATE 및 DELETE 문\"을 참조하세요.

### <a name="cursor-support"></a>커서 지원

공급자가 필요한 OLE DB 기능을 지원하는 경우 분산 쿼리에 대해 스냅샷과 키 집합 커서가 모두 지원됩니다. 동적 커서는 분산 쿼리에 대해 지원되지 않습니다. 분산 쿼리에 대한 동적 커서의 사용자 요청은 키 집합 커서로 다운그레이드됩니다.

스냅샷 커서는 커서를 열 때 채워지고 결과 집합이 변경되지 않은 상태로 유지됩니다. 기본 테이블에 대한 업데이트, 삽입 및 삭제는 커서에 반영되지 않습니다.

키 집합 커서는 커서를 열 때 채워지고 결과 집합이 커서의 수명 동안 변경되지 않은 상태로 유지됩니다. 그러나 행을 방문할 때 기본 테이블에 대한 업데이트 및 삭제가 커서에 표시됩니다. 커서 멤버 자격에 영향을 줄 수 있는 기본 테이블에 대한 삽입은 표시되지 않습니다.

공급자가 원격 테이블의 업데이트 및 삭제 조건을 충족하는 경우 분산 쿼리에 정의되고 원격 테이블을 참조하는 커서를 통해 원격 테이블을 업데이트하거나 삭제할 수 있습니다(예: table `UPDATE` \| DELETE `<remote-table>` `WHERE` CURRENT OF `<cursor-name>`). 자세한 내용은 이 문서의 뒷부분에 있는 \"UPDATE 및 DELETE 문\"을 참조하세요.

#### <a name="keyset-cursor-support-requirements"></a>키 집합 커서 지원 요구 사항

모든 Transact-SQL 구문 요구 사항이 충족되고 다음 중 하나에 해당하는 경우 분산 쿼리에서 키 집합 커서가 지원됩니다.

- OLE DB 공급자가 쿼리의 모든 원격 테이블에서 재사용 가능 책갈피를 지원합니다. 재사용 가능 책갈피를 지정된 테이블의 행 집합과 동일한 테이블의 다른 행 집합에서 사용할 수 있습니다. 재사용 가능 책갈피 지원은 BOOKMARK_DURABILITY 열을 BMK_DURABILITY_INTRANSACTION 이상 내구성으로 설정하여 `IDBSchemaRowset`의 TABLES_INFO 스키마 행 집합을 통해 표시됩니다.

- 모든 원격 테이블이 `IDBSchemaRowset` 인터페이스의 INDEXES 행 집합을 통해 고유 키를 공개합니다. UNIQUE 열이 VARIANT_TRUE로 설정된 인덱스 항목이 있어야 합니다.

키 집합 커서는 *OpenQuery* 함수를 포함하는 분산 쿼리에 대해 지원되지 않습니다.

#### <a name="updatable-keyset-cursor-requirements"></a>업데이트할 수 있는 키 집합 커서 요구 사항

분산 쿼리에 정의된 키 집합 커서를 통해 원격 테이블을 업데이트하거나 삭제할 수 있습니다(예: `UPDATE` \| DELETE `<remote-table>` `WHERE` CURRENT OF `<cursor-name>`). 다음 조건에서는 분산 쿼리에 대해 업데이트할 수 있는 커서가 허용됩니다.

- 공급자가 원격 테이블에 대한 업데이트 및 삭제 조건도 충족하는 경우 업데이트 가능 커서가 허용됩니다. 자세한 내용은 이 문서의 뒷부분에 있는 \"UPDATE 및 DELETE 문\"을 참조하세요.

- 모든 업데이트 가능 키 집합 커서 작업은 격리 수준이 읽기 반복 가능 격리 수준 이상인 사용자 정의 트랜잭션에 있어야 합니다. 또한 공급자는 `ITransactionJoin` 인터페이스를 사용하여 분산 트랜잭션을 지원해야 합니다.

## <a name="ole-db-provider-interaction-phases"></a>OLE DB 공급자 상호 작용 단계

 다음 6개 작업은 모든 분산 쿼리 실행 시나리오에 공통적으로 적용됩니다.

- 연결 설정 및 속성 검색 작업은 SQL Server가 OLE DB 공급자에 연결하는 방법 및 사용되는 공급자 속성을 나타냅니다.

- 테이블 이름 확인 및 메타데이터 검색 작업은 SQL Server에서 연결된 서버 기반 이름 또는 임시 이름 중 하나로 지정된 원격 테이블 이름을 공급자의 적절한 데이터 개체로 확인하는 방법을 나타냅니다. 여기에는 분산 쿼리를 컴파일 및 최적화하기 위해 SQL Server가 공급자에서 검색하는 테이블 메타데이터도 포함됩니다.

- 트랜잭션 관리 작업은 OLE DB 공급자와의 모든 트랜잭션 관련 상호 작용을 지정합니다.

- 데이터 형식 처리 작업은 SQL Server에서 분산 쿼리를 처리하는 동안 OLE DB 공급자의 데이터를 사용하거나 데이터를 OLE DB 공급자로 내보낼 때 OLE DB 데이터 형식을 처리하는 방법을 나타냅니다.

- 오류 처리 작업은 SQL Server에서 공급자의 확장 오류 정보를 사용하는 방법을 나타냅니다.

- 보안 작업은 SQL Server 보안이 공급자의 보안과 상호 작용하는 방법을 지정합니다.

### <a name="connection-establishment-and-property-retrieval"></a>연결 설정 및 속성 검색

SQL Server는 `OPENROWSET` 함수를 사용하여 네 부분으로 구성된 연결된 서버 기반 이름 및 임시 이름의 두 가지 원격 데이터 개체 명명 규칙을 지원합니다.

#### <a name="linked-server-based-names"></a>연결된 서버 기반 이름

연결된 서버는 OLE DB 데이터 원본에 대한 추상화 역할을 합니다. 연결된 서버 기반 이름은 네 부분으로 구성된 `<linked-server>.<catalog>`. `<schema>.<object>` 형식의 이름입니다. 여기서 `<linked-server>`는 연결된 서버의 이름입니다. SQL Server는 `<linked-server>`를 해석하여 공급자에 데이터 원본을 식별하는 연결 특성 및 OLE DB 공급자를 파생합니다. 다른 세 개의 이름 부분은 특정 원격 테이블을 식별하기 위해 OLE DB 데이터 원본에서 해석됩니다. :::

#### <a name="ad-hoc-names"></a>임시 이름

임시 이름은 `OPENROWSET` 또는 `OPENDATASOURCE` 함수를 기반으로 하는 이름입니다. 분산 쿼리에서 원격 테이블을 참조할 때마다 임시 이름에 모든 연결 정보(즉, 사용할 OLE DB 공급자, 데이터 원본을 식별하는 데 필요한 특성, 사용자 ID 및 암호)가 포함됩니다.

sysadmin 역할의 멤버를 제외하고 기본적으로 임시 이름을 사용할 수 없습니다. OLE DB 공급자에 대해 임시 이름을 사용하려면 공급자 옵션 `DisallowAdhocAccess`를 `0`으로 설정해야 합니다.

연결된 서버 이름을 사용하는 경우 SQL Server는 연결된 서버 정의에서 OLE DB 공급자 이름 및 공급자의 초기화 속성을 추출합니다. 임시 이름을 사용하는 경우 SQL Server는 `OPENROWSET` 함수의 인수에서 동일한 정보를 추출합니다.

네 부분으로 구성된 이름 및 임시 이름 기반 구문을 사용하여 연결된 서버를 설정하는 방법에 대한 자세한 내용은 [연결된 서버 만들기](create-linked-servers-sql-server-database-engine.md)를 참조하세요.

### <a name="connecting-to-an-ole-db-provider"></a>OLE DB 공급자에 연결

다음은 SQL Server에서 OLE DB 공급자에 연결할 때 수행하는 대략적인 단계입니다.

1. SQL Server에서 데이터 원본 개체를 만듭니다.

   SQL Server는 공급자의 `ProgID`를 사용하여 해당 DSO(데이터 원본 개체)를 인스턴스화합니다. ProgID는 연결된 서버 구성의 `provider_name` 매개 변수로 지정되거나, 임시 이름의 경우 `OPENROWSET` 함수의 첫 번째 인수로 지정됩니다.

   SQL Server는 OLE DB 서비스 컴포넌트 인터페이스 `IDataInitialize`를 통해 공급자의 DSO를 인스턴스화합니다. 이렇게 하면 서비스 컴포넌트 관리자가 공급자의 기본 기능 이상으로 스크롤 및 업데이트 지원과 같은 서비스를 집계할 수 있습니다. 또한 `IDataInitialize`를 통해 공급자를 인스턴스화하면 OLE DB 서비스 컴포넌트가 공급자에 대한 연결을 풀링하여 일부 연결 및 초기화 오버헤드를 줄일 수 있습니다.

   지정된 공급자를 SQL Server와 동일한 프로세스 또는 자체 프로세스에서 인스턴스화되도록 구성할 수 있습니다. 별도의 프로세스에서 인스턴스화하면 SQL Server 프로세스가 공급자 오류로부터 보호됩니다. 이와 동시에, SQL Server에서 Out of Process로 OLE DB 호출을 마샬링하기 위한 성능 오버헤드가 발생합니다. `Allow In Process` 공급자 옵션을 설정하여 In Process 또는 Out of Process로 인스턴스화되도록 공급자를 구성할 수 있습니다. 자세한 내용은 [공급자 옵션 설정](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)을 참조하세요.

   OLE DB 서비스 컴포넌트 및 세션 풀링을 자세히 알아보려면 공급자 요구 사항에 대한 OLE DB 설명서를 참조하세요.

2. 데이터 원본이 초기화됩니다.

   DSO가 생성된 후에 `IDBProperties` 인터페이스는 서버 구성 옵션 `remote login timeout`이 0보다 큰 경우 DBPROP_INIT_TIMEOUT 초기화 속성을 설정합니다. 이 속성은 필수 속성입니다.

   이러한 속성은 연결된 서버 정의 또는 `OPENROWSET` 함수의 두 번째 인수에 지정되거나 암시된 경우에 설정됩니다.

   - `DBPROP_INIT_PROVIDERSTRING`

   - `DBPROP_INIT_DATASOURCE`

   - `DBPROP_INIT_LOCATION`

   - `DBPROP_INIT_CATALOG`

   - `DBPROP_AUTH_USERID`

   - `DBPROP_AUTH_PASSWORD`

   이러한 속성이 설정된 후에 DSO를 지정된 속성으로 초기화하기 위해 `IDBInitialize::Initialize`가 호출됩니다.

3. SQL Server에서 공급자 특정 정보를 수집합니다.

   SQL Server는 분산 쿼리 평가에 사용할 여러 공급자 속성을 수집합니다. 이러한 속성은 `IDBProperties::GetProperties`를 호출하여 검색합니다. 이러한 속성은 모두 선택 사항입니다. 그러나 관련 속성을 모두 지원하면 SQL Server에서 공급자 기능을 완전히 활용할 수 있습니다. 예를 들어 `DBPROP_SQLSUPPORT`는 SQL Server에서 공급자에 쿼리를 보낼 수 있는지를 결정하는 데 필요합니다. 이 속성이 지원되지 않는 경우 SQL Server는 원격 공급자가 SQL 명령 공급자인 경우에도 SQL 명령 공급자로 사용하지 않습니다. 다음 표의 기본값 열에는 SQL Server에서 공급자가 속성을 지원하지 않는 경우에 사용하는 값이 표시됩니다.

속성| 기본값| 사용 |
|:----|:----|:----|
|`DBPROP_DBMSNAME`|None|오류 메시지에 사용됩니다.|
|`DBPROP_DBMSVER` |None|오류 메시지에 사용됩니다.|
|`DBPROP_PROVIDERNAME`|None|오류 메시지에 사용됩니다.|
|`DBPROP_PROVIDEROLEDBVER1`|1.5|2\.0 기능의 가용성을 결정하는 데 사용됩니다.
|`DBPROP_CONCATNULLBEHAVIOR`|None|공급자의 `NULL` 연결 동작이 SQL Server와 동일한지 여부를 결정하는 데 사용됩니다.|
|`DBPROP_NULLCOLLATION`|None|`NULLCOLLATION`이 SQL Server 인스턴스 null 데이터 정렬 동작과 일치하는 경우에만 정렬/인덱스 사용을 허용합니다.|
|`DBPROP_OLEOBJECTS`|None|공급자가 큰 데이터 개체 열에 대해 구조적 스토리지 인터페이스를 지원하는지를 결정합니다.|
|`DBPROP_STRUCTUREDSTORAGE`|None|큰 개체 형식(`ILockBytes`, `Istream` 및 `ISequentialStream`)에 대해 지원되는 구조적 스토리지 인터페이스를 결정합니다.|
|`DBPROP_MULTIPLESTORAGEOBJECTS`|False|둘 이상의 큰 개체 열을 동시에 열 수 있는지를 결정합니다.|
|`DBPROP_SQLSUPPORT`|None|SQL 쿼리를 공급자에 보낼 수 있는지를 결정합니다.|
|`DBPROP_CATALOGLOCATION`|`DBPROPVAL_CL_START`|여러 부분으로 구성된 테이블 이름을 생성하는 데 사용됩니다.
|`SQLPROP_DYNAMICSQL`|False|SQL Server 특정 속성입니다. `VARIANT_TRUE`를 반환하는 경우 `?` 매개 변수 표식이 매개 변수가 있는 쿼리 실행에 대해 지원됨을 나타냅니다.
|`SQLPROP_NESTEDQUERIES`|False|SQL Server 특정 속성입니다. `VARIANT_TRUE`를 반환하는 경우 공급자가 `FROM` 절에서 중첩된 `SELECT` 문을 지원함을 나타냅니다.
|`SQLPROP_GROUPBY`|False|SQL Server 특정 속성입니다. `VARIANT_TRUE`를 반환하는 경우 공급자가 SQL-92 표준에 지정된 대로 `SELECT` 문에서 GROUP BY 절을 지원함을 나타냅니다.
|`SQLPROP_DATELITERALS `|False|SQL Server 특정 속성입니다. `VARIANT_TRUE`를 반환하는 경우 공급자가 SQL Server Transact-SQL 구문을 기준으로 날짜/시간 리터럴을 지원함을 나타냅니다.
|`SQLPROP_ANSILIKE `|False|SQL Server 특정 속성입니다. 이 속성은 SQL-Minimum 수준을 지원하는 공급자에서 중요하며, SQL-92 항목 수준(\'%\' 및 \'_\' 와일드카드 문자)을 기준으로 `LIKE` 연산자를 지원합니다.
|`SQLPROP_SUBQUERIES `|False|SQL Server 속성입니다. 이 속성은 SQL-Minimum 수준을 지원하는 공급자에서 중요합니다. 이 속성은 공급자가 SQL-92 항목 수준에 지정된 대로 하위 쿼리를 지원함을 나타냅니다. 여기에는 상호 관련된 하위 쿼리, `IN`, `EXISTS`, `ALL` 및 `ANY` 연산자를 지원하는 `SELECT` 목록과 `WHERE` 절의 하위 쿼리가 포함됩니다.
|`SQLPROP_INNERJOIN`|False|SQL Server 특정 속성입니다. 이 속성은 SQL-Minimum 수준을 지원하는 공급자에서 중요합니다. 이 속성은 `FROM` 절에서 여러 테이블을 사용하는 조인이 지원됨을 나타냅니다. ------ ---

`DBLITERAL_CATALOG_SEPARATOR`, `DBLITERAL_SCHEMA_SEPARATOR`(카탈로그, 스키마 및 개체 이름 부분이 지정된 경우 전체 개체 이름 생성) 및 `DBLITERAL_QUOTE`(공급자에 전송된 SQL 쿼리에서 식별자 이름에 따옴표 표시)의 세 가지 리터럴은 `IDBInfo::GetLiteralInfo`에서 검색됩니다.

공급자가 구분 기호 리터럴을 지원하지 않는 경우 SQL Server는 마침표(.)를 기본 구분 문자로 사용합니다. 공급자가 카탈로그 구분 문자만 지원하고 스키마 구분 문자를 지원하지 않는 경우 SQL Server는 카탈로그 구분 문자를 스키마 구분 문자로 사용합니다. 공급자가 `DBLITERAL_QUOTE`를 지원하지 않는 경우 SQL Server는 작은따옴표(`'`)를 따옴표 문자로 사용합니다.

>[!NOTE]
>공급자의 이름 구분 기호 리터럴이 이러한 기본값과 일치하지 않는 경우 공급자는 SQL Server에서 네 부분으로 구성된 이름을 통해 해당 테이블에 액세스할 수 있도록 `IDBInfo`를 통해 이름 구분 기호 리터럴을 공개해야 합니다. 이러한 리터럴이 공개되지 않으면 해당 공급자에 대해 통과 쿼리만 사용할 수 있습니다.

`SQLPROP_DYNAMICSQL` 및 `SQLPROP_NESTEDQUERIES` 속성을 공개하는 방법에 대한 자세한 내용은 [SQL Server 특정 속성](#appendixc)을 참조하세요.

### <a name="table-name-resolution-and-meta-data-retrieval"></a>테이블 이름 확인 및 메타데이터 검색

SQL Server는 분산 쿼리에 지정된 원격 테이블 이름을 OLE DB 데이터 원본의 특정 테이블이나 뷰로 확인합니다. 연결된 서버 기반 명명 스키마와 임시 명명 스키마는 둘 다 공급자에서 해석되는 세 부분으로 구성된 이름을 생성합니다. 연결된 서버 기반 이름의 경우 네 부분으로 구성된 이름의 마지막 세 부분이 카탈로그 이름, 스키마 이름 및 개체 이름을 형성합니다. 임시 이름의 경우 `OPENROWSET` 함수의 세 번째 인수가 카탈로그 이름, 스키마 이름 및 개체 이름을 설명하는 세 부분으로 구성된 이름을 지정합니다. 카탈로그 이름과 스키마 이름 중 하나 또는 둘 다를 비워 둘 수 있습니다. 빈 카탈로그 이름과 스키마 이름이 포함된 네 부분으로 구성된 이름은 `<server-name>...<object-name>`과 같습니다. 이 경우 SQL Server는 `NULL`을 스키마 행 집합 테이블에서 찾을 해당 값으로 사용합니다.

SQL Server에서 사용하는 이름 확인 규칙 및 메타데이터 검색 단계는 공급자가 `Session` 개체의 `IDBSchemaRowset` 인터페이스를 지원하는지 여부에 따라 달라집니다.

`IDBSchemaRowset`가 지원되는 경우 `IDBSchemaRowset` 인터페이스에서 `TABLES`, `COLUMNS`, `INDEXES` 및 `TABLES_INFO` 스키마 행 집합이 사용됩니다. `TABLES_INFO` 스키마 행 집합은 OLE DB 2.0에 정의되어 있습니다. SQL Server는 지정된 원격 테이블 이름 부분과 일치하는 스키마 행을 찾기 위해 `IDBSchemaRowset` 인터페이스에서 반환되는 스키마 행 집합을 제한합니다. 다음은 스키마 행 집합에 대해 공급자가 지원하는 제한 및 SQL Server에서 스키마 행 집합을 사용하여 원격 테이블의 메타데이터를 검색하는 방법과 관련된 규칙입니다.

- `TABLE_NAME` 및 `COLUMN_NAME` 열 제한은 항상 필요합니다.

- 공급자가 `TABLE_CATALOG`(또는 `TABLE_SCHEMA`) 제한을 지원하는 경우 SQL Server는 해당 `TABLE_CATALOG`(또는 `TABLE_SCHEMA`) 제한을 사용합니다. 원격 테이블 이름에 카탈로그(또는 스키마) 이름이 지정되지 않은 경우 `NULL` 값이 해당 제한 값으로 사용됩니다. 카탈로그(또는 스키마) 이름이 지정된 경우 공급자는 해당 `TABLE_CATALOG`(또는 `TABLE_SCHEMA`) 제한을 지원해야 합니다.

- 공급자는 `TABLES` 및 `COLUMNS`에서 모두 `TABLE_SCHEMA` 제한을 지원하거나 둘 다에서 지원하지 않아야 합니다. 공급자는 `TABLES` 및 `COLUMNS` 행 집합에서 모두 카탈로그 이름 제한을 지원하거나 둘 다에서 지원하지 않아야 합니다.

- INDEXES 제한이 지원되는 경우 공급자는 `TABLES` 및 INDE `XES or support them on neither. The provider must either support catalog name restriction on both `TABLES` and `INDEXES` 행 집합의 스키마 제한을 모두 지원하거나 둘 다 지원하지 않아야 합니다.

`TABLES` 스키마 행 집합에서 SQL Server는 위의 규칙에 따라 제한을 설정하여 `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`, `TABLE_TYPE`, `TABLE_GUID` 열을 검색합니다.

`COLUMNS` 스키마 행 집합에서 SQL Server는 `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`, `COLUMN_NAME`, `COLUMN_GUID`, `ORDINAL_POSITION`, `COLUMN_FLAGS`, `IS_NULLABLE`, `DATA_TYPE`, `TYPE_GUID`, `CHARACTER_MAXIMUM_LENGTH`, `NUMERIC_PRECISION` 및 `NUMERIC_SCALE` 열을 검색합니다. `COLUMN_NAME`, `DATA_TYPE` 및 `ORDINAL_POSITION`은 null이 아닌 유효한 값을 반환해야 합니다. `DATA_TYPE`이 `DBTYPE_NUMERIC` 또는 `DBTYPE_DECIMAL`인 경우 해당 `NUMERIC_PRECISION` 및 `NUMERIC_SCALE`은 null이 아닌 유효한 값이어야 합니다.

선택적 `INDEXES` 스키마 행 집합에서 SQL Server는 이전 규칙에 따라 제한을 설정하여 지정된 원격 테이블에서 인덱스를 찾습니다. 이렇게 찾은 일치하는 인덱스 항목에서 SQL Server는 `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`, `INDEX_CATALOG`, `INDEX_SCHEMA`, `INDEX_NAME`, `PRIMARY_KEY`, `UNIQUE`, `CLUSTERED`, `FILL_FACTOR`, `ORDINAL_POSITION`, `COLUMN_NAME`, `COLLATION`, `CARDINALITY` 및 `PAGES` 열을 검색합니다.

선택적 `TABLES_INFO` 행 집합에서 SQL Server는 책갈피 지원, 책갈피의 유형 및 길이와 같은 지정된 원격 테이블에 대한 추가 정보를 찾습니다. `TABLES_INFO` 행 집합의 `DESCRIPTION` 열을 제외한 모든 열이 사용됩니다. `TABLES_INFO` 행 집합의 정보는 다음과 같이 사용됩니다.

- `BOOKMARK_DURABILITY` 열은 더 효율적인 키 집합 커서를 구현하는 데 사용됩니다. 이 열에 `BMK_DURABILITY_INTRANSACTION` 값 이상의 내구성 값이 있는 경우 SQL Server는 키 집합 커서를 구현하기 위해 책갈피 기반의 원격 테이블 행 검색 및 업데이트를 사용합니다.

- `BOOKMARK_TYPE`, `BOOKMARK_DATA TYPE` 및 `BOOKMARK_MAXIMUM_LENGTH` 열은 쿼리 컴파일 시 책갈피 메타데이터를 결정하는 데 사용됩니다. 이러한 열이 지원되지 않는 경우 SQL Server는 컴파일 시 `IOpenRowset`를 통해 기본 테이블 행 집합을 열어 책갈피 정보를 가져옵니다.

`IDBSchemaRowset`가 지원되지 않고 원격 테이블 이름에 카탈로그 이름 또는 스키마 이름이 포함된 경우 SQL Server에 `IDBSchemaRowset`가 필요하므로 오류가 반환됩니다. 그러나 카탈로그 이름과 스키마 이름을 모두 지정하지 않으면 SQL Server는 원격 테이블에 해당하는 행 집합을 열고 행 집합 개체의 필수 `IColumnsInfo` 인터페이스에서 열 메타데이터를 검색합니다.

SQL Server는 `IOpenRowset::OpenRowset`를 호출하여 테이블에 해당하는 행 집합을 엽니다. `OPENROWSET`에 제공되는 테이블 이름은 카탈로그 이름, 스키마 이름 및 개체 이름 부분에서 생성됩니다.

- 각 이름 부분(`catalog`, `schema`, `object name`)은 공급자의 따옴표 문자(`DBLITERAL_QUOTE`)로 묶인 다음 `DBLITERAL_CATALOG_SEPARATOR` 문자와 `DBLITERAL_SCHEMA_SEPARATOR` 문자를 사이에 포함하여 연결됩니다. 이름 생성은 `IOpenRowset`의 OLE DB 규칙을 따릅니다.

- 테이블의 열 메타데이터는 행 집합 개체가 열린 후에 `IColumnsInfo::GetColumnInfo`를 통해 검색됩니다.

`IDBSchemaRowset`가 TABLES, COLUMNS 및 TABLES_INFO 행 집합에서 지원되지 않는 경우 SQL Server는 기본 테이블에 대해 행 집합을 두 번 엽니다. 한 번은 쿼리 컴파일 중에 메타데이터를 검색하기 위해 열고, 다른 한 번은 쿼리 실행 중에 엽니다. 행 집합을 열 때 부작용(예: 실시간 디바이스의 상태를 변경하는 코드 실행, 메일 보내기, 임의의 사용자 제공 코드 실행)이 발생하는 공급자는 이 동작을 인식해야 합니다.

### <a name="statistics-retrieval"></a>통계 검색

공급자가 기본 테이블에 대한 배포 통계를 지원하는 경우 SQL Server는 이러한 통계를 사용합니다. SQL Server 쿼리 프로세서에서 중요한 다음 두 가지 종류의 통계가 있습니다.

- **열(또는 튜플) 카디널리티**. 테이블의 열(또는 열 조합)에 있는 고유 값 개수입니다. 열에 대한 조건자의 선택도를 추정하는 데 사용할 수 있습니다. 배포 통계를 지원하는 공급자는 하나 이상의 카디널리티 유형을 지원해야 합니다.

- **히스토그램**. 값의 분포가 균일하지 않은 경우 고유 값 개수가 조건자의 선택도를 정확하게 추정하는 데 충분하지 않습니다. 이 경우 테이블의 열 값 분포와 관하여 더욱 세분화된 정보가 표시되는 히스토그램을 제공할 수 있습니다.

통계의 가용성에 따라 SQL Server 쿼리 최적화 프로그램에서 쿼리의 중간 작업 카디널리티를 보다 효과적으로 추정하여 더 나은 실행 플랜을 생성할 수 있습니다.

OLE DB 공급자는 다음과 같은 배포 통계를 지원해야 합니다.

- **필수**. 속성 (1) 열 또는 튜플 카디널리티가 지원되는지 여부와 히스토그램이 지원되는지 여부를 나타내는 `DBPROP_TABLESTATISTICS`, (2) 히스토그램이 지원되는지 여부를 `DBPROPVAL_ORS_HISTOGRAM` 비트로 나타내는 `DBPROP_OPENROWSETSUPPORT`를 지원해야 합니다.

- **필수**. `TABLE_STATISTICS` 스키마 행 집합을 지원해야 합니다. `TABLE_STATISTICS` 스키마 행 집합에는 지정된 데이터베이스에서 사용할 수 있는 통계가 나열됩니다. 또한 스키마 행 집합 자체의 열 및 튜플 카디널리티를 포함하며 특정 열에서 히스토그램이 지원되는지 여부를 나타냅니다. SQL Server에서 통계를 사용하려면 이 스키마 행 집합에 `TABLE_NAME`, `STATISTICS_NAME`, `STATISTICS_TYPE`, `COLUMN_NAME` 및 `ORDINAL_POSITION` 열이 필요합니다. `COLUMN_CARDINALITY` 또는 `TUPLE_CARDINALITY` 중 하나 이상이 필요합니다. 히스토그램이 지원되는 경우 `NO_OF_RANGES`도 필요합니다.

- **선택 사항**. 필요에 따라 공급자가 히스토그램을 지원하는 경우 해당 통계의 `DBID`를 지정하여 히스토그램 행 집합을 열 수 있도록 하는 `IOpenRowset::OpenRowset` 메서드의 개선 사항을 지원해야 합니다.

통계 인터페이스에 대한 자세한 내용은 OLE DB 2.6 사양을 참조하세요.

### <a name="constraints"></a>제약 조건

OLE DB 공급자가 OLE DB 2.6 스키마 행 집합 `CHECK_CONSTRAINTS_BY_TABLE`을 지원하는 경우 SQL Server 쿼리 최적화 프로그램은 원격 데이터 원본의 기본 테이블에 정의된 `CHECK` 제약 조건도 사용합니다. 스키마 행 집합의 `CHECK_CLAUSE` 열은 SQL-92 규격 구문의 `CHECK` 절 조건자를 반환해야 합니다. 쿼리 최적화 프로그램은 테이블에 CHECK 제약 조건이 있기 때문에 항상 false 또는 항상 true로 알려진 조건자를 제거하거나 간소화하기 위해 제약 조건 정보를 사용합니다.

### <a name="transaction-management"></a>트랜잭션 관리

SQL Server는 공급자의 `ITransactionLocal`(로컬 트랜잭션) 및 `ITransactionJoin`(분산 트랜잭션) OLE DB 인터페이스를 사용하여 분산 데이터에 대한 트랜잭션 기반 액세스를 지원합니다. SQL Server는 공급자에 대해 로컬 트랜잭션을 시작하여 원자성 쓰기 작업을 보장합니다. 또한 SQL Server는 분산 트랜잭션을 사용하여 여러 노드와 관련된 트랜잭션이 모든 노드에서 동일한 결과(커밋 또는 중단)를 생성하도록 합니다. 공급자가 필요한 OLE DB 트랜잭션 관련 인터페이스를 지원하지 않는 경우 로컬 트랜잭션 컨텍스트에 따라 해당 공급자에 대한 업데이트 작업이 허용되지 않습니다.

다음 표에서는 공급자의 기능과 로컬 트랜잭션 컨텍스트가 지정된 경우 사용자가 분산 쿼리를 실행할 때 발생하는 상황을 설명합니다. 공급자에 대한 읽기 작업은 `SELECT` 문 또는 원격 테이블을 `SELECT INTO`, `INSERT`, `UPDATE` 또는 `DELETE` 문의 입력 쪽으로 읽어오는 경우를 나타냅니다. 공급자에 대한 쓰기 작업은 원격 테이블을 대상 테이블로 사용하는 `INSERT`, `UPDATE` 또는 `DELETE` 문을 나타냅니다.

공급자 기능 및 트랜잭션 컨텍스트를 기반으로 하는 분산 쿼리의 결과:

|분산 쿼리 발생|공급자가 `ITransactionLocal`을 지원하지 않음|공급자 `ITransactionLocal`을 지원하지만 `ITransactionJoin`을 지원하지 않음|공급자가 `ITransactionLocal` 및 `ITransactionJoin`을 모두 지원함|
|:-----|:-----|:-----|:-----|
| 트랜잭션 자체에서(사용자 트랜잭션 없음).|기본적으로 읽기 작업만 허용됩니다. 공급자 수준 옵션 `Nontransacted Updates`를 사용하도록 설정하면 쓰기 작업이 허용됩니다. 이 옵션을 사용하도록 설정하면 SQL Server는 공급자 데이터의 원자성 및 일관성을 보장할 수 없습니다. 이로 인해 실행 취소할 수 없는 쓰기 작업의 부분 결과가 원격 데이터 원본에 적용될 수 있습니다.| 원격 데이터에 대한 모든 문이 허용됩니다. 키 집합 커서는 읽기 전용입니다. 로컬 트랜잭션은 현재 SQL Server 세션의 격리 수준으로 공급자에서 시작되고 성공적으로 문 평가가 끝날 때 커밋됩니다. SQL Server 세션의 기본 격리 수준은 `SET TRANSACTION ISOLATION LEVEL` 문으로 수정하지 않는 한 `READ COMMITTED`입니다. 공급자는 요청된 격리 수준을 지원해야 합니다. | 모든 문이 허용됩니다. 키 집합 커서는 읽기 전용입니다. 로컬 트랜잭션은 현재 SQL Server 세션의 격리 수준으로 공급자에서 시작되고 성공적으로 문 평가가 끝날 때 커밋됩니다. |
| 사용자 트랜잭션에서(즉, `BEGIN TRAN` 또는 `BEGIN DISTRIBUTED TRAN`과 `COMMIT` 사이). | 트랜잭션의 격리 수준이 `READ COMMITTED`(기본값) 이하인 경우 읽기 작업이 허용됩니다. 격리 수준이 더 높으면 분산 쿼리가 허용되지 않습니다. | 읽기 작업만 허용됩니다. 새 분산 트랜잭션은 현재 SQL Server 세션의 격리 수준으로 공급자에서 시작됩니다. |모든 문이 허용됩니다. 새 분산 트랜잭션은 현재 SQL Server 세션의 격리 수준으로 공급자에서 시작되고 사용자 트랜잭션을 커밋할 때 커밋됩니다. 데이터 수정 문의 경우, 기본적으로 SQL Server는 주변 트랜잭션을 중지하지 않고 특정 오류 조건에서 데이터 수정 문을 중지할 수 있도록 분산 트랜잭션에서 중첩 트랜잭션을 시작합니다. `XACT_ABORT SET` 옵션을 사용하도록 설정하면 SQL Server는 중첩 트랜잭션 지원이 필요하지 않으며, 데이터 수정 문에서 오류가 발생할 경우 주변 트랜잭션을 중지합니다. |
|  |  |  |

### <a name="data-type-handling-in-distributed-queries"></a>분산 쿼리의 데이터 형식 처리

OLE DB 공급자는 OLE DB에서 정의된 데이터 형식(OLE DB에서 `DBTYPE`으로 표시됨)을 기준으로 데이터를 공개합니다. SQL Server는 서버 내부에서 외부 데이터를 네이티브 SQL Server 형식으로 처리합니다. 이로 인해 SQL Server에서 데이터를 사용하거나 SQL Server에서 데이터를 내보낼 때 각각 OLE DB 데이터 형식이 SQL Server 네이티브 형식으로 매핑되거나 그 반대로 매핑됩니다. 다른 설명이 없는 한, 이 매핑은 암시적으로 수행됩니다.

분산 쿼리의 데이터 형식은 다음 두 가지 매핑 방법 중 하나를 사용하여 처리됩니다.

- 사용 쪽 매핑은 원격 테이블이 `SELECT` 문과 INSERT, UPDATE 및 DELETE 문의 입력 쪽에 표시되는 경우 사용하는 쪽에서 형식을 OLE DB 데이터 형식에서 SQL Server 네이티브 데이터 형식으로 매핑합니다.

- 내보내기 쪽 매핑은 원격 테이블이 `INSERT` 또는 `UPDATE` 문의 대상 테이블로 표시되는 경우 내보내는 쪽에서 형식을 SQL Server 데이터 형식에서 OLE DB 데이터 형식으로 매핑합니다.

SQL Server 및 OLE DB 데이터 형식 매핑 테이블

| OLE DB 형식 | `DBCOLUMNFLAG` | SQL Server 데이터 형식 |
|-----|-----|-----|
|`DBTYPE_I1`*| |`numeric(3, 0)`|
|`DBTYPE_I2`| |`smallint`|
|`DBTYPE_I4`| |`int`|
|`DBTYPE_I8`| |`numeric(19,0)`|
|`DBTYPE_UI1`| |`tinyint`|
|`DBTYPE_UI2`*| |`numeric(5,0)`|
|`DBTYPE_UI4`*| |`numeric(10,0)`|
|`DBTYPE_UI8`*| |`numeric(20,0)`|
|`DBTYPE_R4`| |`float`|
|`DBTYPE_R8`| |`real`|
|`DBTYPE_NUMERIC`| |`numeric`|
|`DBTYPE_DECIMAL`| |`decimal`|
|`DBTYPE_CY`| |`money`|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`<br>또는<br> 최대 길이 > 4000자|ntext|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`|nchar|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=false`|nvarchar|
|`DBTYPE_IDISPATCH`| |Error|
|`DBTYPE_ERROR`| |Error|
|`DBTYPE_BOOL`| |`bit`|
|`DBTYPE_VARIANT`*| |nvarchar|
|`DBTYPE_IUNKNOWN`| |Error|
|`DBTYPE_GUID`| |`uniqueidentifier`|
|`DBTYPE_BYTES`|`DBCOLUMNFLAGS_ISLONG=true` <br>또는<br> 최대 길이 > 8000|`image`|
|`DBTYPE_BYTES`|`DBCOLUMNFLAGS_ISROWVER=true`, `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`, 열 크기 = 8 <br>또는<br> 최대 길이가 보고되지 않음 | `timestamp` |
|`DBTYPE_BYTES`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `binary` |
|`DBTYPE_BYTES`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `varbinary`|
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `char`|
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `varchar` |
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISLONG=true` <br>또는<br> 최대 길이 > 8000자 <br>또는<br>   최대 길이가 보고되지 않음 | `text`|
|`DBTYPE_WSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` |`nchar`|
|`DBTYPE_WSTR` | `DBCOLUMNFLAGS_ISFIXEDLENGTH=false`|`nvarchar`|
|`DBTYPE_WSTR`| `DBCOLUMNFLAGS_ISLONG=true` <br>또는<br> 최대 길이 > 4000자 <br>또는<br>   최대 길이가 보고되지 않음 | `ntext`|
|`DBTYPE_UDT`| |Error|
|`DBTYPE_DATE`* | | `datetime` |
|`DBTYPE_DBDATE` | | `datetime`(명시적 변환 필요)|
|`DBTYPE_DBTIME`| | `datetime`(명시적 변환 필요)|
|`DBTYPE_DBTIMESTAMP`* | | `datetime`|
|`DBTYPE_ARRAY` | |Error|
|`DBTYPE_BYREF` | | 무시됨 |
|`DBTYPE_VECTOR` | |Error|
|`DBTYPE_RESERVED`| |Error|

\* SQL Server에 정확히 일치하는 데이터 형식이 없기 때문에 SQL Server 형식의 표현으로 변환됨을 나타냅니다. 이러한 변환으로 인해 정밀도 손실, 오버플로 또는 언더플로가 발생할 수 있습니다. 이후 버전의 SQL Server에서 해당 데이터 형식이 지원되는 경우 나중에 기본 암시적 매핑을 변경할 수 있습니다.

>[!NOTE]
>`numeric(p,s)`은 전체 자릿수가 `p`이고 소수 자릿수가 `s`인 SQL Server 데이터 형식 `numeric`을 나타냅니다. `DBTYPE_NUMERIC` 및 `DBTYPE_DECIMAL`에 허용되는 최대 전체 자릿수는 38입니다. 접근자를 만드는 동안 공급자는 `DBTYPE_BSTR` 열에 대한 바인딩을 `DBTYPE_WSTR`로 지원해야 합니다. `DBTYPE_VARIANT` 열은 유니코드 문자열 `nvarchar`로 사용됩니다. 이 경우 공급자에서 `DBTYPE_VARIANT`와 `DBTYPE_WSTR` 간의 변환을 지원해야 합니다. 공급자는 OLE DB에 정의된 대로 이 변환을 구현해야 합니다. 자세한 내용은 [OLE DB 사양의 데이터 형식](#appendixa)을 참조하세요.

#### <a name="interpreting-data-type-mapping"></a>데이터 형식 매핑 해석

SQL Server 형식에 대한 매핑은 OLE DB 데이터 형식과 열 또는 스칼라 값을 설명하는 DBCOLUMNFLAGS 값에 따라 결정됩니다. `COLUMNS` 스키마 행 집합의 경우 `DATA_TYPE` 및 `COLUMN_FLAGS` 열이 해당 값을 나타냅니다. `IColumnsInfo::GetColumnInfo` 인터페이스의 경우 `DBCOLUMNINFO` 구조체의 `wType` 및 `dwFlags` 멤버가 이 정보를 나타냅니다.

특정 `DBTYPE` 및 `DBCOLUMNFLAG` 값으로 지정된 열의 사용 쪽 매핑을 사용하려면 테이블에서 해당 SQL Server 형식을 찾습니다. 식에 포함된 원격 테이블 열의 형식 규칙은 다음과 같은 간단한 규칙으로 설명할 수 있습니다.

>테이블에서 매핑된 해당 SQL Server 형식이 동일한 컨텍스트에서 유효한 경우 Transact-SQL 식에서 지정된 원격 열 값이 유효합니다.

테이블과 규칙은 다음을 정의합니다.

- 비교 및 식

일반적으로 `X <op> <remote-column>`은 `X`의 데이터 형식과 `<remote-column>`이 매핑되는 데이터 형식에서 `<op>`가 유효한 연산자인 경우 유효한 식입니다.

- 명시적 변환

위의 표와 같이 `<remote-column>`의 `DBTYPE`이 네이티브 데이터 형식 `Y`에 매핑되고 `Y`에서 `X`로의 명시적 변환이 허용되는 경우 `Convert(X, <remote-column>)`가 허용됩니다.

사용자가 원격 데이터를 기본값이 아닌 네이티브 데이터 형식으로 변환하려는 경우 명시적 변환을 사용해야 합니다.

원격 테이블에 대한 `UPDATE` 및 `INSERT` 문에서 내보내기 쪽 매핑을 사용하려면 동일한 테이블을 사용하여 네이티브 SQL Server 데이터 형식을 OLE DB 데이터 형식으로 매핑합니다. 다음 중 하나에 해당하는 경우 SQL Server 형식 `S1`에서 지정된 OLE DB 형식 `T`로 매핑할 수 있습니다.

- 매핑 테이블에서 직접 해당 매핑을 찾을 수 있습니다.

- 매핑 테이블에서 `S2`가 `T`에 매핑되도록 `S1`에서 다른 SQL Server 형식 `S2`로의 암시적 변환이 허용됩니다.

#### <a name="large-object-lob-handling"></a>LOB(Large Object) 처리

매핑 테이블에 표시된 것처럼, `DBTYPE_STR`, `DBTYPE_WSTR` 또는 `DBTYPE_BSTR` 형식의 열이 `DBCOLUMNFLAGS_ISLONG`을 보고하거나 최대 길이가 4,000자를 초과하는 경우(또는 최대 길이가 보고되지 않은 경우) SQL Server는 해당 열을 `text` 또는 `ntext`로 적절하게 처리합니다. 마찬가지로, `DBTYPE_BYTES` 열에서 `DBCOLUMNFLAGS_ISLONG`이 설정되었거나 최대 길이가 8,000바이트를 초과하는 경우(또는 최대 길이가 보고되지 않은 경우) 해당 열은 `image` 열로 처리됩니다. `Text`, `ntext` 및 `image` 열을 LOB 열이라고 합니다.

SQL Server는 OLE DB 공급자의 LOB에 대해 전체 텍스트 및 이미지 기능을 공개하지 않습니다. `TEXTPTRS`는 OLE DB 공급자의 LOB(Large Object)에서 지원되지 않으므로 `TEXTPTR` 시스템 함수, `READTEXT`, `WRITETEXT` 및 `UPDATETEXT` 문과 같은 관련 기능이 지원되지 않습니다. 원격 테이블의 전체 LOB(Large Object) 열에 대한 `UPDATE` 및 `INSERT` 문과 마찬가지로 전체 LOB 열을 검색하는 `SELECT` 문이 지원됩니다.

SQL Server는 공급자가 지원하는 경우 LOB 열에서 구조적 스토리지 인터페이스를 사용합니다. 선호도와 기능의 오름차순으로 구조적 스토리지 인터페이스는 `ISequentialStream`, `Istream` 또는 `ILockBytes`입니다. 이러한 인터페이스 중 하나 이상이 지원되는 경우 공급자는 `IDBProperties` 인터페이스를 통해 쿼리될 때 DBPROPVAL_OO_BLOB을 `DBPROP_OLEOBJECTS` 속성의 값으로 반환해야 합니다. 또한 공급자는 `DBPROP_STRUCTUREDSTORAGE` 속성에 지원되는 인터페이스 지원을 나타내야 합니다.

공급자가 LOB 열에서 구조적 스토리지 인터페이스를 지원하지 않는 경우 SQL Server는 이 인터페이스를 자체적으로 구체화하고 `text`, `ntext` 또는 `image` 열로 계속 공개합니다.

#### <a name="accessing-lob-columns"></a>LOB 열 액세스

공급자가 구조적 스토리지 인터페이스 중 하나를 지원하는 경우 SQL Server는 다음 단계를 수행하여 쿼리 실행 중에 LOB 열을 검색합니다.

1. `IOpenRowset::OpenRowset`를 통해 행 집합을 열기 전에 SQL Server는 LOB(Large Object) 열에 대한 하나 이상의 구조적 스토리지 인터페이스(`ISequentialStream`, `Istream` 및 `ILockBytes`) 지원을 요청합니다. 공급자가 지원하는 첫 번째 인터페이스는 필수입니다. 추가인터페이스는 해당 DBPROP 구조체의 *dwOptions* 요소를 DBPROPOPTIONS_SETIFCHEAP로 설정하여 \"set if cheap\"로 요청됩니다. 예를 들어 공급자가 `ISequentialStream`과 `ILockBytes`를 모두 지원하는 경우 `ISequentialStream`은 필수이고 `ILockBytes`는 \"set if cheap\"로 요청됩니다.

4. 행 집합이 열린 후에 SQL Server는 `IRowsetInfo::GetProperties`를 사용하여 행 집합에서 사용할 수 있는 실제 인터페이스를 식별합니다. 공급자가 반환한 마지막 인터페이스 또는 가장 선호하는 인터페이스가 사용됩니다. SQL Server에서 LOB(Large Object) 열에 대한 접근자를 만들 때 이 열은 바인딩에서 DBOBJECT 구조체의 *iid* 요소가 인터페이스로 설정된 DBTYPE_IUNKNOWN으로 바인딩됩니다.

#### <a name="reading-from-lob-columns"></a>LOB 열에서 읽기

`IRowset::GetData`의 행 버퍼에 반환된 요청된 구조적 스토리지 인터페이스의 인터페이스 포인터를 사용하여 LOB(Large Object) 열에서 읽습니다. 공급자가 동시에 열려 있는 여러 개의 LOB를 지원하지 않는 경우(즉, `DBPROP_MULTIPLE_STORAGEOBJECTS`를 지원하지 않는 경우) 행에 LOB(Large Object) 열이 여러 개 있으면 SQL Server는 LOB 열을 로컬 작업 테이블에 복사합니다.

#### <a name="update-and-insert-statements-on-lob-columns"></a>LOB 열에 대한 `UPDATE` 및 `INSERT` 문

SQL Server는 공급자 제공 인터페이스를 사용하여 스토리지 개체를 수정하는 대신 새 스토리지 개체의 포인터를 공급자에 전달합니다. 각 LOB 열에 대해 스토리지 개체에 업데이트되거나 삽입되는 값은 선택한 구조적 스토리지 인터페이스를 사용하여 생성됩니다. `UPDATE` 또는 `INSERT` 작업 인지에 따라 각각 `IRowsetChange::SetData` 또는 `IRowsetChange::InsertRow`를 통해 스토리지 개체 포인터가 공급자에 전달됩니다.

### <a name="error-handling"></a>오류 처리

OLE DB 공급자에 대한 특정 메서드 호출에서 오류 코드가 반환되면 SQL Server는 오류 조건에 대한 정보를 사용자에게 반환하기 전에 공급자의 확장 오류 정보를 찾습니다.

SQL Server는 OLE DB에 지정된 OLE DB 오류 개체를 사용합니다. 개략적인 몇 가지 단계는 다음과 같습니다.

1. 메서드 호출에서 공급자의 오류 코드가 반환되면 SQL Server는 `ISupportErrorInfo` 인터페이스를 찾습니다. 이 인터페이스가 지원되는 경우 SQL Server는 `ISupportErrorInfo::InterfaceSupportsErrorInfo`를 호출하여 오류 코드를 생성한 인터페이스에서 오류 개체를 지원하는지를 확인합니다.

<!-- -->

5. 인터페이스에서 오류 개체를 지원하는 경우 SQL Server는 `GetErrorInfo` 함수를 호출하여 현재 오류 개체의 `IErrorInfo` 인터페이스 포인터를 가져옵니다.

6. SQL Server는 `IErrorInfo` 인터페이스를 사용하여 `IErrorRecords` 인터페이스에 대한 포인터를 가져옵니다.

7. SQL Server는 `IErrorRecords`를 사용하여 개체의 모든 오류 레코드를 반복하고 각 레코드에 해당하는 오류 메시지 텍스트를 가져옵니다.

공급자의 오류 개체를 사용하는 방법에 대한 자세한 내용은 OLE DB 설명서를 참조하세요.

### <a name="security"></a>보안

소비자가 통합 보안 사용자로 인증하려는 경우가 아니면 소비자가 OLE DB 공급자에 연결할 때 일반적으로 공급자가 사용자 ID와 암호를 요구합니다. 분산 쿼리의 경우 SQL Server는 분산 쿼리를 실행하는 SQL Server 로그인 대신 OLE DB 공급자의 소비자 역할을 합니다. SQL Server는 현재 SQL Server 로그인을 연결된 서버의 사용자 ID와 암호로 매핑합니다.

이러한 매핑은 지정된 연결된 서버에 대해 사용자가 지정할 수 있으며, 시스템 저장 프로시저 `sp_addlinkedsrvlogin` 및 `sp_droplinkedsrvlogin`에서 설정하고 관리할 수 있습니다. `IDBProperties::SetProperties`를 통해 초기화 그룹 속성 DBPROP_AUTH_USERID 및 DBPROP_AUTH_PASSWORD를 설정하면 매핑에 따라 결정된 사용자 ID와 암호가 연결 시 공급자에 전달됩니다.

클라이언트가 Windows 인증을 통해 SQL Server에 연결하는 경우 `sp_addlinkedsrvlogin`을 사용하여 로그인에 `self` 매핑이 설정되어 있으면 SQL Server는 클라이언트의 보안 컨텍스트를 가장하고 연결 시 공급자의 `DBPROP_AUTH_INTEGRATED` 속성을 설정합니다. 이 프로세스를 ‘위임’이라고 합니다. 

연결에 사용되는 보안 컨텍스트를 확인한 후에 이 보안 컨텍스트의 인증과 데이터 원본의 데이터 개체에 대한 해당 컨텍스트의 사용 권한 확인은 전적으로 OLE DB 공급자의 책임입니다.

자세한 내용은 [`sp_addlinkedsrvlogin`](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 및 [`sp_droplinkedsrvlogin`](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)을 참조하세요.

## <a name="query-execution-scenarios"></a>쿼리 실행 시나리오

 분산 쿼리를 평가할 때 SQL Server는 다음 시나리오 중 하나 이상에서 OLE DB 공급자와 상호 작용합니다.

- 원격 쿼리

- 인덱싱된 액세스

- 순수 테이블 검색

- `UPDATE` 및 DELETE 문

- `INSERT` 문

- 통과 쿼리

### <a name="remote-query"></a>Remote Query

SQL Server에서 공급자가 전체적으로 평가할 수 있는 원본 쿼리의 일부를 평가하는 SQL 쿼리를 생성합니다. 이 시나리오는 SQL 명령 공급자에만 적용할 수 있습니다. SQL Server에서 SQL 쿼리를 생성하여 작업을 공급자에 푸시하는 익스텐트는 공급자가 지원하는 SQL 문법에 따라 다릅니다. 공급자는 다음을 통해 SQL 지원 수준을 나타내야 합니다.

1. `DBPROP_SQLSUPPORT` 속성을 통해 SQL Minimum, ODBC Core 또는 SQL-92 항목 수준 지원을 나타냅니다. SQL Minimum 구문 수준은 SQL Server에서 지원되는 새로운 수준으로, SQL Server에서 간단한 SQL 하위 집합을 지원하는 간단한 공급자에 원격 쿼리를 보낼 수 있습니다. 이 수준은 하위 쿼리를 포함하지 않는 기본 `SELECT` 문, `FROM` 절의 여러 테이블(조인 없음) 및 GROUP BY를 포함합니다. SQL Server에서 각 구문 수준의 공급자에 대한 원격 쿼리를 생성하는 데 사용하는 SQL 문법의 하위 집합에 대한 자세한 내용은 [원격 쿼리를 생성하는 데 사용되는 SQL 하위 집합](#appendixb)을 참조하세요.

1. DBPROP_SQLSUPPORT에서 보고된 대로, 기본적으로 구문 수준에 포함되지 않는 개별 SQL 기능 지원을 나타내기 위해 다양한 SQL Server 특정 속성을 지원합니다. 속성 목록과 SQL Server에서 속성을 사용하는 방법은 이 섹션의 뒷부분에서 설명합니다.

SQL Server는 Transact-SQL 문자열에서 물음표(?)를 매개 변수 표식으로 사용하여 매개 변수가 있는 쿼리 실행을 사용합니다. 매개 변수가 있는 쿼리 실행은 SQL Server, Microsoft Jet 및 Oracle OLE DB 공급자에 대해 사용됩니다. 공급자가 `Command` 개체에서 `ICommandWithParameters`를 지원하고 다음 조건 중 하나 이상이 충족되는 경우 다른 공급자에 대해 매개 변수가 있는 쿼리 실행이 사용됩니다.

- 공급자가 `DBPROP_SQLSUPPORT` 속성을 통해 SQL Server 지원의 ODBC 핵심 수준을 나타냅니다.

- 공급자가 `IDBPProperties`를 통해 SQLPROP_DYNCMICSQL SQL Server 특정 속성을 지원하여 물음표(?) 매개 변수 표식을 지원합니다. 자세한 내용은 공급자 속성에 대한 다음 섹션을 참조하세요.

- 관리자가 공급자의 `Dynamic Parameters` 공급자 옵션을 설정하여 SQL Server에서 매개 변수가 있는 쿼리를 생성하도록 합니다.

SQL Server에서 원격으로 실행할 SQL 텍스트를 생성하는 경우 `IDBInfo` 인터페이스의 `DBLITERAL_QUOTE` 리터럴을 통해 보고된 공급자의 따옴표 문자로 테이블 이름과 열 이름에 따옴표가 붙습니다. 이 리터럴이 지원되지 않는 경우에는 테이블 이름과 열 이름에 따옴표가 붙지 않습니다.

공급자가 매개 변수가 있는 쿼리 실행을 지원하는 경우 SQL Server는 매개 변수가 있는 쿼리 실행 전략을 고려하여 로컬 테이블과 원격 테이블의 조인을 평가합니다. 매개 변수가 있는 쿼리는 로컬 테이블의 각 행에서 생성된 매개 변수 값에 대해 반복적으로 실행됩니다. 이 전략은 공급자에서 검색되는 행 수를 줄이며, 적은 수의 행을 포함하는 로컬 테이블을 많은 수의 행이 포함된 원격 테이블과 조인하는 경우에 유용합니다. 이 원격 조인 전략은 `REMOTE` 조인 최적화 프로그램 힌트를 통해 적용할 수 있습니다. 매개 변수가 있는 쿼리 실행에 대한 자세한 내용은 [방법: 매개 변수가 있는 쿼리 수행](../../connect/php/how-to-perform-parameterized-queries.md)을 참조하세요.

다음은 원격 쿼리 시나리오의 공급자에 대한 개략적인 단계입니다.

1. SQL Server가 `IDBCreateCommand::CreateCommand`를 사용하여 `Session` 개체에서 `Command` 개체를 만듭니다.

9. `Remote Query Timeout` 서버 구성 옵션이 0보다 큰 값으로 설정된 경우 SQL Server는 `ICommandProperties::SetProperties`를 사용하여 `Command` 개체의 `DBPROP_COMMANDTIMEOUT` 속성을 동일한 값으로 설정합니다. `ICommand::SetCommandText`를 호출하여 명령 텍스트를 생성된 Transact-SQL 문자열로 설정해야 합니다.

10. SQL Server가 `ICommandPrepare::Prepare`를 호출하여 명령을 준비합니다. 공급자가 이 인터페이스를 지원하지 않는 경우 SQL Server는 4단계를 계속 진행합니다.

11. 생성된 쿼리가 매개 변수가 있는 쿼리인 경우 SQL Server가 `ICommandWithParameters::SetParameterInfo`를 사용하여 매개 변수를 설명하고, `IAccessor::CreateAccessor`를 사용하여 매개 변수의 접근자를 만듭니다.

12. SQL Server가 `ICommand::Execute`를 호출하여 명령을 실행하고 행 집합을 만듭니다.

13. SQL Server가 `IRowset` 인터페이스를 사용하여 테이블의 행을 탐색하고 사용합니다. `IRowset::GetNextRows`를 사용하여 행을 가져오고, `IRowset::RestartPosition`을 사용하여 행 집합의 시작 부분으로 위치를 변경하며, `IRowset::ReleaseRows`를 사용하여 행을 해제합니다.

#### <a name="provider-properties-of-interest-for-remote-query-execution"></a>원격 쿼리 실행에서 중요한 공급자 속성

공급자가 DBPROP_SQLSUPPORT에 보고된 구문 수준에서 적용되지 않는 SQL 기능을 지원하는 경우 다양한 공급자 특정 속성을 사용하여 해당 기능을 나타낼 수 있습니다.

- SQLPROP_GROUPBY. 이 속성은 SQL-Minimum 수준을 지원하는 공급자에서 중요합니다. 이 속성은 공급자가 `SELECT` 문에서 GROUP BY 및 HAVING 절을 지원함을 나타냅니다. 또한 이 속성은 공급자가 MIN, MAX, SUM, COUNT 및 AVG의 5가지 집계 함수를 지원함을 나타냅니다. 공급자는 이러한 집계 함수의 인수에서 DISTINCT를 지원하지 않을 수 있습니다.

- SQLPROP_SUBQUERIES. 이 속성은 SQL-Minimum 수준을 지원하는 공급자에서 중요합니다. 이 속성은 공급자가 SQL-92 항목 수준에 지정된 대로 하위 쿼리를 지원함을 나타냅니다. 여기에는 상호 관련된 하위 쿼리, `IN`, `EXISTS`, `ALL` 및 `ANY` 연산자를 지원하는 `SELECT` 목록과 `WHERE` 절의 하위 쿼리가 포함됩니다.

- SQLPROP_DATELITERALS. 이 속성은 SQL-92 항목 수준을 지원하는 공급자를 포함하여 모든 공급자에서 중요합니다. 날짜/시간 리터럴의 표준 리터럴 구문 지원은 SQL-92 항목 수준에 속하지 않습니다. 이 SQL Server 특정 속성은 공급자가 SQL-92 표준에 지정된 대로 날짜/시간 리터럴 구문을 지원함을 나타냅니다.

- SQLPROP_ANSILIKE. 이 속성은 SQL-Minimum 수준을 지원하는 공급자에서 중요합니다. 이 속성은 공급자가 SQL-92 항목 수준(\'%\' 및 \'_\' 와일드카드 문자)을 기준으로 `LIKE` 연산자를 지원함을 나타냅니다. SQL-Minimum 수준에는 `LIKE` 지원이 포함되지 않으므로 SQL-Minimum 수준을 지원하는 공급자에 대해 사용됩니다.

- SQLPROP_INNERJOIN. 이 속성은 SQL-Minimum 수준을 지원하는 공급자에서 중요합니다. 이 속성은 `FROM` 절에서 여러 테이블이 지원됨을 나타냅니다. SQL-Minimum 수준에는 조인 지원이 포함되지 않으므로 SQL-Minimum 수준만 지원하는 공급자에 대해 사용됩니다. 명시적 JOIN 키워드 및 OUTER 조인이 지원됨을 나타내는 것은 아닙니다. 이 속성은 `FROM` 절에서 테이블 목록을 통해 암시적 조인이 지원된다는 것만 나타냅니다.

- SQLPROP_DYNAMICSQL. `?`가 매개 변수 표식으로 지원됨을 나타냅니다. 매개 변수 표식은 `WHERE` 절 또는 `SELECT` 목록에서 스칼라 항목 대신 지원되어야 합니다. `?` 매개 변수 표식이 지원되면 SQL Server에서 매개 변수가 있는 쿼리를 공급자에 보낼 수 있습니다.

- SQLPROP_NESTEDQUERIES. `FROM` 절에서 중첩된 SELECT가 지원됨을 나타냅니다(예: `SELECT * FROM (SELECT * FROM T))`). 대부분의 경우 SQL Server는 원격으로 실행할 쿼리 문자열을 생성할 때 쿼리의 `FROM` 절에 중첩된 `SELECT` 문을 사용합니다. 중첩된 `SELECT` 지원은 SQL-92 항목 수준에서 필요하지 않으므로 공급자가 이 속성을 설정하지 않는 한, SQL Server는 중첩된 `SELECT` 문이 포함된 쿼리를 공급자에 위임하지 않습니다. 또는 관리자가 공급자의 `Nested Queries` 공급자 옵션을 설정하여 SQL Server에서 공급자에 대한 중첩 쿼리를 생성하도록 할 수도 있습니다.

공급자는 `SQLPROPSET_OPTHINTS`라는 SQL Server 특정 속성 집합을 사용하여 이러한 속성을 지원하고 정의된 `PROPID` 값을 사용할 수 있습니다. 속성 집합 `SQLPROPSET_OPTHINTS`와 두 개의 속성은 다음 상수를 사용하여 정의됩니다.

```
extern const GUID `SQLPROPSET_OPTHINTS` = { 0x2344480c, 0x33a7, 0x11d1, { 0x9b, 0x1a, 0x0, 0x60, 0x8, 0x26, 0x8b, 0x9e } };
enum SQLPROPERTIES {
SQLPROP_NESTEDQUERIES = 0x4,
SQLPROP_DYNAMICSQL = 0x5,
SQLPROP_GROUPBY = 0x6,
SQLPROP_DATELITERALS = 0x7,
SQLPROP_ANSILIKE = 0x8,
SQLPROP_INNERJOIN = 0x9,
SQLPROP_SUBQUERIES = 0x10
};
```

#### <a name="character-set-and-sort-order-implications"></a>문자 집합 및 정렬 순서 영향

SQL Server는 열 수준별로 문자 데이터의 데이터 정렬을 지정할 수 있도록 지원합니다. 비유니코드 문자 데이터(`char` 및 `varchar` 열)의 경우 데이터 정렬에 문자 집합 및 정렬 순서 지정이 모두 포함됩니다. 유니코드 데이터(`nchar` 및 `nvarchar` 열)의 경우에는 데이터 정렬이 정렬 순서만 지정합니다.

SQL Server는 연결된 서버에서 사용하는 문자 집합(비유니코드 데이터), 정렬 순서 및 문자열 비교 의미 체계가 로컬 서버에서 사용하는 것과 동일한 경우에만 문자열 비교를 공급자에 위임합니다.

SQL Server 연결된 서버의 경우 SQL Server에서 데이터 정렬 호환성을 자동으로 결정합니다. 다른 공급자의 경우 관리자가 지정된 연결된 서버에서 사용되는 문자 데이터의 데이터 정렬을 SQL Server에 표시해야 합니다. SQL Server에서 `Collation Name`이라는 새 연결된 서버 옵션이 지원됩니다. 관리자가 연결된 서버에서 채택한 데이터 정렬 의미 체계가 SQL Server 표준 데이터 정렬 중 하나임을 확인하면 `Collation Name` 옵션을 해당 데이터 정렬 이름으로 설정할 수 있습니다. `sp_serveroption` 시스템 저장 프로시저를 사용하여 `Collation Name` 옵션을 설정할 수 있습니다. 이 옵션은 다음 조건이 모두 충족되는 경우에만 설정해야 합니다.

- 원격 정렬 순서와 문자 집합이 지정된 SQL Server 데이터 정렬과 동일합니다.

- OLE DB 공급자에서 사용하는 문자열 비교 의미 체계가 SQL-92 표준 사양 또는 SQL Server의 동등한 비교 의미 체계를 따릅니다.

이전 버전과의 호환성을 위해 SQL Server 7.0에서 지원되는 데이터 정렬 호환 옵션이 계속 지원합니다. true로 설정하는 것은 데이터 정렬 이름 옵션을 SQL Server master 데이터베이스의 기본 데이터 정렬로 설정하는 것과 같습니다. 새 애플리케이션은 데이터 정렬 호환 옵션 대신 데이터 정렬 이름 옵션을 사용해야 합니다.

### <a name="indexed-access"></a>인덱싱된 액세스

SQL Server는 공급자가 공개한 인덱스를 사용하여 분산 쿼리의 특정 조건자를 평가합니다. 이 시나리오는 사용자가 `Index as Access Path` 공급자 옵션을 설정하는 경우 인덱스 공급자에 대해서만 가능합니다. 다음은 인덱스를 사용하여 쿼리를 실행하는 동안 SQL Server에서 공급자에 대해 수행하는 개략적인 주요 단계입니다.

1. 전체 테이블 이름과 인덱스 이름을 사용하여 `IOpenRowset::OpenRowset`를 통해 인덱스 행 집합을 엽니다. 전체 테이블 이름과 인덱스 이름은 앞의 원격 쿼리 시나리오에서 설명한 대로 생성됩니다.

1. 전체 테이블 이름을 사용하여 `IOpenRowset::OpenRowset`를 통해 기본 테이블 행 집합을 엽니다.

1. `IRowsetIndex::SetRange`를 통해 쿼리 조건자를 기준으로 인덱스 행 집합에 범위를 설정합니다.

1. 인덱스 행 집합에 대한 `IRowset`를 통해 인덱스 행 집합에서 행을 검색합니다.

1. 검색된 인덱스 행의 책갈피 열을 사용하여 `IRowsetLocate::GetRowsByBookmark`를 통해 기본 테이블 행 집합에서 해당 행을 가져옵니다.

기본 테이블에 대해 열린 행 집합에서 행 집합 속성 `DBPROP_IRowsetLocate` 및 `DBPROP_BOOKMARKS`는 필수입니다.

### <a name="pure-table-scans"></a>순수 테이블 검색

SQL Server는 공급자에서 전체 원격 테이블을 검색하고 모든 쿼리 평가를 로컬에서 수행합니다. `IOpenRowset::OpenRowset`를 호출하여 테이블에 해당하는 행 집합을 엽니다. SQL Server는 다음과 같이 카탈로그 이름, 스키마 이름 및 개체 이름 부분에서 `OPENROWSET`에 적용되는 테이블 이름을 생성합니다.

1. 각 이름 부분은 공급자의 따옴표 문자(`DBLITERAL_QUOTE`)로 묶인 다음 `DBLITERAL_CATALOG_SEPARATOR` 문자를 사이에 포함하여 연결됩니다.

1. 행 집합 개체가 열린 후에 SQL Server는 `IColumnsInfo` 인터페이스를 사용하여 실행 시간 메타데이터가 테이블의 컴파일 시간 메타데이터와 동일한지 확인합니다.

1. SQL Server가 `IRowset` 인터페이스를 사용하여 테이블의 행을 탐색하고 사용합니다. `IRowset::GetNextRows`를 사용하여 행을 가져오고, `IRowset::RestartPosition`을 사용하여 행 집합의 시작 부분으로 위치를 변경하며, `IRowset::ReleaseRows`를 사용하여 행을 해제합니다.

### <a name="update-and-delete-statements"></a>`UPDATE` 및 `DELETE` 문

SQL Server 분산 쿼리에서 원격 테이블을 업데이트하거나 삭제하려면 다음 조건을 충족해야 합니다.

- 공급자는 업데이트하거나 삭제할 테이블에 대한 `IOpenRowset`를 통해 열린 행 집합에서 책갈피를 지원해야 합니다.

- 공급자는 업데이트하거나 삭제할 테이블에 대한 `IOpenRowset`를 통해 열린 행 집합에서 `IRowsetLocate` 및 `IRowsetChange` 인터페이스를 지원해야 합니다.

- `IRowsetChange` 인터페이스는 업데이트(`SetData`) 및 삭제(`DeleteRows`) 메서드를 지원해야 합니다.

- 공급자가 `ITransactionLocal`을 지원하지 않는 경우 `UPDATE` 및 `DELETE` 문은 사용자 트랜잭션에 없고 해당 공급자에 대해 `Non-transacted` 옵션이 설정된 경우에만 허용됩니다.

- 공급자가 `ITransactionJoin`을 지원하지 않는 경우 `UPDATE` 또는 `DELETE` 문은 사용자 트랜잭션에 없는 경우에만 허용됩니다.

업데이트된 테이블에 대해 열린 행 집합에서 행 집합 속성 `DBPROP_IRowsetLocate`, `DBPROP_IRowsetChange` 및 `DBPROP_BOOKMARKS`는 필수입니다. `DBPROP_UPDATABILITY` 행 집합 속성은 수행된 작업이 각각 `UPDATE` 또는 `DELETE`인지에 따라 `DBPROPVAL_UP_CHANGE` 또는 `DBPROPVAL_UP_DELETE`로 설정됩니다.

`UPDATE` 또는 `DELETE` 작업을 처리하기 위해 공급자에 대해 수행되는 개략적인 단계는 다음과 같습니다.

1. SQL Server가 `IOpenRowset` 인터페이스를 통해 기본 테이블 행 집합을 엽니다. SQL Server를 사용하려면 위에 언급한 행 집합 속성이 필요합니다.

1. SQL Server가 업데이트하거나 삭제해야 하는 행 집합을 결정합니다.

1. SQL Server가 책갈피를 사용하여 `IRowsetLocate` 인터페이스를 통해 적격한 행을 찾습니다.

1. `UPDATE` 작업에는 `IRowsetChange::SetData`를 사용하고, 삭제 작업에는 `IRowsetChange::DeleteRows`를 사용하여 적격한 행에서 필요한 변경 작업을 수행합니다.

### <a name="insert-statement"></a>`INSERT` 문

원격 테이블에 대한 `INSERT` 문의 지원 조건은 `UPDATE` 및 `DELETE` 문보다 덜 엄격합니다.

- 공급자가 삽입되는 기본 테이블에서 열린 행 집합에 대해 `IRowsetChange::InsertRow`를 지원해야 합니다.

- 공급자가 `ITransactionLocal`을 지원하지 않는 경우 `INSERT` 문은 사용자 트랜잭션에 없고 해당 연결된 서버에 대해 `Non-transacted updates` 옵션이 설정된 경우에만 허용됩니다.

- 공급자가 `ITransactionJoin`을 지원하지 않는 경우 `INSERT` 문은 사용자 트랜잭션에 없는 경우에만 허용됩니다.

SQL Server는 `IOpenRowset::OpenRowset`를 사용하여 기본 테이블에서 행 집합을 열고, `IRowsetChange::InsertRow`를 호출하여 기본 행 집합에 새 행을 삽입합니다.

### <a name="pass-through-queries"></a>통과 쿼리

이 시나리오는 `ICommand`에 지정된 명령 텍스트가 사용자가 제출한 명령 문자열이고 SQL Server에서 해석되지 않는다는 점을 제외하고 원격 쿼리의 시나리오와 비슷합니다. SQL Server는 `ICommandText::SetCommandText`를 호출할 때 `DBGUID_DEFAULT`를 언어 식별자로 사용합니다. `DBGUID_DEFAULT`는 공급자가 기본 언어를 사용해야 함을 나타냅니다. 이 명령 텍스트가 두 개 이상의 결과 집합을 반환하는 경우(예: 명령이 여러 개의 결과 집합을 반환하는 저장 프로시저를 호출하는 경우), SQL Server는 명령의 첫 번째 결과 집합만 사용합니다.

SQL Server에서 사용하는 모든 OLE DB 인터페이스 목록은 [SQL Server에서 사용하는 OLE DB 인터페이스](#appendixa)를 참조하세요.

### <a name="conclusion"></a>결론

Microsoft SQL Server는 다른 유형의 데이터 원본에 있는 데이터에 액세스하기 위한 가장 강력한 도구 세트를 제공합니다. 개발자는 SQL Server에서 공개하는 OLE DB 인터페이스를 파악하여 분산 쿼리에서 높은 수준의 제어 및 복잡성을 구현할 수 있습니다.

## <a name="ole-db-interfaces-consumed-by-sql-server"></a><a name="appendixa"></a> SQL Server에서 사용하는 OLE DB 인터페이스

다음 표에는 SQL Server에서 사용하는 OLE DB 인터페이스가 모두 나와 있습니다. 필수 열은 인터페이스가 SQL Server에 필요한 최소 OLE DB 기능에 속하는지 아니면 선택적 요소인지를 나타냅니다. 지정된 인터페이스가 필수로 표시되지 않은 경우에도 SQL Server에서 공급자에 액세스할 수 있지만, 특정 SQL Server 기능 또는 최적화를 공급자에 대해 사용할 수 없습니다.

선택적 인터페이스의 경우, 지정된 인터페이스를 사용하는 여섯 가지 시나리오 중 하나 이상이 시나리오 열에 표시됩니다. 예를 들어 기본 테이블 행 집합의 `IRowsetChange` 인터페이스는 선택적 인터페이스입니다. 이 인터페이스는 `UPDATE` 및 DELETE 문과 `INSERT` 문 시나리오에서 사용됩니다. 이 인터페이스가 지원되지 않는 경우 해당 공급자에 대해 UPDATE, DELETE 및 `INSERT` 문을 지원할 수 없습니다. 다른 선택적 인터페이스 중 일부는 시나리오 열에서 \"성능\"으로 표시되어, 인터페이스의 일반 성능이 향상됨을 나타냅니다. 예를 들어 `IDBSchemaRowset` 인터페이스가 지원되지 않는 경우 SQL Server는 메타데이터와 쿼리 실행을 위해 각각 한 번씩, 행 집합을 두 번 열어야 합니다. `IDBSchemaRowset`를 지원하면 SQL Server 성능이 향상됩니다.

|Object|인터페이스|필수|주석|시나리오|
|:-----|:-----|:-----|:-----|:-----|
|Data Source 개체|`IDBInitialize`|예|데이터와 보안 컨텍스트를 초기화 및 설정합니다.| |
| |`IDBCreateSession`|예|DB 세션 개체를 만듭니다.| |
| |`IDBProperties`|예|공급자의 기능 정보를 가져오고 초기화 속성을 설정합니다. 필수 속성: DBPROP_INIT_TIMEOUT| |
| |`IDBInfo`|예|따옴표 리터럴, 카탈로그, 이름, 부분, 구분 기호, 문자 등을 가져옵니다.|원격 쿼리|
|DB Session 개체|`IDBSchemaRowset`|예|테이블/열 메타데이터를 가져옵니다. 필요한 행 집합: `TABLES`, `COLUMNS`, `PROVIDER_TYPES`. 사용 가능한 경우 사용되는 기타 행 집합: `INDEXES`, `TABLE_STATISTICS`|성능, 인덱싱된 액세스|
| |`IOpenRowset`|예|테이블, 인덱스 또는 히스토그램의 행 집합을 엽니다.| |
| |`IGetDataSource`|예|DB 세션 개체에서 DSO로 다시 가져오는 데 사용합니다.| |
| |`IDBCreateCommand`|예|쿼리를 지원하는 공급자에 대한 명령 개체(쿼리)를 만드는 데 사용합니다.|원격 쿼리, 통과 쿼리|
| |`ITransactionLocal`|예|트랜잭션 업데이트에 사용합니다.|`UPDATE`, `DELETE`, `INSERT` 문|
| |`ITransactionJoin`|예|분산 트랜잭션을 지원하는 데 사용합니다.|사용자 트랜잭션에 있는 경우 `UPDATE`, `DELETE`, `INSERT`|
|Rowset 개체|IRowset|예|행을 검색합니다.| |
| |`IAccessor`|예|행 집합의 열에 바인딩합니다.| |
| |`IColumnsInfo`|예|행 집합의 열에 대한 정보를 가져옵니다.| |
| |`IRowsetInfo`|예|행 집합 속성에 대한 정보를 가져옵니다.| |
| |`IRowsetLocate`|예|`UPDATE`/`DELETE` 작업 및 인덱스 기반 조회를 수행하는 데 필요합니다. 책갈피를 기준으로 행을 조회하는 데 사용합니다.|인덱싱된 액세스, `UPDATE` 및 `DELETE` 문|
| |`IRowsetChange`|예|행 집합의 `INSERTS`/`UPDATES`/ `DELETES`에 필요합니다. 기본 테이블의 행 집합은 `INSERT`, `UPDATE` 및 `DELETE` 문에 대해 이 인터페이스를 지원해야 합니다.|`UPDATE`, `DELETE`, `INSERT` 문|
| |`IConvertType`|예|행 집합이 해당 열에서 특정 데이터 형식 변환을 지원하는지 확인하는 데 사용합니다.| |
|인덱스|`IRowset`|예|행을 검색합니다.|인덱싱된 액세스, 성능|
| |`IAccessor`|예|행 집합의 열에 바인딩합니다.|인덱싱된 액세스, 성능|
| |`IColumnsInfo`|예|행 집합의 열에 대한 정보를 가져옵니다.|인덱싱된 액세스, 성능|
| |`IRowsetInfo`|예|행 집합 속성에 대한 정보를 가져옵니다.|인덱싱된 액세스, 성능|
| |`IRowsetIndex`|예|인덱스의 행 집합에만 필요합니다. 인덱싱 기능(범위 설정, 검색)에 사용합니다.|인덱싱된 액세스, 성능|
|명령|`ICommand`|예| |원격 쿼리, 통과 쿼리|
| |`ICommandText`|예|쿼리 텍스트 정의에 사용합니다.|원격 쿼리, 통과 쿼리|
| |`IColumnsInfo`|예|쿼리 결과의 열 메타데이터를 가져오는 데 사용합니다.|원격 쿼리, 통과 쿼리|
| |`ICommandProperties`|예|명령에서 반환된 행 집합의 필수 속성을 지정하는 데 사용합니다.|원격 쿼리, 통과 쿼리|
| |`ICommandWithParameters`|예|매개 변수가 있는 쿼리 실행에 사용합니다.|원격 쿼리, 성능|
| |`ICommandPrepare`|예|메타데이터를 가져오는 명령을 준비하는 데 사용합니다(사용 가능한 경우 통과 쿼리에 사용됨).|원격 쿼리, 성능|
|Error 개체|`IErrorRecords`|예|단일 오류 레코드에 해당하는 `IErrorInfo` 인터페이스에 대한 포인터를 가져오는 데 사용합니다.| |
| |`IErrorInfo`|예|단일 오류 레코드에 해당하는 `IErrorInfo` 인터페이스에 대한 포인터를 가져오는 데 사용합니다.| |
|Any 개체|`ISupportErrorInfo`|예|지정된 인터페이스가 오류 개체를 지원하는지를 확인하는 데 사용합니다.| |
|  |  |  |  |  |

>[!NOTE]
>`Index` 개체, `Command` 개체 및 `Error` 개체는 필수가 아닙니다. 그러나 지원되는 경우 나열된 인터페이스는 필수 열에 지정된 대로 필수입니다.

## <a name="sql-subset-used-for-generating-remote-queries"></a><a name="appendixb"></a>원격 쿼리 생성에 사용되는 SQL 하위 집합

SQL Server 쿼리 프로세서가 SQL 명령 공급자에 대해 생성하는 SQL 하위 집합은 `DBPROP_SQLSUPPORT` 속성에 표시된 대로 공급자가 지원하는 구문 수준에 따라 달라집니다.

SQL 항목 수준 또는 ODBC 핵심을 지원하는 SQL 명령 공급자

SQL Server는 SQL-92 항목 수준 또는 ODBC 핵심을 지원하는 SQL 명령 공급자에서 평가되는 쿼리에 대해 다음과 같은 SQL 언어 하위 집합을 사용합니다.

1. `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `UNION`, `UNION ALL`, `ORDER BY DESC`, `ASC` 및 `HAVING` 절이 포함된 `SELECT` 문

1. `UNION` 및 `UNION ALL`은 SQL-92 항목 수준을 지원하는 공급자에 대해서만 생성되고 ODBC 핵심을 지원하는 공급자에 대해서는 생성되지 않습니다.

1. `SELECT` 절:

   - `SELECT` 목록의 스칼라 하위 쿼리

   - `AS` 키워드가 없는 열 별칭

1. `FROM` 절:

   - 명시적 조인 키워드는 사용되지 않습니다. 쉼표로 구분된 테이블 이름이 내부 조인을 지정하는 데 사용되고, 외부 조인은 원격 쿼리에 지정되지 않습니다.

   - `FROM` ( `<nested query>` ) `<alias>` 형식의 중첩 쿼리

   - AS 키워드가 없는 테이블 별칭

1. `WHERE` 절은 `NOT` `EXISTS`, `ANY`, `ALL`이 포함된 하위 쿼리를 사용합니다.

1. 식:

   - 사용되는 집계 함수: `MIN([DISTINCT])`, `MAX([DISTINCT])`, `COUNT([DISTINCT])`, `SUM([DISTINCT])`, `AVG([DISTINCT])` 및 `COUNT(*)`

   - 비교 연산자: `<`, `=`, `<=`, `>`, `<>`, `>=`, `IS NULL` 및 `IS NOT NULL`

   - 부울 연산자: `AND`, `OR` 및 `NOT`

 - 산술 연산자: `+`, `-`, `*` 및 `/`

1. 상수:

- 숫자 및 화폐 리터럴은 항상 `( )`로 묶습니다.

- 문자 리터럴은 `' '` 따옴표로 묶습니다.

SQL-Minimum 수준을 지원하는 SQL 명령 공급자

SQL-Minimum 수준을 지원하는 SQL 명령 공급자에 대해 SQL Server는 다음 문법을 사용하여 SQL을 생성합니다.

이 문법은 ODBC 3.0에 설명된 SQL-Minimum 문법을 사용하여 파생되었습니다. 이 문법의 모든 차이점이 강조 표시됩니다. `*bold italics`*로 표시된 항목은 ODBC 3.0에 설명된 SQL-Minimum 문법에 추가된 항목입니다. 녹색으로 삭제 표시된 항목은 이 문법에서 제거된 항목입니다.

*select-statement* ::=

`SELECT [ALL | DISTINCT] *select-list* FROM *table-reference-list*[WHERE *search-condition*] [order-by-clause]`

`SELECT` clause

select-list ::= `*` | `select-sublist [, select-sublist]...`

select-sublist ::= expression * [`alias`]*

`*alias ::= user-defined-name`*

`FROM clause`

table-reference-list ::= table-reference

table-identifier ::= user-defined-name

table-name ::= table-identifier

table-reference ::= table-name

`WHERE clause`

search-condition ::= boolean-term \[OR search-condition\]

boolean-term ::= boolean-factor \[AND boolean-term\]

boolean-factor ::= \[NOT\] boolean-primary

boolean-primary ::= comparison-predicate \| ( search-condition )

comparison-predicate ::= expression comparison-operator expression

*\| `expression IS \[NOT\] NULL`*

comparison-operator ::= `< \| >` \| `<= \| >`= \| = \| `<>`

`ORDER BY clause`

order-by-clause ::= ORDER BY sort-specification \[, sort-specification\]\..

sort-specification ::= { \| column-name } \[ASC \| DESC\]

`Common syntactic elements`

expression ::= term \| expression {+\|--} term

term ::= factor \| term {\*\|/} factor

factor ::= \[+\|--\] primary

primary ::= column-name

\| literal

\| ( expression )

column-name ::= \[table-name.\]column-identifier

literal ::= character-string-literal

*\| integer-literal*

*\| exact-numeric-literal*

character-string-literal ::= \'{character}...\'

문자는 드라이버/데이터 원본의 문자 집합에 있는 모든 문자를 의미합니다. character-string-literal에 단일 리터럴 따옴표 문자(\')를 포함하려면 두 개의 리터럴 따옴표 문자(\'\')를 사용합니다.

`*integer-literal ::=* \[*+ \| -*\] *unsigned-integer`*

`*exact-numeric-literal::=* \[*+ \| -*\] *unsigned-integer* \[*period unsigned-integer*\]`

`*\| period unsigned-integer`*

base-table-name ::= base-table-identifier

base-table-identifier ::= user-defined-name

column-identifier ::= user-defined-name

user-defined-name ::= letter\[digit \| letter \| _\]\..

unsigned-integer ::= {digit}...

digit ::= 0 \| 1 \| 2 \| 3 \| 4 \| 5 \| 6 \| 7 \| 8 \| 9

period ::= . 

## <a name="sql-server-specific-properties"></a><a name="appendixc"></a>SQL Server 특정 속성

```
enum SQLPROPERTIES
       {
       SQLPROP_NOHPNEEDED = 0x1,
       SQLPROP_FREETHREADED = 0x2,
       SQLPROP_UMSENABLED = 0x3,
       SQLPROP_NESTEDQUERIES = 0x4,
       SQLPROP_DYNAMICSQL = 0x5,
       SQLPROP_GROUPBY = 0x6,
       SQLPROP_DATELITERALS = 0x7,
       SQLPROP_ANSILIKE = 0x8,
       SQLPROP_INNERJOIN = 0x9,
       SQLPROP_SUBQUERIES = 0x10, 
       SQLPROP_PARALLELSCAN = 0x11,
       SQLPROP_COLUMNCOLLATION = 0x12,
       SQLPROP_CARDINALITY = 0x13,
       SQLPROP_SIMPLEUPDATES = 0x14,
       SQLPROP_SQLLIKE = 0x15,
       SQLPROP_BITREMOTING = 0x16,
       SQLPROP_UNICODELITERALS = 0x17,
       SQLPROP_USELATESTCOLLATIONVERSION = 0x18
       };

```
