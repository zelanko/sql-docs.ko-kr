---
title: CREATE TABLE(SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
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
ms.openlocfilehash: cc76bc81bc1f8573430bec9cdeba62b04e25167f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116950"
---
# <a name="create-table-sql-graph"></a>CREATE TABLE(SQL Server)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

새 SQL 그래프 테이블을 `NODE` 또는 `EDGE` 테이블로 만듭니다. 
  
> [!NOTE]   
>  표준 Transact-SQL 문은 [CREATE TABLE(Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE TABLE   
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition> } [ ,...n ] )   
    AS [ NODE | EDGE ]
[ ; ]  
```  
  
  
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
  
## <a name="remarks"></a>Remarks  
임시 테이블을 노드 또는 에지 테이블로 만드는 것은 지원되지 않습니다.  

노드 또는 에지 테이블을 임시 테이블로 만드는 것은 지원되지 않습니다.

Stretch Database는 노드 또는 에지 테이블에서 지원되지 않습니다.

노드 또는 에지 테이블은 외부 테이블(그래프 테이블에 대한 PolyBase 지원 없음)이 될 수 없습니다. 
  
 
## <a name="examples"></a>예  
  
### <a name="a-create-a-node-table"></a>1\. `NODE` 테이블 만들기
 다음 예에서는 `NODE` 테이블을 만드는 방법을 보여 줍니다.

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>2\. `EDGE` 테이블 만들기
다음 예에서는 `EDGE` 테이블을 만드는 방법을 보여 줍니다.

```
 CREATE TABLE friends (
    id integer PRIMARY KEY,
    start_date date
 ) AS EDGE;

```

```
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;

```


## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT(SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017에서 그래프 처리](../../relational-databases/graphs/sql-graph-overview.md)

