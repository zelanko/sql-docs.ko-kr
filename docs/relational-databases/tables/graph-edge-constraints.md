---
title: 그래프 에지 제약 조건 | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86544dee5262a1d04c1ff1d8e59f8ddac5e9b5ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64774651"
---
# <a name="edge-constraints"></a>에지 제약 조건
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  에지 제약 조건은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 그래프 데이터베이스의 에지 테이블에 데이터 무결성 및 특정 의미 체계를 적용하는 데 사용할 수 있습니다. 
  
이 문서에는 다음과 같은 섹션이 포함되어 있습니다.  
  
[에지 제약 조건](../../relational-databases/tables/graph-edge-constraints.md#Connection)  

[에지 제약 조건](../../relational-databases/tables/graph-edge-constraints.md#Connection)  
  
[관련 작업](../../relational-databases/tables/graph-edge-constraints.md#Tasks)  
  
##  <a name="Connection"></a> 에지 제약 조건
 그래프 기능의 첫 번째 릴리스에서 에지 테이블은 에지 엔드포인트에 대해 어떤 작업도 적용하지 않습니다. 즉, 그래프 데이터베이스의 에지는 해당 형식에 관계없이 노드를 다른 노드에 연결할 수 있습니다. 

 이 릴리스에서는 에지 테이블에 제약 조건을 추가할 수 있도록 하는 에지 제약 조건을 도입하여 특정 의미 체계를 적용하고 데이터 무결성을 유지할 수 있도록 합니다. 에지 제약 조건을 사용하여 새 에지를 에지 테이블에 추가하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 에지가 연결하려고 하는 노드가 적절한 노드 테이블에 있도록 합니다. 또한 노드가 에지에서 여전히 참조되면 노드를 삭제할 수 없도록 합니다. 

 ### <a name="edge-constraint-clauses"></a>에지 제약 조건 절
 각 에지 제약 조건은 하나 이상의 에지 제약 조건 절로 이루어집니다. 에지 제약 조건 절은 지정된 에지가 연결될 수 있는 FROM 및 TO 노드 쌍입니다. 

 그래프에 `Product` 및 `Customer` 노드가 있으며 `Bought` 에지를 사용하여 이러한 노드를 연결한다고 가정합니다. 에지 제약 조건 절은 FROM 및 TO 노드 쌍과 에지 방향을 지정합니다. 이 경우 에지 제약 조건 절은 `Customer` TO `Product`가 됩니다. 즉, `Customer`에서 `Product`로 이동하는 `Bought`를 삽입할 수 있습니다. `Product`에서 `Customer`로 이동하는 에지를 삽입하려고 하면 실패합니다. 
  
- 에지 제약 조건 절은 에지 제약 조건이 적용되는 FROM 및 TO 노드 테이블 쌍을 포함합니다. 
  
- 분리로 적용되는 에지 제약 조건당 여러 에지 제약 조건 절을 지정할 수 있습니다.

- 다중 에지 제약 조건이 단일 에지 테이블에 생성되면 에지는 허용되기 위해 모든 제약 조건을 만족해야 합니다.
  
### <a name="indexes-on-edge-constraints"></a>에지 제약 조건의 인덱스
 에지 제약 조건을 만들어도 에지 테이블의 `$from_id` 및 `$to_id` 열에 해당 인덱스가 자동으로 생성되지 않습니다. `$from_id`에서 인덱스를 수동으로 만들 경우 지점 조회 쿼리 또는 OLTP 워크로드가 있으면 `$to_id` 쌍이 권장됩니다. 

##  <a name="Tasks"></a> 관련 태스크  
 다음 표에서는 에지 제약 조건과 연관된 일반 태스크를 보여 줍니다.  
  
|태스크|아티클|  
|----------|-----------|  
|에지 제약 조건을 만드는 방법을 설명합니다.|[에지 제약 조건 만들기](../../relational-databases/tables/create-edge-constraints.md)|  
|에지 제약 조건을 삭제하는 방법을 설명합니다.|[에지 제약 조건 삭제](../../relational-databases/tables/delete-edge-constraint.md)|  
|에지 제약 조건을 수정하는 방법을 설명합니다.|[에지 제약 조건 수정](../../relational-databases/tables/modify-edge-constraint.md)|  
|에지 제약 조건 속성을 보는 방법을 설명합니다.|[에지 제약 조건 속성 보기](../../relational-databases/tables/view-edge-constraint-properties.md)|  
