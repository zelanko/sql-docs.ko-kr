---
title: 설명 된 Columnstore 인덱스 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
author: mikeraymsft
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6220d6650d2be81cad3f38862ba74213219a28a0
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175945"
---
# <a name="columnstore-indexes-described"></a>Columnstore Indexes Described
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] *메모리 내 columnstore 인덱스* 는 열 기반 데이터 저장소 및 열 기반 쿼리 처리를 사용 하 여 데이터를 저장 하 고 관리 합니다. columnstore 인덱스는 주로 대량 로드 및 읽기 전용 쿼리를 수행하는 데이터 웨어하우징 작업에 효과적입니다. columnstore 인덱스를 사용하면 기존의 행 기반 스토리지보다 최대 **10배의 쿼리 성능** 이익과 압축되지 않은 데이터 크기보다 최대 **7배의 데이터 압축** 을 얻을 수 있습니다.

> [!NOTE]
>  클러스터형 columnstore 인덱스를 대형 데이터 웨어하우징 팩트 테이블을 저장하기 위한 표준으로 보고 대부분의 데이터 웨어하우징 시나리오에 사용될 것으로 예상합니다. 클러스터형 columnstore 인덱스는 업데이트 가능하므로 해당 작업에서 많은 삽입, 업데이트 및 삭제 작업을 수행할 수 있습니다.

## <a name="contents"></a>콘텐츠

