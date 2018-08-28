---
title: Columnstore 인덱스 - 디자인 지침 | Microsoft Docs
ms.custom: ''
ms.date: 12/1/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fc3e22c2-3165-4ac9-87e3-bf27219c820f
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e483a76ece4c87492e1cdd9aa23fbaba6648632
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43068303"
---
# <a name="columnstore-indexes---design-guidance"></a>Columnstore 인덱스 - 디자인 지침
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

columnstore 인덱스 디자인을 위한 고급 권장 사항입니다. 소수의 훌륭한 디자인 결정을 통해 columnstore 인덱스에서 제공하고자 하는 높은 데이터 압축 및 쿼리 성능을 얻을 수 있습니다. 

## <a name="prerequisites"></a>사전 요구 사항

이 문서에서는 columnstore 아키텍처 및 용어에 대해 잘 알고 있다고 가정합니다. 자세한 내용은 [Columnstore 인덱스 - 개요](../../relational-databases/indexes/columnstore-indexes-overview.md) 및 [Columnstore 인덱스 아키텍처](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)를 참조하세요.

### <a name="know-your-data-requirements"></a>데이터 요구 사항 파악
columnstore 인덱스를 디자인하려면 먼저 데이터 요구 사항에 대해 최대한 많이 이해해야 합니다. 예를 들어 다음 질문에 대한 답변을 생각해 보세요.

- 테이블이 얼마나 큰가요?
- 쿼리는 대부분 큰 값 범위를 검색하는 분석을 수행하나요?  columnstore 인덱스는 특정 값 조회가 아닌 큰 범위 검색에 적합하도록 디자인되었습니다.
- 워크로드에서 많은 업데이트 및 삭제를 수행하나요? columnstore 인덱스는 데이터가 안정적일 때 제대로 작동합니다. 쿼리는 행의 10% 미만을 업데이트하고 삭제해야 합니다.
- 데이터 웨어하우스에 대한 팩트 및 차원 테이블이 있나요?
- 트랜잭션 워크로드에 대해 분석을 수행해야 하나요? 이러한 경우 실시간 운영 분석에 대한 columnstore 디자인 지침을 참조하세요.

columnstore 인덱스가 필요하지 않을 수 있습니다. 힙이나 클러스터형 인덱스가 있는 rowstore 테이블은 데이터를 찾는 쿼리, 특정 값을 검색하는 쿼리 또는 작은 범위의 값에 대한 쿼리에 가장 적합합니다. rowstore 인덱스는 큰 범위 테이블 검색 대신 주로 테이블 찾기가 필요한 경향이 있으므로 트랜잭션 워크로드에서 사용됩니다.  

## <a name="choose-the-best-columnstore-index-for-your-needs"></a>요구에 맞는 최상의 columnstore 인덱스 선택

columnstore 인덱스는 클러스터형이거나 비클러스터형입니다.  클러스터형 columnstore 인덱스에는 하나 이상의 비클러스터형 B-트리 인덱스가 있을 수 있습니다. columnstore 인덱스는 쉽게 사용해 볼 수 있습니다. 테이블을 columnstore 인덱스로 만드는 경우 columnstore 인덱스를 삭제하여 테이블을 rowstore 테이블로 다시 쉽게 변환할 수 있습니다. 

다음은 옵션 및 권장 사항에 대한 요약입니다. 

