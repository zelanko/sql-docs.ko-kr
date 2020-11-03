---
description: SQL 그래프 아키텍처
title: SQL Graph 아키텍처 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c742ebd930066c4e242cabff781b0c61af5f566f
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235580"
---
# <a name="sql-graph-architecture"></a>SQL 그래프 아키텍처  
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

SQL 그래프가 설계 되는 방법에 대해 알아봅니다. 기본 사항을 알면 다른 SQL Graph 문서를 보다 쉽게 이해할 수 있게 됩니다.
 
## <a name="sql-graph-database"></a>SQL 그래프 데이터베이스
사용자는 데이터베이스당 하나의 그래프를 만들 수 있습니다. 그래프는 노드 및에 지 테이블의 컬렉션입니다. 노드 또는에 지 테이블은 데이터베이스의 모든 스키마 아래에서 만들 수 있지만 모두 하나의 논리적 그래프에 속합니다. 노드 테이블은 유사한 유형의 노드 컬렉션입니다. 예를 들어 Person 노드 테이블은 그래프에 속하는 모든 Person 노드를 포함 합니다. 마찬가지로 edge 테이블은 비슷한 형식의 가장자리 모음입니다. 예를 들어 친구에 지 테이블은 사람을 다른 사람에 게 연결 하는 모든 가장자리를 보유 합니다. 노드 및 가장자리가 테이블에 저장 되기 때문에 일반 테이블에서 지원 되는 대부분의 작업은 노드 또는에 지 테이블에서 지원 됩니다. 
 
 
![SQL Graph 데이터베이스 아키텍처를 보여 주는 다이어그램](../../relational-databases/graphs/media/sql-graph-architecture.png "Sql graph 데이터베이스 아키텍처")   

그림 1: SQL Graph 데이터베이스 아키텍처
 
## <a name="node-table"></a>노드 테이블
노드 테이블은 그래프 스키마의 엔터티를 나타냅니다. 사용자 정의 열과 함께 노드 테이블을 만들 때마다 `$node_id` 데이터베이스에서 지정 된 노드를 고유 하 게 식별 하는 암시적 열이 생성 됩니다. 의 값은 `$node_id` 자동으로 생성 되며 `object_id` 해당 노드 테이블과 내부적으로 생성 된 bigint 값의 조합입니다. 그러나 `$node_id` 열을 선택 하면 JSON 문자열 형식의 계산 된 값이 표시 됩니다. 또한 `$node_id` 은 (는) 16 진수 문자열을 포함 하는 내부 이름에 매핑되는 의사 (pseudo) 열입니다. 테이블에서를 선택 하면 `$node_id` 열 이름이로 표시 됩니다 `$node_id_<hex_string>` . 쿼리에서 의사 (pseudo) 열 이름을 사용 하는 것이 좋습니다. 내부 열을 쿼리 하 `$node_id` 고 16 진수 문자열을 사용 하 여 내부 이름을 사용 하지 않는 것이 좋습니다.

사용자가 노드 테이블을 만들 때 열에 unique 제약 조건 또는 인덱스를 만드는 것이 좋지만 `$node_id` , 하나를 만들지 않은 경우 기본 고유 비클러스터형 인덱스가 자동으로 만들어집니다. 그러나 graph 의사 열의 인덱스는 기본 내부 열에 생성 됩니다. 즉, 열에 생성 된 인덱스가 `$node_id` 내부 열에 표시 됩니다 `graph_id_<hex_string>` .   


## <a name="edge-table"></a>Edge 테이블
Edge 테이블은 그래프의 관계를 나타냅니다. 가장자리는 항상 두 노드를 향합니다. Edge 테이블을 사용 하면 사용자가 그래프에서 다 대 다 관계를 모델링할 수 있습니다. Edge 테이블에는 사용자 정의 특성이 있을 수도 있고 없을 수도 있습니다. Edge 테이블이 생성 될 때마다 사용자 정의 특성과 함께 세 개의 암시적 열이 edge 테이블에 생성 됩니다.

