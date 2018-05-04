---
title: SQL 그래프 아키텍처 | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
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
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 255d99003dbd37a6edee538e92ef3849f69dc8c0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-graph-architecture"></a>SQL 그래프 아키텍처  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

SQL 그래프의 구성 하는 방법에 대해 알아봅니다. 기본 사항을 알고 있으면 하면 다른 SQL 그래프 문서 이해 하기 쉽습니다.
 
## <a name="sql-graph-database"></a>SQL 그래프 데이터베이스
데이터베이스 마다 하나의 그래프를 만들 수 있습니다. 그래프는 노드 및 가장자리 테이블의 컬렉션입니다. 모두 하나의 논리 그래프에 속하지 있지만 데이터베이스의 모든 스키마에서 노드 또는 edge 테이블을 만들 수 있습니다. 노드 테이블은 비슷한 종류의 노드 컬렉션입니다. 예를 들어 Person 노드 테이블 그래프에 속하는 모든 사람 노드에 보유 합니다. 마찬가지로, edge 테이블은 비슷한 유형의 가장자리의 컬렉션입니다. 예를 들어 친구 edge 테이블을 다른 사용자에 게 사용자를 연결 하는 모든 가장자리 보유 합니다. 노드 및 가장자리 테이블에 저장 되므로, 대부분의 일반적인 테이블에서 지원 되는 작업 노드 또는 edge 테이블에서 지원 됩니다. 
 
 
![sql 그래프 아키텍처](../../relational-databases/graphs/media/sql-graph-architecture.png "Sql 그래프 데이터베이스 아키텍처")   

그림 1: SQL 그래프 데이터베이스 아키텍처
 
## <a name="node-table"></a>노드 테이블
노드 테이블 그래프 스키마의 엔터티를 나타냅니다. 테이블 노드를 만들 때마다, 사용자 정의 열과 함께 암시적 `$node_id` 데이터베이스의 주어진된 노드에 고유 하 게 식별 하는 열이 생성 됩니다. 값 `$node_id` 자동으로 생성 되 고 결합 `object_id` 해당 노드 테이블와 내부적으로 생성 된 bigint 값입니다. 그러나 때는 `$node_id` 열을 선택 하면 JSON 문자열의 형태로 계산 된 값이 표시 됩니다. 또한 `$node_id` 것에 16 진수 문자열이 있는 내부 이름에 매핑되는 의사 열입니다. 선택 하는 경우 `$node_id` 테이블에서 열 이름으로 나타납니다 `$node_id_<hex_string>`합니다. 쿼리에서 의사 열 이름을 사용 하는 것이 좋습니다 내부 쿼리 `$node_id` 열 및 16 진수 문자열이 포함 된 내부 이름을 사용 하 여 피해 야 합니다.

사용자가 unique 제약 조건을 만들거나에서 인덱스 것이 좋습니다는 `$node_id` 열 하나 없으면 노드 테이블 생성 시에 만든 기본 고유, 비클러스터형 인덱스가 자동으로 만들어집니다. 그러나 그래프는 의사 열에 있는 인덱스는 기본 내부 열에서 만들어집니다. 즉, 생성 된 인덱스는 `$node_id` 열을 내부에 표시 됩니다 `graph_id_<hex_string>` 열입니다.   


## <a name="edge-table"></a>Edge 테이블
Edge 테이블에는 그래프의 관계를 나타냅니다. 가장자리는 항상 전송 하 고 두 노드를 연결 합니다. Edge 테이블을 사용 하면 그래프의 모델 다 대 다 관계에 있습니다. Edge 테이블 수도 있습니다 모든 사용자 정의 특성에 들어 있지 않을 수 있습니다. 함께 사용자 정의 특성은 edge 테이블을 만들 때마다 세 개의 암시적 열은 edge 테이블에 만들어집니다.