| columnstore 옵션 | 사용하는 경우에 대한 권장 사항 | 압축 |
| :----------------- | :------------------- | :---------- |
| 클러스터형 columnstore 인덱스 | 다음과 같은 경우에 사용됩니다.<br></br>1) 별모양 또는 눈송이 스키마를 사용하는 기존 데이터 웨어하우스 워크로드<br></br>2) 최소 업데이트 및 삭제로 많은 양의 데이터를 삽입하는 IOT(사물 인터넷) 워크로드 | 평균 10배 |
| 클러스터형 columnstore 인덱스의 비클러스터형 B-트리 인덱스 | 다음을 수행하는 데 사용됩니다.<br></br>    1. 클러스터형 columnstore 인덱스에 기본 키 및 외래 키 제약 조건을 적용합니다.<br></br>    2. 특정 값이나 작은 범위의 값을 검색하는 쿼리의 속도를 향상시킵니다.<br></br>    3. 특정 행의 업데이트 및 삭제 속도를 향상시킵니다.| 평균 10배와 NCI에 대한 약간의 추가 저장소.|
| 디스크 기반 힙 또는 B-트리 인덱스의 비클러스터형 columnstore 인덱스 | 다음과 같은 경우에 사용됩니다. <br></br>1) 몇 가지 분석 쿼리가 있는 OLTP 워크로드. 분석을 위해 만든 B-트리 인덱스를 삭제하고 하나의 비클러스터형 columnstore 인덱스로 바꿀 수 있습니다.<br></br>2) ETL(Extract Transform and Load) 작업을 수행하여 별도의 데이터 웨어하우스로 데이터를 이동하는 기존의 많은 OLTP 워크로드. 일부 OLTP 테이블에 비클러스터형 columnstore 인덱스를 만들어 ETL 및 별도의 데이터 웨어하우스를 제거할 수 있습니다. | NCCI는 평균 10% 더 많은 저장소가 필요한 추가 인덱스입니다.|
| 메모리 내 테이블의 columnstore 인덱스 | 기본 테이블이 메모리 내 테이블이라는 점을 제외하면 디스크 기반 테이블의 비클러스터형 columnstore 인덱스와 권장 사항이 동일합니다. | columnstore 인덱스는 추가 인덱스입니다.|

## <a name="use-a-clustered-columnstore-index-for-large-data-warehouse-tables"></a>큰 데이터 웨어하우스 테이블에 클러스터형 columnstore 인덱스 사용
클러스터형 columnstore 인덱스는 인덱스 이상의 의미가 있으며, 기본 테이블 저장소라고 할 수 있습니다. 큰 데이터 웨어하우징 팩트 및 차원 테이블에서 높은 데이터 압축을 제공하며 쿼리 성능을 현저하게 향상시킵니다. 분석 쿼리는 특정 값을 조회하지 않고 큰 범위의 값에 대해 작업을 수행하는 경향이 있으므로 클러스터형 columnstore 인덱스는 트랜잭션 쿼리가 아닌 분석 쿼리에 가장 적합합니다. 

다음과 같은 경우에 클러스터형 columnstore 인덱스를 사용하는 것이 좋습니다.

- 각 파티션에 백만 개 이상의 행이 있습니다. columnstore 인덱스는 각 파티션 내에 행 그룹을 갖습니다. 테이블이 너무 작아서 각 파티션 내의 행 그룹을 채울 수 없는 경우 columnstore 압축 및 쿼리 성능의 이점을 얻을 수 없습니다.
- 쿼리는 주로 값의 범위에 대해 분석을 수행합니다. 예를 들어 열의 평균 값을 찾으려면 쿼리에서 모든 열 값을 검색해야 합니다. 그런 다음 값을 더하여 집계하고 평균을 결정합니다.
- 대부분의 삽입은 최소한의 업데이트 및 삭제로 많은 양의 데이터에서 수행됩니다. IOT(사물 인터넷) 같은 많은 워크로드에서 최소한의 업데이트 및 삭제로 많은 양의 데이터를 삽입합니다. 이러한 워크로드는 클러스터형 columnstore 인덱스 사용으로 제공되는 압축 및 쿼리 성능 이점을 누릴 수 있습니다.

다음과 같은 경우 클러스터형 columnstore 인덱스를 사용하지 마세요.