|열 이름    |Description  |
|---   |---  |
|`$edge_id`   |데이터베이스의 지정 된 가장자리를 고유 하 게 식별 합니다. 이는 생성 된 열이 고 값은에 지 테이블의 object_id와 내부적으로 생성 된 bigint 값의 조합입니다. 그러나 `$edge_id` 열을 선택 하면 JSON 문자열 형식의 계산 된 값이 표시 됩니다. `$edge_id` 은 (는) 16 진수 문자열을 포함 하는 내부 이름에 매핑되는 의사 (pseudo) 열입니다. 테이블에서를 선택 하면 `$edge_id` 열 이름이로 표시 됩니다 `$edge_id_\<hex_string>` . 쿼리에서 의사 (pseudo) 열 이름을 사용 하는 것이 좋습니다. 내부 열을 쿼리 하 `$edge_id` 고 16 진수 문자열을 사용 하 여 내부 이름을 사용 하지 않는 것이 좋습니다. |
|`$from_id`   |에 지가 발생 `$node_id` 한 노드의를 저장 합니다.  |
|`$to_id`   |에 `$node_id` 지가 종료 되는 노드의를 저장 합니다. |

지정 된 가장자리에 연결할 수 있는 노드는 및 열에 삽입 된 데이터에 의해 제어 됩니다 `$from_id` `$to_id` . 첫 번째 릴리스에서는에 지 테이블에 대 한 제약 조건을 정의 하 여 두 노드 유형의 연결을 제한할 수 없습니다. 즉, 가장자리는 해당 형식에 관계 없이 그래프의 두 노드를 연결할 수 있습니다.

열과 마찬가지로 `$node_id` 사용자는에 지 테이블을 만들 때 열에 대 한 고유한 인덱스나 제약 조건을 만드는 것이 좋지만, 하나를 만들지 않은 `$edge_id` 경우에는이 열에 기본 고유 비클러스터형 인덱스가 자동으로 만들어집니다. 그러나 graph 의사 열의 인덱스는 기본 내부 열에 생성 됩니다. 즉, 열에 생성 된 인덱스가 `$edge_id` 내부 열에 표시 됩니다 `graph_id_<hex_string>` . 또한 OLTP 시나리오의 경우 사용자가 (,) 열에 대 한 인덱스를 `$from_id` 만들어 `$to_id` 가장자리 방향으로 더 빠르게 조회할 수 있도록 하는 것이 좋습니다.  

그림 2에서는 노드 및에 지 테이블을 데이터베이스에 저장 하는 방법을 보여 줍니다. 

![노드 및에 지 테이블 표현을 보여 주는 다이어그램](../../relational-databases/graphs/media/person-friends-tables.png "Person 노드 및 친구에 지 테이블")   

그림 2: 노드 및 edge 테이블 표현



## <a name="metadata"></a>메타데이터
이러한 메타 데이터 뷰를 사용 하 여 노드 또는에 지 테이블의 특성을 볼 수 있습니다.
 
### <a name="systables"></a>sys.tables
다음 새 비트 형식 열이 SYS에 추가 됩니다. 표의. `is_node`이 1로 설정 된 경우이는 테이블이 노드 테이블이 고 `is_edge` 가 1로 설정 된 경우 테이블이에 지 테이블 임을 나타냅니다.
 
|열 이름 |데이터 형식 |Description |
|--- |---|--- |
|is_node |bit |1 = 노드 테이블입니다. |
|is_edge |bit |1 = edge 테이블입니다. |
 
### <a name="syscolumns"></a>sys.columns
`sys.columns`뷰에는 `graph_type` `graph_type_desc` 노드 및에 지 테이블의 열 유형을 나타내는 추가 열 및가 포함 되어 있습니다.
 
|열 이름 |데이터 형식 |Description |
|--- |---|--- |
|graph_type |int |값 집합이 포함 된 내부 열입니다. 그래프 열에 대해 1-8 사이에 값이 있고 다른 값에 대해서는 NULL입니다.  |
|graph_type_desc |nvarchar(60)  |값 집합이 포함 된 내부 열 |
 
다음 표에서는 열에 대 한 유효한 값을 나열 합니다. `graph_type`

