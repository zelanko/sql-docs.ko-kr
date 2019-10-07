---
title: Columnstore 인덱스 - 쿼리 성능 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 83acbcc4-c51e-439e-ac48-6d4048eba189
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc6409f7a8f5fc15568e583aa50552667f2dd874
ms.sourcegitcommit: ffb87aa292fc9b545c4258749c28df1bd88d7342
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71816712"
---
# <a name="columnstore-indexes---query-performance"></a>Columnstore 인덱스 쿼리 성능

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  디자인된 columnstore 인덱스에서 매우 빠른 쿼리 성능을 제공하기 위한 권장 사항에 대해 설명합니다.    
    
 columnstore 인덱스는 일반적인 행 저장소 인덱스의 경우보다 분석 및 데이터 웨어하우징 작업에서는 최대 100배, 데이터 압축 작업에서는 최대 10배까지 성능을 향상시킬 수 있습니다. 이 권장 사항은 쿼리에서 columnstore 인덱스가 제공하는 매우 빠른 성능을 경험하는 데 도움이 됩니다. 끝에 있는 columnstore 성능에 대한 자세한 설명입니다.    
    
## <a name="recommendations-for-improving-query-performance"></a>쿼리 성능 개선을 위한 권장 사항    
 다음은 columnstore 인덱스에서 제공하는 고성능 달성을 위한 몇 가지 권장 사항입니다.    
    
### <a name="1-organize-data-to-eliminate-more-rowgroups-from-a-full-table-scan"></a>1. 전체 테이블 검색에서 더 많은 행 그룹을 제거할 수 있도록 데이터 구성    
    
-   **삽입 순서 활용** 일반적인 데이터 웨어하우스에서 주로 데이터는 시간 순서에, 분석은 시간 차원에 삽입됩니다. 예를 들어 분기별로 판매를 분석하는 경우 이런 종류의 작업에서는 행 그룹이 자동으로 제거됩니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 쿼리 처리의 일부로 건너뛴 숫자 행 그룹을 찾을 수 있습니다.    
    
-   **클러스터형 rowstore 인덱스 활용** 일반 쿼리 조건자가 행의 삽입 순서와 관련되지 않은 열(예: C1)에 있는 경우 열 C1에서 클러스터형 rowstore 인덱스를 만든 다음 클러스터형 rowstore 인덱스를 삭제하여 클러스터형 columnstore 인덱스를 만듭니다. `MAXDOP = 1`를 사용하여 명시적으로 클러스터형 columnstore 인덱스를 만드는 경우에는 결과 클러스터형 columnstore 인덱스가 열 C1에서 완벽하게 정렬됩니다. `MAXDOP = 8`를 지정하면 8개의 행 그룹 전체에서 값 중복이 표시됩니다. 큰 데이터 집합으로 columnstore 인덱스를 처음 만들 때 이 전략을 주로 사용합니다. NCCI(비클러스터형 columnstore 인덱스)의 경우 기본 rowstore 테이블에 클러스터형 인덱스가 있으면 행은 이미 정렬되어 있습니다. 이 경우 결과 비클러스터형 columnstore 인덱스는 자동으로 정렬됩니다. 한 가지 중요한 점으로 columnstore 인덱스는 기본적으로 행 순서를 유지 관리하지 않음을 참고하세요. 새 행이 삽입되거나 더 오래된 행이 업데이트되면 분석 쿼리 성능이 악화될 수 있으므로 프로세스를 반복해야 할 수 있습니다.    
    
-   **테이블 분할 활용** columnstore 인덱스를 분할한 다음 파티션 제거를 사용하여 검색할 행 그룹의 수를 줄일 수 있습니다. 예를 들어 팩트 테이블에 고객 구매 정보가 저장되어 있고, 일반 쿼리 패턴이 특정 고객의 분기별 구매 정보 찾기일 경우 삽입 순서와 고객 열의 분할을 결합할 수 있습니다. 각 파티션에는 특정 고객에 대한 행이 시간 순서로 포함됩니다.    
    
