---
title: 결과에 대한 성능 튜닝
description: 이 문서에서는 다양한 최적화 방법을 테스트한 두 가지 사례 연구의 방법, 결과 및 결론을 요약합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1313cc2074058b104ea0939d02cdac30ddf28595
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486782"
---
# <a name="performance-for-r-services-results-and-resources"></a>R Services에 대한 성능: 결과 및 리소스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서는 R Services에 대한 성능 최적화를 설명하는 시리즈의 네 번째이자 최종입니다. 이 문서에서는 다양한 최적화 방법을 테스트한 두 가지 사례 연구의 방법, 결과 및 결론을 요약합니다.

두 사례 연구는 서로 다른 목표가 있습니다.

+ R Services 개발 팀의 첫 번째 사례 연구는 특정 최적화 방법의 영향을 측정하려고 했습니다.
+ 데이터 과학자 팀이 실시한 두 번째 사례 연구는 특정 대량 점수 매기기 시나리오에 가장 적합한 최적화를 결정하기 위해 여러 가지 방법을 실험했습니다.

이 항목에는 첫 번째 사례 연구의 자세한 결과가 나열되어 있습니다. 두 번째 사례 연구의 경우, 요약은 전체 결과를 설명합니다. 이 항목의 끝 부분에는 모든 스크립트 및 샘플 데이터와 원래 작성자가 사용한 리소스에 대한 링크가 있습니다.

## <a name="performance-case-study-airline-dataset"></a>성능 사례 연구: Airline 데이터 세트

SQL Server R Services 개발 팀의 이 사례 연구는 다양한 최적화의 영향을 테스트했습니다. 단일 rxLogit 모델이 만들어지고 Airline 데이터 세트에서 점수를 계산했습니다. 학습 및 점수 매기기 프로세스 중에 최적화가 적용되어 개별적인 영향을 평가했습니다.