|열 값  |Description  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` 또한는 노드 또는에 지 테이블에 생성 되는 암시적 열에 대 한 정보를 저장 합니다. 다음 정보는 sys. 열에서 검색할 수 있지만 사용자는 노드 또는에 지 테이블에서 이러한 열을 선택할 수 없습니다. 

노드 테이블의 암시적 열

|열 이름    |데이터 형식  |is_hidden  |의견  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |내부 `graph_id` 열  |
|$node _id_\<hex_string> |NVARCHAR   |0  |외부 노드 `node_id` 열  |

Edge 테이블의 암시적 열

|열 이름    |데이터 형식  |is_hidden  |의견  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |내부 `graph_id` 열  |
|$edge _id_\<hex_string> |NVARCHAR   |0  |외부 `edge_id` 열  |
|from_obj_id_\<hex_string>  |INT    |1  |노드의 내부 `object_id`  |
|from_id_\<hex_string>  |bigint |1  |노드의 내부 `graph_id`  |
|$from _id_\<hex_string> |NVARCHAR   |0  |노드의 외부 `node_id`  |
|to_obj_id_\<hex_string>    |INT    |1  |내부 노드 `object_id`  |
|to_id_\<hex_string>    |bigint |1  |내부 노드 `graph_id`  |
|$to _id_\<hex_string>   |NVARCHAR   |0  |노드 외부 `node_id`  |
 
### <a name="system-functions"></a>시스템 함수
다음과 같은 기본 제공 함수가 추가 됩니다. 이를 통해 사용자는 생성 된 열에서 정보를 추출할 수 있습니다. 이러한 메서드는 사용자의 입력에 대 한 유효성을 검사 하지 않습니다. 사용자가 잘못 된를 지정 하는 경우 `sys.node_id` 메서드는 적절 한 부분을 추출 하 고 반환 합니다. 예를 들어 OBJECT_ID_FROM_NODE_ID는를 `$node_id` 입력으로 사용 하 고 테이블의 object_id를 반환 합니다 .이 노드는에 속합니다. 
 
|기본 제공   |Description  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |에서 object_id을 추출 합니다. `node_id`  |
|GRAPH_ID_FROM_NODE_ID  |에서 graph_id을 추출 합니다. `node_id`  |
|NODE_ID_FROM_PARTS |및에서 node_id 생성 `object_id``graph_id`  |
|OBJECT_ID_FROM_EDGE_ID |추출 `object_id` 원본 `edge_id`  |
|GRAPH_ID_FROM_EDGE_ID  |Id 추출 `edge_id`  |
|EDGE_ID_FROM_PARTS |`edge_id` `object_id` 및 id에서 생성  |



## <a name="transact-sql-reference"></a>Transact-SQL 참조 
[!INCLUDE[tsql-md](../../includes/tsql-md.md)]그래프 개체를 만들고 쿼리할 수 있는 SQL Server 및 Azure SQL Database에 도입 된 확장에 대해 알아봅니다. 쿼리 언어 확장은 ASCII art 구문을 사용 하 여 그래프를 쿼리하고 트래버스하는 데 도움이 됩니다.
 
### <a name="data-definition-language-ddl-statements"></a>데이터 정의 언어(DDL) 문

|작업   |관련 문서  |메모
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE` 는 이제 노드 또는에 지로 테이블 만들기를 지원 하도록 확장 되었습니다. Edge 테이블에는 사용자 정의 특성이 있을 수도 있고 없을 수도 있습니다.  |
|ALTER TABLE    |[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|노드 및에 지 테이블은를 사용 하 여 관계형 테이블과 동일한 방식으로 변경할 수 있습니다 `ALTER TABLE` . 사용자는 사용자 정의 열, 인덱스 또는 제약 조건을 추가 하거나 수정할 수 있습니다. 그러나 또는와 같은 내부 그래프 열을 변경 하면 `$node_id` `$edge_id` 오류가 발생 합니다.  |
|CREATE  INDEX   |[CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |사용자는 노드 및에 지 테이블의 의사 (pseudo) 열과 사용자 정의 열에 대해 인덱스를 만들 수 있습니다. 클러스터형 및 비클러스터형 columnstore 인덱스를 비롯 한 모든 인덱스 유형이 지원 됩니다.  |
|에 지 제약 조건 만들기    |[Transact-sql&#41;&#40;에 지 제약 조건 ](../../relational-databases/tables/graph-edge-constraints.md)  |사용자는 이제에 지 테이블에 대 한에 지 제약 조건을 만들어 특정 의미 체계를 적용 하 고 데이터 무결성을 유지할 수 있습니다.  |
|DROP TABLE |[DROP TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |를 사용 하 여 관계형 테이블과 동일한 방식으로 노드 및에 지 테이블을 삭제할 수 있습니다 `DROP TABLE` . 그러나이 릴리스에서는 노드 또는 노드 테이블을 삭제할 때 삭제 된 노드를 가리키는 가장자리가 없으며, 노드 또는 노드 테이블을 삭제 하는 경우에는 연속 되는 가장자리를 삭제할 필요가 없습니다. 노드 테이블을 삭제 하는 경우 사용자는 해당 노드 테이블의 노드에 연결 된 모든 가장자리를 수동으로 삭제 하 여 그래프의 무결성을 유지 하는 것이 좋습니다.  |


### <a name="data-manipulation-language-dml-statements"></a>데이터 조작 언어(DML) 문

|작업   |관련 문서  |메모
|---  |---  |---  |
|INSERT |[INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|노드 테이블에 삽입 하는 것은 관계형 테이블에 삽입 하는 것과 다릅니다. `$node_id`열 값이 자동으로 생성 됩니다. 또는 열에 값을 삽입 `$node_id` 하려고 `$edge_id` 하면 오류가 발생 합니다. 사용자 `$from_id` `$to_id` 는에 지 테이블에 삽입 하는 동안 및 열에 대 한 값을 제공 해야 합니다. `$from_id` 및 `$to_id` 는 `$node_id` 지정 된에 지가 연결 하는 노드의 값입니다.  |
|Delete | [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|노드 또는에 지 테이블의 데이터는 관계형 테이블에서 삭제 되는 것과 동일한 방식으로 삭제할 수 있습니다. 그러나이 릴리스에서는 노드 삭제가 지원 되지 않을 때 삭제 된 노드를 가리키는 가장자리가 없고 종속 된 가장자리를 삭제 하지 않도록 하는 제약 조건이 없습니다. 노드가 삭제 될 때마다 해당 노드에 대 한 모든 연결 가장자리가 삭제 되어 그래프의 무결성을 유지 하는 것이 좋습니다.  |
|UPDATE |[UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |UPDATE 문을 사용 하 여 사용자 정의 열의 값을 업데이트할 수 있습니다. 내부 그래프 열,, `$node_id` 및는 `$edge_id` 업데이트할 `$from_id` `$to_id` 수 없습니다.  |
|MERGE |[MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` 노드 또는에 지 테이블에서 문이 지원 됩니다.  |


### <a name="query-statements"></a>쿼리 문

|작업   |관련 문서  |메모
|---  |---  |---  |
|SELECT |[SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|노드와 가장자리는 내부적으로 테이블로 저장 되므로 SQL Server 또는 Azure SQL Database의 테이블에서 지원 되는 대부분의 작업은 노드 및에 지 테이블에서 지원 됩니다.  |
|MATCH  | [Transact-sql&#41;일치 &#40;](../../t-sql/queries/match-sql-graph.md)|기본 제공 일치는 그래프를 통과 하는 패턴 일치 및 트래버스를 지원 하기 위해 도입 되었습니다.  |



## <a name="limitations-and-known-issues"></a>제한 사항 및 알려진 문제  
이 릴리스에서는 노드 및에 지 테이블에 대 한 특정 제한 사항이 있습니다.
* 로컬 또는 전역 임시 테이블은 노드 또는에 지 테이블 일 수 없습니다.
* 테이블 형식 및 테이블 변수는 노드 또는에 지 테이블로 선언할 수 없습니다. 
* 노드와에 지 테이블은 시스템 버전 관리 된 temporal 테이블로 만들 수 없습니다.   
* 노드 및에 지 테이블은 메모리 액세스에 최적화 된 테이블 일 수 없습니다.  
* 사용자는 `$from_id` `$to_id` update 문을 사용 하 여에 지의 및 열을 업데이트할 수 없습니다. Edge가 연결 하는 노드를 업데이트 하기 위해 사용자는 새 노드를 가리키는 새에 지를 삽입 하 고 이전 노드를 삭제 해야 합니다.
* 그래프 개체에 대 한 데이터베이스 간 쿼리는 지원 되지 않습니다. 


## <a name="next-steps"></a>다음 단계
새 구문을 시작 하려면 [SQL Graph 데이터베이스-샘플](./sql-graph-sample.md) 을 참조 하세요.
 

