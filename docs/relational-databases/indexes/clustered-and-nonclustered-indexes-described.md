---
title: 클러스터형 및 비클러스터형 인덱스 소개 | Microsoft 문서
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- query optimizer [SQL Server], index usage
- index concepts [SQL Server]
ms.assetid: b7d6b323-728d-4763-a987-92e6292f6f7a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3b0fdb182b3623f4461544d94347544d7d19bf6
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68811135"
---
# <a name="clustered-and-nonclustered-indexes-described"></a>클러스터형 및 비클러스터형 인덱스 소개

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

인덱스는 테이블이나 뷰와 관련된 디스크상 구조로서 테이블이나 뷰의 행 검색 속도를 향상시킵니다. 인덱스에는 테이블이나 뷰에 있는 하나 이상의 열로 작성되는 키가 포함됩니다. 이러한 키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 키 값과 연결된 행을 빠르고 효율적으로 찾을 수 있는 구조(B-트리)에 저장됩니다.

테이블이나 뷰에 포함할 수 있는 인덱스 유형은 다음과 같습니다.

- 클러스터형

  - 클러스터형 인덱스는 해당 키 값을 기반으로 테이블이나 뷰의 데이터 행을 정렬하고 저장합니다. 인덱스 정의에 여러 열이 포함됩니다. 데이터 행 자체는 한 가지 순서로만 저장될 수 있으므로 테이블당 클러스터형 인덱스는 하나만 있을 수 있습니다.  
  - 테이블의 데이터 행이 정렬된 순서로 저장될 때만 테이블에 클러스터형 인덱스가 포함됩니다. 클러스터형 인덱스가 포함된 테이블을 클러스터형 테이블이라고 합니다. 테이블에 클러스터형 인덱스가 없으면 해당 데이터 행은 힙이라는 정렬되지 않은 _구조로 저장됩니다.

- 비클러스터형 인덱스

  - 비클러스터형 인덱스의 구조는 데이터 행으로부터 독립적입니다. 비클러스터형 인덱스에는 비클러스터형 인덱스 키 값이 있으며 각 키 값 항목에는 해당 키 값이 포함된 데이터 행에 대한 포인터가 있습니다.
  - 비클러스터형 인덱스의 인덱스 행에서 데이터 행으로의 포인터를 행 로케이터라고 합니다. 행 로케이터의 구조는 데이터 페이지가 힙에 저장되는지 아니면 클러스터형 테이블에 저장되는지에 따라 다릅니다. 힙의 경우 행 로케이터는 행에 대한 포인터입니다. 클러스터형 테이블의 경우 행 로케이터는 클러스터형 인덱스 키입니다.

  - 클러스터형 인덱스의 리프 수준에 키가 아닌 열을 추가하여 기존 키 제한을 무시하고 완전히 포괄되는 인덱싱된 쿼리를 실행할 수 있습니다. 자세한 내용은 [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)을 참조하세요. 인덱스 키 제한에 대한 자세한 내용은 [SQL Server의 최대 용량 사양](../../sql-server/maximum-capacity-specifications-for-sql-server.md)을 참조하세요.

클러스터형 인덱스와 비클러스터형 인덱스 모두 고유 인덱스가 될 수 있습니다. 이 경우 두 행에 인덱스 키에 대한 동일한 값이 있을 수 없습니다. 동일한 값이 있다면 인덱스는 고유하지 않으며 여러 행에서 동일한 키 값을 공유할 수 있습니다. 자세한 내용은 [고유 인덱스 만들기](../../relational-databases/indexes/create-unique-indexes.md)를 참조하세요.

테이블 데이터가 수정될 때마다 테이블이나 뷰에 대한 인덱스가 자동으로 유지 관리됩니다.

다른 유형의 특수 목적 인덱스에 대한 자세한 내용은 [Indexes](../../relational-databases/indexes/indexes.md) 를 참조하십시오.

## <a name="indexes-and-constraints"></a>인덱스 및 제약 조건

