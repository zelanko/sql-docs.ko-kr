---
title: SQL 그래프 아키텍처 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ebf687fb162b1c5c2ec17c0a0a5ec096dcfdd69d
ms.sourcegitcommit: 07d4ebb8438f7c348880c39046e2b452b2152fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2018
ms.locfileid: "47158074"
---
# <a name="sql-graph-architecture"></a>SQL 그래프 아키텍처  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

SQL 그래프를 설계 하는 방법에 대해 알아봅니다. 기본 사항을 알면 되도록 다른 SQL 그래프 문서를 이해 하기 쉽습니다.
 
## <a name="sql-graph-database"></a>SQL 그래프 데이터베이스
데이터베이스당 하나의 그래프를 만들 수 있습니다. 그래프 노드와 지 테이블의 컬렉션인 합니다. 모두 하나의 논리 그래프에 속하지 있지만 데이터베이스의 모든 스키마에서 노드 또는 지 테이블을 만들 수 있습니다. 노드 테이블은 노드의 비슷한 유형의 컬렉션입니다. 예를 들어 Person 노드 테이블을 그래프에 속한 모든 사람 노드를 포함 합니다. 마찬가지로, edge 테이블이 가장자리의 유사한 형식의 컬렉션입니다. 예를 들어, 친구 edge 테이블을 다른 사람에 게 사용자를 연결 하는 모든 가장자리를 보유 합니다. 노드 및에 지 테이블에 저장 되므로, 대부분의 일반적인 테이블에서 지원 되는 작업은 노드 또는 지 테이블에서 지원 됩니다. 
 
 
![sql 그래프 아키텍처](../../relational-databases/graphs/media/sql-graph-architecture.png "Sql 그래프 데이터베이스 아키텍처")   

그림 1: SQL 그래프 데이터베이스 아키텍처
 
## <a name="node-table"></a>노드 테이블
노드 테이블을 그래프 스키마에서 엔터티를 나타냅니다. 노드 테이블을 만들 때마다, 사용자 정의 열과 함께 암시적 `$node_id` 고유 하 게 식별 하는 데이터베이스의 지정된 된 노드 열이 만들어집니다. 에 값 `$node_id` 조합을 자동으로 생성 되며 `object_id` 노드 테이블 및 내부적으로 생성 된 bigint 값을 합니다. 그러나 경우는 `$node_id` 열을 선택 하면 JSON 문자열의 형태로 계산 된 값이 표시 됩니다. 또한 `$node_id` 은 16 진수 문자열을 사용 하 여 내부 이름에 매핑하는 의사 열입니다. 선택 하면 `$node_id` 테이블에서 열 이름으로 나타납니다 `$node_id_<hex_string>`합니다. 쿼리에서 의사 (pseudo) 열 이름을 사용 하 여 권장 되는 방법의 내부 쿼리 `$node_id` 열 및 16 진수 문자열을 사용 하 여 내부 이름을 사용 하 여 피해 야 합니다.

사용자 unique 제약 조건을 만들거나 인덱스가 것이 좋습니다는 `$node_id` 열 하나가 아닌 경우 노드 테이블 생성 시 생성, 기본값 고유, 비클러스터형 인덱스가 자동으로 만들어집니다. 그러나 그래프 의사 열에 있는 인덱스는 기본 내부 열에 만들어집니다. 생성 된 인덱스 이므로 합니다 `$node_id` 열을 내부에 표시 됩니다 `graph_id_<hex_string>` 열입니다.   


## <a name="edge-table"></a>Edge 테이블
Edge 테이블에는 그래프에서 관계를 나타냅니다. 가장자리는 항상 전송 하 고 두 노드를 연결 합니다. Edge 테이블을 그래프에서 다 대 다 관계를 모델링 하는 사용자를 수 있습니다. Edge 테이블을 수도 있습니다에 모든 사용자 정의 특성 없을 수 있습니다. 사용자 정의 특성을 함께 edge 테이블을 만들 때마다 edge 테이블의 세 가지 암시적 열이 생성 됩니다.

