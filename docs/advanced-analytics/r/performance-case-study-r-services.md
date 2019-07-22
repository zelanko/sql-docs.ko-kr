---
title: SQL Server R Services 결과 및 리소스에 대 한 성능
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 08d1fd367572561aaa7235fd037371e30f5b270e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345285"
---
# <a name="performance-for-r-services-results-and-resources"></a>R Services에 대 한 성능: 결과 및 리소스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 R Services에 대 한 성능 최적화를 설명 하는 시리즈의 네 번째 및 최종입니다. 이 문서에서는 다양 한 최적화 방법을 테스트 한 두 사례 연구의 방법, 결과 및 결론을 요약 합니다.

두 사례 연구에는 서로 다른 목표가 있습니다.

+ 첫 번째 사례 연구는 R Services 개발 팀에서 특정 최적화 방법의 영향을 측정 하려고 합니다.
+ 두 번째 사례 연구는 데이터 과학자 팀에 의해 실험는 다양 한 방법을 사용 하 여 특정 대량 점수 매기기 시나리오에 대 한 최적의 최적화를 결정 합니다.

이 항목에서는 첫 번째 사례 연구의 자세한 결과를 나열 합니다. 두 번째 사례 연구의 경우 요약에서는 전체 결과를 설명 합니다. 이 항목의 끝 부분에는 모든 스크립트 및 샘플 데이터와 원래 작성자가 사용한 리소스에 대 한 링크가 나와 있습니다.

## <a name="performance-case-study-airline-dataset"></a>성능 사례 연구: 항공편 데이터 집합

이 사례 연구는 SQL Server R Services 개발 팀에서 다양 한 최적화의 영향을 테스트 했습니다. 단일 rxLogit 모델이 만들어지고 항공 데이터 집합에서 점수를 계산 합니다. 개별 영향을 평가 하기 위해 학습 및 점수 매기기 프로세스 중에 최적화가 적용 되었습니다.