* 테이블에 varchar(max), nvarchar(max) 또는 varbinary(max) 데이터 형식이 필요합니다. 또는 이러한 열이 포함되지 않도록 columnstore 인덱스를 디자인하세요.
* 테이블 데이터가 영구적이지 않습니다. 데이터를 신속하게 저장하고 삭제해야 하는 경우 힙이나 임시 테이블을 사용하는 것이 좋습니다.
* 테이블에 파티션당 백만 개 미만의 행이 있습니다. 
* 테이블에서 수행되는 작업의 10% 이상이 업데이트 및 삭제입니다. 많은 수의 업데이트 및 삭제를 수행하면 조각화가 발생합니다. 조각화는 모든 데이터를 columnstore에 적용하고 조각화를 제거하는 다시 구성이라는 작업을 실행할 때까지 압축률 및 쿼리 성능에 영향을 줍니다. 자세한 내용은 [columnstore 인덱스에서 인덱스 조각화 최소화](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)를 참조하세요.

자세한 내용은 [Columnstore 인덱스-데이터 웨어하우징](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)을 참조하세요.

## <a name="add-b-tree-nonclustered-indexes-for-efficient-table-seeks"></a>효율적인 테이블 검색을 위해 B-트리 비클러스터형 인덱스 추가

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 클러스터형 columnstore 인덱스의 보조 인덱스로 비클러스터형 B-트리 인덱스를 만들 수 있습니다. 비클러스터형 B-트리 인덱스는 columnstore 인덱스가 변경될 때 업데이트됩니다. 이는 유용하게 사용할 수 있는 강력한 기능입니다. 

보조 B-트리 인덱스를 사용하면 모든 행을 검색하지 않고도 특정 행을 효율적으로 검색할 수 있습니다.  다른 옵션도 사용할 수 있습니다. 예를 들어 B-트리 인덱스에서 UNIQUE 제약 조건을 사용하여 기본 키 또는 외래 키 제약 조건을 적용할 수 있습니다. 고유하지 않은 값은 B-트리 인덱스에 삽입되지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 columnstore에 값을 삽입할 수 없습니다. 

다음과 같은 경우 columnstore 인덱스에서 B-트리 인덱스를 사용하는 것이 좋습니다.
* 특정 값 또는 작은 범위의 값을 검색하는 쿼리를 실행합니다.
* 기본 키 또는 외래 키 제약 조건과 같은 제약 조건을 적용합니다.
* 업데이트 및 삭제 작업을 효율적으로 수행합니다. B-트리 인덱스는 전체 테이블 또는 테이블의 파티션을 검색하지 않고도 특정 행에서 업데이트 및 삭제를 신속하게 찾을 수 있습니다.
* B-트리 인덱스를 저장하는 데 사용할 수 있는 추가 저장소가 있습니다.

## <a name="use-a-nonclustered-columnstore-index-for-real-time-analytics"></a>실시간 분석을 위해 비클러스터형 columnstore 인덱스 사용

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 rowstore 디스크 기반 테이블 또는 메모리 내 OLTP 테이블에 비클러스터형 columnstore 인덱스가 있을 수 있습니다. 따라서 트랜잭션 테이블에서 실시간으로 분석을 실행할 수 있습니다. 트랜잭션이 기본 테이블에서 발생하는 동안 columnstore 인덱스에 대해 분석을 실행할 수 있습니다. 한 테이블에서 두 인덱스를 모두 관리하므로 rowstore 및 columnstore 인덱스 모두 실시간으로 변경할 수 있습니다.

columnstore 인덱스는 rowstore 인덱스보다 10배 더 뛰어난 데이터 압축을 제공하므로 약간의 추가 저장소만 있으면 됩니다. 예를 들어 압축된 rowstore 테이블이 20GB를 사용할 경우 columnstore 인덱스에는 추가 2GB가 필요할 수 있습니다. 또한 필요한 추가 공간은 비클러스터형 columnstore 인덱스에 있는 열의 수에 따라 달라집니다. 

 다음과 같은 경우에 비클러스터형 columnstore 인덱스를 사용하는 것이 좋습니다.