### <a name="2-plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>2. 병렬로 columnstore 인덱스를 만들기에 충분한 메모리 계획    
 인덱스 만들기는 메모리가 제한되지 않는 한 기본적으로 병렬 작업입니다. 병렬로 인덱스를 만들려면 직렬로 인덱스를 만들 때보다 많은 메모리가 필요합니다. 메모리가 충분하면 동일한 열에 B-트리를 작성할 때보다 1.5배 많은 메모리가 columnstore 인덱스를 만드는 데 사용됩니다.    
    
 columnstore 인덱스를 만드는 데 필요한 메모리는 열 수, 문자열 열 수, DOP(병렬 처리 수준) 및 데이터의 특징에 따라 다릅니다. 예를 들어, 테이블의 행 수가 100만 개 미만일 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 한 스레드만 사용하여 columnstore 인덱스를 만듭니다.    
    
 테이블 행 수가 100만 개 이상이지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 MAXDOP를 사용하여 인덱스를 만들기에 충분한 메모리 부여를 얻을 수 없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 사용 가능한 메모리 부여에 맞게 필요한 만큼 자동으로 `MAXDOP`를 줄입니다.  일부 경우 제한된 메모리로 인덱스를 작성하도록 DOP를 줄여야 합니다.    
    
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 쿼리는 항상 일괄 처리 모드로 작동합니다. 이전 릴리스에서 일괄 처리는 DOP가 1보다 클 경우에만 실행됩니다.    
    
## <a name="columnstore-performance-explained"></a>Columnstore 성능 설명    
 sColumnstore 인덱스에서는 고속 메모리 내 일괄 처리 모드를 I/O 요구 사항을 크게 줄이는 기술과 결합하여 쿼리 성능이 크게 향상되었습니다.  분석 쿼리에서는 많은 행이 검색되므로 일반적으로 IO 바인딩되며, 이로 인해 쿼리 실행 중 I/O를 줄이는 작업은 columnstore 인덱스 디자인에 매우 중요합니다.  데이터를 메모리로 읽어온 후에는 메모리 내 작업 수를 줄이는 것이 중요합니다.    
    
 Columnstore 인덱스는 I/O는 줄이고, 높은 데이터 압축, columnstore 제거, 행 그룹 제거 및 일괄 처리를 통해 메모리 내 작업을 최적화합니다.    
    
### <a name="data-compression"></a>데이터 압축    
 Columnstore 인덱스는 rowstore 인덱스보다 최고 10배 높은 데이터 압축률을 보여 줍니다. 이를 통해 분석 쿼리를 실행하는 데 필요한 I/O는 크게 줄이고 그에 따라 쿼리 성능이 향상됩니다.    
    
-   Columnstore 인덱스는 디스크에서 압축된 데이터를 읽습니다. 즉, 메모리로 읽어야 하는 데이터 바이트가 적어집니다.    
    
-   Columnstore 인덱스는 데이터를 압축된 형태로 메모리에 저장합니다. 이렇게 하면 동일한 데이터를 메모리로 읽는 횟수가 줄어 I/O도 줄어듭니다. 예를 들어 압축률이 10배인 columnstore 인덱스에서는 데이터를 압축되지 않은 형태로 저장하는 작업과 비교해 볼 때 메모리에 10배 이상의 데이터를 보관할 수 있습니다. 메모리에서 더 많은 데이터를 사용하면 columnstore 인덱스에서는 디스크에서 추가 읽기를 하지 않고도 메모리에 필요한 데이터를 찾을 가능성이 높아집니다.    
    
-   Columnstore 인덱스 높은 압축률을 보여 주는 데이터를 행 대신 열을 기준으로 압축하여 디스크에 저장되는 데이터 크기를 줄입니다. 각 열은 개별적으로 압축되어 저장됩니다.  한 열에 있는 데이터는 항상 형식이 동일하며, 유사한 값을 포함하려는 경향이 있습니다. 데이터 압축 기술은 값이 비슷할 경우 더 높은 압축률을 달성할 수 있습니다.    
    