- Github SQL Server 최적화 학습을 위한 [샘플 데이터 및 스크립트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

### <a name="test-methods"></a>테스트 메서드

1. 항공편 데이터 집합은 10M 행의 단일 테이블로 구성 됩니다. SQL Server에 다운로드 되어 대량으로 로드 되었습니다.
2. 테이블의 복사본이 6 개 생성 되었습니다.
3. 페이지 압축, 행 압축, 인덱싱, 칼럼 형식 데이터 저장소 등의 SQL Server 기능을 테스트 하기 위해 테이블의 복사본에 다양 한 수정 사항이 적용 되었습니다.
4. 각 최적화를 적용 하기 전후에 성능이 측정 되었습니다.

| 테이블 이름| Description|
|------|------|
| *airline* | `rxDataStep`을 사용하여 원래 xdf 파일에서 변환된 데이터|                          |
| *airlineWithIntCol*   | 문자열이 아닌 정수에서 변환된 *DayOfWeek*. *rowNum* 열도 추가합니다.|
| *airlineWithIndex*    | *airlineWithIntCol* 테이블과 데이터가 같지만 *rowNum* 열을 사용하는 단일 클러스터형 인덱스 포함.|
| *airlineWithPageComp* | *airlineWithIndex* 테이블과 데이터가 같지만 페이지 압축이 사용됨. *CRSDepTime* 및 *ArrDelay*에서 계산된 두 개의 열 *CRSDepHour* 및 *Late*도 추가합니다. |
| *airlineWithRowComp*  | *airlineWithIndex* 테이블과 데이터가 같지만 행 압축이 사용됨. *CRSDepTime* 및 *ArrDelay*에서 계산된 두 개의 열 *CRSDepHour* 및 *Late*도 추가합니다. |
| *airlineColumnar*     | 단일 클러스터형 인덱스가 포함된 열 형식 저장소. 이 테이블은 정리된 csv 파일의 데이터로 채워집니다.|

각 테스트는 다음 단계로 구성 됩니다.

1. 각 테스트 전에 R 가비지 수집이 도출되었습니다.
2. 테이블 데이터를 기반으로 로지스틱 회귀 모델을 만들었습니다. 각 테스트에 대한 *rowsPerRead* 값이 500000으로 설정되었습니다.
3. 학습 된 모델을 사용 하 여 점수가 생성 됨
4. 각 테스트는 6 회 실행 되었습니다. 첫 번째 실행 시간 ("콜드 실행")이 삭제 되었습니다. 간헐적으로 발생 하는 이상 값을 허용 하기 위해 나머지 5 개 실행의 **최대** 시간도 삭제 되었습니다. 나머지 4회 실행의 평균을 사용하여 각 테스트의 평균 경과 시간을 컴퓨팅했습니다.
5. 테스트는 *Reportprogress* 매개 변수를 사용 하 여 3 (= report 타이밍 및 progress) 값을 사용 하 여 실행 되었습니다. 각 출력 파일에는 IO, 전환 시간 및 계산 시간에 소요 된 시간에 대 한 정보가 포함 됩니다. 이러한 시간은 문제 해결 및 진단에 유용하게 사용됩니다.
6. 출력 디렉터리의 파일에도 콘솔 출력이 전달 되었습니다.
7. 테스트 스크립트는 이러한 파일의 시간을 처리 하 여 평균 실행 시간을 계산 합니다.

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

R Services 또는 RevoScaleR 함수와 관련 된 문제를 해결 하는 데 도움이 되는 테스트 스크립트를 다운로드 하 여 수정 하는 것이 좋습니다.

### <a name="test-results-all"></a>테스트 결과 (모두)

이 섹션에서는 각 테스트에 대 한 이전 및 이후 결과를 비교 합니다.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>압축 및 열 형식 테이블 저장소를 사용 하는 데이터 크기

첫 번째 테스트에서는 압축 및 칼럼 형식 테이블을 비교 하 여 데이터 크기를 줄입니다.

| 테이블 이름            | 행     | 예약됨   | data       | index_size | 사용 되지 않는  | 단축 비율(%)(예약됨) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816KB | 2972160KB | 6128KB    | 528KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784KB  | 623744KB  | 1352KB    | 688KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520KB | 1258880KB | 2552KB    | 1088KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992KB  | 201624KB  | n/a        | 368KB  | 93%                 |

**결론**

Columnstore 인덱스를 적용 한 다음 페이지 압축을 적용 하 여 데이터 크기를 최대한 줄일 수가 있었습니다.

#### <a name="effects-of-compression"></a>압축 효과

이 테스트는 행 압축, 페이지 압축 및 압축 안 함의 이점을 비교 했습니다. 모델은 서로 다른 세 `rxLinMod` 데이터 테이블의 데이터를 사용 하 여 학습 되었습니다. 모든 테이블에 같은 수식 및 쿼리가 사용되었습니다.

| 테이블 이름            | 테스트 이름       | numTasks | 평균 시간 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression-병렬| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression-병렬 | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression-병렬  | 4        | 5.2375       |

**결론**

압축 만으로는 유용 하지 않습니다. 이 예제에서 압축을 처리 하기 위해 CPU를 늘리면 IO 시간이 감소 합니다.

하지만 *numTasks*를 4로 설정하여 테스트를 병렬로 실행하면 평균 시간이 감소합니다.

더 큰 데이터 집합의 경우 압축의 효과가 눈에 클 수 있습니다. 압축은 데이터 집합 및 값에 따라 달라지므로 압축이 데이터 집합에 미치는 영향을 확인하려면 실험이 필요할 수 있습니다.

### <a name="effect-of-windows-power-plan-options"></a>Windows 전원 계획 옵션의 효과

이 실험에서 `rxLinMod`는 *airlineWithIntCol* 테이블과 함께 사용되었습니다. Windows 전원 관리 요금제가 **균형** 또는 **고성능**으로 설정 되었습니다. 모든 테스트의 경우 *numTasks*는 1로 설정되었습니다. 테스트는 6 회 실행 되었고 두 전원 옵션에서 두 번 수행 되어 결과의 산포도를 조사 했습니다.

**고성능** 전원 옵션:

| 테스트 이름 | \#를 실행합니다. | 경과 시간 | 평균 시간 |
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

| 테스트 이름 | \#를 실행합니다. | 경과 시간 | 평균 시간 |
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

Windows **고성능** 전원 관리를 사용 하는 경우 실행 시간이 더 일관적이 고 더 빠릅니다.

#### <a name="using-integer-vs-strings-in-formulas"></a>수식에서 정수 및 문자열 사용

이 테스트는 문자열 요소와 관련 된 일반적인 문제를 방지 하기 위해 R 코드를 수정할 때의 영향을 평가 했습니다. 특히, 두 테이블을 사용 하 `rxLinMod` 여 모델을 학습 시켰습니다. 첫 번째에서는 요소가 문자열로 저장 되 고 두 번째 테이블에서는 요인이 정수로 저장 됩니다.

+ *항공편* 테이블의 [DayOfWeek] 열에는 문자열이 포함 됩니다. _ColInfo_ 매개 변수는 요소 수준을 지정 하는 데 사용 되었습니다 (월요일, 화요일, ...).

+  *락 Linewithindex* 테이블의 경우 [DayOfWeek]는 정수입니다. _ColInfo_ 매개 변수가 지정 되지 않았습니다.

+ 두 경우에 모두 같은 수식이 사용되었습니다. `ArrDelay ~ CRSDepTime + DayOfWeek`.

| 테이블 이름          | 테스트 이름   | 평균 시간 |
|---------------------|-------------|--------------|
| *항공사*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**결론**

요소에 문자열 대신 정수를 사용 하는 경우에는 분명 한 혜택이 있습니다.

### <a name="avoiding-transformation-functions"></a>변환 함수 방지

이 테스트에서는를 사용 하 여 `rxLinMod`모델을 학습 했지만 두 실행 간에 코드를 변경 했습니다.

+ 첫 번째 실행에서 변환 함수는 모델 작성의 일부로 적용 되었습니다. 
+ 두 번째 실행에서는 기능 값이 사전 계산 되 고 사용 가능 하 여 변환 함수가 필요 하지 않습니다.

| 테스트 이름             | 평균 시간 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**결론**

변환 함수를 사용 **하지 않을** 때 학습 시간이 짧습니다. 즉, 미리 계산 되 고 테이블에 저장 된 열을 사용 하면 모델의 학습 속도가 더 빨라집니다.

더 많은 변환이 있고 데이터 집합이 더 큰 경우 (\> 100M) 절감 액은 더 커질 것으로 예상 됩니다.

### <a name="using-columnar-store"></a>열 형식 저장소 사용

이 테스트는 칼럼 형식 데이터 저장소 및 인덱스를 사용 하 여 성능상의 이점을 평가한 것입니다. 동일한 모델이 데이터 변환을 사용 하 `rxLinMod` 여 학습 되었습니다.

+ 첫 번째 실행에서 데이터 테이블은 표준 행 저장소를 사용 합니다.
+ 두 번째 실행에서는 열 저장소를 사용 했습니다.

| 테이블 이름         | 테스트 이름 | 평균 시간 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**결론**

표준 행 저장소 보다는 열 형식 저장소를 사용 하는 것이 좋습니다. 큰 데이터 집합 (\> 100 M)에서 성능에 상당한 차이가 있을 수 있습니다.

### <a name="effect-of-using-the-cube-parameter"></a>큐브 매개 변수 사용의 영향

이 테스트의 목적은 사전 계산 **cube** 매개 변수를 사용 하기 위한 RevoScaleR의 옵션이 성능을 향상 시킬 수 있는지 여부를 결정 하는 것입니다. 다음 수식을 사용 하 여 `rxLinMod`모델을 학습 했습니다.

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

표에서 *DayOfWeek* 요소는 문자열로 저장 됩니다.

| 테스트 이름     | 큐브 매개 변수 | numTasks | 평균 시간 | 단일 행 예측 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**결론**

큐브 매개 변수 인수를 사용 하면 성능이 명확 하 게 향상 됩니다.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>RxDTree 모델에 대 한 maxDepth 변경 효과

이 실험 `rxDTree` 에서는 알고리즘을 사용 하 여 *airlinecolumnar 테이블과 함께* 테이블에 모델을 만들었습니다. 이 테스트의 경우 *numTasks*는 4로 설정되었습니다. *Maxdepth* 에 대 한 여러 가지 값을 사용 하 여 트리 깊이 변경을 실행 시간에 미치는 영향을 보여 줍니다.

| 테스트 이름       | maxDepth | 평균 시간 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**결론**

트리의 깊이가 증가할수록 전체 노드 수가 급격 하 게 늘어납니다. 모델을 만드는 데 걸리는 시간이 크게 증가 했습니다.

### <a name="prediction-on-a-stored-model"></a>저장 된 모델에 대 한 예측

이 테스트의 목적은 학습 된 모델이 현재 실행 중인 코드의 일부로 생성 되는 것이 아니라 SQL Server 테이블에 저장 될 때 점수를 매기는 성능에 미치는 영향을 확인 하는 것 이었습니다. 점수 매기기의 경우 저장 된 모델은 데이터베이스에서 로드 되 고 예측은 메모리 (로컬 계산 컨텍스트)의 단일 행 데이터 프레임을 사용 하 여 생성 됩니다.

테스트 결과에는 모델을 저장 하는 시간과 모델을 로드 하 고 예측 하는 데 걸린 시간이 표시 됩니다.

| 테이블 이름 | 테스트 이름 | 평균 시간(모델 학습) | 모델 저장/로드 시간|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2.09(예측 시간 포함) |

**결론**

테이블에서 학습 된 모델을 로드 하는 것이 명확 하 게 예측 하는 방법입니다. 모델을 만들고 동일한 스크립트에서 점수 매기기를 수행 하지 않는 것이 좋습니다.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>사례 연구: 다시 시작 일치 태스크에 대 한 최적화

다시 시작 일치 모델은 SQL Server에서 R 코드의 성능을 테스트 하는 데 도움이 되는 Microsoft 데이터 과학자 Ke Huang에 의해 개발 되었으며,이를 통해 확장 가능한 엔터프라이즈 수준 솔루션을 만들 수 있습니다.

### <a name="methods"></a>메서드

RevoScaleR 및 MicrosoftML 패키지는 모두 대량 데이터 집합을 포함 하는 복잡 한 R 솔루션에서 예측 모델을 학습 하는 데 사용 되었습니다. SQL 쿼리와 R 코드는 모든 테스트에서 동일 했습니다. 테스트는 SQL Server 설치 된 단일 Azure VM에서 수행 되었습니다. 그런 다음 작성자는 SQL Server에서 제공 하는 다음 최적화를 제외 하 고 점수 매기기 시간을 비교 합니다.

- 메모리 내 테이블
- Soft-NUMA
- 리소스 관리자

R 스크립트 실행에 대 한 소프트 NUMA의 영향을 평가 하기 위해 데이터 과학 팀은 20 개의 물리적 코어를 사용 하 여 Azure 가상 머신에서 솔루션을 테스트 했습니다. 이러한 실제 코어에서 4 개의 소프트 NUMA 노드가 자동으로 생성 되어 각 노드에 5 개의 코어가 포함 됩니다.

CPU affinitization는 R 작업에 대 한 영향을 평가 하기 위해 다시 시작 일치 시나리오에서 적용 되었습니다. 4 개의 **SQL 리소스 풀** 과 4 개의 **외부 리소스 풀** 을 만들었으며 cpu 선호도를 지정 하 여 각 노드에서 동일한 cpu 집합이 사용 되도록 합니다.

하드웨어 사용률을 최적화 하기 위해 각 리소스 풀이 다른 작업 그룹에 할당 되었습니다. 그 이유는 소프트 NUMA 및 CPU 선호도로 인해 실제 NUMA 노드의 실제 메모리가 분리 될 수 없기 때문입니다. 따라서 동일한 실제 NUMA 노드를 기반으로 하는 모든 소프트 NUMA 노드는 동일한 OS 메모리 블록에서 메모리를 사용 해야 합니다. 즉, 메모리-프로세서 선호도는 없습니다.

이 구성을 만드는 데 사용 된 프로세스는 다음과 같습니다.

1. 기본적으로 SQL Server 할당 된 메모리 양을 줄입니다.

2. R 작업을 병렬로 실행 하기 위한 4 개의 새 풀을 만듭니다.

3. 각 작업 그룹이 리소스 풀과 연결 되도록 네 개의 작업 그룹을 만듭니다.

4. 새 작업 그룹 및 할당을 사용 하 여 Resource Governor을 다시 시작 합니다.

5. 다른 작업 그룹에 서로 다른 작업을 할당 하는 UDF (사용자 정의 분류자 함수)를 만듭니다.

6. 적절 한 작업 그룹에 함수를 사용 하도록 Resource Governor 구성을 업데이트 합니다.

### <a name="results"></a>결과

다시 시작 일치 조사에서 성능이 가장 뛰어난 구성은 다음과 같습니다.

-   SQL Server의 내부 리소스 풀 4 개

-   외부 스크립트 작업의 경우 네 개의 외부 리소스 풀

-   각 리소스 풀은 특정 작업 그룹에 연결 됩니다.

-   각 리소스 풀은 서로 다른 Cpu에 할당 됩니다.

-   최대 내부 메모리 사용량 (SQL Server) = 30%

-   R 세션에서 사용할 최대 메모리 = 70%

다시 시작 일치 모델의 경우 외부 스크립트 사용이 과도 하 게 실행 되었으며 다른 데이터베이스 엔진 서비스가 실행 되 고 있지 않습니다. 따라서 외부 스크립트에 할당 된 리소스가 70%로 증가 하 여 스크립트 성능에 가장 적합 한 구성을 증명 했습니다.

이 구성은 다른 값을 실험 하 여에 도달 했습니다. 다른 하드웨어 또는 다른 솔루션을 사용 하는 경우 최적의 구성이 다를 수 있습니다. 사용자의 사례에 가장 적합 한 구성을 찾으려면 항상 실험 하세요.

최적화 된 솔루션에서 110만의 데이터 행 (100 기능 포함)은 20 코어 컴퓨터의 8.5 초 미만으로 점수가 매겨집니다. 최적화는 점수 매기기 시간 측면에서 성능이 크게 향상 되었습니다.

또한 결과는 **기능 수가** 점수 매기기 시간에 상당한 영향을 미치는 것을 제안 합니다. 예측 모델에서 더 많은 기능을 사용 하면 향상 된 기능이 훨씬 더 두드러집니다.

자세한 논의는이 블로그 문서와 함께 제공 되는 자습서를 참조 하는 것이 좋습니다.

-   [SQL Server에서 machine learning에 대 한 최적화 팁과 요령](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

대부분의 사용자는 R (또는 Python) 런타임이 처음 로드 될 때 약간의 일시 중지가 있음을 언급 했습니다. 이러한 이유로 이러한 테스트에 설명 된 대로 첫 번째 실행 시간이 측정 되는 경우가 많으며 나중에 삭제 됩니다. 이후 캐싱은 첫 번째와 두 번째 실행 사이에 주목할 만한 성능 차이를 일으킬 수 있습니다. 특히 데이터가 SQL Server에서 직접 로드 되는 대신 네트워크를 통해 전달 되는 경우 SQL Server와 외부 런타임 간에 데이터가 이동 될 때 오버 헤드가 발생 합니다.

이러한 모든 이유로 인해 성능 영향은 작업에 따라 크게 달라 지므로 이러한 초기 로드를 완화 하기 위한 단일 솔루션이 없습니다. 예를 들어 일괄 처리의 단일 행 점수 매기기에 대해 캐싱이 수행 됩니다. 따라서 후속 점수 매기기 작업은 훨씬 빠르지만 모델 및 R 런타임이 다시 로드 되지 않습니다. [네이티브 점수 매기기](../sql-native-scoring.md) 를 사용 하 여 R 런타임을 완전히 로드 하지 않도록 할 수도 있습니다.

큰 모델을 학습 하거나 큰 일괄 처리로 점수를 매기는 경우 데이터 이동 방지, 스트리밍 및 병렬 처리의 이점에 비해 오버 헤드가 최소화 될 수 있습니다. 추가 성능 지침은 다음 블로그 게시물을 참조 하세요.

+ [R을 사용 하 여 초당 100만 개 트랜잭션 사기 행위 감지](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>리소스

다음은 이러한 테스트 개발에 사용 되는 정보, 도구 및 스크립트에 대 한 링크입니다.

+ 성능 테스트 스크립트 및 데이터에 대 한 링크: [SQL Server 최적화 학습을 위한 샘플 데이터 및 스크립트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 다시 시작 일치 솔루션을 설명 하는 문서: [SQL Server R Services에 대 한 최적화 팁과 요령](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ 다시 시작 일치 솔루션에 대해 SQL 최적화에 사용 되는 스크립트: [GitHub 리포지토리](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Windows server 관리에 대 한 자세한 정보

+ [How to determine the appropriate page file size for 64-bit versions of Windows](https://support.microsoft.com/kb/2860880)(Windows 64비트 버전에 적절한 페이지 파일 크기를 결정하는 방법)

+ [NUMA 이해](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server NUMA를 지 원하는 방법](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>SQL Server 최적화에 대 한 자세한 정보

+ [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [메모리 액세스에 최적화 된 테이블 소개](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [데모: 메모리 내 OLTP의 성능 향상](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [데이터 압축](../../relational-databases/data-compression/data-compression.md)

+ [테이블 또는 인덱스에 압축 사용](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [테이블 또는 인덱스에서 압축 해제](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>SQL Server 관리에 대해 알아보기

+ [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)

+ [Resource Governor 소개](https://technet.microsoft.com/library/bb895232.aspx)

+ [R Services에 대한 리소스 관리](resource-governance-for-r-services.md)

+ [R에 대 한 리소스 풀을 만드는 방법](how-to-create-a-resource-pool-for-r.md)

+ [Resource Governor 구성 예제](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Tools

+ [DISKSPD storage load generator/performance test tool](https://github.com/microsoft/diskspd)(DISKSPD 저장소 로드 생성기/성능 테스트 도구)

+ [FSUtil utility reference](https://technet.microsoft.com/library/cc753059.aspx)(FSUtil 유틸리티 참조)


## <a name="other-articles-in-this-series"></a>이 시리즈의 다른 문서

[R에 대 한 성능 조정-소개](sql-server-r-services-performance-tuning.md)

[R SQL Server 구성에 대 한 성능 조정](sql-server-configuration-r-services.md)

[R의 성능 튜닝-R 코드 및 데이터 최적화](r-and-data-optimization-r-services.md)

[성능 튜닝-사례 연구 결과](performance-case-study-r-services.md)