* 트랜잭션 rowstore 테이블에 대해 실시간으로 분석을 실행합니다. 분석을 위해 설계된 기존 B-트리 인덱스를 비클러스터형 columnstore 인덱스로 바꿀 수 있습니다. 
  
*   별도 데이터 웨어하우스가 필요하지 않습니다. 일반적으로 회사는 rowstore 테이블에서 트랜잭션을 실행하고 별도의 데이터 웨어하우스에 데이터를 로드하여 분석을 실행합니다. 많은 워크로드에서 트랜잭션 테이블에 비클러스터형 columnstore 인덱스를 만들어 로드 프로세스 및 별도의 데이터 웨어하우스를 제거할 수 있습니다.

  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]은 이 시나리오의 성능을 향상시킬 수 있는 몇 가지 전략을 제공합니다. OLTP 응용 프로그램을 변경하지 않고도 비클러스터형 columnstore 인덱스를 사용할 수 있으므로 매우 쉽게 체험할 수 있습니다. 

처리 리소스를 더 추가하려면 읽기 가능한 보조 복제본에서 분석을 실행할 수 있습니다. 읽기 가능한 보조 복제본 사용으로 트랜잭션 워크로드 및 분석 워크로드의 처리를 구분합니다. 

자세한 내용은 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)을 참조하세요.