|열 이름    |Description  |
|---   |---  |
|`$edge_id`   |데이터베이스에 지정 된 가장자리를 고유 하 게 식별합니다. 생성된 된 열 이며 값은 내부적으로 생성 된 bigint 값을 edge 테이블의 object_id의 조합입니다. 그러나 경우는 `$edge_id` 열을 선택 하면 JSON 문자열의 형태로 계산 된 값이 표시 됩니다. `$edge_id` 16 진수 문자열을 사용 하 여 내부 이름에 매핑하는 의사 (pseudo) 열입니다. 선택 하면 `$edge_id` 테이블에서 열 이름으로 나타납니다 `$edge_id_\<hex_string>`합니다. 쿼리에서 의사 (pseudo) 열 이름을 사용 하 여 권장 되는 방법의 내부 쿼리 `$edge_id` 열 및 16 진수 문자열을 사용 하 여 내부 이름을 사용 하 여 피해 야 합니다. |
|`$from_id`   |저장소는 `$node_id` 가장자리의 원본 위치에서 노드.  |
|`$to_id`   |저장소는 `$node_id` 노드의 가장자리 종료 됩니다. |

지정 된 가장자리를 연결할 수 있는 노드 삽입에 의해 관리 됩니다 합니다 `$from_id` 및 `$to_id` 열입니다. 첫 번째 릴리스에서 edge 테이블 노드의 모든 두 형식을 연결 제한에 대 한 제약 조건을 정의할 수 없습니다. 즉, 가장자리 그래프에서 해당 형식에 관계 없이 두 노드를 연결할 수 있습니다.

비슷합니다는 `$node_id` 열을 것이 좋습니다 사용자가 만든 고유 인덱스 또는 제약 조건에는 `$edge_id` 열 하나가 아닌 경우는 edge 테이블 생성 시 생성, 고유 비클러스터형 인덱스가 자동으로 만들어지고 기본값 이 열입니다. 그러나 그래프 의사 열에 있는 인덱스는 기본 내부 열에 만들어집니다. 생성 된 인덱스 이므로 합니다 `$edge_id` 열을 내부에 표시 됩니다 `graph_id_<hex_string>` 열입니다. 또한 좋습니다, 사용자는 인덱스에 생성 되는 OLTP 시나리오의 경우 (`$from_id`, `$to_id`) 더 빠른 조회 가장자리의 방향에서에 대 한 열입니다.  

그림 2는 노드와 지 테이블은 데이터베이스에 저장 하는 방법을 보여 줍니다. 

![사용자 친구 테이블](../../relational-databases/graphs/media/person-friends-tables.png "Person 노드 및 친구 edge 테이블")   

그림 2: 노드와 지 테이블 표현



## <a name="metadata"></a>메타데이터
이러한 메타 데이터 뷰를 사용 하 여 노드 또는 지 테이블의 특성을 참조 하세요.
 
### <a name="systables"></a>sys.tables
다음의 새로운, bit 형식, SYS에 열이 추가 됩니다. 테이블입니다. 하는 경우 `is_node` 테이블 노드 테이블 인지 여부를 나타내는 1로 설정 된 경우 `is_edge` 테이블이 지 테이블 인지 여부를 나타내는 1로 설정 됩니다.
 
|열 이름 |데이터 형식 |Description |
|--- |---|--- |
|is_node |bit |1 = 노드 테이블입니다. |
|is_edge |bit |1 =는 edge 테이블 |
 
### <a name="syscolumns"></a>sys.columns
`sys.columns` 뷰에 추가 열 `graph_type` 및 `graph_type_desc`, 노드와 지 테이블의 열 형식을 나타내는입니다.
 
|열 이름 |데이터 형식 |Description |
|--- |---|--- |
|graph_type |ssNoversion |값 집합이 포함 된 내부 열입니다. 값은 1 ~ 8 그래프 열에 대 한 다른 사용자에 대 한 NULL 사이 하는 것입니다.  |
|graph_type_desc |nvarchar(60)  |값 집합이 포함 된 내부 열 |
 
다음 표에서 유효한 값은 `graph_type` 열

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


`sys.columns` 또한 노드 또는 지 테이블에 생성 된 암시적 열에 대 한 정보를 저장 합니다. 그러나 Sys.columns에서 다음 정보를 검색할 수 있습니다, 그리고 사용자가 노드 또는 지 테이블에서 이러한 열을 선택할 수 없습니다는 합니다. 

