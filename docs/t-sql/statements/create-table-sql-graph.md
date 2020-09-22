---
description: CREATE TABLE(SQL Server)
title: CREATE TABLE(SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL_GRAPH_TSQL
- TABLE
- CREATE_TABLE_TSQL
- NODE
- NODE_TSQL
- AS_NODE
- AS_NODE_TSQL
- EDGE
- EDGE_TSQL
- AS_EDGE
- AS_EDGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc39fbcb191810f7e357167f15c4d0ca084711d8
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688671"
---
# <a name="create-table-sql-graph"></a>CREATE TABLE(SQL Server)
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

새 SQL 그래프 테이블을 `NODE` 또는 `EDGE` 테이블로 만듭니다. 
  
> [!NOTE]   
>  표준 Transact-SQL 문은 [CREATE TABLE(Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CREATE TABLE   
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition> } 
       | <computed_column_definition>
       | <column_set_definition>
       | [ <table_constraint> ] [ ,... n ]
       | [ <table_index> ] }
          [ ,...n ]
    )   
    AS [ NODE | EDGE ]
    [ ON { partition_scheme_name ( partition_column_name )
           | filegroup
           | "default" } ]
[ ; ] 

< table_constraint > ::=
[ CONSTRAINT constraint_name ]
{
    { PRIMARY KEY | UNIQUE }
        [ CLUSTERED | NONCLUSTERED ]
        (column [ ASC | DESC ] [ ,...n ] )
        [
            WITH FILLFACTOR = fillfactor
           |WITH ( <index_option> [ , ...n ] )
        ]
        [ ON { partition_scheme_name (partition_column_name)
            | filegroup | "default" } ]
    | FOREIGN KEY
        ( column [ ,...n ] )
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
        [ NOT FOR REPLICATION ]
    | CONNECTION
        ( { node_table TO node_table } 
          [ , {node_table TO node_table }]
          [ , ...n ]
        )
        [ ON DELETE { NO ACTION | CASCADE } ]
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )
```  
  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
이 문서는 SQL 그래프와 관련된 인수만 나열합니다. 지원되는 인수의 전체 목록 및 설명은 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.

 *database_name*    
 테이블이 생성된 데이터베이스의 이름입니다. *database_name*은 기존 데이터베이스 이름을 지정해야 합니다. *database_name*을 지정하지 않으면 기본적으로 현재 데이터베이스가 됩니다. 현재 연결에 대한 로그인은 *database_name*에 지정된 데이터베이스의 기존 사용자 ID와 연결되어야 하며 해당 사용자 ID는 CREATE TABLE 권한을 갖고 있어야 합니다.  
  
 *schema_name*    
 새 테이블이 속한 스키마의 이름입니다.  
  
 *table_name*      
 노드 또는 에지 테이블의 이름입니다. 테이블 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 적용되는 규칙을 따라야 합니다. 로컬 임시 테이블 이름(단일 숫자 기호(#)가 접두사로 붙은 이름이며 최대 116자)을 제외하면 *table_name*은 최대 128자가 될 수 있습니다.  
  
 NODE   
 노드 테이블을 만듭니다.

 EDGE  
 에지 테이블을 만듭니다.  
 
 *table_constraint*   
 테이블에 추가한 PRIMARY KEY, UNIQUE, FOREIGN KEY, CONNECTION 제약 조건, CHECK 제약 조건이나 DEFAULT 정의의 속성을 지정합니다.
 
 ON { partition_scheme | filegroup | "default" }    
 테이블이 저장된 파티션 구성표 또는 파일 그룹을 지정합니다. partition_scheme을 지정하면 해당 테이블은 partition_scheme에 지정된 하나 이상의 파일 그룹 세트에 파티션이 저장되는 분할된 테이블이 됩니다. filegroup을 지정한 경우에는 테이블이 명명된 파일 그룹에 저장됩니다. 파일 그룹은 데이터베이스 내에 있어야 합니다. "default"를 지정하거나 ON을 전혀 지정하지 않으면 기본 파일 그룹에 테이블이 저장됩니다. CREATE TABLE에 지정된 테이블의 스토리지 메커니즘은 곧이어 변경할 수 없습니다.

 ON {partition_scheme | filegroup | "default"}    
 PRIMARY KEY나 UNIQUE 제약 조건에도 지정할 수 있습니다. 이러한 제약 조건은 인덱스를 만듭니다. filegroup을 지정한 경우에는 인덱스가 명명된 파일 그룹에 저장됩니다. "default"를 지정하거나 ON을 전혀 지정하지 않으면 테이블과 동일한 파일 그룹에 인덱스가 저장됩니다. PRIMARY KEY 또는 UNIQUE 제약 조건이 클러스터형 인덱스를 만드는 경우에는 테이블에 대한 데이터 페이지가 인덱스와 동일한 파일 그룹에 저장됩니다. CLUSTERED를 지정하거나 아니면 제약 조건이 클러스터형 인덱스를 만들고 테이블 정의의 partition_scheme 또는 filegroup과는 다르게 partition_scheme을 지정하거나 그 반대인 경우에는 제약 조건 정의만 유지하고 나머지는 무시합니다.
  
## <a name="remarks"></a>설명  
임시 테이블을 노드 또는 에지 테이블로 만드는 것은 지원되지 않습니다.  

노드 또는 에지 테이블을 임시 테이블로 만드는 것은 지원되지 않습니다.

Stretch Database는 노드 또는 에지 테이블에서 지원되지 않습니다.

노드 또는 에지 테이블은 외부 테이블(그래프 테이블에 대한 PolyBase 지원 없음)이 될 수 없습니다. 

분할되지 않은 그래프 노드/에지 테이블은 분할된 그래프 노드/에지 테이블로 변경할 수 없습니다. 
  
 
## <a name="examples"></a>예제  
  
### <a name="a-create-a-node-table"></a>A. `NODE` 테이블 만들기
 다음 예에서는 `NODE` 테이블을 만드는 방법을 보여 줍니다.

```sql
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. `EDGE` 테이블 만들기
다음 예에서는 `EDGE` 테이블을 만드는 방법을 보여 줍니다.

```sql
 CREATE TABLE friends (
    id INTEGER PRIMARY KEY,
    start_date DATe
 ) AS EDGE;
```

```sql
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;
```


## <a name="see-also"></a>참고 항목 
 [ALTER TABLE table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT(SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017에서 그래프 처리](../../relational-databases/graphs/sql-graph-overview.md)