테이블 열에 PRIMARY KEY 및 UNIQUE 제약 조건을 정의하면 인덱스가 자동으로 생성됩니다. 예를 들어 사용자가 UNIQUE 제약 조건이 있는 테이블을 만들면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 자동으로 비클러스터형 인덱스를 만듭니다. PRIMARY KEY를 구성하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 자동으로 클러스터형 인덱스를 만듭니다(클러스터형 인덱스가 없는 경우). 기존 테이블에 PRIMARY KEY 제약 조건을 적용하려 하거나 해당 테이블에 클러스터형 인덱스가 이미 있으면 SQL Server는 비클러스터형 인덱스를 사용하여 기본 키를 적용합니다.

자세한 내용은 [Create Primary Keys](../../relational-databases/tables/create-primary-keys.md) 및 [Create Unique Constraints](../../relational-databases/tables/create-unique-constraints.md)를 참조하세요.

## <a name="how-indexes-are-used-by-the-query-optimizer"></a>쿼리 최적화 프로그램의 인덱스 사용 방법

인덱스를 잘 디자인하면 디스크 I/O 작업과 시스템 리소스 사용을 줄일 수 있으므로 쿼리 성능이 향상됩니다. 인덱스는 SELECT, UPDATE, DELETE 또는 MERGE 문을 포함하는 다양한 쿼리에 유용합니다. `SELECT Title, HireDate FROM HumanResources.Employee WHERE EmployeeID = 250` 데이터베이스의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 을 예로 들어 보겠습니다. 이 쿼리가 실행될 때 쿼리 최적화 프로그램은 데이터 검색에 사용할 수 있는 각 방법을 평가하고 가장 효율적인 방법을 선택합니다. 이때 테이블 검색이 선택될 수 있습니다. 가능한 경우 하나 이상의 인덱스 검색이 선택될 수도 있습니다.

테이블 검색을 수행할 때 쿼리 최적화 프로그램은 테이블의 모든 행을 읽고 쿼리 조건에 맞는 행을 추출합니다. 테이블 검색은 많은 디스크 I/O 작업을 생성하고 리소스를 많이 사용할 수 있습니다. 그러나 예를 들어 쿼리 결과 집합의 행이 테이블에서 높은 비율을 차지할 경우 테이블 검색이 가장 효율적인 방법일 수 있습니다.

쿼리 최적화 프로그램은 인덱스 키 열을 검색하고 쿼리에 필요한 행의 스토리지 위치를 찾은 후 해당 위치에서 일치하는 행을 추출하는 방식으로 인덱스를 사용합니다. 일반적으로 인덱스 검색이 테이블 검색보다 훨씬 빠릅니다. 이는 테이블과 달리 인덱스는 행당 열 수가 매우 적고 행이 정렬되기 때문입니다.

 쿼리 최적화 프로그램은 일반적으로 쿼리 실행 시 가장 효율적인 방법을 선택합니다. 그러나 사용 가능한 인덱스가 없을 경우 쿼리 최적화 프로그램은 테이블 검색을 사용해야 합니다. 쿼리 최적화 프로그램에서 선택할 수 있는 효율적인 인덱스가 충분하도록 하려면 환경에 가장 적합한 인덱스를 여러 개 디자인하고 만들어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제공하는 [데이터베이스 엔진 튜닝 관리자](../../relational-databases/performance/database-engine-tuning-advisor.md) 를 사용하면 데이터베이스 환경을 분석하고 적절한 인덱스를 선택하는 데 도움이 됩니다.

> [!IMPORTANT]
> 인덱스 디자인 지침 및 내부 요소에 대한 자세한 내용은 [SQL Server 인덱스 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)를 참조하세요.

## <a name="related-content"></a>관련 콘텐츠

- [SQL Server 인덱스 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)
- [클러스터형 인덱스 만들기](../../relational-databases/indexes/create-clustered-indexes.md)
- [비클러스터형 인덱스 만들기](../../relational-databases/indexes/create-nonclustered-indexes.md)
