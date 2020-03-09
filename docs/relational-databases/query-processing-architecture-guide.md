---
title: 쿼리 처리 아키텍처 가이드 | Microsoft 문서
ms.custom: ''
ms.date: 02/14/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- guide, query processing architecture
- query processing architecture guide
- row mode execution
- batch mode execution
ms.assetid: 44fadbee-b5fe-40c0-af8a-11a1eecf6cb5
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d6f17b46cb396ee34133e67a528e22cab571cceb
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338556"
---
# <a name="query-processing-architecture-guide"></a>쿼리 처리 아키텍처 가이드
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 로컬 테이블, 분할된 테이블 및 여러 서버에 분산된 테이블과 같은 다양한 데이터 스토리지 아키텍처의 쿼리를 처리합니다. 다음 항목에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 실행 계획 캐싱을 통해 쿼리를 처리하고 쿼리 재사용을 최적화하는 방법에 대해 설명합니다.

## <a name="execution-modes"></a>실행 모드
[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]는 두 가지 고유한 처리 모드를 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 처리할 수 있습니다.
- 행 모드 실행
- 일괄 처리 모드 실행

### <a name="row-mode-execution"></a>행 모드 실행
*행 모드 실행*은 데이터가 행 형식으로 저장되어 있는 경우 기존 RDMBS 테이블에서 사용된 쿼리 처리 메서드입니다. 쿼리가 실행되고 행 저장 테이블의 데이터에 액세스하는 경우 실행 트리 연산자 및 자식 연산자는 테이블 스키마에서 지정된 모든 열에 걸쳐 필요한 각 행을 읽습니다. 읽은 각 행에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 SELECT 문, 조인 조건자 또는 필터 조건자에 의해 참조된 것처럼 결과 집합에 필요한 열을 검색합니다.

> [!NOTE]
> 행 모드 실행은 OLTP 시나리오에 매우 효율적이지만 많은 양의 데이터(예를 들어 데이터 웨어하우징 시나리오에서)를 검사할 때는 효율성이 떨어질 수 있습니다.

### <a name="batch-mode-execution"></a>일괄 처리 모드 실행  
*일괄 처리 모드 실행*은 여러 행을 함께 처리하는 쿼리 처리 방법입니다(따라서 용어 일괄처리). 일괄 처리 내에서 각 열은 메모리의 별도 영역에 벡터로 저장되므로 일괄 처리 모드는 벡터 기반 처리입니다. 또한 일괄 처리 모드 처리는 다중 코어 CPU에 최적화된 알고리즘 및 최신 하드웨어에 있는 증가된 메모리 처리량을 사용합니다.      

