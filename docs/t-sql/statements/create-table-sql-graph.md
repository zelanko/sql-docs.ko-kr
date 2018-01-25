---
title: "테이블 (SQL 그래프) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 05/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
dev_langs: TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: 
caps.latest.revision: "1"
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fe8ace1b8f8c55c14d4807514fcb1436f6966fed
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-sql-graph"></a>테이블 (SQL 그래프) 만들기
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

새 테이블을 만들고 SQL 그래프로는 `NODE` 또는 `EDGE` 테이블입니다. 
  
> [!NOTE]   
>  표준 TRANSACT-SQL 문을 참조 하십시오. [CREATE TABLE (TRANSACT-SQL)](../../t-sql/statements/create-table-transact-sql.md)합니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
    AS [ NODE | EDGE ]
[ ; ]  
```  
  
  
## <a name="arguments"></a>인수  
이 문서는 SQL 그래프와 관련 된 인수에만 나열 합니다. 전체 목록과 설명은 지원 되는 인수에 대 한 참조 [CREATE TABLE (TRANSACT-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *database_name*    
 테이블이 생성된 데이터베이스의 이름입니다. *a s e _* 기존 데이터베이스의 이름을 지정 해야 합니다. 지정 하지 않으면 *database_name* 현재 데이터베이스에 대 한 기본값입니다. 현재 연결에 대 한 로그인에 지정 된 데이터베이스의 기존 사용자 ID와 연결 되어 있어야 *database_name*, 되며 해당 사용자 ID는 CREATE TABLE 권한을 갖고 있어야 합니다.  
  
 *schema_name*    
 새 테이블이 속한 스키마의 이름입니다.  
  
 *table_name*    
 노드 또는 edge 테이블의 이름이입니다. 테이블 이름에 대 한 규칙을 따라야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다. *table_name* 최대 로컬 임시 테이블 이름 제외 하 고 128 자가 될 수 있습니다 (단일 숫자 기호를 접두사로 붙은 이름이 (#))는 116 자를 초과할 수 없습니다.  
  
 노드   
 노드 테이블을 만듭니다.

 가장자리  
 Edge 테이블을 만듭니다.  
  
## <a name="remarks"></a>주의  
노드로 임시 테이블 또는 edge 테이블을 만들 수 없습니다.  

노드 또는 edge 테이블을 임시 테이블로 만들 수 없습니다.

스트레치 데이터베이스 노드 또는 edge 테이블에 대해 지원 되지 않습니다.

노드 또는 edge 테이블에는 외부 테이블 (그래프 테이블에 대 한 polybase 지원 없음) 될 수 없습니다. 
  
 
## <a name="examples"></a>예  
  
### <a name="a-create-a-node-table"></a>1. 만들기는 `NODE` 테이블
 만드는 방법을 보여 주는 다음 예제는 `NODE` 테이블

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>2. 만들기는 `EDGE` 테이블
다음 예제를 만드는 방법을 보여 `EDGE` 테이블

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


## <a name="see-also"></a>관련 항목:  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (SQL 그래프)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017을 사용 하 여 처리 하는 그래프](../../relational-databases/graphs/sql-graph-overview.md)