|열 이름    |Description  |
|---   |---  |
|`$edge_id`   |데이터베이스에 지정 된 가장자리를 고유 하 게 식별 합니다. 생성 된 열이 고 값은 내부적으로 생성 된 bigint 값 및 edge 테이블의 object_id의 조합입니다. 그러나 때는 `$edge_id` 열을 선택 하면 JSON 문자열의 형태로 계산 된 값이 표시 됩니다. `$edge_id` 16 진수 문자열에 있는 내부 이름에 매핑되는 의사 열입니다. 선택 하는 경우 `$edge_id` 테이블에서 열 이름으로 나타납니다 `$edge_id_\<hex_string>`합니다. 쿼리에서 의사 열 이름을 사용 하는 것이 좋습니다 내부 쿼리 `$edge_id` 열 및 16 진수 문자열이 포함 된 내부 이름을 사용 하 여 피해 야 합니다. |
|`$from_id`   |저장소는 `$node_id` 가장자리 시작 되는 위치에서 노드.  |
|`$to_id`   |저장소는 `$node_id` 가장자리 종료 되는 노드의 합니다. |

지정 된 가장자리를 연결할 수 있는 노드에 삽입 된 데이터에 의해 관리는 `$from_id` 및 `$to_id` 열입니다. 첫 번째 릴리스에서 두 가지 유형의 노드를 연결 하지 못하도록 제한 하는 edge 테이블에 제약 조건을 정의 수 없으면입니다. 즉, 가장자리는 해당 형식에 관계 없이 그래프의 두 노드에 연결할 수 있습니다.

비슷합니다는 `$node_id` 열 것이 좋습니다 사용자 고유 인덱스 또는 제약 조건에서 만들는 `$edge_id` 열 하나가 되지 것 이지만 edge 테이블의 생성 시에 만든 고유한 비클러스터형 인덱스가 자동으로 만들어지고 기본 다운로드할 수 있습니다. 그러나 그래프는 의사 열에 있는 인덱스는 기본 내부 열에서 만들어집니다. 즉, 생성 된 인덱스는 `$edge_id` 열을 내부에 표시 됩니다 `graph_id_<hex_string>` 열입니다. 또한 좋습니다, 사용자가 인덱스를 만들 수 있는 OLTP 시나리오에 대 한 (`$from_id`, `$to_id`) 가장자리의 방향에서 더 빠른 조회에 대 한 열입니다.  

그림 2는 노드 및 가장자리 테이블은 데이터베이스에 저장 하는 방법을 보여 줍니다. 

![사용자 친구 테이블](../../relational-databases/graphs/media/person-friends-tables.png "Person 노드 및 friend 가장자리 테이블")   

그림 2: 노드 및 가장자리 테이블 표현



## <a name="metadata"></a>메타데이터
이러한 메타 데이터 뷰를 사용 하 여 노드 또는 edge 테이블의 특성을 참조 하십시오.
 
### <a name="systables"></a>sys.tables
다음 새로 만들었거나, 비트 형식, SYS에 열이 추가 됩니다. 테이블입니다. 경우 `is_node` 테이블 노드 테이블 인지 여부를 나타내는 1로 설정 된 경우 `is_edge` 테이블은 edge 테이블 임을 나타내는 1로 설정 됩니다.
 
|열 이름 |데이터 형식 |Description |
|--- |---|--- |
|is_node |bit |1 =이 테이블은 노드 테이블 |
|is_edge |bit |1 =이 테이블은 edge 테이블 |
 
### <a name="syscolumns"></a>sys.columns
`sys.columns` 추가 열이 뷰에 포함 `graph_type` 및 `graph_type_desc`, 노드 및 가장자리 테이블의 열 유형을 지정 하는 합니다.
 
|열 이름 |데이터 형식 |Description |
|--- |---|--- |
|graph_type |int |값 집합으로 내부 열입니다. 값은 그래프 열에 대해 1-8에서 다른 사용자에 대 한 NULL 까지입니다.  |
|graph_type_desc |nvarchar(60)  |값 집합으로 내부 열 |
 
다음 표에서 유효한 값에 대 한 `graph_type` 열