최상의 columnstore 인덱스를 선택하는 방법에 대한 자세한 내용은 Sunil Agarwal의 블로그 [Which columnstore index is right for my workload?](https://blogs.msdn.microsoft.com/sql_server_team/columnstore-index-which-columnstore-index-is-right-for-my-workload)(내 워크로드에 적합한 columnstore 인덱스는 무엇일까요?)를 참조하세요.

## <a name="use-table-partitions-for-data-management-and-query-performance"></a>데이터 관리 및 쿼리 성능을 위해 테이블 파티션 사용
columnstore 인덱스는 데이터를 관리하고 보관하는 적합한 방법인 분할을 지원합니다. 또한 분할에서는 하나 이상의 파티션으로 작업을 제한하여 쿼리 성능이 향상됩니다.

### <a name="use-partitions-to-make-the-data-easier-to-manage"></a>파티션을 사용하여 더 쉽게 데이터 관리
큰 테이블에서 실제로 많은 데이터를 관리할 수 있는 유일한 방법은 파티션 사용입니다. rowstore 테이블에 파티션을 사용할 때의 장점이 columnstore 인덱스에도 적용됩니다. 

예를 들어 rowstore와 columnstore 테이블 모두 파티션을 사용하여 다음을 수행합니다.

- 증분 백업의 크기를 제어합니다. 파티션을 별도의 파일 그룹에 백업한 다음 읽기 전용으로 표시할 수 있습니다. 이렇게 하면 이후 백업에서 읽기 전용 파일 그룹을 건너뜁니다. 
- 오래된 파티션을 저렴한 저장소로 이동하여 저장소 비용을 절감합니다. 예를 들어 파티션 전환을 사용하여 저렴한 저장소 위치로 파티션을 이동할 수 있습니다.
- 작업을 파티션으로 제한하여 효율적으로 작업을 수행합니다. 예를 들어 인덱스 유지 관리를 위해 조각화된 파티션만 대상으로 지정할 수 있습니다.

또한 columnstore 인덱스에서는 분할을 사용하여 다음을 수행합니다.

* 저장소 비용을 추가 30% 절감합니다. COLUMNSTORE_ARCHIVE 압축 옵션을 사용하여 오래된 파티션을 압축할 수 있습니다. 쿼리 성능을 위해 데이터 속도가 느려지므로 파티션이 자주 쿼리되는 경우 적합합니다.

### <a name="use-partitions-to-improve-query-performance"></a>파티션을 사용하여 쿼리 성능 향상

파티션을 사용하면 검색할 행 수를 제한하는 특정 파티션만 검색하도록 쿼리를 제한할 수 있습니다. 예를 들어 인덱스가 연도별로 분할되고 쿼리가 작년의 데이터를 분석하는 경우 한 파티션의 데이터만 검색하면 됩니다. 

### <a name="use-fewer-partitions-for-a-columnstore-index"></a>columnstore 인덱스에 더 적은 수의 파티션 사용

데이터 크기가 충분히 크지 않은 경우 columnstore 인덱스는 rowstore 인덱스에 사용할 수 있는 것보다 더 적은 파티션으로 최상의 성능을 얻을 수 있습니다. 파티션당 백만 개 이상의 행이 있지 않으면 대부분의 행이 columnstore 압축의 성능 혜택을 받지 못하는 deltastore로 이동할 수 있습니다. 예를 들어 10개의 파티션이 있는 테이블에 100만 개 행을 로드하고 각 파티션에서 100, 000개 행을 받으면 모든 행이 델타 행 그룹으로 이동합니다. 

예:
* 1,000,000개 행을 하나의 파티션 또는 분할되지 않은 테이블에 로드합니다. 1,000,000개 행이 있는 압축된 행 그룹 하나를 받습니다. 높은 데이터 압축 및 빠른 쿼리 성능에 적합합니다.
* 1,000,000개 행을 10개의 파티션에 균등하게 로드합니다. 각 파티션은 columnstore 압축의 최소 임계값보다 작은 100,000개 행을 받습니다. 결과적으로 columnstore 인덱스에는 각각 100,000개 행이 있는 10개의 델타 행 그룹이 생성됩니다. columnstore에 델타 행 그룹을 적용하는 방법이 있습니다. 그러나 columnstore 인덱스에 행만 있는 경우 압축된 행 그룹이 너무 작아서 최상의 압축 및 쿼리 성능을 제공할 수 없습니다.

분할에 대한 자세한 내용은 Sunil Agarwal의 블로그 게시물 [Should I partition my columnstore index?](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-should-i-partition-my-columnstore-index/)(내 columnstore 인덱스를 분할해야 하나요?)를 참조하세요.

## <a name="choose-the-appropriate-data-compression-method"></a>적절한 데이터 압축 방법 선택
columnstore 인덱스에서는 columnstore 압축 및 보관 압축이라는 두 가지 데이터 압축 옵션을 제공합니다. 인덱스를 만들 때 압축 옵션을 선택하거나 나중에 [ALTER INDEX ... REBUILD](../../t-sql/statements/alter-index-transact-sql.md)를 사용하여 변경할 수 있습니다.

### <a name="use-columnstore-compression-for-best-query-performance"></a>최적의 쿼리 성능을 위해 columnstore 압축 사용
일반적으로 columnstore 압축은 rowstore 인덱스에 비해 10배 더 뛰어난 압축률을 제공합니다. columnstore 인덱스에 대한 표준 압축 방법이며 빠른 쿼리 성능을 사용할 수 있도록 합니다. 

### <a name="use-archive-compression-for-best-data-compression"></a>최상의 데이터 압축을 위해 보관 압축 사용
보관 압축은 쿼리 성능이 중요하지 않은 경우 최대 압축을 위해 설계되었습니다. 이 압축은 columnstore 압축보다 더 높은 데이터 압축률을 제공하지만 가격이 함께 제공됩니다. 데이터를 압축하고 압축 해제하는 데 더 오래 걸리므로 빠른 쿼리 성능에는 적합하지 않습니다. 

## <a name="use-optimizations-when-you-convert-a-rowstore-table-to-a-columnstore-index"></a>rowstore 테이블을 columnstore 인덱스로 변환할 때 최적화 사용

데이터가 이미 rowstore 테이블에 있는 경우 [CREATE COLUMNSTORE INDEX](../../t-sql/statements/create-columnstore-index-transact-sql.md)를 사용하여 테이블을 클러스터형 columnstore 인덱스로 변환할 수 있습니다. 테이블을 변환한 후 쿼리 성능을 향상시키는 몇 가지 최적화 방법이 있으며, 이어서 설명하겠습니다.

### <a name="use-maxdop-to-improve-rowgroup-quality"></a>MAXDOP를 사용하여 행 그룹 품질 향상
힙 또는 클러스터형 B-트리 인덱스를 columnstore 인덱스로 변환하기 위해 최대 수의 프로세서를 구성할 수 있습니다. 프로세서를 구성하려면 최대 병렬 처리 수준 옵션(MAXDOP)을 사용합니다. 

데이터가 많은 경우 MAXDOP 1은 너무 느릴 수 있습니다.  MAXDOP를 4로 높이면 제대로 작동합니다. 행 수가 최적이 아닌 몇 개의 행 그룹이 생성되면 [ALTER INDEX REORGANIZE](../../t-sql/statements/alter-index-transact-sql.md)를 실행하여 백그라운드에서 병합할 수 있습니다.

### <a name="keep-the-sorted-order-of-a-b-tree-index"></a>B-트리 인덱스의 정렬된 순서 유지
B-트리 인덱스는 정렬된 순서로 행을 저장하므로 행이 columnstore 인덱스로 압축될 때 해당 순서를 유지하면 쿼리 성능을 향상시킬 수 있습니다.

columnstore 인덱스는 데이터를 정렬하지 않지만 메타데이터를 사용하여 각 행 그룹에서 각 열 세그먼트의 최소값과 최대값을 추적합니다.  값 범위를 검색할 때 행 그룹을 건너뛸 시기를 신속하게 계산할 수 있습니다. 데이터가 정렬되면 더 많은 행 그룹을 건너뛸 수 있습니다. 

변환하는 동안 정렬된 순서를 유지하려면
* DROP_EXISTING 절과 함께 [CREATE COLUMNSTORE INDEX](../../t-sql/statements/create-columnstore-index-transact-sql.md)를 사용합니다. 그러면 인덱스의 이름도 유지됩니다. rowstore 인덱스의 이름을 이미 사용하는 스크립트가 있는 경우 해당 스크립트를 업데이트할 필요가 없습니다. 

    다음 예제에서는 `MyFactTable`이라는 테이블의 클러스터형 rowstore 인덱스를 클러스터형 columnstore 인덱스로 변환합니다. 인덱스 이름 `ClusteredIndex_d473567f7ea04d7aafcac5364c241e09`가 동일하게 유지됩니다.

    ```sql
    CREATE CLUSTERED COLUMNSTORE INDEX ClusteredIndex_d473567f7ea04d7aafcac5364c241e09  
    ON MyFactTable  
    WITH (DROP_EXISTING = ON);  
    ```

## <a name="related-tasks"></a>관련 작업  
다음은 columnstore 인덱스를 만들고 유지하기 위한 태스크입니다. 
  
|태스크|참조 항목|참고|  
|----------|----------------------|-----------|  
|테이블을 columnstore로 만듭니다.|[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 테이블을 클러스터형 columnstore 인덱스로 만들 수 있습니다. 먼저 rowstore 테이블을 만든 다음 이를 columnstore로 변환할 필요가 없습니다.|  
|columnstore 인덱스가 포함된 메모리 테이블을 만듭니다.|[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 columnstore 인덱스가 포함된 메모리 최적화 테이블을 만들 수 있습니다. 테이블을 만든 후 ALTER TABLE ADD INDEX 구문을 사용하여 columnstore 인덱스를 추가할 수도 있습니다.|  
|rowstore 테이블을 columnstore로 변환합니다.|[CREATE COLUMNSTORE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|기존 힙 또는 이진 트리를 columnstore로 변환합니다. 예제에서는 이 변환을 수행할 때 기존 인덱스 및 인덱스 이름을 처리하는 방법을 보여 줍니다.|  
|columnstore 테이블을 rowstore로 변환합니다.|[CREATE CLUSTERED INDEX(Transact-SQL) 또는 DROP INDEX](../../t-sql/statements/create-columnstore-index-transact-sql.md)|일반적으로 이 작업은 필요하지 않지만 이 변환을 수행해야 하는 경우가 있을 수 있습니다. 예제에서는 columnstore를 힙 또는 클러스터형 인덱스로 변환하는 방법을 보여 줍니다.|  
|Rowstore 테이블에 columnstore 인덱스를 만듭니다.|[CREATE COLUMNSTORE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|Rowstore 테이블에는 하나의 columnstore 인덱스가 있을 수 있습니다.  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 columnstore 인덱스에 필터링된 조건이 있을 수 있습니다. 예제에서는 기본 구문을 보여 줍니다.|  
|운영 분석에 대한 고성능 인덱스를 만듭니다.|[실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)|OLTP 쿼리에서는 B-트리 인덱스를 사용하고 분석 쿼리에서는 columnstore 인덱스를 사용하도록 상호 보완적인 columnstore 및 B-트리 인덱스를 만드는 방법을 설명합니다.|  
|데이터 웨어하우징용 고성능 columnstore 인덱스를 만듭니다.|[Columnstore 인덱스 - 데이터 웨어하우징](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)|Columnstore 테이블에서 B-트리 인덱스를 사용하여 고성능 데이터 웨어하우징 쿼리를 만드는 방법을 설명합니다.|  
|B-트리 인덱스를 사용하여 columnstore 테이블에서 기본 키 제약 조건을 적용합니다.|[Columnstore 인덱스 - 데이터 웨어하우징](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)|B-트리 및 columnstore 인덱스를 결합하여 columnstore 인덱스에서 기본 키 제약 조건을 적용하는 방법을 보여 줍니다.|  
|Columnstore 인덱스를 삭제합니다.|[DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)|Columnstore 인덱스 삭제에서는 B-트리 인덱스에서 사용하는 표준 DROP INDEX 구문을 사용합니다. 클러스터형 columnstore 인덱스를 삭제하면 columnstore 테이블이 힙으로 변환됩니다.|  
|Columnstore 인덱스에서 행을 삭제합니다.|[DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|행을 삭제하려면 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) 를 사용합니다.<br /><br /> **columnstore** 행: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 행을 논리적으로 삭제된 것으로 표시하지만, 인덱스가 다시 작성될 때까지는 행에 대한 물리적 저장소를 회수하지 않습니다.<br /><br /> **deltastore** 행: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 행을 논리적 및 물리적으로 삭제합니다.|  
|Columnstore 인덱스의 행을 업데이트합니다.|[UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|행을 삭제하려면 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) 를 사용합니다.<br /><br /> **columnstore** 행:  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 행을 논리적으로 삭제됨으로 표시한 다음 업데이트된 행을 deltastore에 삽입합니다.<br /><br /> **deltastore** 행: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 deltastore에 있는 행을 업데이트합니다.|  
|deltastore의 모든 행을 강제로 columnstore로 이동합니다.|[ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) ... REBUILD<br /><br /> [Columnstore 인덱스 - 조각 모음](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)|REBUILD 옵션과 함께 ALTER INDEX를 사용하면 모든 행이 강제로 columnstore로 이동합니다.|  
|Columnstore 인덱스를 조각 모음합니다.|[ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)|ALTER INDEX … REORGANIZE는 columnstore 인덱스를 온라인으로 조각 모음합니다.|  
|테이블을 columnstore 인덱스와 병합합니다.|[MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)|


## <a name="next-steps"></a>다음 단계
빈 columnstore 인덱스를 만들려면

* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 경우 [CREATE TABLE(Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.
* [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]의 경우 [CREATE TABLE(Azure SQL Data Warehouse)](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)을 참조하세요.

기존 rowstore 힙 또는 B-트리 인덱스를 클러스터형 columnstore 인덱스로 변환하는 방법 또는 비클러스터형 columnstore 인덱스를 만드는 방법에 대한 자세한 내용은 [CREATE COLUMNSTORE INDEX(TRANSACT-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)를 참조하세요.