-   예를 들어 팩트 테이블에 고객 주소가 저장되어 있고 국가에 대한 열이 하나 있는 경우 가능한 총 값 수는 200개 미만입니다. 이러한 값 중 일부는 여러 번 반복됩니다. 팩트 테이블에 1억 개의 행이 있는 경우에는 국가 열이 쉽게 압축되므로 요구되는 스토리지 크기는 매우 작습니다. 행 단위 압축은 이 방식으로 열 값의 유사성을 활용할 수 없어 국가 열의 값을 압축하는 데 더 많은 바이트를 사용합니다.    
    
### <a name="column-elimination"></a>열 제거    
 Columnstore 인덱스는 쿼리 결과에 필요 없는 열은 읽기를 건너뜁니다. 열 제거라고 하는 이 기능은 또한 쿼리 실행에 필요한 I/O를 줄이므로 쿼리 성능이 향상됩니다.    
    
-   열 제거는 데이터가 열 단위로 구성되고 압축되기 때문에 가능합니다. 반면, 데이터가 행별로 저장된 경우 각 행의 열 값은 물리적으로 함께 저장되어 쉽게 구분할 수 없습니다. 쿼리 프로세서에서 특정 열 값을 검색하려면 전체 행에서 읽어야 합니다. 이럴 경우 추가 데이터를 불필요하게 메모리로 읽어오게 되어 I/O가 늘어납니다.    
    
-   예를 들어 테이블에 열이 50개 있고, 쿼리에서 그중 5개만 사용할 경우 columnstore 인덱스는 디스크에서 해당 5개 열만 가져옵니다. 나머지 45개 열은 읽기를 건너뜁니다. 이렇게 하면 열 크기가 모두 비슷하다고 가정할 때 90%까지 I/O가 줄어듭니다. 동일한 데이터가 rowstore에 저장되면 쿼리 프로세서는 추가로 45개 열을 모두 읽어야 합니다.    
    
### <a name="rowgroup-elimination"></a>행 그룹 제거    
 전체 테이블 검색의 경우 대부분의 데이터가 쿼리 조건자의 조건에 맞지 않습니다. 메타데이터를 사용하면 columnstore 인덱스는 쿼리 결과에 필요한 데이터가 없는 rowgroup의 읽기를 실제 I/O없이 모두 건너뛸 수 있습니다. 행 그룹 제거라고 하는 이 기능은 전체 테이블 검색에 필요한 I/O를 줄이므로 쿼리 성능이 향상됩니다.    
    
 **columnstore 인덱스는 전체 테이블 검색을 언제 수행해야 하나요?**    
    
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 rowstore 힙에서와 같이 클러스터형 columnstore 인덱스에서 하나 이상의 일반 비클러스터형 B-트리 인덱스를 만들 수 있습니다. 비클러스터형 B-트리 인덱스는 같음 조건자 또는 작은 값 범위를 가진 조건자가 있는 쿼리의 속도를 높일 수 있습니다.  더 복잡한 조건자의 경우 쿼리 최적화 프로그램에서 전체 테이블 검색을 선택할 수도 있습니다. 행 그룹을 건너뛸 수 없다면 전체 테이블 검색은 특히 큰 테이블의 경우 시간이 많이 소요됩니다.    
    
 **분석 쿼리에서 전체 테이블 검색 시 행 그룹 제거를 언제 활용하나요?**    
    
 예를 들어 소매점에서 클러스터형 columnstore 인덱스가 포함된 팩트 테이블을 사용하여 판매 데이터를 모델링했을 경우 새로운 상점은 제품이 판매된 날짜를 비롯하여 거래에 대한 다양한 특성을 저장합니다. 흥미롭게도 columnstore 인덱스는 정렬된 순서를 보장하지 않지만 이 테이블의 행은 날짜로 정렬된 순서대로 로드됩니다. 시간이 지남에 따라 이 테이블은 증가합니다. 소매업은 지난 10년에 대한 판매 데이터를 보관할 수는 있지만 분석 쿼리에서는 마지막 분기에 대한 집계를 컴퓨팅하기만 하면 됩니다. Columnstore 인덱스는 날짜 열에 대한 메타데이터만 살펴보고 이전 39개 분기에 대한 데이터에 대한 액세스를 제거할 수 있습니다. 이 작업은 메모리로 읽어와 처리되는 데이터의 양을 추가로 97% 절감하였습니다.    
    
 **전체 테이블 검색에서는 어떤 행 그룹을 건너뛰나요?**    
    
 제거할 행 그룹을 결정하려면 columnstore 인덱스는 메타데이터를 사용하여 각 행 그룹에 대한 각 열 세그먼트의 최소값 및 최대값을 저장합니다. 열 세그먼트 범위 중 어떤 것도 쿼리 조건자의 조건에 맞지 않을 경우 실제 IO를 수행하지 않고 행 그룹 전체를 건너뜁니다. 데이터가 주로 정렬된 순서대로 로드되고, 행 정렬이 보장되지 않더라도 유사한 데이터 값이 보통 동일한 행 그룹 또는 인접한 행 그룹에 위치하므로 이 작업이 가능합니다.    
    
 행 그룹에 대한 자세한 내용은 Columnstore 인덱스 가이드를 참조하세요.    
    