|열 값  |Description  |
|---   |---   |
|1.  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` 또한 노드 또는 edge 테이블에서 만든 암시적 열에 대 한 정보를 저장 합니다. 하지만 Sys.columns에서 다음 정보를 검색할 수 있습니다 사용자가 수 없는이 열을 선택 하 이러한 노드 또는 edge 테이블에서 합니다. 

노드 테이블의 암시적 열  
|열 이름    |데이터 형식  |is_hidden  |설명  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1.  |내부 graph_id 열  |
|$node_id_\<hex_string> |NVARCHAR   |0  |Id 열을 외부 노드  |

Edge 테이블의 암시적 열  
|열 이름    |데이터 형식  |is_hidden  |설명  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1.  |내부 graph_id 열  |
|$edge_id_\<hex_string> |NVARCHAR   |0  |외부에 지 id 열  |
|from_obj_id_\<hex_string>  |INT    |1.  |내부 노드 개체 id에서  |
|from_id_\<hex_string>  |bigint |1.  |내부 노드 graph_id에서  |
|$from_id_\<hex_string> |NVARCHAR   |0  |외부에서 노드 id  |
|to_obj_id_\<hex_string>    |INT    |1.  |내부 개체의 노드 id  |
|to_id_\<hex_string>    |bigint |1.  |노드 graph_id 내부  |
|$to_id_\<hex_string>   |NVARCHAR   |0  |노드 id에 대 한 외부  |
 
### <a name="system-functions"></a>시스템 함수
다음 기본 제공 함수 추가 됩니다. 이러한 생성 된 열에서 정보를 추출 하는 사용자가 할 수 있습니다. 참고 이러한 메서드는 사용자의 입력, 검사 하지 것입니다. 잘못 된 지정 된 경우 `sys.node_id` 메서드가 적절 한 부분을 추출 하 고 반환 됩니다. OBJECT_ID_FROM_NODE_ID 걸립니다 예를 들어는 `$node_id` 입력로 object_id는 반환이 노드가 속한 테이블의 합니다. 
 
|기본 제공   |Description  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |Object_id는 node_id에서 추출  |
|GRAPH_ID_FROM_NODE_ID  |graph_id 한 node_id에서 추출  |
|NODE_ID_FROM_PARTS |Object_id 및는 graph_id node_id를 생성 합니다.  |
|OBJECT_ID_FROM_EDGE_ID |Object_id edge_id에서 추출  |
|GRAPH_ID_FROM_EDGE_ID  |Identity edge_id에서 추출  |
|EDGE_ID_FROM_PARTS |Object_id 및 id에서 edge_id 생성  |



## <a name="transact-sql-reference"></a>TRANSACT-SQL 참조 
자세한 내용은 [!INCLUDE[tsql-md](../../includes/tsql-md.md)] 확장 SQL Server 및 Azure SQL 데이터베이스에 도입 하는 활성화 만들기 및 개체 그래프를 쿼리 합니다. 쿼리 언어 확장 쿼리 도움말과 ASCII 아트 구문을 사용 하 여 그래프를 트래버스하여 합니다.
 
### <a name="data-definition-language-ddl-statements"></a>데이터 정의 언어 (DDL) 문
|태스크   |관련된 항목  |참고
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE ` AS 노드 또는 AS EDGE 테이블 만들기를 지원 하도록 확장 이제 됩니다. 정의 된 특성을 참고 하 edge 테이블 되거나 모든 사용자를 사용할 수 없습니다.  |
|ALTER TABLE    |[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|노드 및 가장자리 테이블에 관계형 테이블을 사용 하 여 동일한 방식으로 변경할 수는 `ALTER TABLE`합니다. 사용자가 추가 또는 사용자 정의 된 열, 인덱스 또는 제약 조건을 수정할 수 있습니다. 그러나 같은 내부 graph 열 변경 `$node_id` 또는 `$edge_id`, 오류가 발생 합니다.  |
|CREATE  INDEX   |[CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |의사 열과 노드 및 가장자리 테이블의 사용자 정의 된 열에 인덱스를 만들 수 있습니다. 클러스터형 및 비클러스터형 columnstore 인덱스를 포함 하 여 모든 인덱스 유형에 지원 됩니다.  |
|DROP TABLE |[DROP TABLE &#40;Transact SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |노드 및 가장자리 테이블에 관계형 테이블을 사용 하 여 동일한 방식으로 삭제할 수는 `DROP TABLE`합니다. 그러나이 릴리스에서 제약 조건이 없는 없는 가장자리 삭제 된 노드를 가리키도록 하 고 가장자리는 노드 또는 노드 테이블을 삭제 하기 연계 삭제는 지원 되지 않습니다. 노드 테이블이 삭제 되 면 사용자가 수동으로 그래프의 무결성을 유지 하려면 해당 노드 테이블의 노드에 연결 된 모든 가장자리를 삭제 하는 것이 좋습니다.  |


### <a name="data-manipulation-language-dml-statements"></a>데이터 조작 언어 (DML) 문
|태스크   |관련된 항목  |참고
|---  |---  |---  |
|INSERT |[INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|노드 테이블에 삽입 하는 것은 관계형 테이블에 삽입 하는 방법과 다르지 않습니다. 에 대 한 값 `$node_id` 열이 자동으로 생성 됩니다. 값을 삽입 하려고 `$node_id` 또는 `$edge_id` 열에서 오류가 발생 합니다. 사용자에 대 한 값을 제공 해야 `$from_id` 및 `$to_id` edge 테이블에 삽입 하는 동안 열입니다. `$from_id` 및 `$to_id` 됩니다는 `$node_id` 지정 된 가장자리를 연결 하는 노드의 값입니다.  |
|DELETE | [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|노드 또는 edge 테이블의에서 데이터는 관계형 테이블에서 삭제 하는 대로 동일한 방식으로 삭제할 수 있습니다. 그러나이 릴리스에서 제약 조건이 없는 없는 가장자리 삭제 된 노드를 가리키도록 하 고 가장자리는 노드를 삭제 하기 연계 삭제는 지원 되지 않습니다. 노드가 삭제 될 때마다 해당 노드에 대 한 모든 연결 가장자리는도 삭제 되도록, 그래프의 무결성을 유지 하는 것이 좋습니다.  |
|UPDATE |[UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |UPDATE 문을 사용 하 여 사용자 정의 열에 값을 업데이트할 수 있습니다. 내부 그래프 열 업데이트 `$node_id`, `$edge_id`, `$from_id` 및 `$to_id` 허용 되지 않습니다.  |
|MERGE |[MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` 노드 또는 edge 테이블에는 문이 지원 되지 않습니다.  |


### <a name="query-statements"></a>쿼리 문
|태스크   |관련된 항목  |참고
|---  |---  |---  |
|SELECT |[SELECT &#40;TRANSACT-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|대부분의 SQL Server 또는 Azure SQL 데이터베이스 테이블에서 지원 되는 작업의 노드 및 가장자리 테이블에 사용할 수 있으므로, 노드 및 가장자리 내부 테이블로 저장 됩니다.  |
|MATCH  | [일치 &#40;Transact SQL&#41;](../../t-sql/queries/match-sql-graph.md)|기본 제공 일치 하는 패턴 일치 및 그래프를 통해 통과 지원 하기 위해 도입 되었습니다.  |



## <a name="limitations-and-known-issues"></a>제한 사항 및 알려진된 문제  
이 릴리스에서 노드 및 가장자리 테이블에 특정 제한이 있습니다.
* 로컬 또는 전역 임시 테이블에는 노드 또는 edge 테이블 일 수 없습니다.
* 노드 또는 edge 테이블로 테이블 형식 및 테이블 변수를 선언할 수 없습니다. 
* 노드 및 가장자리 테이블은 시스템 버전 임시 테이블로 만들 수 없습니다.   
* 노드 및 가장자리 테이블 메모리 최적화 된 테이블 일 수 없습니다.  
* 사용자가 from_id $ 및 $to_id 열에 UPDATE 문을 사용 하 여 모서리 업데이트할 수 없습니다. 연결 하는 노드를 업데이트 하려면 사용자가 새 노드를 가리키는 새 가장자리를 삽입 하 고 이전 즐겨찾기를 삭제 해야 합니다.
* 데이터베이스 간 그래프 개체에 대 한 쿼리는 지원 되지 않습니다. 


## <a name="next-steps"></a>다음 단계
새 구문을 사용 하 여 시작 하려면 참조 [SQL 그래프 데이터베이스-샘플](./sql-graph-sample.md)
 