노드 테이블의 암시적 열  
|열 이름    |데이터 형식  |is_hidden  |설명  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |내부 `graph_id` 열  |
|$node_id_\<hex_string> |NVARCHAR   |0  |외부 노드 `node_id` 열  |

Edge 테이블에 암시적 열  
|열 이름    |데이터 형식  |is_hidden  |설명  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |내부 `graph_id` 열  |
|$edge_id_\<hex_string> |NVARCHAR   |0  |외부 `edge_id` 열  |
|from_obj_id_\<hex_string>  |INT    |1  |노드에서 내부 `object_id`  |
|from_id_\<hex_string>  |bigint |1  |노드에서 내부 `graph_id`  |
|$from_id_\<hex_string> |NVARCHAR   |0  |노드에서 외부 `node_id`  |
|to_obj_id_\<hex_string>    |INT    |1  |노드 내부 `object_id`  |
|to_id_\<hex_string>    |bigint |1  |노드 내부 `graph_id`  |
|$to_id_\<hex_string>   |NVARCHAR   |0  |노드 외부 `node_id`  |
 
### <a name="system-functions"></a>시스템 함수
다음 기본 제공 함수를 추가 됩니다. 이러한 하면 사용자가 생성 된 열에서 정보를 추출 합니다. 이러한 메서드는 사용자 로부터 입력을 확인 하지 않습니다는 참고 합니다. 사용자 지정 유효 하지 않은 경우 `sys.node_id` 메서드는 적절 한 부분을 추출 하 고 반환 합니다. OBJECT_ID_FROM_NODE_ID 걸립니다 예를 들어를 `$node_id` 입력과 object_id를 반환 하는이 노드가 속한 테이블의 합니다. 
 
|기본 제공   |Description  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |Object_id에서 추출 된 `node_id`  |
|GRAPH_ID_FROM_NODE_ID  |graph_id 추출를 `node_id`  |
|NODE_ID_FROM_PARTS |node_id를 생성 한 `object_id` 및 `graph_id`  |
|OBJECT_ID_FROM_EDGE_ID |추출 `object_id` 에서 `edge_id`  |
|GRAPH_ID_FROM_EDGE_ID  |id를 추출 합니다. `edge_id`  |
|EDGE_ID_FROM_PARTS |생성할 `edge_id` 에서 `object_id` 및 id  |



## <a name="transact-sql-reference"></a>TRANSACT-SQL 참조 
에 대해 알아봅니다는 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] SQL Server 및 Azure SQL Database에 도입 된 확장 수 있도록 만들고 그래프 개체를 쿼리 합니다. 쿼리 언어 확장 쿼리 도움말과 ASCII art 구문을 사용 하 여 그래프를 트래버스 합니다.
 