### <a name="batch-mode-execution"></a>일괄 처리 모드 실행    
 일괄 처리 모드 실행이란 실행 효율성을 위해 일반적으로 최대 900개의 행을 함께 행 집합으로 처리하는 것을 말합니다. 예를 들어 `SELECT SUM (Sales) FROM SalesData` 쿼리는 SalesData 테이블에서의 총 판매액을 집계합니다. 일괄 처리 모드 실행에서 쿼리 실행 엔진은 집계를 900개 값으로 이루어진 그룹으로 계산합니다. 이렇게 하면 각 행에 대한 비용을 부담하지 않고 모든 행에서 메타데이터 액세스 비용과 기타 오버헤드 유형을 일괄 처리로 분산하여 코드 경로가 상당히 줄어듭니다. 일괄 처리 모드는 가능한 경우 압축된 데이터에서 작동하고 행 모드 처리에서 사용하는 교환 연산자 중 일부를 제거합니다. 이렇게 하면 크기 순서대로 정렬되어 분석 쿼리 실행 속도가 향상됩니다.    
    
 일부 쿼리 실행 연산자는 일괄 처리 모드에서 실행할 수 없습니다. 예를 들어 Insert, Delete 또는 Update와 같은 DML 작업은 한 번에 행에서 실행됩니다. 일괄 처리 모드 연산자는 쿼리 성능 속도 향상을 위해 Scan, Join, Aggregate, Sort 등과 같은 연산자를 대상으로 합니다. Columnstore 인덱스는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 처음으로 사용되었으므로 일괄 처리 모드로 실행할 수 있는 연산자를 지속적으로 확장하려고 노력합니다. 다음 표에서 제품 버전에 따라 일괄 처리 모드로 실행되는 연산자를 보여 줍니다.    
    