-   [기본 사항](#basics)

-   [데이터 로드](#dataload)

-   [성능 팁](#performance)

-   [관련 태스크 및 항목](#related)

##  <a name="basics"></a> 기본 사항
 *Columnstore 인덱스* 는 columnstore 라는 칼럼 형식 데이터 형식을 사용 하 여 데이터를 저장, 검색 및 관리 하는 기술입니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 클러스터형 columnstore 인덱스와 비클러스터형 columnstore 인덱스를 모두 지원합니다. 둘 다 동일한 메모리 내 columnstore 기술을 사용하지만 용도와 지원 기능에 차이가 있습니다.

###  <a name="benefits"></a> 이점
 columnstore 인덱스는 대개 큰 데이터 집합을 분석하는 읽기 전용 쿼리에 적합합니다. 주로 데이터 웨어하우징 작업에 대한 쿼리가 여기에 해당합니다. columnstore 인덱스는 전체 테이블 검색을 사용하는 쿼리에는 뛰어난 성능을 제공하지만 특정 값을 찾아 데이터를 검색하는 쿼리에는 부적합합니다.

 columnstore 인덱스의 이점:

-   열에는 비슷한 데이터가 있기 때문에 높은 압축 비율을 나타냅니다.

-   압축 비율이 높으면 메모리 내 사용 공간이 감소되어 쿼리 성능이 향상됩니다. 또한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 더 많은 쿼리 및 데이터 작업을 메모리 내에서 수행할 수 있으므로 쿼리 성능도 개선할 수 있습니다.

-   배치 모드 실행이라는 새로운 쿼리 실행 메커니즘이 SQL Server에 추가되어 CPU 사용량을 크게 줄입니다. 배치 모드 실행은 columnstore 스토리지 형식과 긴밀히 통합되고 그에 맞게 최적화되어 있습니다. 배치 모드 실행을 벡터 기반 또는 벡터화된 실행이라고도 합니다.

-   쿼리는 대개 테이블에서 적은 수의 열만 선택하므로 실제 미디어의 총 I/O가 감소됩니다.

### <a name="columnstore-versions"></a>columnstore 버전
 SQL Server 2012, SQL Server 2012 Parallel Data Warehouse 및 SQL Server 2014 모두 columnstore 인덱스를 사용하여 일반적인 데이터 웨어하우스 쿼리 속도를 높입니다. SQL Server 2012에는 비클러스터형 columnstore 인덱스와 "배치" 단위로 데이터를 처리하는 벡터 기반 쿼리 실행이라는 두 가지 기능이 새로 도입되었습니다. SQL Server 2014는 SQL Server 2012의 기능과 함께 업데이트 가능한 클러스터형 columnstore 인덱스 기능을 제공합니다.

### <a name="key-characteristics"></a>주요 특징

||
|-|
|**적용**대상: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]까지|

 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 클러스터형 columnstore 인덱스는 다음과 같습니다.

-   Enterprise, Developer 및 Evaluation 버전으로 사용할 수 있습니다.

-   업데이트할 수 있습니다.

-   전체 테이블의 주 스토리지 방법입니다.

-   키 열이 없습니다. 모든 열이 포괄 열입니다.

-   테이블에 있는 유일한 인덱스입니다. 다른 인덱스와 함께 사용할 수 없습니다.

-   columnstore 또는 columnstore 보관 압축을 사용하도록 구성할 수 있습니다.

-   열을 정렬 순서에 따라 물리적으로 저장하지 않습니다. 그 대신 압축과 성능을 개선할 수 있는 방법으로 데이터를 저장합니다.

||
|-|
|**적용**대상: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]까지|

 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 비클러스터형 columnstore 인덱스는 다음과 같습니다.

-   열의 하위 집합을 클러스터형 인덱스 또는 힙으로 인덱싱할 수 있습니다. 예를 들어, 자주 사용하는 열을 인덱싱할 수 있습니다.

-   인덱스의 열 복사본을 저장할 추가 스토리지가 필요합니다.

-   인덱스를 다시 작성 하거나 파티션을 전환 하거나 체크 아웃 하 여 업데이트 됩니다. Insert, update, delete 등의 DML 작업을 사용 하 여 업데이트할 수 없습니다.

-   테이블의 다른 인덱스와 결합할 수 있습니다.

-   columnstore 또는 columnstore 보관 압축을 사용하도록 구성할 수 있습니다.

-   열을 정렬 순서에 따라 물리적으로 저장하지 않습니다. 그 대신 압축과 성능을 개선할 수 있는 방법으로 데이터를 저장합니다. columnstore 인덱스 작성 전 데이터 사전 정렬은 필수는 아니지만 columnstore 압축을 향상시킵니다.

###  <a name="Concepts"></a>주요 개념 및 용어
 다음은 columnstore 인덱스와 관련된 주요 용어와 개념입니다.

 columnstore 인덱스 columnstore *인덱스* 는 columnstore 라는 칼럼 형식의 데이터 형식을 사용 하 여 데이터를 저장, 검색 및 관리 하는 기술입니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 클러스터형 columnstore 인덱스와 비클러스터형 columnstore 인덱스를 모두 지원합니다. 둘 다 동일한 메모리 내 columnstore 기술을 사용하지만 용도와 지원 기능에 차이가 있습니다.

 columnstore *columnstore* 는 행과 열이 포함 된 테이블로 논리적으로 구성 되 고 열 단위 데이터 형식으로 물리적으로 저장 되는 데이터입니다.

 rowstore는 행과 열이 있는 테이블로 논리적으로 구성 된 다음 행 단위 데이터 형식으로 물리적으로 저장 되는 *데이터입니다.* 이 방식은 관계형 테이블 데이터를 저장하는 전통적인 방법이었습니다.

 행 그룹 및 열 세그먼트-고성능 및 높은 압축률을 위해 columnstore 인덱스는 테이블을 행 그룹 이라는 행 그룹으로 분할 한 다음 열 단위 방식으로 각 행 그룹을 압축 합니다. 행 그룹의 행 수는 압축률을 높일 만큼 크고, 메모리 내 작업을 활용할 만큼 작아야 합니다.

 행 그룹 A *행 그룹* 은 columnstore 형식으로 동시에 압축 되는 행의 그룹입니다.

 열 세그먼트 *열 세그먼트* 는 행 그룹 내의 데이터 열입니다.

-   열 그룹에는 대개 1,048,576개(행 그룹당 최대 행 수)의 행이 포함됩니다.

-   각 행 그룹에는 테이블의 모든 열에 대해 각각 하나의 열 세그먼트가 포함됩니다.

-   각 열 세그먼트는 함께 압축되며 실제 미디어에 저장됩니다.

 ![열 세그먼트](../../database-engine/media/sql-server-pdw-columnstore-columnsegment.gif "열 세그먼트")

 비클러스터형 columnstore 인덱스 *비클러스터형 columnstore 인덱스* 는 기존 클러스터형 인덱스 또는 힙 테이블에 생성 된 읽기 전용 인덱스입니다. 여기에는 테이블의 모든 열을 포함한 열 하위 집합의 복사본이 들어 있습니다. 테이블은 비클러스터형 columnstore 인덱스를 포함 하는 동안 읽기 전용입니다.

 비클러스터형 columnstore 인덱스는 원래 테이블에 대해 읽기 전용 작업을 수행하면서 동시에 분석 쿼리를 실행하기 위해 columnstore 인덱스를 포함하는 방법을 제공합니다.

 ![비클러스터형 columnstore 인덱스](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage-nonclustered.gif "비클러스터형 columnstore 인덱스")

 클러스터형 columnstore 인덱스 *클러스터형 columnstore 인덱스* 는 전체 테이블에 대 한 물리적 저장소 이며 테이블의 유일한 인덱스입니다. 클러스터형 인덱스는 업데이트할 수 있습니다. 인덱스에 대해 삽입, 삭제 및 업데이트 작업을 수행할 수 있으며, 인덱스로 데이터를 대량 로드할 수 있습니다.

 ![클러스터형 Clustered 인덱스](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage.gif "클러스터형 Clustered 인덱스")

 열 세그먼트의 조각화를 줄이고 성능을 향상시키기 위해 columnstore 인덱스는 삭제된 행에 대한 ID의 B-트리와 함께 deltastore라는 rowstore 테이블에 일부 데이터를 임시로 저장할 수 있습니다. deltastore 작업은 백그라운드에서 처리됩니다. 정확한 쿼리 결과를 반환하기 위해 클러스터형 columnstore 인덱스는 columnstore와 deltastore의 쿼리 결과를 모두 결합합니다.

 deltastore는 클러스터형 columnstore 인덱스에만 사용 되며, *deltastore* 는 행 수가 columnstore로 이동 하기에 충분히 클 때까지 행을 저장 하는 rowstore 테이블입니다. deltastore는 다른 DML 작업과 로드 성능을 향상을 위해 클러스터형 columnstore 인덱스와 함께 사용됩니다.

 대규모 대량 로드 중에 대부분의 행은 deltastore를 통과하지 않고 columnstore로 곧바로 이동합니다. 대량 로드 끝부분의 일부 행은 수가 너무 적어서 행 그룹의 최소 크기(102,400개 행)에 맞지 않을 수 있습니다. 이 경우 최종 행은 columnstore 대신 deltastore로 이동합니다. 행 수가 102,400개 미만인 소규모 대량 로드의 경우 모든 행이 deltastore로 곧바로 이동합니다.

 deltastore가 최대 행 수에 도달하면 닫힙니다. tuple-move 프로세스는 닫힌 행 그룹이 있는지 확인합니다. 닫힌 행 그룹을 찾으면 압축하여 columnstore에 저장합니다.

##  <a name="dataload"></a>데이터 로드 중

###  <a name="dataload_nci"></a>비클러스터형 Columnstore 인덱스로 데이터 로드
 비클러스터형 columnstore 인덱스로 데이터를 로드 하려면 먼저 힙 또는 클러스터형 인덱스로 저장 된 기존의 rowstore 테이블로 데이터를 로드 한 다음 [CREATE COLUMNSTORE index &#40;transact-sql&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)를 사용 하 여 비클러스터형 columnstore 인덱스를 만듭니다.

 ![데이터를 columnstore 인덱스로 로드](../../database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "데이터를 columnstore 인덱스로 로드")

 비클러스터형 columnstore 인덱스가 있는 테이블은 인덱스가 삭제되거나 비활성화될 때까지 읽기 전용입니다. 테이블과 비클러스터형 columnstore 인덱스를 업데이트 하려면 파티션을 내부 및 외부로 전환할 수 있습니다. 인덱스를 사용 하지 않도록 설정 하 고 테이블을 업데이트 한 다음 인덱스를 다시 작성할 수도 있습니다.

 자세한 내용은 [Using Nonclustered Columnstore Indexes](indexes.md)을 참조하세요.

###  <a name="dataload_cci"></a>클러스터형 Columnstore 인덱스로 데이터 로드
 ![클러스터형 columnstore 인덱스로 로드](../../database-engine/media/sql-server-pdw-columnstore-loadprocess.gif "클러스터형 columnstore 인덱스로 로드")

 다이어그램과 같이, 클러스터형 columnstore 인덱스에 데이터를 로드하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 다음 작업을 수행합니다.

1.  최대 크기의 행 그룹을 columnstore에 직접 삽입합니다. 데이터가 로드되면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]은 열려 있는 행 그룹에 데이터 행을 선착순으로 할당합니다.

2.  각 행 그룹에 대해 행 그룹이 최대 크기에 도달한 후 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 다음을 수행합니다.

    1.  행 그룹을 CLOSED로 표시합니다.

    2.  deltastore를 무시합니다.

    3.  columnstore 압축을 사용하여 행 그룹이 있는 각 열 세그먼트를 압축합니다.

    4.  각 압축 열 세그먼트를 columnstore에 물리적으로 저장합니다.

3.  다음과 같이 나머지 행을 columnstore 또는 deltastore에 삽입합니다.

    1.  행 수가 행 그룹당 최대 행 요구 사항을 충족하면 행이 columnstore에 추가됩니다.

    2.  행 수가 행 그룹당 최대 행보다 적으면 행이 deltastore에 추가됩니다.

 deltastore 태스크와 프로세스에 대한 자세한 내용은 [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md)을 참조하세요.

##  <a name="performance"></a>성능 팁

### <a name="plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>병렬로 columnstore 인덱스를 만들기에 충분한 메모리 계획
 인덱스 만들기는 메모리가 제한되지 않는 한 기본적으로 병렬 작업입니다. 병렬로 인덱스를 만들려면 직렬로 인덱스를 만들 때보다 많은 메모리가 필요합니다. 메모리가 충분하면 동일한 열에 B-트리를 작성할 때보다 1.5배 많은 메모리가 columnstore 인덱스를 만드는 데 사용됩니다.

 columnstore 인덱스를 만드는 데 필요한 메모리는 열 수, 문자열 열 수, DOP(병렬 처리 수준) 및 데이터의 특징에 따라 다릅니다. 예를 들어, 테이블의 행 수가 100만 개 미만일 경우 SQL Server는 한 스레드만 사용하여 columnstore 인덱스를 만듭니다.

 테이블 행 수가 100만 개 이상이지만 SQL Server에서 MAXDOP를 사용하여 인덱스를 만들기에 충분한 메모리 부여를 얻을 수 없는 경우 SQL Server에서 사용 가능한 메모리 부여에 맞게 필요한 만큼 자동으로 MAXDOP를 줄입니다.  일부 경우 제한된 메모리로 인덱스를 작성하도록 DOP를 줄여야 합니다.

##  <a name="related"></a>관련 태스크 및 항목

### <a name="nonclustered-columnstore-indexes"></a>비클러스터형 columnstore 인덱스
 일반 태스크는 [Using Nonclustered Columnstore Indexes](../../database-engine/using-nonclustered-columnstore-indexes.md)을 참조하세요.

-   [Transact-sql&#41;&#40;COLUMNSTORE 인덱스 만들기](/sql/t-sql/statements/create-columnstore-index-transact-sql)

-   [ALTER INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/alter-index-transact-sql) (다시 작성).

-   [DROP INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)

### <a name="clustered-columnstore-indexes"></a>클러스터형 columnstore 인덱스
 일반 태스크는 [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md)을 참조하세요.

-   [Transact-sql&#41;&#40;클러스터형 COLUMNSTORE 인덱스 만들기](/sql/t-sql/statements/create-columnstore-index-transact-sql)

-   [ALTER INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/alter-index-transact-sql) 다시 작성 하거나 다시 구성 합니다.

-   [DROP INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)

-   [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)

-   [UPDATE&#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)

-   [DELETE&#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)

### <a name="metadata"></a>메타데이터
 columnstore 인덱스에 있는 모든 열이 메타데이터에 포괄 열로 저장됩니다. columnstore 인덱스에는 키 열이 없습니다.

-   [sys.indexes&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)

-   [sys.index_columns&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)

-   [&#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-partitions-transact-sql)

-   [column_store_segments &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-segments-transact-sql)

-   [column_store_dictionaries &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql)

-   [column_store_row_groups &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql)