- GitHub: SQL Server 최적화 연구를 위한 [샘플 데이터 및 스크립트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

### <a name="test-methods"></a>테스트 방법

1. Airline 데이터 세트는 10M 행의 단일 테이블로 구성됩니다. SQL Server에 다운로드되어 대량으로 로드되었습니다.
2. 여섯 개의 테이블 복사본이 만들어졌습니다.
3. 페이지 압축, 행 압축, 인덱싱, 열 형식 데이터 저장소 등의 SQL Server 기능을 테스트하기 위해 테이블의 복사본에 다양한 수정 사항이 적용되었습니다.
4. 각 최적화를 적용하기 전후에 성능을 측정했습니다.

| 테이블 이름| Description|
|------|------|
| *airline* | `rxDataStep`을 사용하여 원래 xdf 파일에서 변환된 데이터|                          |
| *airlineWithIntCol*   | 문자열이 아닌 정수에서 변환된 *DayOfWeek*. *rowNum* 열도 추가합니다.|
| *airlineWithIndex*    | *airlineWithIntCol* 테이블과 데이터가 같지만 *rowNum* 열을 사용하는 단일 클러스터형 인덱스 포함.|
| *airlineWithPageComp* | *airlineWithIndex* 테이블과 데이터가 같지만 페이지 압축이 사용됨. *CRSDepTime* 및 *ArrDelay*에서 계산된 두 개의 열 *CRSDepHour* 및 *Late*도 추가합니다. |
| *airlineWithRowComp*  | *airlineWithIndex* 테이블과 데이터가 같지만 행 압축이 사용됨. *CRSDepTime* 및 *ArrDelay*에서 계산된 두 개의 열 *CRSDepHour* 및 *Late*도 추가합니다. |
| *airlineColumnar*     | 단일 클러스터형 인덱스가 포함된 열 형식 저장소. 이 테이블은 정리된 csv 파일의 데이터로 채워집니다.|

각 테스트는 다음 단계로 구성되었습니다.

1. 각 테스트 전에 R 가비지 수집이 도출되었습니다.
2. 테이블 데이터를 기반으로 로지스틱 회귀 모델을 만들었습니다. 각 테스트에 대한 *rowsPerRead* 값이 500000으로 설정되었습니다.
3. 학습된 모델을 사용하여 점수가 생성됨
4. 각 테스트는 6회씩 실행되었습니다. 첫 번째 실행("시험 실행") 시간이 삭제되었습니다. 가끔 발생하는 이상값을 허용하기 위해 나머지 5회 실행 중 **최대** 시간도 삭제되었습니다. 나머지 4회 실행의 평균을 사용하여 각 테스트의 평균 경과 시간을 컴퓨팅했습니다.
5. 값 3(=보고 시간 및 진행률)과 함께 *reportProgress* 매개 변수를 사용하여 테스트를 실행했습니다. 각 출력 파일에는 IO에 사용된 시간, 전환 시간 및 컴퓨팅 시간에 관한 정보가 포함됩니다. 이러한 시간은 문제 해결 및 진단에 유용하게 사용됩니다.
6. 콘솔 출력도 출력 디렉터리의 파일에 전달됩니다.
7. 테스트 스크립트는 이러한 파일의 시간을 처리하여 평균 실행 시간을 계산했습니다.

예를 들어 다음 결과는 단일 테스트의 시간입니다. 필요한 주 타이밍은 **총 읽기 시간**(IO 시간) 및 **전환 시간**(계산을 위한 프로세스 설정 시의 오버헤드)입니다.

**샘플 타이밍**

```text
Running IntCol Test. Using airlineWithIntCol table.
run 1 took 3.66 seconds
run 2 took 3.44 seconds
run 3 took 3.44 seconds
run 4 took 3.44 seconds
run 5 took 3.45 seconds
run 6 took 3.75 seconds
  
Average Time: 3.4425
metric time pct
1 Total time 3.4425 100.00
2 Overall compute time 2.8512 82.82
3 Total read time 2.5378 73.72
4 Transition time 0.5913 17.18
5 Total non IO time 0.3134 9.10
```

R Services 또는 RevoScaleR 함수와 관련된 문제를 해결하는 데 도움이 되도록 테스트 스크립트를 다운로드하여 수정하는 것이 좋습니다.

### <a name="test-results-all"></a>테스트 결과(모두)

이 섹션에서는 각 테스트의 전후 결과를 비교합니다.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>압축 및 열 형식 테이블 저장소가 있는 데이터 크기

첫 번째 테스트에서는 데이터 크기를 줄이기 위해 압축 및 열 형식 테이블의 사용을 비교했습니다.

| 테이블 이름            | 행     | Reserved   | 데이터       | index_size | 사용 안 함  | 단축 비율(%)(예약됨) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816KB | 2972160KB | 6128KB    | 528KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784KB  | 623744KB  | 1352KB    | 688KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520KB | 1258880KB | 2552KB    | 1088KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992KB  | 201624KB  | 해당 없음        | 368KB  | 93%                 |

**결론**

columnstore 인덱스를 적용한 후 페이지 압축을 적용하여 데이터 크기를 최대한 줄일 수가 있었습니다.

#### <a name="effects-of-compression"></a>압축 효과

이 테스트는 행 압축, 페이지 압축 및 압축 안 함의 이점을 비교했습니다. 모델은 세 개의 서로 다른 데이터 테이블의 데이터에 대해 `rxLinMod`를 사용하여 학습되었습니다. 모든 테이블에 같은 수식 및 쿼리가 사용되었습니다.

| 테이블 이름            | 테스트 이름       | numTasks | 평균 시간 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression - 병렬| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression - 병렬 | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression - 병렬  | 4        | 5.2375       |

**결론**

압축만으로는 유용하지 않습니다. 이 예제에서 압축을 처리하기 위한 CPU를 늘리면 IO 시간이 감소합니다.

하지만 *numTasks*를 4로 설정하여 테스트를 병렬로 실행하면 평균 시간이 감소합니다.

더 큰 데이터 집합의 경우 압축의 효과가 눈에 클 수 있습니다. 압축은 데이터 집합 및 값에 따라 달라지므로 압축이 데이터 집합에 미치는 영향을 확인하려면 실험이 필요할 수 있습니다.

### <a name="effect-of-windows-power-plan-options"></a>Windows 전원 계획 옵션의 효과

이 실험에서 `rxLinMod`는 *airlineWithIntCol* 테이블과 함께 사용되었습니다. Windows 전원 계획은 **균형 조정** 또는 **고성능**으로 설정되었습니다. 모든 테스트의 경우 *numTasks*는 1로 설정되었습니다. 테스트는 6회 실행되었고 결과의 가변성을 조사하기 위해 전원 옵션을 둘 다 적용하여 두 번 수행되었습니다.

**고성능** 전원 옵션:

| 테스트 이름 | \#을 실행합니다. | 경과 시간 | 평균 시간 |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3.57초 |              |
|           | 2      | 3.45초 |              |
|           | 3      | 3.45초 |              |
|           | 4      | 3.55초 |              |
|           | 5      | 3.55초 |              |
|           | 6      | 3.45초 |              |
|           |        |              | 3.475        |
|           | 1      | 3.45초 |              |
|           | 2      | 3.53초 |              |
|           | 3      | 3.63초 |              |
|           | 4      | 3.49초 |              |
|           | 5      | 3.54초 |              |
|           | 6      | 3.47초 |              |
|           |        |              | 3.5075       |

**균형 조정** 전원 옵션:

| 테스트 이름 | \#을 실행합니다. | 경과 시간 | 평균 시간 |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3.89초 |              |
|           | 2      | 4.15초 |              |
|           | 3      | 3.77초 |              |
|           | 4      | 5초    |              |
|           | 5      | 3.92초 |              |
|           | 6      | 3.8초  |              |
|           |        |              | 3.91         |
|           | 1      | 3.82초 |              |
|           | 2      | 3.84초 |              |
|           | 3      | 3.86초 |              |
|           | 4      | 4.07초 |              |
|           | 5      | 4.86초 |              |
|           | 6      | 3.75초 |              |
|           |        |              | 3.88         |

**결론**

Windows **고성능** 전원 계획을 사용할 때 실행 시간이 더 일관되고 빠릅니다.

#### <a name="using-integer-vs-strings-in-formulas"></a>수식에서 정수 및 문자열 사용

이 테스트는 문자열 요소와 관련된 일반적인 문제를 방지하기 위해 R 코드를 수정할 때의 영향을 평가했습니다. 특히 두 개의 테이블을 통해 `rxLinMod`를 사용하여 모델을 학습했습니다. 첫 번째 테이블에서는 요소가 문자열로 저장됩니다. 두 번째 테이블에서는 요소가 정수로 저장됩니다.

+ *airline* 테이블의 경우 [DayOfWeek] 열에는 문자열이 포함되어 있습니다. _colInfo_ 매개 변수는 요소 수준(월요일, 화요일, ...)을 지정하는 데 사용되었습니다.

+  *airlineWithIndex* 테이블의 경우 [DayOfWeek]는 정수입니다. _colInfo_ 매개 변수가 지정되지 않았습니다.

+ 두 경우에 모두 같은 수식이 사용되었습니다. `ArrDelay ~ CRSDepTime + DayOfWeek`.

| 테이블 이름          | 테스트 이름   | 평균 시간 |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**결론**

요소에 문자열 대신 정수를 사용하는 경우에는 분명한 혜택이 있습니다.

### <a name="avoiding-transformation-functions"></a>변환 함수 방지

이 테스트에서는 `rxLinMod`를 사용하여 모델을 학습했지만 두 실행 간에 코드가 변경되었습니다.

+ 첫 번째 실행에서 변환 함수는 모델 작성의 일부로 적용되었습니다. 
+ 두 번째 실행에서는 기능 값이 사전 계산되어 사용할 수 있으므로 변환 함수가 필요하지 않습니다.

| 테스트 이름             | 평균 시간 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**결론**

변환 함수를 사용하지 **않을** 때는 학습 시간이 단축되었습니다. 즉, 미리 계산되고 테이블에 저장된 열을 사용할 때 모델이 더 빨리 학습되었습니다.

변환이 더 많고 데이터 세트가 더 크면(\> 100M) 절감 효과가 더 클 것으로 예상됩니다.

### <a name="using-columnar-store"></a>열 형식 저장소 사용

이 테스트는 열 형식 데이터 저장소 및 인덱스를 사용할 때의 성능 이점을 평가했습니다. 동일한 모델이 `rxLinMod`를 사용하여 학습되었으며 데이터 변환은 없었습니다.

+ 첫 번째 실행에서 데이터 테이블은 표준 행 저장소를 사용했습니다.
+ 두 번째 실행에서는 열 저장소가 사용되었습니다.

| 테이블 이름         | 테스트 이름 | 평균 시간 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**결론**

표준 행 저장소보다 열 형식 저장소의 성능이 더 좋습니다. 데이터 세트가 클수록(\> 100 M) 성능에 큰 차이가 있을 수 있습니다.

### <a name="effect-of-using-the-cube-parameter"></a>큐브 매개 변수 사용의 효과

이 테스트의 목적은 사전 계산된 **cube** 매개 변수를 사용하기 위한 RevoScaleR의 옵션이 성능을 향상시킬 수 있는지 여부를 확인하는 것입니다. 다음 수식을 통해 `rxLinMod`를 사용하여 모델을 학습했습니다.

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

표에서 요소 *DayOfWeek*는 문자열로 저장됩니다.

| 테스트 이름     | 큐브 매개 변수 | numTasks | 평균 시간 | 단일 행 예측(ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**결론**

큐브 매개 변수 인수를 사용하면 성능이 명확하게 향상됩니다.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>rxDTree 모델의 maxDepth 변경 효과

이 실험에서 `rxDTree` 알고리즘은 *airlineColumnar* 테이블에서 모델을 만드는 데 사용되었습니다. 이 테스트의 경우 *numTasks*는 4로 설정되었습니다. 트리 깊이 변경이 런타임에 미치는 영향을 보여 주기 위해 *maxDepth*에 대한 다양한 값이 사용되었습니다.

| 테스트 이름       | maxDepth | 평균 시간 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**결론**

트리의 깊이가 증가함에 따라 전체 노드 수가 기하급수적으로 증가합니다. 모델을 만드는 데 걸리는 시간도 크게 증가했습니다.

### <a name="prediction-on-a-stored-model"></a>저장된 모델에 대한 예측

이 테스트의 목적은 학습된 모델이 현재 실행 중인 코드의 일부로 생성되는 것이 아니라 SQL Server 테이블에 저장될 때 점수를 매기는 성능에 미치는 영향을 확인하는 것입니다. 점수 매기기의 경우 저장된 모델이 데이터베이스에서 로드되고 메모리(로컬 컴퓨팅 컨텍스트)에서 단일 행 데이터 프레임을 사용하여 예측이 생성됩니다.

테스트 결과는 모델 저장 시간 및 모델을 로드하고 예측하는 데 걸린 시간을 보여 줍니다.

| 테이블 이름 | 테스트 이름 | 평균 시간(모델 학습) | 모델 저장/로드 시간|
|------------|------------|------------|------------|
| 항공사    | SaveModel| 21.59| 2.08|
| 항공사    | LoadModelAndPredict | | 2.09(예측 시간 포함) |

**결론**

테이블에서 학습된 모델을 로드하는 것이 예측을 수행하는 가장 빠른 방법입니다. 모델을 만들고 동일한 스크립트에서 모든 점수 매기기를 수행하지 않는 것이 좋습니다.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>사례 연구: 다시 시작 일치 태스크에 대한 최적화

다시 시작 일치 모델은 Microsoft 데이터 과학자인 Ke Huang이 SQL Server에서 R 코드의 성능을 테스트하기 위해 개발했으며, 이를 통해 데이터 과학자가 확장 가능한 엔터프라이즈 수준 솔루션을 만들 수 있습니다.

### <a name="methods"></a>메서드

RevoScaleR 및 MicrosoftML 패키지는 모두 대량 데이터 세트를 포함하는 복잡한 R 솔루션에서 예측 모델을 학습하는 데 사용되었습니다. SQL 쿼리와 R 코드는 모든 테스트에서 동일했습니다. 테스트는 SQL Server가 설치된 단일 Azure VM에서 수행되었습니다. 그런 다음, 작성자는 SQL Server에서 제공하는 다음 최적화를 제외하고 점수 매기기 시간을 비교했습니다.

- 메모리 내 테이블
- Soft-NUMA
- 관리

R 스크립트 실행에 대한 소프트 NUMA의 영향을 평가하기 위해 데이터 과학 팀은 20개의 물리적 코어가 있는 Azure 가상 머신에서 솔루션을 테스트했습니다. 이러한 물리적 코어에서 4개의 소프트 NUMA 노드가 자동으로 생성되어 각 노드에 5개의 코어가 포함되었습니다.

CPU affinitization은 R 작업에 대한 영향을 평가하기 위해 다시 시작 일치 시나리오에 적용되었습니다. 4개의 **SQL 리소스 풀** 및 4개의 **외부 리소스 풀**이 생성되었으며, CPU 선호도는 각 노드에서 동일한 CPU 세트가 사용되도록 지정되었습니다.

하드웨어 사용률을 최적화하기 위해 각 리소스 풀이 다른 작업 그룹에 할당되었습니다. 그 이유는 소프트 NUMA 및 CPU 선호도로 인해 실제 NUMA 노드에서 실제 메모리를 분리할 수 없기 때문입니다. 따라서 정의에 따라 동일한 실제 NUMA 노드를 기반으로 하는 모든 소프트 NUMA 노드는 동일한 OS 메모리 블록에서 메모리를 사용해야 합니다. 즉, 메모리-프로세서 선호도는 없습니다.

이 구성을 만드는 데 사용된 프로세스는 다음과 같습니다.

1. 기본적으로 SQL Server에 할당된 메모리 양을 줄입니다.

2. R 작업을 병렬로 실행하기 위한 4개의 새로운 풀을 만듭니다.

3. 각 작업 그룹이 리소스 풀과 연결되도록 네 개의 작업 그룹을 만듭니다.

4. 새 작업 그룹 및 할당을 사용하여 Resource Governor를 다시 시작합니다.

5. UDF(사용자 정의 분류자 함수)를 생성하여 다른 작업 그룹에 서로 다른 작업을 할당합니다.

6. 적절한 작업 그룹에 대한 함수를 사용하도록 Resource Governor 구성을 업데이트합니다.

### <a name="results"></a>결과

다시 시작 일치 연구에서 성능이 가장 뛰어난 구성은 다음과 같습니다.

-   4개의 내부 리소스 풀(SQL Server용)

-   4개의 외부 리소스 풀(외부 스크립트 작업용)

-   각 리소스 풀은 특정 작업 그룹과 연결됩니다.

-   각 리소스 풀은 서로 다른 CPU에 할당됩니다.

-   최대 내부 메모리 사용량(SQL Server) = 30%

-   R 세션에서 사용할 최대 메모리 = 70%

다시 시작 일치 모델의 경우 외부 스크립트 사용이 과도했으며 다른 데이터베이스 엔진 서비스가 실행되고 있지 않습니다. 따라서 외부 스크립트에 할당된 리소스가 70%로 증가하여 스크립트 성능에 가장 적합한 구성을 증명했습니다.

이 구성은 다른 값으로 실험함으로써 달성했습니다. 다른 하드웨어 또는 다른 솔루션을 사용하는 경우 최적의 구성이 다를 수 있습니다. 사용자의 사례에 가장 적합한 구성을 찾도록 항상 실험하세요!

최적화된 솔루션에서 110만의 데이터 행(100개의 기능 포함)은 20개의 코어 컴퓨터에서 8.5초 미만으로 점수가 매겨집니다. 최적화는 점수 매기기 시간 측면에서 성능을 크게 향상시켰습니다.

또한 결과는 **기능 수**가 점수 매기기 시간에 상당한 영향을 미쳤음을 시사했습니다. 예측 모델에 더 많은 기능이 사용되면 개선이 더 두드러졌습니다.

자세한 논의는 이 블로그 문서와 함께 제공되는 자습서를 참조하는 것이 좋습니다.

-   [SQL Server에서 기계 학습을 위한 최적화 팁과 요령](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

많은 사용자는 R(또는 Python) 런타임이 처음 로드될 때 약간의 일시 중지가 있음을 언급했습니다. 이러한 이유로 이 테스트에 설명된 대로 첫 번째 실행 시간이 측정되는 경우가 많으며 나중에 삭제됩니다. 후속 캐싱은 첫 번째와 두 번째 실행 사이에 현저한 성능 차이가 발생할 수 있습니다. 특히 데이터가 SQL Server에서 직접 로드되는 대신 네트워크를 통해 데이터가 전달되는 경우 SQL Server와 외부 런타임 간에 데이터가 이동될 때 약간의 오버헤드가 발생합니다.

이러한 모든 이유로 인해 성능에 미치는 영향은 작업에 따라 크게 달라지므로 이 초기 로딩 시간을 완화할 수 있는 단일 솔루션은 없습니다. 예를 들어 캐싱은 단일 행 점수 매기기에 대해 일괄 처리로 수행됩니다. 따라서 후속 점수 매기기 작업은 훨씬 빨라지고 모델 및 R 런타임이 다시 로드되지 않습니다. [네이티브 점수 매기기](../sql-native-scoring.md)를 사용하여 R 런타임을 완전히 로드하지 않도록 할 수도 있습니다.

큰 모델을 학습하거나 큰 일괄 처리로 점수를 매기는 경우 데이터 이동을 방지하거나 스트리밍 및 병렬 처리를 통해 얻는 이점에 비해 오버헤드가 최소화될 수 있습니다. 추가 성능 지침은 다음 블로그 게시물을 참조하세요.

+ [R을 사용하여 초당 100만 건의 트랜잭션에서 사기 행위 감지](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>리소스

다음은 이러한 테스트 개발에 사용되는 정보, 도구 및 스크립트에 대한 링크입니다.

+ 성능 테스트 스크립트 및 데이터에 대한 링크: [SQL Server 최적화 연구를 위한 샘플 데이터 및 스크립트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 다시 시작 일치 솔루션을 설명하는 문서: [SQL Server R Services에 대한 최적화 팁과 요령](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ 다시 시작 일치 솔루션을 위해 SQL 최적화에 사용되는 스크립트: [GitHub 리포지토리](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching)

### <a name="learn-about-windows-server-management"></a>Windows 서버 관리에 대한 자세한 정보

+ [How to determine the appropriate page file size for 64-bit versions of Windows](https://support.microsoft.com/kb/2860880)(Windows 64비트 버전에 적절한 페이지 파일 크기를 결정하는 방법)

+ [NUMA 이해](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server가 NUMA를 지원하는 방법](https://technet.microsoft.com/library/ms180954.aspx)

+ [소프트 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>SQL Server 최적화에 대한 자세한 정보

+ [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [메모리 최적화 테이블 소개](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [데모: 메모리 내 OLTP의 성능 향상](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [데이터 압축](../../relational-databases/data-compression/data-compression.md)

+ [테이블 또는 인덱스에 압축 사용](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [테이블 또는 인덱스에서 압축 해제](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>SQL Server 관리에 대한 자세한 정보

+ [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)

+ [Resource Governor 소개](https://technet.microsoft.com/library/bb895232.aspx)

+ [Resource Governor 구성 예제](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>도구

+ [DISKSPD storage load generator/performance test tool](https://github.com/microsoft/diskspd)(DISKSPD 스토리지 로드 생성기/성능 테스트 도구)

+ [FSUtil utility reference](https://technet.microsoft.com/library/cc753059.aspx)(FSUtil 유틸리티 참조)


## <a name="other-articles-in-this-series"></a>이 시리즈의 다른 문서

[R의 성능 튜닝 - 소개](sql-server-r-services-performance-tuning.md)

[R의 성능 조정 - SQL Server 구성](sql-server-configuration-r-services.md)

[R의 성능 조정 - R 코드 및 데이터 최적화](r-and-data-optimization-r-services.md)

[성능 조정 - 사례 연구 결과](performance-case-study-r-services.md)