|일괄 처리 모드 연산자|언제 사용하나요?|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]<sup>1</sup>|주석|    
|---------------------------|------------------------|---------------------|---------------------|---------------------------------------|--------------|    
|DML 작업(insert, delete, update, merge)||아니요|아니요|아니요|DML 병렬이 아니므로 일괄 처리 모드 작업이 아닙니다. 직렬 모드 일괄 처리를 사용하도록 설정하더라도 DML을 일괄 처리 모드로 처리함으로써 크게 향상되는 것은 없습니다.|    
|Columnstore 인덱스 검색|SCAN|NA|예|예|Columnstore 인덱스에서 조건자를 SCAN 노드로 푸시할 수 있습니다.|    
|columnstore 인덱스 Scan(비클러스터형)|SCAN|예|예|예|예|    
|index seek||NA|NA|아니요|rowmode에서 비클러스터형 B-트리 인덱스를 통해 seek 작업을 수행합니다.|    
|compute scalar|스칼라 값으로 평가되는 식입니다.|예|예|예|데이터 형식에 몇 가지 제한 사항이 있습니다. 모든 일괄 처리 모드 연산자에 적용됩니다.|    
|연결(concatenation)|UNION 및 UNION ALL|아니요|예|예||    
|filter|조건자 적용|예|예|예||    
|hash match|해시 기반 집계 함수, 외부 해시 조인, 오른쪽 해시 조인, 왼쪽 해시 조인, 오른쪽 내부 조인, 왼쪽 내부 조인|예|예|예|집계에 대한 제한 사항: 문자열에 min/max가 없습니다. 사용할 수 있는 집계 함수는 sum/count/avg/min/max입니다.<br />조인에 대한 제한 사항: 일치하지 않는 형식은 정수가 아닌 형식에 조인되지 않습니다.|    
|merge join||아니요|아니요|아니요||    
|다중 스레드 쿼리||예|예|예||    
|중첩 루프||아니요|아니요|아니요||    
|MAXDOP 1에서 실행되는 단일 스레드 쿼리||아니요|아니요|예||    
|직렬 쿼리 계획을 사용하는 단일 스레드 쿼리||아니요|아니요|예||    
|sort|columnstore 인덱스를 사용하여 SCAN 시 절을 기준으로 정렬합니다.|아니요|아니요|예||    
|위쪽 정렬||아니요|아니요|예||    
|창 집계||NA|NA|예|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 새 연산자.|    
    
<sup>1</sup> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 프리미엄 계층, 표준 계층 - S3 이상 및 모든 vCore 계층 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 적용    
    
### <a name="aggregate-pushdown"></a>집계 푸시 다운    
 SCAN 노드에서 조건에 맞는 행을 가져와 일괄 처리 모드에서 값을 집계하는 집계 계산을 위한 일반 실행 경로입니다. 이러한 실행으로 좋은 성능이 제공되긴 하지만 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 집계 작업은 SCAN 노드로 푸시되어 다음 조건이 충족되면 일괄 처리 모드 실행 시 크기 순서대로 정렬되므로 집계 계산 성능을 향상시킬 수 있습니다. 
 
-    집계는 `MIN`, `MAX`, `SUM`, `COUNT` 및 `COUNT(*)`입니다. 
-  집계 연산자는 `GROUP BY`를 사용하여 SCAN 노드 또는 SCAN 노드 맨 위에 있어야 합니다.
-  이 집계는 고유한 집계가 아닙니다.
-  집계 열은 문자열 열이 아닙니다.
-  집계 열은 가상의 열이 아닙니다. 
-  입력 및 출력 데이터 형식은 다음 중 하나여야 하며 64비트 이내여야 합니다.
    -  `tinyint`, `int`, `bigint`, `smallint`, `bit`
    -  전체 자릿수가 18 이하인 `smallmoney`, `money`, `decimal` 및 `numeric`
    -  `smalldate`, `date`, `datetime`, `datetime2`, `time`
    
 집계 푸시다운은 캐시에서 사용하는 실행에서 압축되거나 인코딩된 데이터를 효율적으로 집계하고 SIMD를 활용하여 좀 더 가속화됩니다.    
    
 ![aggregate pushdown](../../relational-databases/indexes/media/aggregate-pushdown.jpg "aggregate pushdown")    
    
예를 들어 집계 푸시다운은 아래 쿼리 모두에서 수행됩니다.    
    
```sql     
SELECT  productkey, SUM(TotalProductCost)    
FROM FactResellerSalesXL_CCI    
GROUP BY productkey    
    
SELECT  SUM(TotalProductCost)    
FROM FactResellerSalesXL_CCI    
```    
    