배치 모드 실행은 columnstore 스토리지 형식과 긴밀히 통합되고 그에 맞게 최적화되어 있습니다. 일괄 처리 모드는 가능한 경우 압축된 데이터에서 작동하고 행 모드 실행에서 사용하는 [교환 연산자](../relational-databases/showplan-logical-and-physical-operators-reference.md#exchange)를 제거합니다. 그 결과로 병렬 처리가 더 나아졌고 성능이 더 빨라졌습니다.    

쿼리가 일괄 처리 모드에서 실행되고 columnstore 인덱스의 데이터에 액세스할 경우 실행 트리 연산자 및 자식 연산자는 열 세그먼트에서 함께 여러 행을 읽습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 SELECT 문, 조인 조건자 또는 필터 조건자에 의해 참조된 것처럼 결과에 필요한 열만 읽습니다.    
columnstore 인덱스에 대한 자세한 내용은 [Columnstore 인덱스 아키텍처](../relational-databases/sql-server-index-design-guide.md#columnstore_index)를 참조하세요.  

> [!NOTE]
> 일괄 처리 모드 실행은 많은 양의 데이터를 읽고 집계할 경우 매우 효율적인 데이터 웨어하우징 시나리오입니다.

## <a name="sql-statement-processing"></a>SQL 문 처리
단일 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 처리는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행하는 가장 기본적인 방법입니다. 이러한 기본 프로세스의 예로 뷰 또는 원격 테이블이 없는 로컬 기본 테이블만 참조하는 단일 `SELECT` 문을 처리하는 경우를 들 수 있습니다.

### <a name="logical-operator-precedence"></a>논리 연산자 선행 규칙
문에 논리 연산자가 두 개 이상 사용되면 `NOT`이 가장 먼저 평가되고 다음으로 `AND`, `OR`의 순서로 평가됩니다. 산술 및 비트 연산자는 논리 연산자보다 먼저 처리됩니다. 자세한 내용은 [연산자 우선 순위](../t-sql/language-elements/operator-precedence-transact-sql.md)를 참조하세요.

다음 예제에서 `AND`가 `OR`보다 우선하므로 제품 모델 21에는 색상 조건이 적용되지만 제품 모델 20에는 적용되지 않습니다.

```sql
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR ProductModelID = 21
  AND Color = 'Red';
GO
```

`OR`를 먼저 평가하도록 괄호를 추가하면 쿼리의 의미를 변경할 수 있습니다. 다음 쿼리에서는 제품 모델 20 및 21에서 색상이 빨강인 제품만 찾습니다.

```sql
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE (ProductModelID = 20 OR ProductModelID = 21)
  AND Color = 'Red';
GO
```

꼭 필요한 경우가 아니라도 괄호를 사용하면 쿼리의 가독성을 높이고 연산자 우선 순위로 인한 사소한 실수를 줄일 수 있습니다. 괄호를 사용하더라도 성능에는 거의 영향을 미치지 않습니다. 다음 예제는 첫 번째 예제와 구문적으로는 동일하지만 파악하기가 더 쉽습니다.

```sql
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR (ProductModelID = 21
  AND Color = 'Red');
GO
```

### <a name="optimizing-select-statements"></a>SELECT 문 최적화
`SELECT` 문은 프로시저를 통하지 않습니다. 즉, 데이터베이스 서버가 요청한 데이터를 검색하는 데 사용해야 하는 정확한 단계를 지정하고 있지 않습니다. 이는 데이터베이스 서버가 문을 분석하여 요청한 데이터를 추출하는 가장 효율적인 방법을 판단해야 함을 의미합니다. 이것을 `SELECT` 문 최적화라고 하며 이를 위한 구성 요소를 쿼리 최적화 프로그램이라고 합니다. 최적화 프로그램에 대한 입력은 쿼리, 데이터베이스 스키마(테이블 및 인덱스 정의) 및 데이터베이스 통계로 이루어집니다. 쿼리 최적화 프로그램의 출력은 쿼리 실행 계획이며 경우에 따라 쿼리 계획이나 실행 계획이라고 합니다. 실행 계획의 내용은 이 항목의 뒷부분에서 보다 자세히 설명됩니다.

다음 도표는 단일 `SELECT` 문을 최적화하는 동안 쿼리 최적화 프로그램에 입력되는 내용과 출력 내용을 보여 줍니다.

![query_processor_io](../relational-databases/media/query-processor-io.gif)

`SELECT` 문은 다음 사항만 정의합니다.  
* 결과 집합의 서식. 대부분 SELECT 목록에 지정됩니다. 하지만 `ORDER BY` 및 `GROUP BY` 와 같은 다른 절도 결과 집합의 최종 서식에 영향을 줍니다.
* 원본 데이터를 포함하는 테이블. 테이블은 `FROM` 절에서 지정됩니다.
* 테이블이 `SELECT` 문의 목적과 논리적으로 관련되는 방식. 조인 사양에 정의되며 `WHERE` 뒤에 따라오는 `ON` 절이나 `FROM`절에 포함될 수 있습니다.
* 원본 테이블의 행이 `SELECT` 문의 결과에 포함되기 위해 만족시켜야 할 조건. 조건은 `WHERE` 및 `HAVING` 절에 지정됩니다.

쿼리 실행 계획은 다음 사항을 정의합니다. 

- **원본 테이블이 액세스되는 순서** 일반적으로 데이터베이스 서버는 다양한 방법으로 기본 테이블에 액세스하여 결과 집합을 작성할 수 있습니다. 예를 들어 `SELECT` 문이 세 개의 테이블을 참조하는 경우 데이터베이스 서버는 먼저 `TableA`에 액세스하고, `TableA` 의 데이터를 사용하여 `TableB`에서 일치하는 행을 추출한 후 `TableB` 의 데이터를 사용하여 `TableC`에서 데이터를 추출합니다. 다음은 데이터베이스 서버가 테이블에 액세스할 수 있는 여러 순서입니다.  
  `TableC`, `TableB`, `TableA`또는  
  `TableB`, `TableA`, `TableC`또는  
  `TableB`, `TableC`, `TableA`또는  
  `TableC`, `TableA`, `TableB`  

- **각 테이블에서 데이터를 추출하는 데 사용하는 방법**  
  일반적으로 각 테이블의 데이터에 액세스하는 방법에는 여러 가지가 있습니다. 특정 키 값을 가진 몇몇 행만 필요한 경우 데이터베이스 서버는 인덱스를 사용할 수 있습니다. 테이블의 모든 행이 필요한 경우 데이터베이스 서버는 인덱스를 무시하고 테이블을 검색할 수 있습니다. 테이블의 모든 행이 필요하지만 키 열이 `ORDER BY`에 있는 인덱스가 있으면 테이블 검색 대신 인덱스 검색을 수행하여 다른 종류의 결과 집합을 저장할 수 있습니다. 테이블이 매우 작은 경우 테이블 검색은 거의 모든 테이블 액세스를 위한 가장 효율적인 방법일 수 있습니다.
  
- **계산 컴퓨팅에 사용되는 방법과 각 테이블의 데이터를 필터링, 집계, 정렬하는 방법**  
  데이터가 테이블에서 액세스되므로, 컴퓨팅 스칼라 값과 같은 데이터에 대한 계산 수행 방법과 쿼리 텍스트(예: `GROUP BY` 또는 `ORDER BY` 절을 사용하는 경우)와 데이터 필터링 방법(예: `WHERE` 또는 `HAVING` 절을 사용하는 경우)에 정의된 대로 데이터를 집계하고 정렬하는 방법에는 여러 가지가 있습니다.

여러 가능한 실행 계획 중에서 하나의 실행 계획을 선택하는 프로세스를 최적화라고 합니다. 쿼리 최적화 프로그램은 [!INCLUDE[ssde_md](../includes/ssde_md.md)]의 가장 중요한 구성 요소 중 하나입니다. 쿼리 최적화 프로그램에서 쿼리를 분석하고 계획을 선택할 때 오버헤드가 발생하지만 효율적인 실행 계획을 선택하면 오버헤드가 상당히 절감됩니다. 예를 들어 두 개의 건설 회사에 하나의 집에 대한 동일한 청사진이 제공될 수 있습니다. 한 회사에서는 며칠 동안 그 집을 어떻게 지을지 계획을 하는 동안 다른 회사는 계획 없이 집을 짓기 시작할 경우 프로젝트를 계획하는 데 시간을 소요한 회사가 먼저 작업을 끝내는 것과 같습니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 비용을 기반으로 하는 최적화 프로그램입니다. 가능한 각 실행 계획은 사용되는 컴퓨팅 리소스의 양과 관련하여 비용을 추산합니다. 쿼리 최적화 프로그램은 가능한 실행 계획을 분석하고 예상 비용이 가장 낮은 계획을 선택해야 합니다. 일부 복잡한 `SELECT` 문은 가능한 수많은 실행 계획을 포함합니다. 이 경우에 쿼리 최적화 프로그램은 가능한 모든 조합을 분석하지는 않습니다. 대신 복잡한 알고리즘을 사용하여 가장 최소 비용에 근접하는 실행 계획을 찾습니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램이 리소스 비용이 가장 낮은 실행 계획만 선택하는 것은 아닙니다. 쿼리 최적화 프로그램은 타당한 리소스 비용을 사용하여 사용자에게 결과를 반환하고 가장 빠른 결과를 반환하는 계획을 선택합니다. 예를 들어 병렬로 쿼리를 처리하는 것은 대개 직렬로 처리하는 것보다 많은 리소스를 사용하지만 쿼리를 좀 더 빠르게 끝냅니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 서버 로드에 나쁜 영향을 미치지 않는 경우 병렬 실행 계획을 사용하여 결과를 반환합니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 테이블 또는 인덱스에서 정보를 추출하는 다른 방법의 리소스 비용을 예상할 때 배포 통계를 이용합니다. 배포 통계는 열과 인덱스에 대해 유지되며, 기본 데이터의 밀도<sup>1</sup>에 대한 정보를 보유합니다. 이는 특정 인덱스 또는 열에서 값의 선택도를 표시하는 데 사용됩니다. 예를 들어 자동차를 나타내는 테이블에서 많은 차가 동일한 제조업체의 것이지만 각 차는 고유의 차량 등록 번호(VIN)를 갖습니다. VIN의 밀도가 제조업체보다 낮으므로 VIN의 인덱스가 제조업체의 인덱스보다 더 선택적입니다. 인덱스 통계가 현재의 데이터가 아니면 쿼리 최적화 프로그램은 테이블의 현재 상태에 대해 최상의 선택을 하지 못할 수 있습니다. 밀도에 대한 자세한 내용은 [통계](../relational-databases/statistics/statistics.md#density)를 참조하세요. 

<sup>1</sup> 밀도는 데이터에 존재하는 고유 값의 분포 또는 지정된 열에 대한 중복 값의 평균 개수를 정의합니다. 밀도가 감소하면 값의 선택도가 증가합니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 프로그래머나 데이터베이스 관리자의 입력을 요청하지 않고 데이터베이스 서버가 데이터베이스의 조건 변화에 맞춰 동적으로 조정될 수 있게 하므로 중요합니다. 이를 통해 프로그래머는 쿼리의 최종 결과를 설명하는 데 주안점을 둘 수 있습니다. 프로그래머는 문이 실행될 때마다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램이 데이터베이스의 상태에 맞게 효율적인 실행 계획을 세운다는 것을 신뢰할 수 있습니다.

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에는 실행 계획을 표시하는 세 가지 옵션이 있습니다.        
> -  쿼리 최적화 프로그램에서 생성한 컴파일된 계획인 ***[예상 실행 계획](../relational-databases/performance/display-the-estimated-execution-plan.md)***.        
> -  컴파일된 계획 및 관련 실행 컨텍스트와 동일한 ***[실제 실행 계획](../relational-databases/performance/display-an-actual-execution-plan.md)***. 여기에는 실행 경고와 같이 실행이 완료된 후에 사용할 수 있는 런타임 정보가 포함되거나 최신 버전의 [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서는 실행 중에 사용되는 경과 및 CPU 시간이 포함됩니다.        
> -  컴파일된 계획 및 관련 실행 컨텍스트와 동일한 ***[활성 쿼리 통계](../relational-databases/performance/live-query-statistics.md)***. 여기에는 실행되는 동안 제공되는 런타임 정보가 포함되며 1초마다 업데이트됩니다. 예를 들어 런타임 정보에는 연산자를 통해 흐르는 실제 행 수가 포함됩니다.       

### <a name="processing-a-select-statement"></a>SELECT 문 처리
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 단일 SELECT 문을 처리하는 데 사용하는 기본 단계는 다음과 같습니다. 

1. 파서는 `SELECT` 문을 검색하고 그 결과를 키워드, 식, 연산자 및 식별자와 같은 논리 단위로 분류합니다.
2. 시퀀스 트리라고도 하는 쿼리 트리가 작성되어 결과 집합에서 필요로 하는 서식으로 원본 데이터를 변환하는 데 필요한 논리 단계를 정의합니다.
3. 쿼리 최적화 프로그램은 원본 테이블에 액세스할 수 있는 여러 다른 방법을 분석합니다. 그런 후 리소스 사용을 줄이는 동시에 결과를 가장 빨리 반환하는 일련의 단계를 선택합니다. 쿼리 트리는 이러한 일련의 단계가 기록되도록 업데이트됩니다. 최적화된 최종 쿼리 트리 버전은 실행 계획이라고 합니다.
4. 관계형 엔진이 실행 계획을 실행하기 시작합니다. 기본 테이블의 데이터를 필요로 하는 단계가 처리될 때 관계형 엔진은 스토리지 엔진이 관계형 엔진에서 요청된 행 집합의 데이터를 무시하도록 요청합니다.
5. 관계형 엔진은 스토리지 엔진에서 반환된 데이터를 결과 집합에 대해 정의된 서식으로 처리하고 클라이언트에 결과 집합을 반환합니다.

### <a name="ConstantFolding"></a> 상수 폴딩 및 식 평가 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 일부 상수 식을 초기에 평가하여 쿼리 성능을 향상시킵니다. 이를 상수 폴딩이라고 합니다. 상수는 `3`, `'ABC'`, `'2005-12-31'`, `1.0e3` 또는 `0x12345678` 같은 [!INCLUDE[tsql](../includes/tsql-md.md)] 리터럴입니다.

#### <a name="foldable-expressions"></a>폴딩 가능 식
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 다음 유형의 식에 상수 폴딩을 사용합니다.
- 상수만 포함된 산술 식(예: 1+1, 5/3*2)
- 상수만 포함된 논리 식(1=1 and 1>2 AND 3>4)
- `CAST` 및 `CONVERT`를 비롯하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 폴딩 가능한 것으로 간주하는 기본 제공 함수. 일반적으로 입력으로만 사용되고, SET 옵션, 언어 설정, 데이터베이스 옵션 및 암호화 키와 같은 다른 컨텍스트 정보를 제공하지 않는 내장 함수가 폴딩 가능한 함수입니다. 비결정적 함수는 폴딩 가능하지 않습니다. 몇 가지 예외를 제외하고 결정적 기본 제공 함수는 폴딩 가능 함수입니다.
- CLR 사용자 정의 형식의 결정적 메서드 및 결정적 스칼라 반환 CLR 사용자 정의 함수([!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터). 자세한 내용은 [CLR 사용자 정의 함수 및 메서드를 위한 상수 폴딩](https://docs.microsoft.com/sql/database-engine/behavior-changes-to-database-engine-features-in-sql-server-2014#constant-folding-for-clr-user-defined-functions-and-methods)을 참조하세요.

> [!NOTE] 
> 큰 개체 유형의 경우에는 예외입니다. 폴딩 프로세스의 출력 유형이 큰 개체 유형(text, ntext, image, nvarchar(max), varchar(max), varbinary(max) 또는 XML)이면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 식을 폴딩하지 않습니다.

#### <a name="nonfoldable-expressions"></a>폴딩 가능하지 않은 식
다른 모든 식 유형은 폴딩할 수 없습니다. 특히 다음 식 유형은 폴딩할 수 없습니다.
- 비상수 식(예: 열 값에 따라 결과가 달라지는 식)
- 지역 변수 또는 매개 변수에 따라 결과가 달라지는 식(예: @x)
- 비결정적 함수
- 사용자 정의 [!INCLUDE[tsql](../includes/tsql-md.md)] 함수<sup>1</sup>.
- 언어 설정에 따라 결과가 달라지는 식
- SET 옵션에 따라 결과가 달라지는 식
- 서버 구성 옵션에 따라 결과가 달라지는 식

<sup>1</sup> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 이전에는 결정적 스칼라 반환 CLR 사용자 정의 함수와 CLR 사용자 정의 형식의 메서드를 폴딩할 수 없었습니다. 

#### <a name="examples-of-foldable-and-nonfoldable-constant-expressions"></a>폴딩 가능 식 및 폴딩 가능하지 않은 식의 예
다음과 같은 쿼리를 고려해 보세요.

```sql
SELECT *
FROM Sales.SalesOrderHeader AS s 
INNER JOIN Sales.SalesOrderDetail AS d 
ON s.SalesOrderID = d.SalesOrderID
WHERE TotalDue > 117.00 + 1000.00;
```

이 쿼리에 대해 `PARAMETERIZATION` 데이터베이스 옵션이 `FORCED`로 설정되어 있지 않으면 `117.00 + 1000.00` 식이 평가된 다음, 쿼리를 컴파일하기 전에 평가 결과인 `1117.00`으로 바뀝니다. 이러한 상수 폴딩의 이점은 다음과 같습니다.
- 런타임에 식을 반복해서 평가할 필요가 없습니다.
- 식 평가 후 쿼리 최적화 프로그램에서 식 값을 사용하여 쿼리의 `TotalDue > 117.00 + 1000.00` 부분에 대한 결과 집합의 크기를 추정합니다.

반면 `dbo.f`가 스칼라 사용자 정의 함수인 경우에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용자 정의 함수가 포함된 식을 계산하지 않으므로 `dbo.f(100)` 식이 폴딩되지 않습니다. 사용자 정의 함수가 결정적 함수인 경우에도 마찬가지입니다. 매개 변수화에 대한 자세한 내용은 이 문서의 뒷부분에서 [강제 매개 변수화](#ForcedParam)를 참조하세요.

#### <a name="ExpressionEval"></a>식 평가 
뿐만 아니라 상수 폴딩 가능 식이 아니지만 해당 인수를 컴파일 시간에 알 수 없는 일부 식은 최적화 중 최적화 프로그램의 구성 요소인 결과 집합 크기(카디널리티) 평가자에 의해 평가됩니다. 이때 인수가 매개 변수인지 또는 상수인지 여부는 고려하지 않습니다.

특히 기본 제공 함수 `UPPER`, `LOWER`, `RTRIM`, `DATEPART( YY only )`, `GETDATE`, `CAST` 및 `CONVERT`와 특수 연산자는 해당 입력을 모두 알 수 있는 경우 컴파일 시간에 평가됩니다. 다음 연산자도 해당 입력을 모두 알 수 있는 경우 컴파일 시간에 평가됩니다.
- 산술 연산자: +, -, \*, /, 단항 -
- 논리 연산자: `AND`, `OR`, `NOT`
- 비교 연산자: <, >, <=, >=, <>, `LIKE`, `IS NULL`, `IS NOT NULL`

이외에 다른 함수나 연산자는 카디널리티 예측 중에 쿼리 최적화 프로그램에서 평가되지 않습니다.

#### <a name="examples-of-compile-time-expression-evaluation"></a>컴파일 시간 식 평가의 예
다음과 같은 저장 프로시저를 고려할 수 있습니다.

```sql
USE AdventureWorks2014;
GO
CREATE PROCEDURE MyProc( @d datetime )
AS
SELECT COUNT(*)
FROM Sales.SalesOrderHeader
WHERE OrderDate > @d+1;
```

프로시저의 `SELECT` 문을 최적화하는 동안 쿼리 최적화 프로그램은 `OrderDate > @d+1` 조건에 대한 결과 집합의 예상 카디널리티를 평가하려고 합니다. `@d+1`가 매개 변수이므로 `@d` 식은 상수 폴딩 가능 식이 아닙니다. 그러나 최적화할 때 매개 변수 값이 알려집니다. 따라서 쿼리 최적화 프로그램은 결과 집합의 크기를 정확하게 예측하여 적절한 쿼리 계획을 선택할 수 있습니다.

이제 앞의 예와 유사한 다음 예를 살펴보십시오. 지역 변수로 `@d2` 대신 `@d+1`가 사용되고, 식이 쿼리 내에서가 아니라 SET 문에서 실행된다는 점만 다릅니다.

```sql 
USE AdventureWorks2014;
GO
CREATE PROCEDURE MyProc2( @d datetime )
AS
BEGIN
  DECLARE @d2 datetime
  SET @d2 = @d+1
  SELECT COUNT(*)
  FROM Sales.SalesOrderHeader
  WHERE OrderDate > @d2
END;
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 *MyProc2*의 `SELECT` 문을 최적화할 때 `@d2` 값이 알려지지 않습니다. 따라서 쿼리 최적화 프로그램에서는 `OrderDate > @d2`의 선택도에 대해 기본 추정값(이 예의 경우 30%)을 사용합니다.

### <a name="processing-other-statements"></a>다른 문 처리
`SELECT` 문 처리를 위해 설명된 기본 단계는 `INSERT`, `UPDATE` 및 `DELETE`와 같은 다른 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에도 적용됩니다. `UPDATE` 및 `DELETE` 문은 둘 다 수정되거나 삭제될 행 집합을 대상으로 해야 합니다. 이러한 행을 식별하는 프로세스는 `SELECT` 문의 결과 집합을 구하는 데 사용되는 원본 행을 식별하는 방식과 동일합니다. `UPDATE` 및 `INSERT` 문은 모두 업데이트되거나 삽입될 데이터 값을 제공하는 `SELECT` 문을 포함할 수 있습니다.

`CREATE PROCEDURE` 또는 `ALTER TABLE`과 같은 DDL(데이터 정의 언어) 문조차 결과적으로 시스템 카탈로그 테이블에서, 때로는(예: `ALTER TABLE ADD COLUMN`) 데이터 테이블에 대해 일련의 관계형 연산으로 해석됩니다.

### <a name="worktables"></a>작업 테이블
관계형 엔진은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에 지정된 논리 작업을 수행하기 위해 작업 테이블을 작성해야 합니다. 작업 테이블은 중간 결과를 보관하는 데 사용되는 내부 테이블입니다. 특정 `GROUP BY`, `ORDER BY`또는 `UNION` 쿼리에 대해 작업 테이블이 생성됩니다. 예를 들어 `ORDER BY` 절이 인덱스 범위에 해당하지 않는 열을 참조하는 경우 관계형 엔진은 요청되는 순서로 결과 집합을 정렬하기 위해 작업 테이블을 만들어야 할 수 있습니다. 작업 테이블은 쿼리 계획 일부의 실행 결과를 임시 보관하는 스풀로 사용되기도 합니다. 작업 테이블은 tempdb에 작성되며, 더 이상 필요하지 않으면 자동으로 삭제됩니다.

### <a name="view-resolution"></a>뷰 확인
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 프로세서에서는 인덱싱된 뷰와 인덱싱되지 않은 뷰가 다르게 처리됩니다. 

* 인덱싱된 뷰의 행은 테이블과 동일한 형식으로 데이터베이스에 저장됩니다. 쿼리 프로세서에서 쿼리 계획에 인덱싱된 뷰를 사용하기로 결정하면 인덱싱된 뷰는 기본 테이블과 동일한 방법으로 처리됩니다.
* 인덱싱되지 않은 뷰의 정의만 저장되고 뷰의 행은 저장되지 않습니다. 쿼리 최적화 프로그램은 인덱싱되지 않은 뷰를 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에 대해 작성하는 실행 계획에 뷰 정의의 논리를 추가합니다. 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램에서 인덱싱된 뷰의 사용 시기를 결정하는 데 사용되는 논리는 테이블 인덱스의 사용 시기를 결정하는 데 사용되는 논리와 유사합니다. 인덱싱된 뷰의 데이터가 [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 전체나 일부를 포괄하고 해당 뷰의 인덱스가 저렴한 비용의 액세스 경로로 확인되면, 쿼리에서 이름별로 뷰가 참조되는지 여부와 관계없이 인덱스가 선택됩니다.

[!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 인덱싱되지 않은 뷰를 참조할 경우 파서와 쿼리 최적화 프로그램은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 원본과 뷰의 원본을 모두 분석하고 단일 실행 계획을 세웁니다. [!INCLUDE[tsql](../includes/tsql-md.md)] 문과 뷰에 대해 별도의 계획이 있는 것은 아닙니다.

예를 들어 다음과 같은 뷰가 있습니다.

```sql
USE AdventureWorks2014;
GO
CREATE VIEW EmployeeName AS
SELECT h.BusinessEntityID, p.LastName, p.FirstName
FROM HumanResources.Employee AS h 
JOIN Person.Person AS p
  ON h.BusinessEntityID = p.BusinessEntityID;
GO
```

이 뷰를 기반으로 두 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이 모두 기본 테이블에 대해 동일한 작업을 수행하고 동일한 결과를 생성합니다.

```sql
/* SELECT referencing the EmployeeName view. */
SELECT LastName AS EmployeeLastName, SalesOrderID, OrderDate
FROM AdventureWorks2014.Sales.SalesOrderHeader AS soh
JOIN AdventureWorks2014.dbo.EmployeeName AS EmpN
  ON (soh.SalesPersonID = EmpN.BusinessEntityID)
WHERE OrderDate > '20020531';

/* SELECT referencing the Person and Employee tables directly. */
SELECT LastName AS EmployeeLastName, SalesOrderID, OrderDate
FROM AdventureWorks2014.HumanResources.Employee AS e 
JOIN AdventureWorks2014.Sales.SalesOrderHeader AS soh
  ON soh.SalesPersonID = e.BusinessEntityID
JOIN AdventureWorks2014.Person.Person AS p
  ON e.BusinessEntityID =p.BusinessEntityID
WHERE OrderDate > '20020531';
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio 실행 계획 기능을 통해 관계형 엔진이 두 `SELECT` 문에 대해 동일한 실행 계획을 세우는 것을 알 수 있습니다.

### <a name="using-hints-with-views"></a>뷰에 힌트 사용
쿼리의 뷰에 힌트를 넣으면 뷰가 확장되어 기본 테이블에 액세스할 때 발견되는 다른 힌트와 서로 충돌할 수 있습니다. 이러한 경우 쿼리에서 오류를 반환합니다. 예를 들어 다음과 같이 뷰 정의에 테이블 힌트가 포함되어 있습니다.

```sql
USE AdventureWorks2014;
GO
CREATE VIEW Person.AddrState WITH SCHEMABINDING AS
SELECT a.AddressID, a.AddressLine1, 
    s.StateProvinceCode, s.CountryRegionCode
FROM Person.Address a WITH (NOLOCK), Person.StateProvince s
WHERE a.StateProvinceID = s.StateProvinceID;
```

다음 쿼리를 입력한다고 가정합니다.

```sql
SELECT AddressID, AddressLine1, StateProvinceCode, CountryRegionCode
FROM Person.AddrState WITH (SERIALIZABLE)
WHERE StateProvinceCode = 'WA';
```

쿼리의 뷰 `SERIALIZABLE` 에 적용되는 힌트 `Person.AddrState` 가 뷰 확장 시 뷰의 `Person.Address` 테이블과 `Person.StateProvince` 테이블에 모두 전파되기 때문에 이 쿼리는 실패합니다. 그러나 뷰가 확장될 때 `NOLOCK` 의 `Person.Address`힌트도 나타납니다. `SERIALIZABLE` 힌트와 `NOLOCK` 힌트가 충돌하기 때문에 결과 쿼리가 올바르지 않습니다. 

`PAGLOCK`, `NOLOCK`, `ROWLOCK`, `TABLOCK`또는 `TABLOCKX` 테이블 힌트도 `HOLDLOCK`, `NOLOCK`, `READCOMMITTED`, `REPEATABLEREAD`, `SERIALIZABLE` 테이블 힌트처럼 서로 충돌합니다.

여러 수준의 중첩된 뷰를 통해 힌트가 전파될 수 있습니다. 예를 들어 뷰 `HOLDLOCK` 에 `v1`힌트를 적용하는 쿼리가 있다고 가정합니다. `v1` 이 확장될 때 이 뷰의 정의에 `v2` 뷰가 포함되어 있음을 확인했습니다. `v2`정의에는 이 뷰의 기본 테이블 중 하나에 대한 `NOLOCK` 힌트가 있습니다. 그러나 이 테이블에는 `HOLDLOCK` 뷰의 쿼리로부터 `v1`힌트도 상속됩니다. `NOLOCK` 힌트와 `HOLDLOCK` 힌트가 충돌하므로 쿼리가 실패합니다.

뷰를 포함하는 쿼리에 `FORCE ORDER` 힌트를 사용하면 정렬된 구조체에서의 뷰 위치에 따라 뷰 내의 테이블 조인 순서가 결정됩니다. 예를 들어 다음 쿼리는 세 개의 테이블과 한 개의 뷰에서 선택합니다.

```sql
SELECT * FROM Table1, Table2, View1, Table3
WHERE Table1.Col1 = Table2.Col1 
    AND Table2.Col1 = View1.Col1
    AND View1.Col2 = Table3.Col2;
OPTION (FORCE ORDER);
```

`View1` 은 다음과 같이 정의됩니다.

```sql
CREATE VIEW View1 AS
SELECT Colx, Coly FROM TableA, TableB
WHERE TableA.ColZ = TableB.Colz;
```

쿼리 계획의 조인 순서는 `Table1`, `Table2`, `TableA`, `TableB`, `Table3`입니다.

### <a name="resolving-indexes-on-views"></a>뷰의 인덱스 확인

인덱스와 마찬가지로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 쿼리 최적화 프로그램에서 쿼리 계획에 인덱싱된 뷰를 사용하는 것이 효과적이라고 판단한 경우에만 인덱싱된 뷰를 사용합니다.

모든 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 인덱싱된 뷰를 만들 수 있습니다. 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전의 쿼리 최적화 프로그램은 인덱싱된 뷰를 사용할지 자동으로 검토합니다. 일부 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 인덱싱된 뷰를 사용하려면 `NOEXPAND` 테이블 힌트를 사용해야 합니다. 세부 내용은 각 버전의 설명서를 참조하세요.

다음 조건에 맞을 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램에서 인덱싱된 뷰를 사용합니다. 

* 다음 세션 옵션이 `ON`으로 설정되어 있습니다. 
  * `ANSI_NULLS`
  * `ANSI_PADDING`
  * `ANSI_WARNINGS`
  * `ARITHABORT`
  * `CONCAT_NULL_YIELDS_NULL`
  * `QUOTED_IDENTIFIER` 
* 세션 옵션 `NUMERIC_ROUNDABORT` 이 OFF로 설정되어 있습니다.
* 쿼리 최적화 프로그램에서 쿼리의 요소와 뷰 인덱스 열 간의 일치 사항을 찾습니다. 예를 들어 다음과 같은 사항이 일치합니다. 
  * WHERE 절의 검색 조건 조건자
  * 조인 작업
  * 집계 함수
  * `GROUP BY` 절
  * 테이블 참조
* 인덱스 사용 시 예상 비용이 쿼리 최적화 프로그램에서 고려하는 액세스 메커니즘의 비용 중에서 가장 낮습니다. 
* 인덱싱된 뷰의 테이블 참조에 해당하는 쿼리에서 뷰를 확장하여 기본 테이블에 액세스하는 방식으로 테이블을 참조하거나 직접 테이블을 참조하는 경우 쿼리에서 참조하는 모든 테이블에 같은 힌트 집합이 적용되어 있어야 합니다.

> [!NOTE] 
> 이 컨텍스트에서 `READCOMMITTED` 힌트와 `READCOMMITTEDLOCK` 힌트는 현재 트랜잭션 격리 수준과 관계없이 항상 다른 힌트로 간주됩니다.
 
`SET` 옵션 및 테이블 힌트에 대한 요구 사항을 제외하고 위의 사항은 쿼리 최적화 프로그램에서 쿼리가 테이블 인덱스 범위에 해당하는지 즉, 테이블 인덱스로 쿼리를 처리할 수 있는지 여부를 확인하는 데 사용하는 규칙과 동일합니다. 인덱싱된 뷰를 사용하기 위해 쿼리에 아무 것도 추가로 지정할 필요가 없습니다.

쿼리 최적화 프로그램에서 인덱싱된 뷰를 사용하도록 쿼리의 `FROM` 절에서 인덱싱된 뷰를 명시적으로 참조할 필요가 없습니다. 쿼리가 인덱싱된 뷰에도 있는 기본 테이블의 열에 대한 참조를 포함하고 쿼리 최적화 프로그램에서 해당 인덱싱된 뷰를 사용할 때 비용이 가장 저렴한 액세스 메커니즘을 제공할 수 있을 것으로 예상하는 경우 쿼리 최적화 프로그램은 기본 테이블 인덱스가 쿼리에서 직접 참조되지 않을 때 이러한 기본 테이블 인덱스를 선택하는 것과 유사한 방법으로 인덱싱된 뷰를 선택합니다. 쿼리에서 참조하지 않는 열을 포함하는 뷰의 경우 뷰가 쿼리에 지정된 하나 이상의 열을 포괄하기 위한 가장 저렴한 비용 옵션을 제공하면 쿼리 최적화 프로그램에서 이 뷰를 선택할 수 있습니다.

쿼리 최적화 프로그램은 `FROM` 절에서 참조하는 인덱싱된 뷰를 표준 뷰로 간주하고 처리합니다. 쿼리 최적화 프로그램은 최적화 프로세스 시작 시 뷰의 정의를 쿼리로 확장합니다. 그런 다음 인덱싱된 뷰 일치가 수행됩니다. 쿼리 최적화 프로그램에서 선택하는 최종 실행 계획에 인덱싱된 뷰가 사용될 수 있습니다. 또는 계획이 뷰에서 참조하는 기본 테이블에 액세스하여 뷰에서 필요한 데이터를 구체화할 수 있습니다. 쿼리 최적화 프로그램에서는 이 중 가장 저렴한 비용의 방법이 선택됩니다.

#### <a name="using-hints-with-indexed-views"></a>인덱싱된 뷰에 힌트 사용
`EXPAND VIEWS` 쿼리 힌트를 사용하여 쿼리에 뷰 인덱스가 사용되지 않도록 하거나 `NOEXPAND` 테이블 힌트를 사용하여 쿼리의 `FROM` 절에 지정된 인덱싱된 뷰에 인덱스가 사용되도록 할 수 있습니다. 그러나 쿼리 최적화 프로그램이 각 쿼리에 사용할 최상의 액세스 방법을 동적으로 결정하도록 해야 합니다. `EXPAND` 와 `NOEXPAND` 는 성능을 크게 향상하는 것으로 확인된 특정 경우에만 사용합니다.

`EXPAND VIEWS` 옵션은 쿼리 최적화 프로그램이 전체 쿼리에 뷰 인덱스를 사용하지 않도록 지정합니다. 

뷰에 `NOEXPAND` 를 지정하면 쿼리 최적화 프로그램은 뷰에 정의된 인덱스의 사용을 고려합니다. 선택적`NOEXPAND` 절을 사용하여 `INDEX()` 를 지정하면 쿼리 최적화 프로그램은 지정된 인덱스를 사용합니다. `NOEXPAND` 는 인덱싱된 뷰에만 지정할 수 있고 인덱싱되지 않은 뷰에는 지정할 수 없습니다.

뷰를 포함하는 쿼리에서 `NOEXPAND` 와 `EXPAND VIEWS` 를 지정하지 않으면 뷰가 확장되어 기본 테이블에 액세스합니다. 뷰를 구성하는 쿼리에 테이블 힌트가 포함된 경우 해당 힌트는 기본 테이블로 전파됩니다. 이 프로세스는 뷰 확인에서 자세히 설명합니다. 뷰의 기본 테이블에 있는 힌트 집합이 모두 동일하면 쿼리를 인덱싱된 뷰와 일치시킬 수 있습니다. 대부분의 경우 이러한 힌트는 뷰에서 직접 상속되기 때문에 서로 일치합니다. 그러나 쿼리가 뷰 대신 테이블을 참조하고 이러한 테이블에 직접 적용된 힌트가 동일하지 않으면 쿼리를 인덱싱된 뷰와 일치시킬 수 없습니다. 뷰 확장 후 쿼리에서 참조하는 테이블에 `INDEX`, `PAGLOCK`, `ROWLOCK`, `TABLOCKX`, `UPDLOCK`또는 `XLOCK` 힌트가 적용되면 쿼리를 인덱싱된 뷰와 일치시킬 수 없습니다.

`INDEX (index_val[ ,...n] )` 형식의 테이블 힌트가 쿼리의 뷰를 참조하는 경우 `NOEXPAND` 힌트를 지정하지 않으면 인덱스 힌트가 무시됩니다. 특정 인덱스를 사용하도록 지정하려면 `NOEXPAND`를 사용합니다. 

일반적으로 쿼리 최적화 프로그램이 인덱싱된 뷰를 쿼리와 일치시키면 쿼리의 테이블이나 뷰에 지정된 모든 힌트가 인덱싱된 뷰에 직접 적용됩니다. 쿼리 최적화 프로그램이 인덱싱된 뷰를 사용하지 않도록 선택하면 모든 힌트가 뷰에서 참조하는 테이블로 직접 전파됩니다. 자세한 내용은 뷰 확인을 참조하세요. 이 전파는 조인 힌트에는 적용되지 않습니다. 쿼리 내의 원래 위치에서만 적용됩니다. 쿼리 최적화 프로그램에서 쿼리를 인덱싱된 뷰와 일치시킬 때 조인 힌트는 고려되지 않습니다. 쿼리 계획에서 조인 힌트가 포함된 쿼리의 일부와 일치하는 인덱싱된 뷰를 사용하는 경우 해당 계획에 조인 힌트가 사용되지 않습니다.

인덱싱된 뷰 정의에는 힌트가 허용되지 않습니다. 호환 모드 80 이상에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 인덱싱된 뷰 정의를 유지 관리할 때나 인덱싱된 뷰를 사용하는 쿼리를 실행할 때 인덱싱된 뷰 정의 내의 힌트를 무시합니다. 80 호환 모드에서는 인덱싱된 뷰 정의에 힌트를 사용해도 구문 오류가 발생하지 않지만 힌트가 무시됩니다.

### <a name="resolving-distributed-partitioned-views"></a>분산형 분할 뷰 확인
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 프로세서에서는 분산형 분할 뷰의 성능을 최적화합니다. 분산형 분할 뷰 성능의 가장 중요한 측면은 멤버 서버 간에 전송되는 데이터의 양을 최소화하는 것입니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 분산 쿼리를 효율적으로 사용하여 원격 멤버 테이블의 데이터에 액세스하는 지능적이고 동적인 계획을 작성합니다. 

* 먼저 쿼리 프로세서는 OLE DB를 사용하여 각 멤버 테이블에서 check 제약 조건 정의를 검색합니다. 쿼리 프로세서는 이를 통해 멤버 테이블에 키 값을 분산하여 매핑할 수 있습니다.
* 쿼리 프로세서는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 `WHERE` 절에 지정된 키 범위를 멤버 테이블에 행이 배포되는 방식을 보여주는 맵과 비교합니다. 그런 다음, 쿼리 프로세서는 분산 쿼리를 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 완료하는 데 필요한 원격 행만 검색하는 쿼리 실행 계획을 작성합니다. 또한 실행 계획은 데이터 또는 메타데이터가 요청될 때까지 이러한 데이터를 얻기 위해 원격 멤버 테이블에 액세스하는 것을 연기하는 방식으로도 작성됩니다.

예를 들어 Server1(1부터 3299999까지의`CustomerID` ), Server2(3300000부터 6599999까지의`CustomerID` ) 및 Server3(6600000부터 9999999까지의`CustomerID` )에 걸쳐 customers 테이블이 분할된 시스템이 있다고 가정합니다.

Server1에서 실행되는 다음 쿼리에 대해 작성된 실행 계획을 검토합니다.

```sql
SELECT *
FROM CompanyData.dbo.Customers
WHERE CustomerID BETWEEN 3200000 AND 3400000;
```

이 쿼리에 대한 실행 계획은 로컬 멤버 테이블에서 3200000에서 3299999까지의 `CustomerID` 키 값을 포함하는 행을 추출하고 분산 쿼리를 실행하여 Server2에서 3300000에서 3400000까지의 키 값을 포함하는 행을 검색합니다.

또한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 프로세서는 실행 계획이 작성되어야 할 때 키 값이 알려지지 않은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에 대해 동적 논리를 쿼리 실행 계획으로 작성할 수 있습니다. 예를 들면 다음 저장 프로시저가 있습니다.

```sql
CREATE PROCEDURE GetCustomer @CustomerIDParameter INT
AS
SELECT *
FROM CompanyData.dbo.Customers
WHERE CustomerID = @CustomerIDParameter;
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 프로시저가 실행될 때마다 `@CustomerIDParameter` 매개 변수에서 어떤 키 값을 제공하는지 예측할 수 없습니다. 키 값을 예측할 수 없으므로 쿼리 프로세서는 어떤 멤버 테이블을 액세스해야 하는지도 예측할 수 없습니다. 이러한 경우를 처리하기 위해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 어떤 멤버 테이블이 입력 매개 변수 값에 기반하여 액세스되는지 제어하기 위한 조건부 논리(동적 필터)를 포함하는 실행 계획을 작성합니다. `GetCustomer` 저장 프로시저가 Server1에서 실행되었다고 가정했을 때 실행 계획 논리를 다음과 같이 나타낼 수 있습니다.

```sql
IF @CustomerIDParameter BETWEEN 1 and 3299999
   Retrieve row from local table CustomerData.dbo.Customer_33
ELSE IF @CustomerIDParameter BETWEEN 3300000 and 6599999
   Retrieve row from linked table Server2.CustomerData.dbo.Customer_66
ELSE IF @CustomerIDParameter BETWEEN 6600000 and 9999999
   Retrieve row from linked table Server3.CustomerData.dbo.Customer_99
```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 매개 변수가 없는 쿼리에 대해서도 이러한 유형의 동적 실행 계획을 작성할 때가 있습니다. 실행 계획을 다시 사용할 수 있도록 쿼리 최적화 프로그램이 쿼리를 매개 변수화할 수 있습니다. 쿼리 최적화 프로그램이 분할된 뷰를 참조하는 쿼리를 매개 변수화하는 경우 쿼리 최적화 프로그램에서는 지정된 기본 테이블에서 필요한 행이 나오는 것으로 간주하지 않게 되므로 실행 계획에서 동적 필터를 사용해야 합니다.

## <a name="stored-procedure-and-trigger-execution"></a>저장 프로시저 및 트리거 실행
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 저장 프로시저와 트리거의 원본만 저장합니다. 저장 프로시저나 트리거가 먼저 실행될 때 원본은 실행 계획으로 컴파일됩니다. 실행 계획이 메모리에서 에이징되기 전에 저장 프로시저나 트리거가 다시 실행되는 경우 관계형 엔진은 기존 계획을 검색하고 다시 사용합니다. 계획이 메모리에서 에이징되면 새 계획이 작성됩니다. 이 프로세스는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 모든 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에 대해 수행하는 프로세스와 유사합니다. 성능 면에서 동적 [!INCLUDE[tsql](../includes/tsql-md.md)]의 일괄 처리와 비교했을 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 저장 프로시저와 트리거의 주요 이점은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이 항상 동일하다는 것입니다. 따라서 관계형 엔진이 기존 실행 계획과 SQL 문을 쉽게 대응시킵니다. 또한 저장 프로시저와 트리거 계획이 쉽게 다시 사용됩니다.

저장 프로시저나 트리거의 실행 계획은 저장 프로시저를 호출하거나 트리거를 실행하는 일괄 처리의 실행 계획과는 별도로 실행됩니다. 따라서 저장 프로시저와 트리거 실행 계획을 더 많이 다시 사용할 수 있습니다.

## <a name="execution-plan-caching-and-reuse"></a>실행 계획 캐싱 및 다시 사용
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에는 실행 계획과 데이터 버퍼를 모두 저장하는 데 사용되는 메모리 풀이 있습니다. 실행 계획이나 데이터 버퍼에 할당되는 풀 비율은 시스템 상태에 따라 동적으로 변동됩니다. 실행 계획을 저장하는 데 사용되는 메모리 풀 부분을 계획 캐시라고 합니다.

계획 캐시에는 컴파일된 모든 계획을 위한 두 개의 저장소가 있습니다.
-  지속형 개체(저장 프로시저, 함수 및 트리거)에 관련된 계획에 사용되는 **Object Plans** 캐시 저장소(OBJCP).
-  자동으로 매개 변수화된 쿼리, 동적 쿼리 또는 준비된 쿼리에 관련된 계획에 사용되는 **SQL Plans** 캐시 저장소(SQLCP).

아래 쿼리는 두 가지 관련 캐시 저장소의 메모리 사용량 정보를 제공합니다.

```sql
SELECT * FROM sys.dm_os_memory_clerks
WHERE name LIKE '%plans%';
```

> [!NOTE]
> 계획 캐시에는 계획을 저장하는 데 사용되지 않는 두 개의 추가 저장소가 있습니다.     
> -  뷰, 제약 조건 및 기본값에 대한 계획 컴파일 중에 사용되는 데이터 구조에 사용되는 **Bound Trees** 캐시 저장소(PHDR). 해당 구조를 Bound Trees 또는 Algebrizer Trees라고 합니다.      
> -  Transact-SQL 문을 사용하지 않고 DLL을 사용하여 정의되는 `sp_executeSql` 또는 `xp_cmdshell` 같이 미리 정의된 시스템 프로시저에 사용되는 **확장 저장 프로시저** 캐시 저장소(XPROC). 캐시된 구조에는 프로시저가 구현되는 함수 이름과 DLL 이름만 포함됩니다.      

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 실행 계획은 다음으로 구성됩니다. 

- **컴파일된 계획**(또는 쿼리 계획)     
  컴파일 프로세스에서 생성되는 쿼리 계획은 주로 여러 사용자가 사용하는 재진입용 읽기 전용 데이터 구조입니다. 다음 정보를 저장합니다.
  -  논리 연산자가 설명한 작업을 구현하는 물리 연산자. 
  -  데이터가 액세스, 필터링 및 집계되는 순서를 결정하는 해당 작업의 순서. 
  -  연산자를 통해 흐르는 예상 행 수. 
  
     > [!NOTE]
     > 최신 버전의 [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서 [카디널리티 예측](../relational-databases/performance/cardinality-estimation-sql-server.md)에 사용된 통계 개체에 관한 정보도 저장됩니다.
     
  -  tempdb의 [작업 테이블](#worktables) 또는 작업 파일 같이 만들어야 하는 지원 개체. 
  사용자 컨텍스트 또는 런타임 정보는 쿼리 계획에 저장되지 않습니다. 메모리에는 쿼리 계획의 복사본이 한 개나 두 개만 있습니다. 하나는 모든 직렬 실행용이고 다른 하나는 모든 병렬 실행용입니다. 병렬 복사본은 병렬 처리 수준에 관계없이 모든 병렬 실행에 적용됩니다.   
  
- **실행 컨텍스트**     
  쿼리를 현재 실행하고 있는 각 사용자는 매개 변수 값 등의 해당 실행 관련 데이터를 보유하는 데이터 구조를 갖습니다. 이 데이터 구조를 실행 컨텍스트라고 합니다. 실행 컨텍스트 데이터 구조는 다시 사용되지만 해당 콘텐츠는 다시 사용되지 않습니다. 다른 사용자가 동일한 쿼리를 실행하는 경우 데이터 구조는 새 사용자의 컨텍스트를 사용하여 다시 초기화됩니다. 

  ![execution_context](../relational-databases/media/execution-context.gif)

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행할 때 [!INCLUDE[ssde_md](../includes/ssde_md.md)]은 먼저 계획 캐시를 조사하여 동일한 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에 대해 기존 실행 계획이 있는지 확인합니다. [!INCLUDE[tsql](../includes/tsql-md.md)] 문은 문자 그대로 문자당 캐시된 계획 및 문자 하나와 이전에 실행된 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이 일치하는 경우 존재하는 것으로 규정합니다. 기존 계획을 찾으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 그것을 재사용하기 때문에 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 다시 컴파일하기 위한 오버헤드가 발생하지 않습니다. 실행 계획이 없는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 쿼리에 대해 새로운 실행 계획이 생성됩니다.

> [!NOTE]
> rowstore에서 실행 중인 대량 작업 명령문이나 크기가 8KB를 넘는 문자열 리터럴이 포함된 문과 같은 일부 [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 실행 계획은 일부 문은 계획 캐시에서 지속되지 않습니다. 해당 계획은 쿼리가 실행되는 동안에만 존재합니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에는 특정 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에 대한 기존 실행 계획을 찾는 효율적인 알고리즘이 있습니다. 대부분의 시스템에서 이러한 검색에 사용되는 최소 리소스는 모든 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 컴파일하는 대신 기존 계획을 다시 사용함으로써 절약되는 리소스보다도 적습니다.

계획 캐시에서 사용되지 않는 기존 실행 계획과 새 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 대응시키는 알고리즘을 적용하려면 모든 개체 참조가 정규화되어야 합니다. 예를 들어 `Person`은 아래 `SELECT` 문을 실행하는 사용자의 기본 스키마입니다. 이 예제에서는 `Person` 테이블이 실행되기 위해 정규화되어야 할 필요가 없는 반면, 두 번째 명령문은 기존 계획과 일치하지 않지만 세 번째 명령문은 일치한다는 의미입니다.

```sql
USE AdventureWorks2014;
GO
SELECT * FROM Person;
GO
SELECT * FROM Person.Person;
GO
SELECT * FROM Person.Person;
GO
```

지정된 실행에 대해 다음 SET 옵션을 변경하면 계획을 다시 사용하는 기능에 영향을 줍니다. 이는 [!INCLUDE[ssde_md](../includes/ssde_md.md)]이 [상수 폴딩](#ConstantFolding)을 수행하고 이 옵션이 해당 식의 결과에 영향을 주기 때문입니다.

|||   
|-----------|------------|------------|    
|ANSI_NULL_DFLT_OFF|FORCEPLAN|ARITHABORT|    
|DATEFIRST|ANSI_PADDING|NUMERIC_ROUNDABORT|    
|ANSI_NULL_DFLT_ON|LANGUAGE|CONCAT_NULL_YIELDS_NULL|    
|DATEFORMAT|ANSI_WARNINGS|QUOTED_IDENTIFIER|    
|ANSI_NULLS|NO_BROWSETABLE|ANSI_DEFAULTS|    

### <a name="caching-multiple-plans-for-the-same-query"></a>동일한 쿼리의 여러 계획 캐싱 
쿼리와 실행 계획은 지문과 비슷하게 [!INCLUDE[ssde_md](../includes/ssde_md.md)]에서 고유하게 식별할 수 있습니다.
-  **쿼리 계획 해시**는 지정된 쿼리의 실행 계획에서 계산되는 이진 해시 값으로, 비슷한 실행 계획을 고유하게 식별하는 데 사용됩니다. 
-  **쿼리 해시**는 쿼리의 [!INCLUDE[tsql](../includes/tsql-md.md)] 텍스트에서 계산되는 이진 해시 값으로, 쿼리를 고유하게 식별하는 데 사용됩니다. 

계획이 캐시에 남아 있는 동안에만 일정하게 유지되는 임시 식별자인 **계획 핸들**을 사용하여 계획 캐시에서 컴파일된 계획을 검색할 수 있습니다. 계획 핸들은 전체 일괄 처리의 컴파일된 계획에서 파생되는 해시 값입니다. 일괄 처리에서 하나 이상의 문이 다시 컴파일되는 경우에도 컴파일된 계획의 계획 핸들은 동일하게 유지됩니다.

> [!NOTE]
> 계획이 단일 문 대신 일괄 처리용으로 컴파일된 경우 계획 핸들 및 문 오프셋을 사용하여 일괄 처리에 있는 개별 문의 계획을 검색할 수 있습니다.     
> `sys.dm_exec_requests` DMV는 현재 실행 중인 일괄 처리 또는 지속형 개체의 현재 실행 중인 문을 참조하는 각 레코드의 `statement_start_offset` 및 `statement_end_offset` 열을 포함합니다. 자세한 내용은 [dm_exec_requests(Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)를 참조하세요.       
> `sys.dm_exec_query_stats` DMV는 일괄 처리 또는 지속형 개체 내에서 문의 위치를 참조하는 각 레코드의 해당 열도 포함합니다. 자세한 내용은 [dm_exec_query_stats(Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)를 참조하세요.     

일괄 처리의 실제 [!INCLUDE[tsql](../includes/tsql-md.md)] 텍스트는 **SQL 관리자** 캐시(SQLMGR)라는 계획 캐시의 별도 메모리 공간에 저장됩니다. 식별자를 참조하는 하나 이상의 계획이 계획 캐시에 남아 있는 동안에만 일정하게 유지되는 임시 식별자인 **SQL 핸들**을 사용하여 SQL 관리자 캐시에서 컴파일된 계획의 [!INCLUDE[tsql](../includes/tsql-md.md)] 텍스트는 검색할 수 있습니다. SQL 핸들은 전체 일괄 처리 텍스트에서 파생되는 해시 값이며 모든 일괄 처리에서 고유하게 됩니다.

> [!NOTE]
> 컴파일된 계획처럼 [!INCLUDE[tsql](../includes/tsql-md.md)] 텍스트는 주석을 포함하여 일괄 처리별로 저장됩니다. SQL 핸들은 전체 일괄 처리 텍스트의 MD5 해시를 포함하며 모든 일괄 처리에서 고유하게 됩니다.

아래 쿼리는 SQL 관리자 캐시의 메모리 사용량 정보를 제공합니다.

```sql
SELECT * FROM sys.dm_os_memory_objects
WHERE type = 'MEMOBJ_SQLMGR';
```

SQL 핸들과 계획 핸들 간에는 1:N 관계가 있습니다. 해당 조건은 컴파일된 계획의 캐시 키가 서로 다른 경우 발생합니다. 이 조건은 동일한 일괄 처리의 두 실행 간에 SET 옵션이 변경되기 때문에 발생할 수 있습니다.

다음 저장 프로시저를 고려해 보세요.

```sql
USE WideWorldImporters;
GO
CREATE PROCEDURE usp_SalesByCustomer @CID int
AS
SELECT * FROM Sales.Customers
WHERE CustomerID = @CID
GO

SET ANSI_DEFAULTS ON
GO

EXEC usp_SalesByCustomer 10
GO
```

아래 쿼리를 사용하여 계획 캐시에서 찾을 수 있는 항목을 확인합니다.

```sql
SELECT cp.memory_object_address, cp.objtype, refcounts, usecounts, 
    qs.query_plan_hash, qs.query_hash,
    qs.plan_handle, qs.sql_handle
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text (cp.plan_handle)
CROSS APPLY sys.dm_exec_query_plan (cp.plan_handle)
INNER JOIN sys.dm_exec_query_stats AS qs ON qs.plan_handle = cp.plan_handle
WHERE text LIKE '%usp_SalesByCustomer%'
GO
```

[!INCLUDE[ssResult](../includes/ssresult-md.md)]

```
memory_object_address   objtype   refcounts   usecounts   query_plan_hash    query_hash
---------------------   -------   ---------   ---------   ------------------ ------------------ 
0x000001CC6C534060      Proc      2           1           0x3B4303441A1D7E6D 0xA05D5197DA1EAC2D  

plan_handle                                                                               
------------------------------------------------------------------------------------------
0x0500130095555D02D022F111CD01000001000000000000000000000000000000000000000000000000000000

sql_handle
------------------------------------------------------------------------------------------
0x0300130095555D02C864C10061AB000001000000000000000000000000000000000000000000000000000000
```

이제 실행 컨텍스트는 변경하지 않지만 다른 매개 변수를 사용하여 저장 프로시저를 실행합니다.

```sql
EXEC usp_SalesByCustomer 8
GO
```

계획 캐시에서 찾을 수 있는 항목을 다시 확인합니다. [!INCLUDE[ssResult](../includes/ssresult-md.md)]

```
memory_object_address   objtype   refcounts   usecounts   query_plan_hash    query_hash
---------------------   -------   ---------   ---------   ------------------ ------------------ 
0x000001CC6C534060      Proc      2           2           0x3B4303441A1D7E6D 0xA05D5197DA1EAC2D  

plan_handle                                                                               
------------------------------------------------------------------------------------------
0x0500130095555D02D022F111CD01000001000000000000000000000000000000000000000000000000000000

sql_handle
------------------------------------------------------------------------------------------
0x0300130095555D02C864C10061AB000001000000000000000000000000000000000000000000000000000000
```

`usecounts`가 2로 증가했습니다. 즉, 실행 컨텍스트 데이터 구조가 다시 사용되었으므로 동일한 캐시된 계획이 그대로 다시 사용되었습니다. 이제 `SET ANSI_DEFAULTS` 옵션을 변경하고 동일한 매개 변수를 사용하여 저장 프로시저를 실행합니다.

```sql
SET ANSI_DEFAULTS OFF
GO

EXEC usp_SalesByCustomer 8
GO
```

계획 캐시에서 찾을 수 있는 항목을 다시 확인합니다. [!INCLUDE[ssResult](../includes/ssresult-md.md)]

```
memory_object_address   objtype   refcounts   usecounts   query_plan_hash    query_hash
---------------------   -------   ---------   ---------   ------------------ ------------------ 
0x000001CD01DEC060      Proc      2           1           0x3B4303441A1D7E6D 0xA05D5197DA1EAC2D  
0x000001CC6C534060      Proc      2           2           0x3B4303441A1D7E6D 0xA05D5197DA1EAC2D

plan_handle                                                                               
------------------------------------------------------------------------------------------
0x0500130095555D02B031F111CD01000001000000000000000000000000000000000000000000000000000000
0x0500130095555D02D022F111CD01000001000000000000000000000000000000000000000000000000000000

sql_handle
------------------------------------------------------------------------------------------
0x0300130095555D02C864C10061AB000001000000000000000000000000000000000000000000000000000000
0x0300130095555D02C864C10061AB000001000000000000000000000000000000000000000000000000000000
```

이제 `sys.dm_exec_cached_plans` DMV 출력에 두 개의 항목이 있습니다.
-  `usecounts` 열에는 `SET ANSI_DEFAULTS OFF`를 사용하여 한 번 실행된 계획인 첫 번째 레코드의 `1` 값이 표시됩니다.
-  `usecounts` 열에는 두 번 실행되었기 때문에 `SET ANSI_DEFAULTS ON`을 사용하여 실행된 계획인 두 번째 레코드의 `2` 값이 표시됩니다.    
-  다른 `memory_object_address`는 계획 캐시의 다른 실행 계획 항목을 참조합니다. 그러나 두 항목 모두 동일한 일괄 처리를 참조하므로 두 항목의 `sql_handle` 값은 동일합니다. 
   -  `ANSI_DEFAULTS`가 OFF로 설정된 실행은 새로운 `plan_handle`을 포함하며 동일한 SET 옵션 세트가 포함된 호출에 다시 사용될 수 있습니다. 변경된 SET 옵션으로 인해 실행 컨텍스트가 다시 초기화되었으므로 새 계획 핸들이 필요합니다. 그러나 다시 컴파일을 트리거하지 않습니다. 동일한 `query_plan_hash` 및 `query_hash` 값에서 알 수 있듯이 두 항목은 모두 동일한 계획 및 쿼리를 참조합니다.

이는 동일한 일괄 처리에 해당하는 두 개의 계획 항목이 캐시에 있음을 의미하며, 계획 다시 사용에 맞게 최적화하고 계획 캐시 크기를 필요한 최솟값으로 유지하기 위해 동일한 쿼리를 반복해서 실행하는 경우 SET 옵션에 영향을 주는 계획 캐시가 동일한지 확인하는 것의 중요성을 강조합니다. 

> [!TIP]
> 일반적인 문제는 클라이언트에 따라 SET 옵션의 기본값이 다를 수 있다는 것입니다. 예를 들어 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 통해 설정된 연결은 자동으로 `QUOTED_IDENTIFIER`를 ON으로 설정하는 반면, SQLCMD는 `QUOTED_IDENTIFIER`를 OFF로 설정합니다. 위의 예제에 설명된 것처럼 두 클라이언트에서 동일한 쿼리를 실행하면 여러 계획이 생성됩니다.

### <a name="removing-execution-plans-from-the-plan-cache"></a>계획 캐시에서 실행 계획 제거
실행 계획은 이를 저장하기에 충분한 메모리가 있는 한 계획 캐시에 계속 남아 있습니다. 메모리의 여유가 많지 않으면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 비용을 기반으로 한 방법을 사용하여 계획 캐시에서 어떤 실행 계획을 제거할지 결정합니다. 비용을 기반으로 한 결정을 내리기 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 다음 요인에 따라 각 실행 계획에 대한 현재 비용 변수를 늘리거나 줄입니다.

사용자 프로세스에서 캐시에 실행 계획을 삽입하는 경우 현재 비용을 원래 쿼리 컴파일 비용과 같게 설정하고, 임시 실행 계획의 경우 사용자 프로세스에서 현재 비용을 0으로 설정합니다. 그 후 사용자 프로세스에서 실행 계획을 참조할 때마다 현재 비용을 원래 컴파일 비용으로 다시 설정하고, 임시 실행 계획의 경우 사용자 프로세스에서 현재 비용을 늘립니다. 모든 계획의 경우 현재 비용의 최대값은 원래 컴파일 비용입니다.

메모리의 여유가 많지 않으면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 계획 캐시에서 실행 계획을 제거하여 이에 대처합니다. 어떤 계획을 제거할지 결정하기 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 각 실행 계획의 상태를 반복 조사하고 현재 비용이 0인 계획을 제거합니다. 메모리가 부족하다는 이유만으로는 현재 비용이 0인 실행 계획이 자동으로 제거되지 않습니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 계획을 조사하여 현재 비용이 0이라는 사실을 확인했을 때만 해당 계획이 제거됩니다. 실행 계획을 조사할 때 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 쿼리에 현재 사용되고 있지 않은 계획에 대해 현재 비용을 0에 가깝게 점차 줄여나갑니다.

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 메모리 요구 사항을 충족하기에 충분할 만큼 실행 계획이 제거될 때까지 실행 계획을 되풀이하여 조사합니다. 그 결과로 메모리가 부족한 상태에서 실행 계획의 비용이 여러 차례에 걸쳐 증감할 수 있습니다. 충분한 메모리가 다시 확보되면 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 사용되지 않는 실행 계획의 현재 비용을 더 이상 줄이지 않으며 해당 비용이 0인 계획을 포함한 모든 실행 계획이 계획 캐시에 계속 남습니다.

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서는 리소스 모니터와 사용자 작업자 스레드를 사용하여 계획 캐시에서 메모리를 확보하여 메모리 부족 문제에 대처합니다. 리소스 모니터와 사용자 작업자 스레드를 통해 계획의 실행 여부를 동시에 조사하여 사용되지 않는 실행 계획 각각의 현재 비용을 줄일 수 있습니다. 전체적인 메모리 부족 현상이 발생하면 리소스 모니터를 통해 계획 캐시에서 실행 계획이 제거됩니다. 리소스 모니터에서는 시스템 메모리, 프로세스 메모리, 리소스 풀 메모리 및 모든 캐시의 최대 크기에 대한 정책을 따르는 방식으로 메모리를 확보합니다. 

모든 캐시의 최대 크기는 버퍼 풀 크기에 따라 결정되며 최대 서버 메모리를 초과할 수 없습니다. 최대 서버 메모리를 구성하는 방법에 대한 자세한 내용은 `max server memory` 에서 `sp_configure`설정을 참조하세요. 

단일 캐시 메모리 부족 현상이 발생하면 사용자 작업자 스레드를 통해 계획 캐시에서 실행 계획이 제거됩니다. 이때는 단일 캐시의 최대 크기와 단일 캐시의 최대 항목 수에 대한 정책을 따릅니다. 

다음 예제에서는 어떤 실행 계획이 계획 캐시에서 제거되는지 보여 줍니다.

* 실행 계획은 자주 참조되므로 비용이 절대로 0이 되지 않습니다. 메모리가 부족하지 않고 현재 비용이 0이 아닌 경우 계획이 계획 캐시에 남아 있고 제거되지 않습니다.
* 임시 실행 계획이 삽입되고 메모리 부족 현상이 발생하기 전에 다시 참조되지 않습니다. 임시 계획의 현재 비용이 0으로 초기화되므로 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 실행 계획을 조사할 때 현재 비용이 0임을 확인하고 해당 계획을 계획 캐시에서 제거합니다. 메모리가 부족하지 않으면 현재 비용이 0인 임시 실행 계획이 계획 캐시에 남아 있습니다.

단일 계획이나 모든 계획을 캐시에서 수동으로 제거하려면 [DBCC FREEPROCCACHE](../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)를 사용하세요. [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]부터 `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE`를 사용하여 범위에 있는 데이터베이스의 프로시저(계획) 캐시를 지웁니다.

### <a name="recompiling-execution-plans"></a>실행 계획 다시 컴파일

데이터베이스에서 특정 항목을 변경하면 데이터베이스의 새로운 상태에 따라 실행 계획이 비효율적으로 또는 유효하지 않게 될 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 이렇게 실행 계획을 무효화하고 계획을 유효하지 않도록 만드는 변경 사항을 감지합니다. 이러한 경우에는 쿼리를 실행하는 다음 연결을 위해 새 계획을 다시 컴파일해야 합니다. 다음과 같은 조건에서 계획이 무효화될 수 있습니다. 

* 쿼리에서 참조하는 테이블이나 뷰가 변경된 경우(`ALTER TABLE` 및 `ALTER VIEW`).
* 단일 프로시저가 변경된 경우. 이 경우 해당 프로시저의 모든 계획이 캐시에서 삭제됩니다(`ALTER PROCEDURE`).
* 실행 계획에 사용되는 인덱스가 변경된 경우
* `UPDATE STATISTICS`등의 문에서 명시적으로 생성되거나 자동으로 생성되어 실행 계획에 사용되는 통계가 업데이트된 경우.
* 실행 계획에 사용되는 인덱스가 삭제된 경우
* `sp_recompile`에 대한 명시적 호출.
* 쿼리에서 참조하는 테이블을 수정하는 다른 사용자가 `INSERT` 또는 `DELETE` 문으로 키를 많이 변경한 경우.
* 트리거가 있는 테이블의 경우 inserted 또는 deleted 테이블의 행 수가 현저하게 증가하는 경우.
* `WITH RECOMPILE` 옵션을 사용하여 저장 프로시저를 실행하는 경우.

대부분의 다시 컴파일은 문 정확성이나 잠재적으로 더 빠른 쿼리 실행 계획을 얻는 데 필요합니다.

2005 이전 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전에서는 일괄 처리 내의 문이 다시 컴파일을 발생시킬 때마다 저장 프로시저, 트리거, 임시 일괄 처리 또는 준비된 문을 통해 제출되었는지와 관계없이 전체 일괄 처리가 다시 컴파일됩니다. [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]부터 다시 컴파일을 트리거하는 일괄 처리 내의 문만 다시 컴파일됩니다. 또한 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 이상 버전에서는 기능 세트가 확장되어 더 많은 다시 컴파일 유형을 제공합니다.

다시 컴파일을 유발하고 이에 따라 CPU 시간 및 잠금과 관련하여 성능 저하를 일으키는 문의 수는 대개 적으므로 문 수준 다시 컴파일이 성능에 유리합니다. 문 수준 다시 컴파일을 사용하면 다시 컴파일하지 않아도 되는 일괄 처리 내의 다른 문의 경우 이러한 성능 저하가 발생하지 않습니다.

`sql_statement_recompile` 확장 이벤트(xEvent)는 문 수준의 재컴파일이 있는지 보고합니다. 어떠한 종류의 일괄 처리에서든 문 수준의 재컴파일이 필요한 경우 이 xEvent가 발생합니다. 여기에는 저장 프로시저, 트리거, 임시 일괄 처리 및 쿼리가 포함됩니다. 일괄 처리는 sp_executesql, 동적 SQL, Prepare 메서드 또는 Execute 메서드를 비롯한 여러 인터페이스를 통해 제출할 수 있습니다.
`sql_statement_recompile` xEvent의 `recompile_cause` 열에는 다시 컴파일된 이유를 나타내는 정수 코드가 들어 있습니다. 다음 표에는 가능한 이유가 나와 있습니다.

|||
|----|----|  
|스키마가 변경됨|통계가 변경됨|  
|컴파일이 지연됨|SET 옵션이 변경됨|  
|임시 테이블이 변경됨|원격 행 집합이 변경됨|  
|`FOR BROWSE` 권한이 변경됨|쿼리 알림 환경이 변경됨|  
|분할 뷰가 변경됨|커서 옵션이 변경됨|  
|`OPTION (RECOMPILE)` 이 요청되었습니다.|매개 변수가 있는 계획이 플러시됨|  
|데이터베이스 버전에 영향을 주는 계획이 변경됨|쿼리 저장소 계획 강제 적용 정책이 변경됨|  
|쿼리 저장소 계획 강제 적용이 실패함|쿼리 저장소에 계획이 누락됨|

> [!NOTE]
> xEvent를 사용할 수 없는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전에서는 문 수준의 재컴파일을 보고하기 위한 동일한 목적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로파일러 [SP:Recompile](../relational-databases/event-classes/sp-recompile-event-class.md) 추적 이벤트를 사용할 수 있습니다.
> 추적 이벤트 `SQL:StmtRecompile`도 문 수준의 다시 컴파일을 보고하며, 다시 컴파일을 추적하고 디버그하는 데에도 이 추적 이벤트를 사용할 수 있습니다. `SP:Recompile` 은 저장 프로시저와 트리거에 대해서만 생성되는 반면 `SQL:StmtRecompile` 은 `sp_executesql`, 준비된 쿼리 및 동적 SQL을 사용하여 실행되는 저장 프로시저, 트리거, 임시 일괄 처리 및 일괄 처리에 대해 생성됩니다.
> `SP:Recompile` 및 `SQL:StmtRecompile`의 *EventSubClass* 열에는 다시 컴파일할 이유를 나타내는 정수 코드가 들어 있습니다. 코드에 대한 설명은 [여기](../relational-databases/event-classes/sql-stmtrecompile-event-class.md)에 있습니다.

> [!NOTE]
> `AUTO_UPDATE_STATISTICS` 데이터베이스 옵션을 `ON`으로 설정하면 마지막 실행 이후 통계가 업데이트되거나 카디널리티가 크게 변경된 테이블이나 인덱싱된 뷰를 대상으로 하는 쿼리가 모두 다시 컴파일됩니다. 이러한 동작은 일반 사용자 정의 테이블, 임시 테이블 및 DML 트리거로 생성된 삽입 테이블과 삭제 테이블에 적용됩니다. 과도한 재컴파일로 인해 쿼리 성능이 저하되면 이 설정을 `OFF`로 변경하세요. `AUTO_UPDATE_STATISTICS` 데이터베이스 옵션을 `OFF`로 설정하면 통계나 카디널리티 변경 내용에 따른 재컴파일은 발생하지 않습니다. 단, DML `INSTEAD OF` 트리거에 의해 생성되는 삽입 테이블과 삭제 테이블은 예외입니다. 두 테이블은 tempdb에 생성되므로 두 테이블에 액세스하는 쿼리의 다시 컴파일은 tempdb의 `AUTO_UPDATE_STATISTICS` 설정에 따라 결정됩니다. 2005 이전 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 이 설정이 `OFF`인 경우에도 DML 트리거에 의한 삽입 테이블과 삭제 테이블의 카디널리티 변경 내용에 따라 계속하여 쿼리가 다시 컴파일됩니다.

### <a name="PlanReuse"></a> 매개 변수 및 실행 계획 재사용
ADO, OLE DB 및 ODBC 애플리케이션의 매개 변수 표식을 포함하여 매개 변수를 사용하면 실행 계획을 좀 더 많이 재사용할 수 있습니다. 

> [!WARNING] 
> 또한 최종 사용자가 입력한 값을 갖는 매개 변수 또는 매개 변수 표식을 사용하는 것이 데이터 액세스 API 메서드, `EXECUTE` 문 또는 `sp_executesql` 저장 프로시저 중 하나를 사용하여 실행하는 문자열에 값을 연결하는 것보다 안전합니다.
 
다음의 두 `SELECT` 문 간의 유일한 차이점은 `WHERE` 절에서 비교된 값이 다르다는 것입니다.

```sql
SELECT * 
FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 1;
```

```sql
SELECT * 
FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 4;
```

이러한 쿼리에 대한 실행 계획 간의 유일한 차이점은 `ProductSubcategoryID` 열을 비교할 때 저장되는 값이 다르다는 것입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 항상 해당 명령문이 기본적으로 동일한 계획을 생성하고 그 계획을 재사용한다는 것을 인식하게 하려는 것이 목적이지만 때때로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 복잡한 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 이러한 사실을 탐지하지 못합니다.

매개 변수를 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 상수를 분리하면 관계형 엔진이 중복된 계획을 인식하는 데 도움이 됩니다. 다음 방법으로 매개 변수를 사용할 수 있습니다. 

* [!INCLUDE[tsql](../includes/tsql-md.md)]에서 `sp_executesql`을 사용합니다. 

   ```sql
   DECLARE @MyIntParm INT
   SET @MyIntParm = 1
   EXEC sp_executesql
     N'SELECT * 
     FROM AdventureWorks2014.Production.Product 
     WHERE ProductSubcategoryID = @Parm',
     N'@Parm INT',
     @MyIntParm
   ```

   SQL 문을 동적으로 생성하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트, 저장 프로시저 또는 트리거에 대해서는 이 메서드를 사용하는 것이 좋습니다. 

* ADO, OLE DB 및 ODBC는 매개 변수 표식을 사용합니다. 매개 변수 표식은 SQL 문의 상수를 대신하는 물음표(?)로 프로그램 변수에 바인딩됩니다. 예를 들어 ODBC 애플리케이션에서는 다음을 수행합니다. 

   * `SQLBindParameter` 를 사용하여 SQL 문에서 정수 변수를 첫째 매개 변수 표식에 바인딩합니다.
   * 변수에 정수 값을 배치합니다.
   * 매개 변수 표식(?)을 지정하여 문을 실행합니다. 

   ```
   SQLExecDirect(hstmt, 
     "SELECT * 
     FROM AdventureWorks2014.Production.Product 
     WHERE ProductSubcategoryID = ?",
     SQL_NTS);
   ```

   애플리케이션에서 매개 변수 표식이 사용된 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 포함된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client OLE DB 공급자와 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 `sp_executesql`을 사용하여 문을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 보냅니다. 

* 기본적으로 매개 변수를 사용하는 저장 프로시저를 디자인합니다.

애플리케이션 디자인 내에 매개 변수를 명시적으로 구축하지 않은 경우에는 단순 매개 변수화의 기본 동작을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램에서 특정 쿼리를 자동으로 매개 변수화할 수 있습니다. 또는 `ALTER DATABASE` 문의 `PARAMETERIZATION` 옵션을 `FORCED`로 설정하여 데이터베이스의 모든 쿼리를 강제 매개 변수화하도록 쿼리 최적화 프로그램을 설정할 수 있습니다.

강제 매개 변수화를 설정한 경우에도 단순 매개 변수화가 계속해서 수행될 수 있습니다. 예를 들어 다음 쿼리는 강제 매개 변수화 규칙에 따라 매개 변수화할 수 없습니다.

```sql
SELECT * FROM Person.Address
WHERE AddressID = 1 + 2;
```

그러나 단순 매개 변수화 규칙에 따르면 매개 변수화할 수 있습니다. 강제 매개 변수화를 시도한 후 실패하면 그 다음으로는 단순 매개 변수화를 시도합니다.

### <a name="SimpleParam"></a> 단순 매개 변수화
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 Transact-SQL 문에 매개 변수 또는 매개 변수 표식을 사용하여 새 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 이전에 컴파일된 기존의 실행 계획과 일치시키는 관계형 엔진의 성능을 향상시킵니다.

> [!WARNING] 
> 최종 사용자가 입력한 값을 갖는 매개 변수 또는 매개 변수 표식을 사용하는 것이 데이터 액세스 API 메서드, `EXECUTE` 문 또는 `sp_executesql` 저장 프로시저 중 하나를 사용하여 실행되는 문자열에 값을 연결하는 것보다 안전합니다.

매개 변수를 사용하지 않고 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이 실행되면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 내부적으로 해당 문을 매개 변수화하여 기존 실행 계획과 일치할 가능성을 높입니다. 이 프로세스를 단순 매개 변수화라고 합니다. 2005 이전 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전에서는 이 프로세스를 자동 매개 변수화라고 했습니다.

다음 문을 고려해 보십시오.

```sql
SELECT * FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 1;
```

문 끝의 값 1은 매개 변수로 지정될 수 있습니다. 관계형 엔진은 마치 값 1 대신 매개 변수가 지정된 것처럼 이 일괄 처리에 대해 실행 계획을 작성합니다. 이러한 단순 매개 변수화로 인해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 다음 두 문이 기본적으로 동일한 실행 계획을 생성한다는 것을 확인하고 두 번째 문에 대해 첫 번째 계획을 재사용합니다.

```sql
SELECT * FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 1;
```
```sql
SELECT * FROM AdventureWorks2014.Production.Product 
WHERE ProductSubcategoryID = 4;
```

복잡한 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 처리할 때 관계형 엔진은 매개 변수화할 수 있는 식을 결정하기가 어려울 수 있습니다. 복잡한 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 사용되지 않은 기존 실행 계획과 일치시키는 관계형 엔진의 성능을 향상하려면 sp_executesql 또는 매개 변수 표식을 사용하여 매개 변수를 명시적으로 지정합니다. 

> [!NOTE]
> +, -, \*, / 또는 % 산술 연산자를 사용하여 암시적 또는 명시적으로 int, smallint, tinyint 또는 bigint 상수 값을 float, real, decimal 또는 numeric의 데이터 형식으로 변환할 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 특정 규칙에 따라 식 결과의 형식과 전체 자릿수를 계산합니다. 그러나 이러한 규칙은 쿼리의 매개 변수화 여부에 따라 다릅니다. 따라서 쿼리에서 유사한 식을 사용해도 다른 결과가 발생하는 경우가 있습니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 단순 매개 변수화의 기본 동작에 따라 비교적 작은 클래스의 쿼리를 매개 변수화합니다. 그러나 `PARAMETERIZATION` 명령의 `ALTER DATABASE` 옵션을 `FORCED`로 설정하여 데이터베이스의 모든 쿼리를 특정 제한 사항에 따라 매개 변수화하도록 지정할 수 있습니다. 이렇게 하면 쿼리 컴파일 빈도를 낮추어 대량의 동시 쿼리가 발생하는 데이터베이스의 성능이 향상될 수 있습니다.

또는 구문은 동일하고 매개 변수 값만 다른 쿼리 및 단일 쿼리를 매개 변수화하도록 지정할 수 있습니다. 

### <a name="ForcedParam"></a> 강제 매개 변수화
데이터베이스의 모든 `SELECT`, `INSERT`, `UPDATE` 및 `DELETE` 문이 특정 제한에 따라 매개 변수화되도록 지정하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 기본 단순 매개 변수화 동작을 재정의할 수 있습니다. 강제 매개 변수화는 `PARAMETERIZATION` 문에서 `FORCED` 옵션을 `ALTER DATABASE` 로 설정하면 적용됩니다. 강제 매개 변수화를 사용하여 쿼리 컴파일 및 재컴파일 빈도를 줄여 특정 데이터베이스의 성능을 향상시킬 수 있습니다. 일반적으로 POS(Point of Sale) 애플리케이션과 같은 원본으로부터 대량의 동시 쿼리를 처리하는 데이터베이스에서 강제 매개 변수화를 사용하면 도움이 될 수 있습니다.

`PARAMETERIZATION` 옵션을 `FORCED`로 설정하면 임의의 형식으로 전송된 `SELECT`, `INSERT`, `UPDATE`또는 `DELETE` 문에 표시되는 리터럴 값이 쿼리 컴파일 중에 매개 변수로 변환됩니다. 그러나 다음 쿼리 구문에 나타나는 리터럴은 예외입니다. 

* `INSERT...EXECUTE` 문.
* 저장 프로시저, 트리거 또는 사용자 정의 함수의 본문 안에 있는 문. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 이미 이러한 루틴에 대한 쿼리 계획을 재사용하고 있습니다.
* 클라이언트 쪽 애플리케이션에서 이미 매개 변수화된 준비된 문
* XQuery 메서드 호출이 포함된 문. 이러한 문에서는 `WHERE` 절과 같이 해당 인수가 일반적으로 매개 변수화되는 컨텍스트에서 메서드가 나타납니다. 해당 인수가 매개 변수화되지 않는 컨텍스트에서 메서드가 나타날 경우에는 문의 나머지 부분이 매개 변수화됩니다.
* [!INCLUDE[tsql](../includes/tsql-md.md)] 커서 내의 문. API 커서 내의`SELECT` 문은 매개 변수화됩니다.
* 사용되지 않는 쿼리 구문
* `ANSI_PADDING` 또는 `ANSI_NULLS` 를 `OFF`로 설정한 컨텍스트에서 실행되는 모든 문.
* 매개 변수화하기에 적합한 리터럴이 2,097개 이상 포함된 문
* `WHERE T.col2 >= @bb`와 같은 변수를 참조하는 문
* `RECOMPILE` 쿼리 힌트를 포함하는 문.
* `COMPUTE` 절을 포함하는 문.
* `WHERE CURRENT OF` 절을 포함하는 문.

또한 다음 쿼리 절은 매개 변수화되지 않습니다. 이러한 경우 해당 절만 매개 변수화되지 않습니다. 동일한 쿼리 내의 다른 절에는 강제 매개 변수화가 적용될 수 있습니다.

* 모든 `SELECT` 문의 <select_list>. 여기에는 하위 쿼리의 `SELECT` 목록과 `INSERT` 문 내의 `SELECT` 목록도 포함됩니다.
* `SELECT` 문에 나타나는 하위 쿼리 `IF` 문.
* 쿼리의 `TOP`, `TABLESAMPLE`, `HAVING`, `GROUP BY`, `ORDER BY`, `OUTPUT...INTO` 또는 `FOR XML` 절.
* `OPENROWSET`, `OPENQUERY`, `OPENDATASOURCE`, `OPENXML`또는 모든 `FULLTEXT` 연산자에 대한 직접 인수 또는 하위 식으로서의 인수.
* `LIKE` 절의 pattern 및 escape_character 인수.
* `CONVERT` 절의 style 인수.
* `IDENTITY` 절 내의 정수 상수
* ODBC 확장 구문을 사용하여 지정한 상수
* `+`, `-`, `*`, `/`, `%` 연산자의 인수인 상수 폴딩 가능 식. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 식이 강제 매개 변수화에 적합한지 결정할 때 다음 조건 중 하나가 True이면 상수 폴딩 가능 식으로 간주합니다.  
  * 식에 열, 변수 또는 하위 쿼리가 나타나지 않습니다.  
  * 식에 `CASE` 절이 포함됩니다.  
* 쿼리 힌트 절에 대한 인수. 여기에는 `FAST` 쿼리 힌트의 *number_of_rows* 인수, `MAXDOP` 쿼리 힌트의 *number_of_processors* 인수 및 `MAXRECURSION` 쿼리 힌트의 *number* 인수가 포함됩니다.

매개 변수화는 개별 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 수준에서 수행됩니다. 다시 말해 일괄 처리 내의 개별 문이 매개 변수화됩니다. 컴파일 후 매개 변수가 있는 쿼리는 쿼리가 원래 전송되었던 일괄 처리의 컨텍스트에서 실행됩니다. 쿼리의 실행 계획이 캐시된 경우에는 sys.syscacheobjects 동적 관리 뷰의 sql 열을 참조하여 쿼리가 매개 변수화되었는지 여부를 확인할 수 있습니다. 쿼리가 매개 변수화된 경우 \@1 tinyint와 같이 이 열에서 매개 변수의 이름 및 데이터 형식은 전송된 일괄 처리 텍스트 앞에 옵니다.

> [!NOTE]
> 매개 변수 이름은 임의로 지정하므로 사용자나 애플리케이션에서는 특정 명명 순서를 따를 필요가 없습니다. 또한 다음 요소는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 서비스 팩 업그레이드의 버전에 따라 달라질 수 있습니다. 매개 변수 이름, 매개 변수화되는 리터럴 선택 항목 및 매개 변수화된 텍스트의 공백이 여기에 포함됩니다.

#### <a name="data-types-of-parameters"></a>매개 변수의 데이터 형식
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 리터럴을 매개 변수화하면 매개 변수가 다음 데이터 형식으로 변환됩니다.

* 정수 리터럴은 그 크기가 int 데이터 형식에 적합하면 int로 매개 변수화됩니다. 비교 연산자와 관련된 조건자의 일부인 큰 정수 리터럴(<, \<=, =, !=, >, >=, , !\<, !>, <>, `ALL`, `ANY`, `SOME`, `BETWEEN` 및 `IN` 포함)은 numeric(38,0)으로 매개 변수화됩니다. 비교 연산자와 관련된 조건자의 일부가 아닌 큰 리터럴은 전체 자릿수가 리터럴의 크기를 지원할 만큼 크고 소수 자릿수가 0인 numeric으로 매개 변수화됩니다.
* 비교 연산자와 관련된 조건자의 일부인 고정 소수점 숫자 리터럴은 전체 자릿수가 38이고 소수 자릿수가 리터럴의 크기를 지원할 만큼 큰 numeric으로 매개 변수화됩니다. 비교 연산자와 관련된 조건자의 일부가 아닌 고정 소수점 숫자 리터럴은 전체 자릿수 및 소수 자릿수가 리터럴의 크기를 지원할 만큼 큰 numeric으로 매개 변수화됩니다.
* 부동 소수점 숫자 리터럴은 float(53)으로 매개 변수화됩니다.
* 비유니코드 문자열 리터럴은 리터럴의 크기가 8,000자 내일 때는 varchar(8000)로 매개 변수화되고 8,000자보다 클 때는 varchar(max)로 매개 변수화됩니다.
* 유니코드 문자열 리터럴은 리터럴의 크기가 유니코드 문자로 4,000자 내일 때는 nvarchar(4000)로 매개 변수화되고 4,000자보다 클 때는 nvarchar(max)로 매개 변수화됩니다.
* 이진 리터럴은 리터럴 크기가 8,000바이트 내일 때는 varbinary(8000)로 매개 변수화되고 8,000바이트보다 클 때는 varbinary(max)로 변환됩니다.
* 통화 유형 리터럴은 money로 매개 변수화됩니다.

#### <a name="ForcedParamGuide"></a> 강제 매개 변수화 사용 지침
`PARAMETERIZATION` 옵션을 FORCED로 설정할 때는 다음 사항을 고려해야 합니다.

* 강제 매개 변수화를 적용하면 쿼리 컴파일 시 쿼리의 리터럴 상수가 매개 변수로 변경됩니다. 따라서 쿼리 최적화 프로그램에서는 만족스럽지 못한 쿼리 계획을 선택할 수 있습니다. 특히 쿼리 최적화 프로그램에서는 인덱싱된 뷰 또는 계산 열의 인덱스에 쿼리를 대응시키지 못할 수 있습니다. 또한 분할된 테이블 및 분산형 분할 뷰에 대해 만족스럽지 못한 쿼리 계획을 선택할 수도 있습니다. 계산 열의 인덱스 및 인덱싱된 뷰를 많이 사용하는 환경에서는 강제 매개 변수화를 사용하면 안 됩니다. 일반적으로 `PARAMETERIZATION FORCED` 옵션은 숙련된 데이터베이스 관리자가 성능에 영향을 주지 않는다는 것을 확인한 후에만 사용해야 합니다.
* 둘 이상의 데이터베이스를 참조하는 분산 쿼리에 강제 매개 변수화를 사용하면 좋습니다. 단, 쿼리가 실행되는 데이터베이스의 컨텍스트에서 `PARAMETERIZATION` 옵션이 `FORCED` 로 설정되어 있어야 합니다.
* `PARAMETERIZATION` 옵션을 `FORCED` 로 설정하면 현재 컴파일되거나 다시 컴파일되거나 실행되고 있는 쿼리 계획을 제외한 모든 쿼리 계획이 데이터베이스의 계획 캐시에서 플러시됩니다. 설정을 변경할 때 컴파일 또는 실행 중이었던 쿼리 계획은 다음에 쿼리가 실행될 때 매개 변수화됩니다.
* `PARAMETERIZATION` 옵션을 설정하는 작업은 온라인으로 수행되므로 데이터베이스 수준의 배타적 잠금이 필요하지 않습니다.
* 현재 `PARAMETERIZATION` 옵션 설정은 데이터베이스를 다시 연결하거나 복원할 때도 그대로 유지됩니다.

단일 쿼리 또는 구문은 동일하고 매개 변수 값만 다른 기타 쿼리는 단순 매개 변수화되지 않도록 지정하여 강제 매개 변수화의 동작을 무시할 수 있습니다. 반대로 데이터베이스에서 강제 매개 변수화가 해제된 경우에도 구문이 동일한 쿼리에 한해 강제 매개 변수화가 수행되도록 지정할 수 있습니다. 이와 같은 작업을 수행할 때[계획 지침](../relational-databases/performance/plan-guides.md) 을 사용합니다.

> [!NOTE]
> `PARAMETERIZATION` 옵션이 `FORCED`로 설정되어 있으면 `PARAMETERIZATION` 옵션이 `SIMPLE`로 설정되어 있는 경우와 오류 메시지 보고가 다를 수 있습니다. 강제 매개 변수화에서는 여러 오류 메시지가 보고될 수 있지만 단순 매개 변수화에서는 더 적은 메시지가 보고되며, 오류가 발생한 줄 번호가 잘못 보고될 수 있습니다.

### <a name="preparing-sql-statements"></a>SQL 문 준비
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관계형 엔진에서는 실행하기 전에 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 준비할 수 있는 기능을 제공합니다. 애플리케이션에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 여러 번 실행해야 하는 경우에는 데이터베이스 API를 사용하여 다음을 수행할 수 있습니다. 

* 문을 한 번 준비합니다. 이렇게 하면 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이 실행 계획으로 컴파일됩니다.
* 문을 실행해야 할 때마다 미리 컴파일한 실행 계획을 실행합니다. 이렇게 하면 첫 번째 실행 이후 실행할 때마다 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 다시 컴파일할 필요가 없습니다.   
  문 준비 및 실행은 API 함수 및 메서드에 의해 제어됩니다. 이것은 [!INCLUDE[tsql](../includes/tsql-md.md)] 언어의 일부분이 아닙니다. [!INCLUDE[tsql](../includes/tsql-md.md)] 문 실행에 대한 준비/실행 모델은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 의해 지원됩니다. 준비 요청 시 공급자 또는 드라이버가 문 준비 요청과 함께 문을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 보냅니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 실행 계획을 컴파일하고 해당 계획에 대한 핸들을 공급자 또는 드라이버에 반환합니다. 실행 요청 시, 공급자 또는 드라이버는 핸들과 관련된 계획의 실행 요청을 서버에 보냅니다. 

준비된 문은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 임시 개체를 만드는 데 사용할 수 없습니다. 준비된 문은 임시 테이블과 같은 임시 개체를 만드는 시스템 저장 프로시저를 참조할 수 없습니다. 이러한 프로시저는 직접 실행해야 합니다.

준비/실행 모델을 과도하게 사용하면 성능이 저하될 수 있습니다. 문이 한 번만 실행되는 경우 직접 실행은 서버로의 네트워크 왕복을 1회만 필요로 합니다. 한 번만 실행되는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 준비하고 실행하면 네트워크 왕복이 추가로 필요합니다. 즉 명령문을 준비하는 데 한 번, 명령문을 실행하는 데 한 번이 필요합니다.

매개 변수 표식이 사용되는 경우 문을 준비하는 것이 좀 더 효과적입니다. 예를 들어 애플리케이션이 종종 `AdventureWorks` 샘플 데이터베이스의 제품 정보 검색 요청을 받는 경우를 생각해 봅시다. 애플리케이션에서는 두 가지 방법으로 이를 처리할 수 있습니다. 

첫째, 애플리케이션이 요청된 각 제품에 대해 별도의 쿼리를 실행할 수 있습니다.

```sql
SELECT * FROM AdventureWorks2014.Production.Product
WHERE ProductID = 63;
```

둘째, 애플리케이션에서 다음을 수행합니다. 

1. 매개 변수 표식(?)을 포함하는 문을 준비합니다.  
   ```sql
   SELECT * FROM AdventureWorks2014.Production.Product  
   WHERE ProductID = ?;
   ```
2. 프로그램 변수를 매개 변수 표식에 바인딩합니다.
3. 제품 정보가 필요할 때마다 키 값으로 바인딩된 변수를 채우고 문을 실행합니다.

두 번째 방법은 문이 네 번 이상 실행될 때 좀 더 효율적입니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 준비/실행 모델이 직접 실행에 비해 성능상의 큰 이점이 없는데 이는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 실행 계획을 재사용하기 때문입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에는 현재 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 동일한 [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 사전 실행을 위해 생성된 실행 계획과 일치시키기 위한 효율적인 알고리즘이 있습니다. 애플리케이션이 매개 변수 표식을 사용하여 여러 번 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 해당 계획이 계획 캐시에서 에이징되지 않는 이상 두 번째 실행부터는 첫 번째 실행의 실행 계획을 재사용합니다. 준비/실행 모델은 여전히 다음과 같은 이점을 제공합니다. 

* 식별 핸들로 실행 계획을 찾는 것이 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 기존 실행 계획과 비교하는 데 사용되는 알고리즘보다 더 효율적입니다.
* 애플리케이션이 실행 계획이 만들어지고 재사용되는 시기를 제어할 수 있습니다.
* 준비/실행 모델은 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 비롯한 다른 데이터베이스로 이식 가능합니다.

### <a name="ParamSniffing"></a> 매개 변수 검색
“매개 변수 검사”는 컴파일 또는 재컴파일을 수행하는 동안 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 현재 매개 변수 값을 “검사”하고 쿼리 최적화 프로그램에 전달하여 해당 값이 더욱 효율적인 쿼리 실행 계획을 생성하는 데 사용될 수 있도록 하는 프로세스를 나타냅니다.

컴파일 또는 재컴파일을 수행하는 동안 다음 유형의 일괄 처리에 대해 매개 변수 값을 검사합니다.

-  저장 프로시저
-  sp_executesql을 통해 제출된 쿼리 
-  준비된 쿼리

잘못된 매개 변수 스니핑 문제 해결에 대한 자세한 내용은 [매개 변수가 중요한 쿼리 실행 계획 문제로 쿼리 문제 해결](https://docs.microsoft.com/azure/sql-database/sql-database-monitor-tune-overview#troubleshoot-performance-problems)을 참조하세요.

> [!NOTE]
> `RECOMPILE` 힌트를 사용하는 쿼리는 매개 변수 값과 지역 변수의 현재 값을 모두 검사합니다. 검사되는 매개 변수 및 지역 변수 값은 `RECOMPILE` 힌트가 포함된 문 바로 앞에 있는 일괄 처리 위치의 값입니다. 특히 매개 변수의 경우 일괄 처리 호출과 함께 사용된 값은 검사하지 않습니다.

## <a name="parallel-query-processing"></a>병렬 쿼리 처리
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 마이크로프로세서(CPU)를 두 개 이상 사용하는 컴퓨터에서 쿼리 실행과 인덱스 작업을 최적화하는 병렬 쿼리 기능을 제공합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 여러 개의 운영 체제 작업자 스레드로 쿼리나 인덱스 작업을 병렬 수행할 수 있으므로 작업을 빠르고 효율적으로 완료할 수 있습니다.

쿼리를 최적화하는 동안 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 병렬 실행에 적합한 쿼리나 인덱스 작업을 찾습니다. 이러한 쿼리에 대해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 쿼리 실행 계획에 교환 연산자를 삽입하여 병렬 실행할 쿼리를 준비합니다. 교환 연산자는 프로세스 관리, 데이터 재배포 및 흐름 제어를 제공하는 쿼리 실행 계획의 연산자입니다. 교환 연산자에는 하위 유형으로 `Distribute Streams`, `Repartition Streams`및 `Gather Streams` 논리 연산자가 포함되며 이 중에서 하나 이상이 병렬 쿼리에 대한 쿼리 계획의 실행 계획 출력에 표시될 수 있습니다. 

> [!IMPORTANT]
> 특정 구문은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 실행 계획의 전체 또는 일부에서 병렬 처리를 활용할 수 있는 기능을 방해합니다.

병렬 처리를 방해하는 구문은 다음과 같습니다.
-   **스칼라 UDF**        
    스칼라 사용자 정의 함수에 대한 자세한 내용은 [사용자 정의 함수 만들기](../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar)를 참조하세요. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]부터 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 이러한 함수를 인라인 처리하고, 쿼리를 처리하는 도중 병렬 처리 사용을 잠금 해제할 수 있습니다. 스칼라 UDF 인라인 처리에 대한 자세한 내용은 [SQL 데이터베이스의 인텔리전트 쿼리 처리](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining)를 참조하세요.
    
-   **원격 쿼리**        
    원격 쿼리에 대한 자세한 내용은 [실행 계획 논리 및 물리 연산자 참조](../relational-databases/showplan-logical-and-physical-operators-reference.md)를 참조하세요.
    
-   **동적 커서**        
    커서에 대한 자세한 내용은 [DECLARE CURSOR](../t-sql/language-elements/declare-cursor-transact-sql.md)를 참조하세요.
    
-   **재귀 쿼리**        
    재귀에 대한 자세한 내용은 [재귀 공통 테이블 식 정의 및 사용 지침](../t-sql/queries/with-common-table-expression-transact-sql.md#guidelines-for-defining-and-using-recursive-common-table-expressions) 및 [T-SQL의 재귀](https://msdn.microsoft.com/library/aa175801(v=sql.80).aspx)를 참조하세요.

-   **TVF(테이블 반환된 함수)**         
    TVF에 대한 자세한 내용은 [사용자 정의 함수 만들기(데이터베이스 엔진)](../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)를 참조하세요.
    
-   **TOP 키워드**        
    자세한 내용은 [TOP(Transact-SQL)](../t-sql/queries/top-transact-sql.md)을 참조하세요.

교환 연산자를 삽입하면 병렬 쿼리 실행 계획이 완성됩니다. 병렬 쿼리 실행 계획은 작업자 스레드를 여러 개 사용할 수 있습니다. 병렬이 아닌(직렬) 쿼리에서 사용하는 직렬 실행 계획은 해당 실행에 작업자 스레드 한 개만 사용합니다. 병렬 쿼리에서 사용하는 실제 작업자 스레드 수는 쿼리 계획 실행 초기화 시 결정되며 계획의 복잡성과 병렬 처리 수준에 따라 다릅니다. 

DOP(병렬 처리 수준)에 따라 사용되는 최대 CPU 수가 결정됩니다. 사용되는 작업자 스레드 수를 의미하지는 않습니다. DOP 제한은 [작업](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)별로 설정됩니다. [요청](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)별 또는 쿼리 제한별로 수행되지 않습니다. 즉, 병렬 쿼리 실행 중에 단일 요청은 [스케줄러](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)에 할당되는 여러 작업을 생성할 수 있습니다. 여러 작업을 동시에 실행하는 경우, 특정 쿼리 실행 지점에서 MAXDOP로 지정된 개수보다 많은 프로세서가 동시에 사용될 수 있습니다. 자세한 내용은 [스레드 및 태스크 아키텍처 가이드](../relational-databases/thread-and-task-architecture-guide.md)를 참조하세요.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 다음 중 해당하는 조건이 있을 경우 병렬 실행 계획을 사용하지 않습니다.

* 쿼리의 직렬 실행 비용이 크지 않아 병렬 실행 계획을 대안으로 고려할 필요가 없습니다. 
* 직렬 실행 계획이 특정 쿼리에 사용 가능한 병렬 실행 계획보다 더 빠릅니다.
* 쿼리에 병렬로 실행할 수 없는 스칼라 또는 관계형 연산자가 포함되어 있습니다. 특정 연산자는 쿼리 계획의 한 섹션이 직렬 모드로 실행되도록 하거나 전체 계획이 직렬 모드로 실행되도록 할 수 있습니다.

### <a name="DOP"></a> 병렬 처리 수준
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 병렬 쿼리 실행 또는 인덱스 DDL(데이터 정의 언어) 작업 각각의 인스턴스에 대해 가장 적합한 병렬 처리 수준이 자동으로 검색됩니다. 이것은 다음과 조건을 기준으로 수행됩니다. 

1. SMP(대칭적 다중 처리) 컴퓨터와 같이 **둘 이상의 마이크로프로세서 또는 CPU가 있는 컴퓨터**에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 실행 중인지 여부. 두 개 이상의 CPU가 있는 컴퓨터에서만 병렬 쿼리를 사용할 수 있습니다. 

2. **사용할 수 있는 작업자 스레드 수가 충분**한지 여부. 각 쿼리 또는 인덱스 작업을 실행하려면 일정 수의 작업자 스레드가 필요합니다. 병렬 계획을 실행하려면 직렬 계획보다 많은 작업자 스레드가 필요하고, 필요한 작업자 스레드의 수는 병렬 처리 수준에 따라 증가합니다. 특정 병렬 처리 수준에 대한 병렬 계획의 작업자 스레드 요구 사항이 충족되지 않는 경우에는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 병렬 처리 수준을 자동으로 낮추거나 지정된 작업 컨텍스트의 병렬 계획을 완전히 중단합니다. 그런 다음 하나의 작업자 스레드만 사용되는 직렬 계획을 실행합니다. 

3. **실행한 쿼리 또는 인덱스 작업의 유형**. 병렬 계획은 인덱스를 새로 작성 또는 다시 작성하거나 클러스터형 인덱스 및 CPU 주기 사용량이 큰 쿼리를 삭제하는 등의 인덱스 작업에 적합합니다. 예를 들어 대형 테이블의 조인, 대규모 집계 및 대형 결과 집합의 정렬이 병렬 쿼리에 적절합니다. 주로 트랜잭션 처리 애플리케이션에서 사용되는 단순 쿼리의 경우 이 쿼리를 병렬로 실행하는 데 필요한 추가 조정 작업은 성능을 향상시키기보다는 부담이 됩니다. 병렬 처리로 유용한 쿼리와 그렇지 않은 쿼리를 구분하기 위해, [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 쿼리 또는 인덱스 작업 실행 시 예상 비용을 [병렬 처리에 대한 비용 임계값](../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md) 값과 비교합니다. 적절한 테스트를 통해 다른 값이 워크로드 실행에 더 적합하다고 확인되는 경우 사용자들은 [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하여 기본값 5를 변경할 수 있습니다. 

4. **처리할 행 수가 충분**한지 여부. 쿼리 최적화 프로그램에서 행 수가 부족하다고 판단하는 경우 행을 배포하기 위해 교환 연산자를 사용하지 않습니다. 결과적으로 연산자는 직렬로 실행됩니다. 시작, 배포 및 조정 비용이 병렬 연산자 실행으로 얻은 이익보다 큰 경우 연산자를 직렬 계획으로 실행하면 이 시나리오를 피할 수 있습니다.

5. **최신 배포 통계를 사용**할 수 있는지 여부. 가장 높은 병렬 처리 수준을 제공할 수 없는 경우 병렬 처리를 중단하기 전에 더 낮은 병렬 처리 수준이 가능한지 확인합니다. 예를 들어 뷰에서 클러스터형 인덱스를 만드는 경우 클러스터형 인덱스가 아직 생성되지 않았으므로 배포 통계를 계산할 수 없습니다. 이 경우 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 이 인덱스 작업에는 가장 높은 병렬 처리 수준을 할당하지 않습니다. 그러나 이 경우에도 정렬 또는 검색과 같은 일부 연산자에는 병렬 처리의 이점이 적용될 수 있습니다.

> [!NOTE]
> 병렬 인덱스 작업은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise, Developer 및 Evaluation Edition에서만 사용할 수 있습니다.
 
[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 실행 시 앞서 설명한 현재 시스템 작업과 구성 정보에서 병렬 실행이 가능한지 확인합니다. 병렬 실행이 보장되는 경우 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 최적의 작업자 스레드 수를 결정하고 이 작업자 스레드에 병렬 계획을 분산하여 실행합니다. 병렬 실행을 위해 쿼리 또는 인덱스 작업이 여러 작업자 스레드에서 실행되기 시작하면 해당 작업이 완료될 때까지 동일한 수의 작업자 스레드가 사용됩니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 계획 캐시에서 실행 계획을 가져올 때마다 최적의 작업자 스레드 수를 다시 검사합니다. 예를 들어 쿼리를 한 번 실행할 때는 직렬 계획을 사용할 수 있고 동일한 쿼리를 두 번째 실행할 때는 세 개의 작업자 스레드를 사용하는 병렬 계획을 사용할 수 있으며 이 쿼리를 세 번째로 실행할 때는 네 개의 작업자 스레드를 사용하는 병렬 계획을 사용할 수 있습니다.

병렬 쿼리 실행 계획에서 삽입, 업데이트 및 삭제 작업은 직렬로 실행됩니다. 그러나 UPDATE 또는 DELETE 문의 WHERE 절이나 INSERT 문의 SELECT 부분은 병렬로 실행될 수 있습니다. 그런 다음 실제 데이터 변경 내용은 데이터베이스에 직렬로 적용됩니다.

정적 커서 및 키 집합 커서는 병렬 실행 계획에 따라 채워질 수 있습니다. 그러나 동적 커서의 동작은 직렬 실행에 의해서만 제공될 수 있습니다. 쿼리 최적화 프로그램은 동적 커서에 포함된 쿼리에 대해서는 항상 직렬 실행 계획을 생성합니다.

#### <a name="overriding-degrees-of-parallelism"></a>병렬 처리 수준 재정의
병렬 처리 수준은 병렬 계획 실행에 사용할 프로세서 수를 설정합니다. 이 구성은 다음과 같은 여러 수준에서 설정할 수 있습니다.

1.  서버 수준, **최대 병렬 처리 수준(MAXDOP)** [서버 구성 옵션](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 사용</br> **적용 대상:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

    > [!NOTE]
    > [!INCLUDE [sssqlv15-md](../includes/sssqlv15-md.md)]에서는 설치하는 동안 MAXDOP 서버 구성 옵션을 설정하기 위한 자동 권장 사항이 도입되었습니다. 설정 사용자 인터페이스를 사용하여 권장 설정을 적용하거나 사용자 고유 값을 입력할 수 있습니다. 자세한 내용은 [데이터베이스 엔진 구성 - MaxDOP 페이지](../sql-server/install/instance-configuration.md#maxdop)를 참조하세요.

2.  워크로드 수준, **MAX_DOP** [Resource Governor 작업 그룹 구성 옵션](../t-sql/statements/create-workload-group-transact-sql.md) 사용</br> **적용 대상:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

3.  데이터베이스 수준, **MAXDOP** [데이터베이스 범위 구성](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 사용</br> **적용 대상:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 

4.  쿼리 또는 인덱스 문 수준, **MAXDOP** [쿼리 힌트](../t-sql/queries/hints-transact-sql-query.md) 또는 **MAXDOP** 인덱스 옵션 사용. 예를 들어 MAXDOP 옵션을 사용하여 온라인 인덱스 작업 전용으로 사용되는 프로세서의 수를 늘리거나 줄일 수 있습니다. 이런 방법으로 인덱스 작업에 사용되는 리소스와 동시 사용자의 리소스 간에 균형을 유지할 수 있습니다.</br> **적용 대상:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 

최대 병렬 처리 수준 옵션을 0(기본값)으로 설정하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용 가능한 모든 프로세서(최대 64개)를 병렬 계획 실행에 사용할 수 있습니다. MAXDOP 옵션을 0으로 설정하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 64개 논리적 프로세서의 런타임 대상을 설정해도 필요한 경우 다른 값을 수동으로 설정할 수 있습니다. 쿼리와 인덱스에 대해 MAXDOP를 0으로 설정하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용 가능한 모든 프로세서(최대 64개)를 병렬 계획 실행의 지정된 쿼리 또는 인덱스에 대해 사용할 수 있습니다. MAXDOP는 일부 병렬 쿼리에만 적용되는 값이나 병렬 처리에 적합한 모든 쿼리의 미정 대상입니다. 즉, 런타임에 사용할 수 있는 작업자 스레드가 충분하지 않은 경우 MAXDOP 서버 구성 옵션보다 낮은 병렬 처리 수준으로 쿼리를 실행할 수 있습니다.

> [!TIP]
> MAXDOP 구성에 대한 지침은 [설명서 페이지](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)를 참조하세요.

### <a name="parallel-query-example"></a>병렬 쿼리 예제
다음 쿼리에서는 2000년 4월 1일에 시작하는 특정 분기 동안의 주문 수를 계산합니다. 이 기간 동안에는 최소한 한 개의 주문 상품이 약속한 날짜보다 늦게 고객에게 배달되었습니다. 이 쿼리는 각 주문 우선 순위에 따라 그룹화되고 우선 순위를 오름차순으로 정렬하여 각 주문의 수를 표시합니다. 

다음 예에서는 가상의 테이블 및 열 이름을 사용합니다.

```sql
SELECT o_orderpriority, COUNT(*) AS Order_Count
FROM orders
WHERE o_orderdate >= '2000/04/01'
   AND o_orderdate < DATEADD (mm, 3, '2000/04/01')
   AND EXISTS
         (
          SELECT *
            FROM    lineitem
            WHERE l_orderkey = o_orderkey
               AND l_commitdate < l_receiptdate
         )
   GROUP BY o_orderpriority
   ORDER BY o_orderpriority
```

다음 인덱스가 `lineitem` 및 `orders` 테이블에서 정의된다고 가정합니다.

```sql
CREATE INDEX l_order_dates_idx 
   ON lineitem
      (l_orderkey, l_receiptdate, l_commitdate, l_shipdate)

CREATE UNIQUE INDEX o_datkeyopr_idx
   ON ORDERS
      (o_orderdate, o_orderkey, o_custkey, o_orderpriority)
```

다음은 위에 표시된 쿼리에 대해 생성될 수 있는 병렬 계획 중 하나입니다.

```
|--Stream Aggregate(GROUP BY:([ORDERS].[o_orderpriority])
                  DEFINE:([Expr1005]=COUNT(*)))
    |--Parallelism(Gather Streams, ORDER BY:
                  ([ORDERS].[o_orderpriority] ASC))
         |--Stream Aggregate(GROUP BY:
                  ([ORDERS].[o_orderpriority])
                  DEFINE:([Expr1005]=Count(*)))
              |--Sort(ORDER BY:([ORDERS].[o_orderpriority] ASC))
                   |--Merge Join(Left Semi Join, MERGE:
                  ([ORDERS].[o_orderkey])=
                        ([LINEITEM].[l_orderkey]),
                  RESIDUAL:([ORDERS].[o_orderkey]=
                        [LINEITEM].[l_orderkey]))
                        |--Sort(ORDER BY:([ORDERS].[o_orderkey] ASC))
                        |    |--Parallelism(Repartition Streams,
                           PARTITION COLUMNS:
                           ([ORDERS].[o_orderkey]))
                        |         |--Index Seek(OBJECT:
                     ([tpcd1G].[dbo].[ORDERS].[O_DATKEYOPR_IDX]),
                     SEEK:([ORDERS].[o_orderdate] >=
                           Apr  1 2000 12:00AM AND
                           [ORDERS].[o_orderdate] <
                           Jul  1 2000 12:00AM) ORDERED)
                        |--Parallelism(Repartition Streams,
                     PARTITION COLUMNS:
                     ([LINEITEM].[l_orderkey]),
                     ORDER BY:([LINEITEM].[l_orderkey] ASC))
                             |--Filter(WHERE:
                           ([LINEITEM].[l_commitdate]<
                           [LINEITEM].[l_receiptdate]))
                                  |--Index Scan(OBJECT:
         ([tpcd1G].[dbo].[LINEITEM].[L_ORDER_DATES_IDX]), ORDERED)
```

아래 그림은 병렬 처리 수준이 4로 실행되고 두 개의 테이블 조인을 포함하는 쿼리 최적화 프로그램 계획을 보여 줍니다.

![parallel_plan](../relational-databases/media/parallel-plan.gif)

이 병렬 계획에는 세 개의 Parallelism 연산자가 포함됩니다. `o_datkey_ptr` 인덱스의 Index Seek 연산자와 `l_order_dates_idx` 인덱스의 Index Scan 연산자가 모두 병렬로 처리됩니다. 몇 개의 배타적 스트림이 생성됩니다. 이것은 각각 Index Scan 및 Index Seek 연산자 위의 가장 가까운 Parallelism 연산자에서 결정될 수 있습니다. 두 연산자는 모두 교환 유형을 다시 분할합니다. 즉, 입력 스트림 수와 동일한 수의 출력 스트림을 생성하는 스트림 사이에서 단지 데이터의 순서를 섞는 것입니다. 이 스트림 수는 병렬 처리 수준과 같습니다.

`l_order_dates_idx` Index Scan 연산자 위의 Parallelism 연산자는 `L_ORDERKEY` 값을 키로 사용하여 입력 스트림을 다시 분할합니다. 이러한 방식으로 동일한 `L_ORDERKEY` 값은 동일한 출력 스트림을 생성합니다. 동시에 출력 스트림은 `L_ORDERKEY` 열에서 그 순서를 유지하여 Merge Join 연산자의 입력 요구 사항을 충족시킵니다.

Index Seek 연산자 위의 Parallelism 연산자는 `O_ORDERKEY` 값을 사용하여 입력 스트림을 다시 분할합니다. 이 입력은 `O_ORDERKEY` 열 값을 기준으로 정렬되지 않았으며 `Merge Join` 연산자를 통한 조인 열이므로 Parallelism 연산자와 Merge Join 연산자 사이에 있는 Sort 연산자가 `Merge Join` 연산자에 대한 입력을 조인 열을 기준으로 정렬합니다. `Sort` 연산자는 Merge Join 연산자처럼 병렬로 처리됩니다.

최상위 Parallelism 연산자는 여러 스트림의 결과를 단일 스트림으로 수집합니다. 그런 다음 Parallelism 연산자 아래의 Stream Aggregate 연산자에서 수행하는 부분 집계는 Parallelism 연산자 위의 Stream Aggregate 연산자의 서로 다른 각각의 `O_ORDERPRIORITY` 값에 대해 단일 `SUM` 값으로 누적됩니다. 이 계획에는 병렬 처리 수준이 4인 두 개의 교환 세그먼트가 있으므로 8개의 작업자 스레드가 사용됩니다.

이 예에 사용된 연산자에 대한 자세한 내용은 [실행 계획 논리 및 물리 연산자 참조](../relational-databases/showplan-logical-and-physical-operators-reference.md)를 참조하세요.

### <a name="parallel-index-operations"></a>병렬 인덱스 작업

인덱스를 만들거나 다시 작성하는 인덱스 작업 또는 클러스터형 인덱스를 삭제하는 인덱스 작업을 위해 작성된 쿼리 계획에서는 여러 마이크로프로세서가 있는 컴퓨터에서 병렬 다중 작업자 스레드 작업을 할 수 있습니다.

> [!NOTE]
> 병렬 인덱스 작업은 [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)]부터 Enterprise Edition에서만 사용할 수 있습니다.
 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 다른 쿼리에 사용하는 것과 동일한 알고리즘을 사용하여 인덱스 작업에 대한 병렬 처리 수준(실행할 총 개별 작업자 스레드 수)을 결정합니다. 인덱스 작업에 대한 최대 병렬 처리 수준은 [max degree of parallelism](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 서버 구성 옵션을 따릅니다. CREATE INDEX, ALTER INDEX, DROP INDEX 및 ALTER TABLE 문에서 MAXDOP 인덱스 옵션을 설정하여 개별 인덱스 작업에 대한 max degree of parallelism 값을 재정의할 수 있습니다.

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 인덱스 실행 계획을 작성하는 경우 병렬 작업의 수는 다음 중에서 가장 낮은 값으로 설정됩니다. 

* 컴퓨터의 마이크로프로세서의 수 또는 CPU의 수
* max degree of parallelism 서버 구성 옵션에 지정된 수
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 작업자 스레드에 대해 수행된 작업의 임계값을 아직 넘지 않은 CPU의 수

예를 들어 8개의 CPU가 있으나 최대 병렬 처리 수준이 6으로 설정된 컴퓨터의 경우 인덱스 작업에 대해 생성될 수 있는 최대 병렬 작업자 스레드 수는 6개입니다. 인덱스 실행 계획을 작성할 때 컴퓨터에 있는 5개의 CPU가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 작업의 임계값을 초과하는 경우 실행 계획은 3개의 병렬 작업자 스레드만 지정합니다.

병렬 인덱스 작업의 주요 단계는 다음과 같습니다. 

* 조정 작업자 스레드는 신속하게 무작위로 테이블을 검색하여 인덱스 키의 분포를 예상합니다. 조정 작업자 스레드는 병렬 작업 수준에 해당하는 여러 키 범위를 만드는 키 경계를 설정합니다. 여기서 각 키 범위는 비슷한 개수의 행을 포함할 수 있도록 결정됩니다. 예를 들어 테이블에 4백만 개의 행이 있고 병렬 처리 수준이 4인 경우 조정 작업자 스레드는 각 집합에서 백만 개의 행을 갖는 4개의 행 집합을 구분하는 키 값을 결정합니다. 모든 CPU를 사용하도록 충분한 키 범위를 설정할 수 없는 경우 병렬 처리 수준도 이에 따라 줄어듭니다.  
* 조정 작업자 스레드는 병렬 작업 수준에 해당하는 여러 작업자 스레드를 디스패치하고 이러한 작업자 스레드가 작업을 완료할 때까지 대기합니다. 각 작업자 스레드는 해당 작업자 스레드에 할당된 범위 내의 키 값을 갖는 행만 검색하는 필터를 사용하여 기본 테이블을 검색합니다. 각 작업자 스레드는 키 범위에서 행의 인덱스 구조를 작성합니다. 분할된 인덱스의 경우 각 작업자 스레드는 지정한 수만큼의 파티션을 작성합니다. 파티션은 작업자 스레드 간에 공유되지 않습니다.  
* 모든 병렬 작업자 스레드가 완료된 후 조정 작업자 스레드는 인덱스 하위 단위를 단일 인덱스에 연결합니다. 이 단계는 오프라인 인덱스 작업에만 적용됩니다.

개별 `CREATE TABLE` 또는 `ALTER TABLE` 문에는 인덱스를 생성해야 하는 여러 제약 조건이 있을 수 있습니다. 각 개별 인덱스 만들기 작업은 여러 CPU가 있는 컴퓨터에서 병렬로 수행될 수 있지만 이러한 여러 인덱스 만들기 작업은 연속해서 수행됩니다.

## <a name="distributed-query-architecture"></a>분산 쿼리 아키텍처
Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 다른 유형의 OLE DB 데이터 원본을 참조하는 두 가지 메서드를 지원합니다.

* 연결된 서버 이름  
  시스템 저장 프로시저 `sp_addlinkedserver` 와 `sp_addlinkedsrvlogin` 은 OLE DB 데이터 원본에 서버 이름을 제공하는 데 사용됩니다. [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서는 4부분으로 된 이름을 사용하여 이러한 연결 서버의 개체를 참조할 수 있습니다. 예를 들어 연결된 서버 이름 `DeptSQLSrvr`이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 다른 인스턴스에 대해 정의되는 경우 다음 문은 해당 서버의 테이블을 참조합니다. 
  
  ```sql
  SELECT JobTitle, HireDate 
  FROM DeptSQLSrvr.AdventureWorks2014.HumanResources.Employee;
  ```

   또한 연결된 서버 이름은 OLE DB 데이터 원본에서 행 집합을 열도록 `OPENQUERY` 문에 지정될 수 있습니다. 그런 다음 이 행 집합은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 테이블처럼 참조될 수 있습니다. 

* 임의 커넥터 이름  
  데이터 원본이 자주 참조되지 않는 경우 연결된 서버에 연결하는 데 필요한 정보로 `OPENROWSET` 또는 `OPENDATASOURCE` 함수가 지정됩니다. 그런 다음 행 집합은 테이블이 [!INCLUDE[tsql](../includes/tsql-md.md)] 문에서 참조되는 방법과 동일하게 참조될 수 있습니다. 
  
  ```sql
  SELECT *
  FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',
        'c:\MSOffice\Access\Samples\Northwind.mdb';'Admin';'';
        Employees);
  ```

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 OLE DB를 사용하여 관계형 엔진과 스토리지 엔진 간에 통신합니다. 관계형 엔진은 각 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 기본 테이블의 스토리지 엔진에서 연 단순 OLE DB 행 집합에 대한 일련의 작업으로 분류합니다. 이것은 관계형 엔진도 OLE DB 데이터 원본의 단순 OLE DB 행 집합을 열 수 있음을 의미합니다.  
![oledb_storage](../relational-databases/media/oledb-storage.gif)  
관계형 엔진은 OLE DB API(애플리케이션 프로그래밍 인터페이스)를 사용하여 연결된 서버에서 행 집합을 열고, 그 행을 인출하고, 트랜잭션을 관리합니다.

연결된 서버로 액세스되는 각 OLE DB 데이터 원본에 대해 OLE DB 공급자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 실행 중인 서버에 있어야 합니다. 특정 OLE DB 데이터 원본에 대해 사용할 수 있는 [!INCLUDE[tsql](../includes/tsql-md.md)] 연산 집합은 OLE DB 공급자의 기능에 따라 다릅니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 인스턴스마다 `sysadmin` 고정 서버 역할의 멤버는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] `DisallowAdhocAccess` 속성을 사용하여 OLE DB 공급자에 대한 임시 커넥터 이름의 사용을 설정 또는 해제할 수 있습니다. 임의 액세스가 활성화되어 있는 경우 해당 인스턴스에 로그온된 모든 사용자는 OLE DB 공급자를 사용하여 액세스할 수 있는 네트워크에서 데이터 원본을 참조하며 임의 커넥터 이름이 있는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행할 수 있습니다. 데이터 원본에 대한 액세스를 제어하기 위해 `sysadmin` 역할의 멤버는 해당 OLE DB 공급자에 대한 임의 액세스를 비활성화하고 그에 따라 사용자를 관리자가 정의한 연결된 서버 이름에서 참조한 데이터 원본으로만 제한합니다. 기본적으로 임의 액세스는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] OLE DB 공급자에 대해 활성화되어 있고 기타 모든 OLE DB 공급자에 대해서는 비활성화되어 있습니다.

분산 쿼리를 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스가 실행 중인 Microsoft Windows 계정의 보안 컨텍스트에서 다른 데이터 원본(예: 파일, Active Directory 같은 비관계형 데이터 원본 등)에 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 Windows 로그인에서는 적절하게 로그인을 가장하지만 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인에서는 그렇지 못합니다. 이렇게 하면 사용 권한이 없는 다른 데이터 원본에 대한 액세스를 분산 쿼리 사용자에게 허용할 수 있지만 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스가 실행 중인 계정에는 사용 권한이 없습니다. `sp_addlinkedsrvlogin` 을 사용하여 연결된 해당 서버에 액세스할 권한이 부여된 특정 로그인을 정의할 수 있습니다. 이 제어는 임의 이름에 대해 사용할 수 없으므로 임의 액세스에 대해 OLE DB 공급자를 활성화할 경우 조심해야 합니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 가능하면 조인, 제한, 투영, 정렬, 그룹화 같은 관계형 연산을 연산별로 OLE DB 데이터 원본에 푸시합니다. 기본적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 기본 테이블을 검색하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 전송한 후 자체적으로 관계형 연산을 수행하지는 않습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 OLE DB 공급자에게 공급자에서 지원하는 SQL 문법 수준을 확인하도록 쿼리하고 이 정보에 따라 가능한 한 많은 관계형 연산을 공급자에게 푸시합니다. 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 OLE DB 공급자가 OLE DB 데이터 원본에서 키 값이 배포되는 방식을 나타내는 통계를 반환하기 위한 메커니즘을 지정합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 각 [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 요구 사항에 대해 데이터 원본의 데이터의 패턴을 좀 더 잘 분석하므로 최적의 실행 계획을 생성하는 쿼리 최적화 프로그램의 기능을 향상시킬 수 있습니다. 

## <a name="query-processing-enhancements-on-partitioned-tables-and-indexes"></a>분할된 테이블 및 인덱스에서의 향상된 쿼리 처리

[!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)]에서는 여러 병렬 계획에 대해 분할된 테이블에서의 쿼리 처리 성능이 향상되었고, 병렬 및 직렬 계획이 표시되는 방식이 변경되었으며 컴파일 시간 및 런타임 실행 계획에 제공되는 분할 정보가 개선되었습니다. 이 항목에서는 이러한 향상된 기능에 대해 설명하고, 분할된 테이블 및 인덱스의 쿼리 실행 계획을 해석하는 방법에 대해 안내하며, 분할된 개체에서의 쿼리 성능 향상을 위한 최선의 방법을 알려 줍니다. 

> [!NOTE]
> 분할된 테이블 및 인덱스는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise, Developer 및 Evaluation Edition에서만 지원됩니다.

### <a name="new-partition-aware-seek-operation"></a>새 파티션 인식 Seek 연산

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 분할된 테이블을 나타내는 내부 표현이 변경되어 이제 테이블이 선행 열처럼 `PartitionID`가 있는 다중 열 인덱스로 쿼리 프로세서에 나타납니다. `PartitionID` 는 특정 행을 포함하는 파티션의 `ID` 를 나타내기 위해 내부에서 사용하는 숨겨진 계산 열입니다. 예를 들어 `T(a, b, c)`로 정의되는 테이블은 a 열에서 분할되고 b 열에 클러스터형 인덱스가 있다고 가정합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 이렇게 분할된 테이블은 내부적으로 `T(PartitionID, a, b, c)` 스키마와 복합 키 `(PartitionID, b)`에 클러스터형 인덱스가 있는 분할되지 않은 테이블로 취급됩니다. 이로 인해 쿼리 최적화 프로그램은 분할된 테이블 또는 인덱스에서 `PartitionID`를 기준으로 seek 연산을 수행할 수 있습니다. 

이제 파티션 제거는 이 seek 연산에서 수행됩니다.

In addition, the Query Optimizer is extended so that a seek or scan operation with one condition can be done on `PartitionID` (논리적 선행 열)과 가능한 다른 인덱스 키 열에서 수행된 후, 두 번째 수준의 seek 연산은 다른 조건을 사용하여 첫 번째 수준의 seek 연산에 대한 제한을 충족시키는 각각의 고유 값에 대해 수행될 수 있습니다. 즉 skip scan이라고 하는 이 연산을 통해 쿼리 최적화 프로그램은 seek 또는 scan 연산을 하나의 조건을 기준으로 수행하여 액세스할 파티션을 결정하고 해당 연산자에서 두 번째 수준 index seek 연산을 수행하여 다른 조건을 충족시키는 이러한 파티션에서 행을 반환할 수 있습니다. 예를 들어 다음 쿼리를 살펴보십시오.

```sql
SELECT * FROM T WHERE a < 10 and b = 2;
```

이 예에서 `T(a, b, c)`로 정의되는 T 테이블은 a 열에서 분할되고 b 열에 클러스터형 인덱스가 있다고 가정합니다. T 테이블의 파티션 경계는 다음 파티션 함수로 정의됩니다.

```sql
CREATE PARTITION FUNCTION myRangePF1 (int) AS RANGE LEFT FOR VALUES (3, 7, 10);
```

쿼리를 해결하려면 쿼리 프로세서는 첫 번째 수준 seek 연산을 수행하여 `T.a < 10`조건을 충족시키는 행을 포함하는 모든 파티션을 찾습니다. 이 작업을 통해 액세스할 파티션을 식별합니다. 식별된 각 파티션에서 쿼리 프로세서는 열에서 클러스터형 인덱스로 두 번째 수준 seek 연산을 수행하여 `T.b = 2` 및 `T.a < 10`조건을 충족시키는 행을 찾습니다. 

다음 그림은 skip scan 연산을 논리적으로 표현한 것으로 `T` 및 `a` 열의 데이터와 함께 `b` 테이블을 보여 줍니다. 파티션은 세로줄 파선으로 표시되는 파티션 경계와 함께 1에서 4까지 번호가 매겨져 있습니다. 파티션에 대한 첫 번째 수준 seek 연산(그림에는 표시되지 않음)에서는 파티션 1, 2 및 3이 `a` 열에 테이블 및 조건자에 대해 정의된 분할로 포함된 검색 조건을 충족시키는지 확인했습니다. 즉 `T.a < 10`입니다. skip scan 연산의 두 번째 수준 seek 부분에 의해 이동된 경로는 곡선으로 표시됩니다. 기본적으로 skip scan 연산은 `b = 2`조건을 충족시키는 행을 이러한 파티션마다 검색합니다. skip scan 연산의 총 비용은 세 가지 개별 index seek 연산의 총 비용과 같습니다.   

![skip_scan](../relational-databases/media/skip-scan.gif)

### <a name="displaying-partitioning-information-in-query-execution-plans"></a>쿼리 실행 계획의 분할 정보 표시

분할 테이블과 인덱스에서의 쿼리 실행 계획은 [!INCLUDE[tsql](../includes/tsql-md.md)] `SET` 문 `SET SHOWPLAN_XML` 또는 `SET STATISTICS XML`을 사용하거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio의 그래픽 실행 플랜 출력을 사용하여 검사할 수 있습니다. 예를 들어 쿼리 편집기 도구 모음에서 *예상 실행 계획 표시* 를 클릭하여 컴파일 시간 실행 계획을 표시할 수 있고 *실제 실행 계획 포함*을 클릭하여 런타임 계획을 표시할 수 있습니다. 

이러한 도구를 사용하여 다음 정보를 확인할 수 있습니다.

* `scans`, `seeks`, `inserts`, `updates`, `merges`, `deletes` 같은 작업에서 분할된 테이블이나 인덱스에 액세스함.
* 쿼리에 의해 액세스되는 파티션. 예를 들어 액세스한 총 파티션 수 및 액세스한 근접 파티션의 범위가 런타임 실행 계획에서 사용할 수 있습니다.
* 한 개 이상의 파티션에서 데이터를 검색하기 위해 skip scan 연산이 seek 또는 scan 연산에서 사용되는 경우

#### <a name="partition-information-enhancements"></a>향상된 파티션 정보 기능

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 컴파일 시간과 런타임 실행 계획 모두에 대한 향상된 분할 정보를 제공합니다. 실행 계획은 현재 다음 정보를 제공합니다.

* 분할된 테이블에서 `Partitioned` , `seek`, `scan`, `insert`, `update`, `merge`같은 연산자가 실행되었음을 나타내는 선택적 `delete`특성.  
* `SeekPredicateNew` 에서 범위 검색을 지정하는 선행 인덱스 키 열 및 필터 조건으로 `SeekKeys` 를 포함하는 새로운 `PartitionID` 요소와 `PartitionID`하위 요소. `SeekKeys` 하위 요소 두 개의 존재는 `PartitionID` 에서 skip scan 연산이 사용되는 것을 나타냅니다.   
* 액세스한 총 파티션 수를 제공하는 요약 정보. 이 정보는 런타임 계획에서만 사용할 수 있습니다. 

그래픽 실행 계획 출력 및 XML 실행 계획 출력 모두에 이 정보가 표시되는 방법을 보여 주려면 분할된 테이블 `fact_sales`의 다음 쿼리를 살펴봅니다. 이 쿼리는 두 개의 파티션에 있는 데이터를 업데이트합니다. 

```sql
UPDATE fact_sales
SET quantity = quantity * 2
WHERE date_id BETWEEN 20080802 AND 20080902;
```

다음 그림에서는 이 쿼리에 대해 컴파일 시간 실행 계획의 `Clustered Index Seek` 연산자 속성을 보여 줍니다. `fact_sales` 테이블의 정의 및 파티션 정의를 보려면 이 항목의 “예”를 참조하세요.  

![clustered_index_seek](../relational-databases/media/clustered-index-seek.gif)

#### <a name="partitioned-attribute"></a>Partitioned 특성

Index Seek와 같은 연산자가 분할된 테이블 또는 인덱스에서 실행되면 `Partitioned` 특성이 컴파일 시간 및 런타임 계획에 나타나고 이 특성이 `True` (1)로 설정됩니다. 이 특성이 `False` (0)로 설정되면 표시되지 않습니다.

`Partitioned` 특성은 다음 물리적 및 논리적 연산자에서 나타날 수 있습니다.  
|||
|--------|--------|
|Table Scan|Index Scan|
|Index Seek|삽입|
|업데이트|DELETE|
|병합||

앞의 그림과 같이 이 특성은 자신이 정의된 연산자의 속성에서 표시됩니다. XML 실행 계획 출력에서 이 특성은 자신이 정의된 연산자의 `Partitioned="1"` 노드에서 `RelOp` 로 표시됩니다.

#### <a name="new-seek-predicate"></a>새 검색 조건자

XML 실행 계획 출력에서 `SeekPredicateNew` 요소는 자신이 정의된 연산자에 표시됩니다. 이 출력에는 `SeekKeys` 하위 요소를 2개까지 포함할 수 있습니다. 첫 번째 `SeekKeys` 항목은 논리적 인덱스의 파티션 ID 수준에 첫 번째 수준 seek 연산을 지정합니다. 즉 이 seek 연산에서는 쿼리 조건을 충족시키기 위해 액세스해야 하는 파티션을 결정합니다. 두 번째 `SeekKeys` 항목은 첫 번째 수준 seek 연산자에서 식별된 각 파티션에서 발생하는 skip scan 연산의 두 번째 수준 seek 부분을 지정합니다. 

#### <a name="partition-summary-information"></a>파티션 요약 정보

런타임 실행 계획에서 파티션 요약 정보에는 액세스한 파티션의 수 및 액세스한 실제 파티션의 식별이 제공됩니다. 이 정보를 사용하여 쿼리에서 액세스한 올바른 파티션을 확인하면 모든 다른 파티션이 고려 대상에서 제외됩니다.

`Actual Partition Count`와 `Partitions Accessed`에 대한 정보가 제공됩니다. 

`Actual Partition Count` 는 쿼리에서 액세스한 총 파티션 개수입니다.

XML 실행 계획 출력에서`Partitions Accessed`는 새 `RuntimePartitionSummary` 요소 내에 Partitions Accessed가 정의된 연산자의 `RelOp` 노드에 나타나는 파티션 요약 정보입니다. 다음 예에서는 액세스한 총 2개의 파티션(파티션 2와 3)을 나타내는 `RuntimePartitionSummary` 요소의 내용을 보여 줍니다.
```
<RunTimePartitionSummary>

    <PartitionsAccessed PartitionCount="2" >

        <PartitionRange Start="2" End="3" />

    </PartitionsAccessed>

</RunTimePartitionSummary>
```

#### <a name="displaying-partition-information-by-using-other-showplan-methods"></a>다른 실행 계획 방법을 사용하여 파티션 정보 표시

실행 계획 메서드인 `SHOWPLAN_ALL`, `SHOWPLAN_TEXT`, `STATISTICS PROFILE` 은 다음과 같은 경우를 제외하고 이 항목에서 설명한 파티션 정보를 보고하지 않습니다. `SEEK` 조건자의 일부로서 액세스할 파티션이 파티션 ID를 나타내는 계산 열에서 범위 조건자로 식별됩니다. 다음 예제에서는 `SEEK` 연산자의 `Clustered Index Seek` 조건자를 보여 줍니다. 파티션 2와 3에 액세스하고 seek 연산자는 `date_id BETWEEN 20080802 AND 20080902`조건을 충족시키는 행에 필터를 설정합니다.
```
|--Clustered Index Seek(OBJECT:([db_sales_test].[dbo].[fact_sales].[ci]), 

        SEEK:([PtnId1000] >= (2) AND [PtnId1000] \<= (3) 

                AND [db_sales_test].[dbo].[fact_sales].[date_id] >= (20080802) 

                AND [db_sales_test].[dbo].[fact_sales].[date_id] <= (20080902)) 

                ORDERED FORWARD)
```

#### <a name="interpreting-execution-plans-for-partitioned-heaps"></a>분할된 힙의 실행 계획 해석

분할된 힙이 파티션 ID의 논리적 인덱스로 취급됩니다. 분할된 힙에서의 파티션 제거는 파티션 ID의 `Table Scan` 조건자를 사용하는 `SEEK` 연산자로 실행 계획에 나타납니다. 다음 예는 제공된 실행 계획 정보를 보여 줍니다.
```
|-- Table Scan (OBJECT: ([db].[dbo].[T]), SEEK: ([PtnId1001]=[Expr1011]) ORDERED FORWARD)
```

#### <a name="interpreting-execution-plans-for-collocated-joins"></a>배치된 조인의 실행 계획 해석

같거나 상응하는 파티션 함수를 사용하여 두 개의 테이블이 분할되고 조인의 양쪽 면에서 분할 열을 사용하여 쿼리의 조인 조건에 되면 조인 콜러케이션이 발생합니다. 쿼리 최적화 프로그램은 동일한 파티션 ID가 있는 각 테이블의 파티션이 개별적으로 조인되는 계획을 생성할 수 있습니다. 배치된 조인은 메모리와 처리 시간이 덜 필요로 할 수 있으므로, 배치된 조인이 배치되지 않은 조인보다 더 빠를 수 있습니다. 쿼리 최적화 프로그램에서는 비용 예측을 기준으로 배치되지 않은 계획 또는 배치된 계획을 선택합니다.

배치된 계획에서 `Nested Loops` 조인은 내부 측면에서 조인된 테이블 또는 인덱스 파티션을 하나 이상 읽습니다. `Constant Scan` 연산자의 숫자는 파티션 번호를 나타냅니다. 

배치된 조인에 대한 병렬 계획을 분할된 테이블 또는 인덱스에 대해 생성하면 `Constant Scan` 과 `Nested Loops` 조인 연산자 사이에 Parallelism 연산자가 표시됩니다. 이 경우 조인 외부 측면의 여러 작업자 스레드가 각각 서로 다른 파티션을 읽고 작업합니다. 

다음 그림은 배치된 조인에 대한 병렬 쿼리 계획을 보여 줍니다.   
![colocated_join](../relational-databases/media/colocated-join.gif)


#### <a name="parallel-query-execution-strategy-for-partitioned-objects"></a>분할된 개체에 대한 병렬 쿼리 실행 전략

쿼리 프로세서에서는 분할된 개체에서 선택하는 쿼리에 대해 병렬 실행 전략을 사용합니다. 실행 전략의 일부로 쿼리 프로세서에서는 쿼리에 필요한 테이블 파티션과 각 파티션에 할당할 작업자 스레드 수를 결정합니다. 대부분의 경우 쿼리 프로세서는 동일하거나 거의 동일한 수의 작업자 스레드를 각 파티션에 할당한 다음 전체 파티션에서 병렬로 쿼리를 실행합니다. 다음 단락에서는 작업자 스레드 할당에 대해 자세히 설명합니다.  

![worker thread1](../relational-databases/media/thread1.gif)

작업자 스레드 수가 파티션 수보다 적은 경우 쿼리 프로세서는 각 작업자 스레드를 서로 다른 파티션에 할당합니다. 따라서 처음에는 하나 이상의 파티션에 작업자 스레드가 할당되지 않습니다. 파티션에서 작업자 스레드가 실행을 완료하면 쿼리 프로세서는 각 파티션에 하나의 작업자 스레드가 할당될 때까지 이 작업자 스레드를 다음 파티션에 할당합니다. 이런 경우에만 쿼리 프로세서가 작업자 스레드를 다른 파티션에 다시 할당합니다.  
완료 후 재할당된 작업자 스레드를 표시합니다. 작업자 스레드 수가 파티션 수와 같은 경우 쿼리 프로세서는 각 파티션에 하나의 작업자 스레드를 할당합니다. 이때 작업자 스레드가 완료되어도 다른 파티션에 다시 할당되지 않습니다.  

![worker thread2](../relational-databases/media/thread2.gif)  

작업자 스레드 수가 파티션 수보다 많은 경우 쿼리 프로세서는 각 파티션에 동일한 수의 작업자 스레드를 할당합니다. 작업자 스레드 수가 파티션 수의 정확한 배수가 아닌 경우 쿼리 프로세서는 사용 가능한 작업자 스레드를 모두 사용하기 위해 일부 파티션에 하나의 작업자 스레드를 추가로 할당합니다. 파티션이 하나뿐인 경우 해당 파티션에 모든 작업자 스레드가 할당됩니다. 아래 다이어그램에서는 4개의 파티션과 14개의 작업자 스레드가 있습니다. 이 경우 각 파티션에 3개의 작업자 스레드가 할당되고 총 14개의 작업자 스레드를 할당하기 위해 2개의 파티션에 추가 작업자 스레드가 하나씩 할당됩니다. 이때 작업자 스레드가 완료되어도 다른 파티션에 다시 할당되지 않습니다.  

![worker thread3](../relational-databases/media/thread3.gif)  

위의 예에서는 작업자 스레드를 할당하는 간단한 방법을 제시하지만 실제 전략은 더욱 복잡하며 쿼리 실행 시 발생하는 다른 변수들을 고려해야 합니다. 예를 들어 테이블이 분할되어 있고 테이블의 A 열에 클러스터형 인덱스가 있으며 쿼리에 조건자 절 `WHERE A IN (13, 17, 25)`가 있는 경우 쿼리 프로세서는 각 테이블 파티션이 아니라 이러한 3개의 검색 값(A=13, A=17, A=25)에 각각 하나 이상의 작업자 스레드를 할당합니다. 이러한 값을 포함하는 파티션에서만 쿼리를 실행하면 되며 이러한 검색 조건자가 모두 동일한 파티션에 있는 경우 모든 작업자 스레드가 동일한 테이블 파티션에 할당됩니다.

또 다른 예로, 경계 포인트(10, 20, 30)가 있는 열 A에는 파티션 4개가 있고 열 B에는 인덱스가 있는 테이블과 조건자 절 `WHERE B IN (50, 100, 150)`을 갖는 쿼리가 있다고 가정합니다. 테이블 파티션은 A 값이 기준이기 때문에 B 값은 어느 테이블 파티션에서도 나타날 수 있습니다. 따라서 쿼리 프로세서는 4개의 각 테이블 파티션에서 3개의 B 값(50, 100, 150)을 각각 검색합니다. 쿼리 프로세서는 이러한 12개의 각 쿼리 검색을 병렬로 실행할 수 있도록 작업자 스레드를 균형 있게 할당합니다.

|A 열을 기반으로 하는 테이블 파티션 |각 테이블 파티션에서 B 열 검색 |
|----|----|
|테이블 파티션 1: A < 10   |B=50, B=100, B=150 |
|테이블 파티션 2: A >= 10 및 A < 20   |B=50, B=100, B=150 |
|테이블 파티션 3: A >= 20 및 A < 30   |B=50, B=100, B=150 |
|테이블 파티션 4: A >= 30  |B=50, B=100, B=150 |

### <a name="best-practices"></a>모범 사례

분할된 대형 테이블과 인덱스에서 많은 양의 데이터에 액세스하는 쿼리의 성능을 향상시키려면 다음과 같은 최선의 구현 방법을 권장합니다.

* 여러 디스크 간에 각 파티션을 스트라이프합니다. 특히 이 작업은 회전 디스크를 사용할 때 적합합니다.
* 가능하면 충분한 주 메모리가 있는 서버를 사용하여 자주 액세스하는 파티션이나 모든 파티션을 메모리 크기에 맞춰서 I/O 비용을 줄입니다.
* 쿼리한 데이터가 메모리 크기에 맞지 않을 경우 해당 테이블과 인덱스를 압축합니다. 이렇게 하면 I/O 비용이 줄어듭니다.
* 빠른 프로세서와 가능한 많은 프로세서 코어가 장착된 서버를 사용하여 병렬 쿼리 처리 기능을 이용합니다.
* 서버에 충분한 I/O 컨트롤러 대역폭이 있는지 확인합니다. 
* 모든 분할된 대형 테이블에 클러스터형 인덱스를 만들어 B-트리 검색 최적화를 이용합니다.
* 데이터를 분할된 테이블에 대량으로 로드하는 경우에는 [데이터 로드 성능 가이드](https://msdn.microsoft.com/library/dd425070.aspx) 백서의 모범 사례 권장 사항을 따르세요.

### <a name="example"></a>예제

다음 예에서는 7개의 파티션이 있는 단일 테이블이 포함된 테스트 데이터베이스를 만듭니다. 이 예에서 쿼리를 실행할 때 이전에 설명한 도구를 사용하여 컴파일 시간과 런타임 계획 모두에 대한 분할 정보를 확인합니다. 

> [!NOTE]
> 이 예에서는 백만 개 이상의 행을 테이블로 삽입합니다. 이 예를 실행하는 데에는 하드웨어에 따라 시간이 몇 분 정도 걸릴 수 있습니다. 이 예를 실행하기 전에 1.5GB 이상의 사용 가능한 디스크 공간이 있는지 확인하십시오. 
 
```sql
USE master;
GO
IF DB_ID (N'db_sales_test') IS NOT NULL
    DROP DATABASE db_sales_test;
GO
CREATE DATABASE db_sales_test;
GO
USE db_sales_test;
GO
CREATE PARTITION FUNCTION [pf_range_fact](int) AS RANGE RIGHT FOR VALUES 
(20080801, 20080901, 20081001, 20081101, 20081201, 20090101);
GO
CREATE PARTITION SCHEME [ps_fact_sales] AS PARTITION [pf_range_fact] 
ALL TO ([PRIMARY]);
GO
CREATE TABLE fact_sales(date_id int, product_id int, store_id int, 
    quantity int, unit_price numeric(7,2), other_data char(1000))
ON ps_fact_sales(date_id);
GO
CREATE CLUSTERED INDEX ci ON fact_sales(date_id);
GO
PRINT 'Loading...';
SET NOCOUNT ON;
DECLARE @i int;
SET @i = 1;
WHILE (@i<1000000)
BEGIN
    INSERT INTO fact_sales VALUES(20080800 + (@i%30) + 1, @i%10000, @i%200, RAND() * 25, (@i%3) + 1, '');
    SET @i += 1;
END;
GO
DECLARE @i int;
SET @i = 1;
WHILE (@i<10000)
BEGIN
    INSERT INTO fact_sales VALUES(20080900 + (@i%30) + 1, @i%10000, @i%200, RAND() * 25, (@i%3) + 1, '');
    SET @i += 1;
END;
PRINT 'Done.';
GO
-- Two-partition query.
SET STATISTICS XML ON;
GO
SELECT date_id, SUM(quantity*unit_price) AS total_price
FROM fact_sales
WHERE date_id BETWEEN 20080802 AND 20080902
GROUP BY date_id ;
GO
SET STATISTICS XML OFF;
GO
-- Single-partition query.
SET STATISTICS XML ON;
GO
SELECT date_id, SUM(quantity*unit_price) AS total_price
FROM fact_sales
WHERE date_id BETWEEN 20080801 AND 20080831
GROUP BY date_id;
GO
SET STATISTICS XML OFF;
GO
```

##  <a name="Additional_Reading"></a> 더 보기  
 [실행 계획 논리 및 물리 연산자 참조](../relational-databases/showplan-logical-and-physical-operators-reference.md)  
 [확장 이벤트](../relational-databases/extended-events/extended-events.md)  
 [쿼리 저장소에 대한 모범 사례](../relational-databases/performance/best-practice-with-the-query-store.md)  
 [카디널리티 추정](../relational-databases/performance/cardinality-estimation-sql-server.md)  
 [지능형 쿼리 처리](../relational-databases/performance/intelligent-query-processing.md)   
 [연산자 우선 순위](../t-sql/language-elements/operator-precedence-transact-sql.md)    
 [실행 계획](../relational-databases/performance/execution-plans.md)    
 [SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 성능 센터](../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)