### <a name="data-definition-language-ddl-statements"></a>DDL (데이터 정의 언어) 문이
|태스크   |관련된 문서  |참고
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE ` 가 이제 AS 노드 또는 지 AS 테이블 만들기를 지원 하도록 확장 됩니다. 참고 하는 edge 테이블 되거나 사용자 정의 특성이 없을 수 있습니다.  |
|ALTER TABLE    |[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|노드 및에 지 테이블이 관계형 테이블을 사용 하 여 동일한 방식으로 변경할 수는 `ALTER TABLE`합니다. 사용자를 추가 하거나 사용자 정의 열, 인덱스 또는 제약 조건을 수정할 수 있습니다. 그러나 같은 내부 그래프 열 변경 `$node_id` 또는 `$edge_id`, 오류가 발생 합니다.  |
|CREATE  INDEX   |[CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |의사 (pseudo) 열과 노드와 지 테이블의 사용자 정의 열에 인덱스를 만들 수 있습니다. 클러스터형 및 비클러스터형 columnstore 인덱스를 포함 하 여 모든 인덱스 유형에 지원 됩니다.  |
|에 지 제약 조건 만들기    |[에 지 제약 조건은 &#40;TRANSACT-SQL&#41;](../../relational-databases/tables/graph-edge-constraints.md)  |사용자 이제에 지 제약 조건은 특정 의미 체계를 적용할 edge 테이블을 만들 수 있습니다 및 데이터 무결성 유지 관리할 수도  |
|DROP TABLE |[DROP TABLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |노드 및에 지 테이블이 관계형 테이블을 사용 하 여 동일한 방식으로 삭제할 수는 `DROP TABLE`합니다. 그러나이 릴리스에서 제약 조건이 없는 경우가 없는 가장자리 삭제 된 노드를 가리키도록 하 고 가장자리는 노드 또는 노드 테이블 삭제 시 계단식된 삭제는 지원 되지 않습니다. 노드 테이블을 삭제, 사용자가 그래프의 무결성을 유지 하기 위해 수동으로 노드 테이블의 노드에 연결 된 모든 가장자리를 삭제 하는 것이 좋습니다.  |


### <a name="data-manipulation-language-dml-statements"></a>데이터 조작 언어 (DML) 문
|태스크   |관련된 문서  |참고
|---  |---  |---  |
|INSERT |[INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|노드 테이블에 삽입 관계형 테이블에 삽입 하는 데 다르지 않습니다. 값 `$node_id` 열이 자동으로 생성 됩니다. 값을 삽입 하려고 `$node_id` 또는 `$edge_id` 열 오류가 발생 합니다. 사용자에 대 한 값을 제공 해야 합니다 `$from_id` 고 `$to_id` edge 테이블에 삽입 하는 동안 열입니다. `$from_id` 및 `$to_id` 되는 `$node_id` 지정 된 가장자리를 연결 하는 노드의 값입니다.  |
|Delete | [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|노드 또는 지 테이블의 데이터를에서 관계형 테이블에서 삭제 되었으므로 동일한 방식으로 삭제할 수 있습니다. 그러나이 릴리스에서 제약 조건이 없는 없습니다 가장자리 삭제 된 노드를 가리키도록 하 고 가장자리 노드의 삭제 시 계단식된 삭제는 지원 되지 않습니다. 노드 삭제 될 때마다 해당 노드에 대 한 모든 연결 가장자리도를 삭제 했는지 그래프의 무결성을 유지 하는 것이 좋습니다.  |
|UPDATE |[UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |UPDATE 문을 사용 하 여 사용자 정의 열에 값을 업데이트할 수 있습니다. 내부 그래프 열을 업데이트 `$node_id`, `$edge_id`하십시오 `$from_id` 및 `$to_id` 허용 되지 않습니다.  |
|MERGE |[MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` 노드 또는 지 테이블 문이 지원 됩니다.  |


### <a name="query-statements"></a>쿼리 문
|태스크   |관련된 문서  |참고
|---  |---  |---  |
|SELECT |[SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|노드 및 가장자리 내부 테이블로 저장 됩니다., 그리고 노드와 지 테이블에 대부분의 SQL Server 또는 Azure SQL Database의 테이블에서 지원 되는 작업 이므로 지원 됩니다.  |
|MATCH  | [일치 &#40;TRANSACT-SQL&#41;](../../t-sql/queries/match-sql-graph.md)|기본 제공 일치 하는 패턴 일치 및 graph 통해 통과 지원 하기 위해 도입 되었습니다.  |



## <a name="limitations-and-known-issues"></a>제한 사항 및 알려진 문제  
이 릴리스에서 노드와 지 테이블에 특정 제한이 있습니다.
* 로컬 또는 전역 임시 테이블에는 노드 또는 지 테이블 일 수 없습니다.
* 노드 또는 지 테이블로 테이블 형식 및 테이블 변수를 선언할 수 없습니다. 
* 시스템 버전 temporal 테이블로 노드와 지 테이블을 만들 수 없습니다.   
* 노드 및에 지 테이블이 메모리 액세스에 최적화 된 테이블 일 수 없습니다.  
* 사용자가 업데이트할 수 없습니다는 `$from_id` 및 `$to_id` UPDATE 문을 사용 하 여에 지의 열입니다. 연결 하는 노드를 업데이트 하려면 사용자가 새 노드를 가리키는 새 edge를 삽입 하 고 이전에 삭제 해야 합니다.
* 데이터베이스 간 쿼리 그래프 개체에서 지원 되지 않습니다. 


## <a name="next-steps"></a>다음 단계
새 구문을 사용 하 여 시작 하려면 참조 [SQL 그래프 데이터베이스-샘플](./sql-graph-sample.md)
 