### <a name="string-predicate-pushdown"></a>문자열 조건자 푸시다운    
데이터 웨어하우스 스키마를 디자인할 때 하나 이상의 팩트 테이블과 많은 차원 테이블로 구성된 별 모양 스키마 또는 눈송이 스키마를 스키마 모델링으로 사용하는 것이 권장됩니다. [팩트 테이블](https://wikipedia.org/wiki/Fact_table) 에는 비즈니스 측정값 또는 트랜잭션을 저장하고, [차원 테이블](https://wikipedia.org/wiki/Dimension_table) 에는 분석해야 하는 팩트 전체에 대한 차원을 저장합니다.    
    
예를 들어 팩트는 특정 지역에서 특정 제품의 판매를 나타내는 레코드일 수 있으며, 차원은 지역, 제품 등의 집합을 나타냅니다. 팩트 테이블과 차원 테이블은 기본/외래 키 관계를 통해 연결됩니다. 가장 일반적으로 사용되는 분석 쿼리는 하나 이상의 차원 테이블을 팩트 테이블에 조인하는 것입니다.    
    
`Products` 차원 테이블이 있다고 가정해 봅시다. 일반적인 기본 키는 주로 string 데이터 형식으로 표현되는 `ProductCode`가 됩니다. 쿼리 성능을 위해 일반적으로 정수 열인 대리 키를 만들어 팩트 테이블에서 차원 테이블의 행을 참조하는 것이 가장 좋습니다. 
    
columnstore 인덱스는 숫자 또는 정수를 기반으로 하는 키가 포함된 조인/조건자를 사용하여 분석 쿼리를 매우 효율적으로 실행합니다. 그러나 많은 고객 작업에서 팩트/차원 테이블을 연결하는 문자열 기반 열이 사용되고 있고 그 결과 columnstore 인덱스를 사용하는 쿼리 성능은 직접 수행할 때와는 다릅니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]는 문자열 열이 있는 조건자를 SCAN 노드로 푸시다운하여 문자열 기반의 열을 사용하는 분석 쿼리의 성능을 크게 향상시켰습니다.    
    
문자열 조건자 푸시다운을 통해 열에서 만든 주/보조 사전을 활용하여 쿼리 성능을 개선합니다. 예를 들어 100개의 개별 문자열 값으로 구성된 행 그룹에서 문자열 열 세그먼트가 있다고 간주해 보겠습니다. 즉, 1백만 개의 행이라고 가정하면 각 개별 문자열 값은 평균 10,000번 참조됩니다.    
    
문자열 조건자 푸시다운을 사용하면 쿼리 실행 시 사전에 있는 값으로 조건자를 계산하고 조건을 충족할 경우 사전 값을 참조하는 모든 행이 자동으로 조건이 충족됩니다. 이렇게 하면 두 가지 방법으로 성능이 향상됩니다.
1.  정규화된 행만 반환되어 SCAN 노드에서 받아야 하는 행 수를 줄입니다. 
2.  문자열 비교 수가 상당히 줄어듭니다. 이 예제에서는 1백만 개의 비교에 대해 100개의 문자열 비교만 필요합니다. 아래 설명된 대로 몇 가지 제한 사항이 있습니다.    

    -   델타 행 그룹에 대한 문자열 조건자 푸시다운이 없습니다. 델타 행 그룹의 열에 대한 사전이 없습니다.    
    -   사전 항목이 64KB 항목을 초과하면 문자열 조건자 푸시다운이 없습니다.    
    -   Null을 평가하는 식이 지원되지 않습니다.    
    
## <a name="see-also"></a>참고 항목    
 [Columnstore 인덱스 디자인 지침](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)   
 [Columnstore 인덱스 데이터 로드 지침](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [실시간 운영 분석을 위한 Columnstore 시작](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)     
 [데이터 웨어하우스용 Columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)    
 [Columnstore 인덱스 아키텍처](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)    
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)     
  
