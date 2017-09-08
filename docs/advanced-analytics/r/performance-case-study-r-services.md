---
title: "R 서비스-결과 및 리소스에 대 한 성능 | Microsoft Docs"
ms.custom: 
ms.date: 07/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 8
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f14e3d744a6d65891f6162bf63e69d682d08a971
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="performance-for-r-services-results-and-resources"></a>R 서비스에 대 한 성능: 결과 및 리소스

이 문서는 네 번째 및 R 서비스에 대 한 성능 최적화를 설명 하는 일련의 최종 합니다. 이 문서에는 메서드, 결과, 및 다양 한 최적화 메서드를 테스트 하는 두 개의 사례 연구 결론 요약 되어 있습니다.

두 사례 연구에는 다른 목표 있었습니다.

+ 첫 번째 사례 연구 R Services 개발 팀에서 하는 방법을 선택 영향이 측정 되 고 특정 최적화 기법
+ 두 번째 사례 연구는 데이터 과학자 팀로 실험 특정 대량 점수 매기기 시나리오에 대 한 최상의 최적화 효과 확인 하는 여러 메서드.

이 항목에서는 첫 번째 사례 연구의 자세한 결과 보여 줍니다. 두 번째 사례 연구에 대 한 요약 전체 결과 설명합니다. 이 항목의 끝에 있는 모든 스크립트 및 예제 데이터 및 원래 작성자가 사용 되는 리소스 링크를 찾을 수 있습니다.

## <a name="performance-case-study-airline-dataset"></a>성능 사례 연구: Airline 데이터 집합

SQL Server R Services 개발 팀이 사례 연구는 다양 한 최적화의 효과 테스트합니다. 단일 rxLogit 모델을 만들 및 점수 매기기 Airline 데이터 집합에 수행 합니다. 최적화는 교육 및 개별 영향을 평가 하는 프로세스를 평가 하는 동안 적용 했습니다.

- Github: [예제 데이터 및 스크립트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) SQL Server 최적화 연구

### <a name="test-methods"></a>테스트 메서드

1. Airline 데이터 집합에는 M 10 개의 행의 단일 테이블 구성 됩니다. 다운로드 하 고 SQL Server에 대량 로드 합니다.
2. 테이블의 6 개 복사본 수행 됩니다.
3. 다양 한 수정 된 페이지 압축을 행 압축, 인덱싱, 등 칼럼 형식 데이터 저장소와 같은 SQL Server 기능을 테스트 하는 테이블의 복사본에 적용 됩니다.
4. 각 최적화가 적용 전과 후 성능 측정 되었습니다.

| 테이블 이름| Description|
|------|------|
| *airline* | `rxDataStep`을 사용하여 원래 xdf 파일에서 변환된 데이터|                          |
| *airlineWithIntCol*   | 문자열이 아닌 정수에서 변환된 *DayOfWeek*. *rowNum* 열도 추가합니다.|
| *airlineWithIndex*    | *airlineWithIntCol* 테이블과 데이터가 같지만 *rowNum* 열을 사용하는 단일 클러스터형 인덱스 포함.|
| *airlineWithPageComp* | *airlineWithIndex* 테이블과 데이터가 같지만 페이지 압축이 사용됨. *CRSDepTime* 및 *ArrDelay*에서 계산된 두 개의 열 *CRSDepHour* 및 *Late*도 추가합니다. |
| *airlineWithRowComp*  | *airlineWithIndex* 테이블과 데이터가 같지만 행 압축이 사용됨. *CRSDepTime* 및 *ArrDelay*에서 계산된 두 개의 열 *CRSDepHour* 및 *Late*도 추가합니다. |
| *airlineColumnar*     | 단일 클러스터형 인덱스가 포함된 열 형식 저장소. 이 테이블은 정리된 csv 파일의 데이터로 채워집니다.|

다음이 단계 중 각 테스트 구성 되었습니다.

1. 각 테스트 전에 R 가비지 수집이 도출되었습니다.
2. 로지스틱 회귀 모델은 테이블 데이터에 따라 만들어졌습니다. 각 테스트에 대한 *rowsPerRead* 값이 500000으로 설정되었습니다.
3. 점수는 학습 된 모델을 사용 하 여 생성 된
4. 각 테스트 6 번 실행 합니다. 첫 번째 실행 ("콜드 실행")의 시간 삭제 되었습니다. 가끔 이상 값을 허용 하는 **최대** 나머지 5 개의 실행 간에 시간도 삭제 되었습니다. 나머지 4회 실행의 평균을 사용하여 각 테스트의 평균 경과 시간을 계산했습니다.
5. 사용 하 여 테스트 실행의 *reportProgress* 매개 변수 (보고서 시간 및 진행률 =) 값 3 사용 합니다. 각 출력 파일 IO, 전환 시간 및 시간 계산에 사용 된 시간에 대 한 정보를 포함 합니다. 이러한 시간은 문제 해결 및 진단에 유용하게 사용됩니다.
6. 또한 콘솔 출력은 출력 디렉터리에 파일을 지시 합니다.
7. 테스트 스크립트 실행에서 평균 시간을 계산 하는 데 이러한 파일이에서 시간을 처리 합니다.

예를 들어 다음 결과 단일 테스트 까지의 시간입니다. 필요한 주 타이밍은 **총 읽기 시간**(IO 시간) 및 **전환 시간**(계산을 위한 프로세스 설정 시의 오버헤드)입니다.

**샘플 타이밍**

```
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

다운로드 RevoScaleR 함수 또는 R 서비스 문제를 해결 하기 위해 테스트 스크립트를 수정 하는 것이 좋습니다.

### <a name="test-results-all"></a>테스트 결과 (모두)

이 여기서 각 테스트에 대 한 이전 및 이후 결과 비교합니다.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>압축 및 칼럼 형식 테이블 저장소와 데이터 크기

첫 번째 테스트 압축 및 데이터의 크기를 줄이려면 열 테이블의 사용을 비교 합니다.

| 테이블 이름            | 행     | 예약됨   | 데이터       | index_size | 사용 안 함  | 단축 비율(%)(예약됨) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816KB | 2972160KB | 6128KB    | 528KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784KB  | 623744KB  | 1352KB    | 688KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520KB | 1258880KB | 2552KB    | 1088KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992KB  | 201624KB  | n/a        | 368KB  | 93%                 |

**결론을 내리기**

가장 큰 데이터 크기를 줄이는 뒤에 페이지 압축으로 columnstore 인덱스를 적용 하 여 수행 됩니다.

#### <a name="effects-of-compression"></a>압축의 효과

이 테스트에는 행 압축과 페이지 압축 압축의 장점을 비교합니다. 사용 하 여 모델을 학습 `rxLinMod` 세 개의 서로 다른 데이터 테이블의 데이터에 대해 합니다. 모든 테이블에 같은 수식 및 쿼리가 사용되었습니다.

| 테이블 이름            | 테스트 이름       | numTasks | 평균 시간 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression-병렬| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression-병렬 | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression-병렬  | 4        | 5.2375       |

**결론을 내리기**

압축만가 도움이 것 같습니다. 이 예제에서는 압축을 처리 하는 CPU의 폭주 IO 시간에서 감소에 대 한 보정 합니다.

하지만 *numTasks*를 4로 설정하여 테스트를 병렬로 실행하면 평균 시간이 감소합니다.

더 큰 데이터 집합의 경우 압축의 효과가 눈에 클 수 있습니다. 압축은 데이터 집합 및 값에 따라 달라지므로 압축이 데이터 집합에 미치는 영향을 확인하려면 실험이 필요할 수 있습니다.

### <a name="effect-of-windows-power-plan-options"></a>Windows 전원 관리 옵션의 효과

이 실험에서 `rxLinMod`는 *airlineWithIntCol* 테이블과 함께 사용되었습니다. Windows 전원 관리 옵션 설정 되어 **균형** 또는 **고성능**합니다. 모든 테스트의 경우 *numTasks*는 1로 설정되었습니다. 테스트가 6 번 실행 및 결과의 가변성을 조사할 전원 옵션을 모두에서 두 번 수행 합니다.

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

**결론을 내리기**

Windows를 사용 하는 경우 보다 일관 되 고 더 빠르게 실행 시간은입니다 **고성능** 전원 관리 옵션입니다.

#### <a name="using-integer-vs-strings-in-formulas"></a>수식에 문자열 및 정수를 사용 하 여

이 테스트 문자열 요인의 일반적인 문제를 방지 하기 위해 R 코드를 수정 하는의 영향을 평가 합니다. 특히, 모델을 사용 하 여 학습 된 `rxLinMod` 두 테이블을 사용 하 여: 요인 정수로 저장 된 두 번째 테이블의; 첫 번째 요소는 문자열로 저장 됩니다.

+ 에 대 한는 *airline* 문자열 테이블에서 [DayOfWeek] 열을 포함 합니다. _colInfo_ 비율 수준 (월요일, 화요일,...)를 지정 하려면 매개 변수가 사용 되었으므로

+  에 대 한는 *airlineWithIndex* 테이블 [DayOfWeek]는 정수입니다. _colInfo_ 매개 변수가 지정 되지 않았습니다.

+ 두 경우에 모두 같은 수식이 사용되었습니다. `ArrDelay ~ CRSDepTime + DayOfWeek`.

| 테이블 이름          | 테스트 이름   | 평균 시간 |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**결론을 내리기**

요소에 대 한 문자열이 아닌 정수를 사용 하는 경우 분명 한 이점이 있습니다.

### <a name="avoiding-transformation-functions"></a>변환 함수를 방지합니다.

사용 하 여 모델을 학습 하는이 테스트에서는 `rxLinMod`, 코드는 두 실행 간에 변경 되었습니다.

+ 첫 번째 실행에서 변환 함수를 모델 작성의 일부로 적용 되었습니다. 
+ 두 번째 실행에서 기능 값 변환 함수를 필요한 수 있는지를 사용할 수 및 사전 계산 했습니다.

| 테스트 이름             | 평균 시간 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**결론을 내리기**

경우에 더 짧은 학습 시간은 **하지** 변환 함수를 사용 하 여 합니다. 즉, 모델을 학습 더 빠르게 미리 계산 된 테이블에서 유지 되는 열을 사용 하는 경우.

공간 절약에 대해서는 많은 많은 변환을 더 큰 데이터 집합 않은 있을 경우 수 해야 (\> 100 M).

### <a name="using-columnar-store"></a>열 형식 저장소를 사용 하 여

이 테스트는 칼럼 형식 데이터 저장소와 인덱스를 사용 하는 성능 이점을 평가 합니다. 사용 하 여 동일한 모델을 학습 `rxLinMod` 및 데이터 변환은 없습니다.

+ 첫 번째 실행에서 데이터 테이블 표준 행 저장소를 사용 합니다.
+ 두 번째 실행에서 열 저장소 사용 되었습니다.

| 테이블 이름         | 테스트 이름 | 평균 시간 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**결론을 내리기**

성능이 표준 행 저장소를 사용 하 여 보다 칼럼 형식 저장소 사용 향상 됩니다. 더 큰 데이터 집합에 예상 되는 성능에 큰 차이가 (\> 100 M).

### <a name="effect-of-using-the-cube-parameter"></a>큐브 매개 변수를 사용 하 여의 효과

결정 하는 것이 테스트의 목적은 여부 RevoScaleR에는 미리 계산 된 사용을 위한 옵션 **큐브** 매개 변수는 성능을 향상 시킬 수 있습니다. 사용 하 여 모델을 학습 `rxLinMod`,이 수식을 사용 하 여:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

요인 표에 *DayOfWeek* 문자열로 저장 합니다.

| 테스트 이름     | 큐브 매개 변수 | numTasks | 평균 시간 | 단일 행 예측 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**결론을 내리기**

명확 하 게 큐브 매개 변수 인수를 사용에는 성능이 향상 됩니다.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>MaxDepth rxDTree 모델에 대 한 변경의 영향

이 실험에는 `rxDTree` 알고리즘에서 모델을 만드는 데 사용 된 *airlineColumnar* 테이블입니다. 이 테스트의 경우 *numTasks*는 4로 설정되었습니다. 여러 다른 값 *maxDepth* 트리 깊이 변경 실행된 시간에 미치는 영향을 보여 주기 위해 사용 되었습니다.

| 테스트 이름       | maxDepth | 평균 시간 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**결론을 내리기**

트리의 수준이 증가 하면 총 노드 수는 기하급수적으로 늘어납니다. 또한 모델을 만들기 위한 경과 시간 크게 증가 합니다.

### <a name="prediction-on-a-stored-model"></a>저장 된 모델에 대 한 예측

이 테스트의 목적은 현재 실행 중인 코드의 일부로 생성 대신 학습 된 모델은 SQL Server 테이블에 저장 하는 경우 점수 매기기에 성능에 영향을 결정 하는 것 이었습니다. 상태 평가 대 한 저장 된 모델은 데이터베이스에서 로드 하 고 예측의 메모리 (로컬 계산 컨텍스트)에 한 행 데이터 프레임을 사용 하 여이 생성 됩니다.

테스트 결과 모델을 저장할 시간 및 모델을 로드 하 고 예측 하는 데 걸린 시간을 보여 줍니다.

| 테이블 이름 | 테스트 이름 | 평균 시간(모델 학습) | 모델 저장/로드 시간|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2.09(예측 시간 포함) |

**결론을 내리기**

테이블에서 로드 하는 학습된 된 모델은 예측을 수행 하는 빠른 방법은입니다. 모델을 만들고 동일한 스크립트에 모든 점수 매기기를 수행 하지 않는 것이 좋습니다.

## <a name="case-study-optimization-for-resume-matching-task"></a>사례 연구: 일치 작업 다시 시작에 대 한 최적화

Resume 일치 하는 모델은 Microsoft 데이터 과학자를 SQL Server에서 R 코드의 성능을 테스트 하 고 확장 및 엔터프라이즈 수준의 솔루션을 지원 하기 위해 데이터 과학자를 사용 하려면 Ke Huang가 개발 되었습니다.

### <a name="methods"></a>메서드

MicrosoftML와 RevoScaleR 패키지는 큰 데이터 집합과 관련 된 복잡 한 R 솔루션의 예측 모델의 학습에 사용 되었습니다. SQL 쿼리 및 R 코드와 동일한 기능 이었습니다. SQL Server가 설치 된 단일 Azure VM에서 모든 테스트 수행 되었습니다. 그런 다음 작성자와 SQL Server에서 제공 하는 이러한 최적화 없는 점수 매기기 시간을 비교:

- 메모리 내 테이블
- Soft-NUMA
- 리소스 관리자

R 스크립트 실행에 소프트 NUMA의 영향을 평가 하기 위해 데이터 과학 팀 20 개의 실제 코어를 Azure 가상 컴퓨터에서 솔루션을 테스트 했습니다. 이러한 물리적 코어에서 4 개의 소프트 NUMA 노드 각 노드에 5 개의 코어를 포함 자동으로 생성 되었습니다.

CPU affinitization resume 일치 하는 시나리오에서는 R 작업에 미치는 영향을 평가 하기 위해 적용 되었습니다. 4 개의 **SQL 리소스 풀** 4 **외부 리소스 풀** 만들어진 CPU 선호도 Cpu의 동일한 집합은 사용 되는 각 노드에 하도록 지정 했습니다.

하드웨어 사용률을 최적화 하기 위해 다른 작업 그룹에 할당 된 각 리소스 풀. 이유는 소프트 NUMA 및 CPU 선호도 실제 NUMA 노드;에 있는 실제 메모리를 나눌 수 없습니다. 따라서 정의 동일한 실제 NUMA 노드를 기반으로 하는 모든 소프트 NUMA 노드 해야 사용 메모리 같은 운영 체제 메모리 블록에 합니다. 즉, 메모리 프로세서로 선호도 없는 경우

다음 프로세스는이 구성을 만드는 데 사용 된:

1. SQL Server에 기본적으로 할당 된 메모리의 양을 줄입니다.

2. 동시에 R 작업 실행을 위한 4 개의 새 풀을 만듭니다.

3. 각 작업 그룹은 리소스 풀과 연결 되도록 네 개의 작업 그룹을 만듭니다.

4. 새 작업 그룹 및 할당 된 리소스 관리자를 다시 시작 합니다.

5. 분류자 사용자 정의 함수 (UDF) 다른 작업 그룹에 대해 다른 작업을 할당을 만듭니다.

6. 함수를 사용 하 여 적절 한 작업 그룹에 대 한 리소스 관리자 구성을 업데이트 합니다.

### <a name="results"></a>결과

연구 resume 일치에서 최상의 성능을 수 있었던 구성을 다음과 같습니다.

-   내부 리소스 풀 (SQL Server) 용 4 개

-   (외부 스크립트 작업)에 대 한 외부 리소스 풀 4 개

-   각 리소스 풀은 특정 작업 그룹

-   각 리소스 풀은 서로 다른 Cpu에 할당 된

-   최대 내부 메모리 사용 (SQL Server 용) = 30%

-   R 세션에서 사용할 최대 메모리 = 70%입니다.

Resume 일치 하는 모델에 대 한 외부 스크립트 사용 하 여 많은 였으며 다른 데이터베이스 엔진 서비스를 실행 했습니다. 따라서 외부 스크립트에 할당 된 리소스는 스크립트 성능에 대 한 최상의 구성을 이전의 70%로 증가 되었습니다.

이 구성 된 값이 서로 다른 실험 하 여에 도착 합니다. 다른 하드웨어 또는 다른 솔루션을 사용 하는 경우에 가장 적합 한 구성 달라질 수 있습니다.

> [!IMPORTANT]
> 케이스에 대 한 최상의 구성의 찾는 데 실험!

최적화 된 솔루션에서는 1.1 백만 행의 데이터 (100 기능)으로 20 코어 컴퓨터에서 8.5 초 이내에 점수가 매겨진 합니다. 최적화에는 점수 매기기 시간을 기준으로 성능이 크게 향상 되었습니다.

결과 있는 항목을 또한 제안는 **기능의 숫자** 점수 매기기 시간에 큰 영향입니다. 예측 모델에 사용 된 많은 기능이 향상 훨씬 더 중요 했습니다.

이 블로그 게시물 및에 대 한 자세한 내용은 해당 자습서를 읽는 것이 좋습니다.

-   [SQL Server의 기계 학습을 위한 최적화 팁과 힌트](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

## <a name="resources"></a>리소스

정보, 도구 및 이러한 테스트의 개발에 사용 되는 스크립트에 대 한 링크는 다음과 같습니다.

+ 성능 테스트 스크립트 및 데이터에 대 한 링크: [예제 데이터 및 SQL Server 최적화 연구에 대 한 스크립트](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Resume 일치 하는 솔루션을 설명 하는 문서: [최적화 팁과 요령 SQL Server R Services에 대 한](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Resume 일치 하는 솔루션에 대 한 SQL 최적화에 사용 되는 스크립트: [GitHub 리포지토리](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Windows server 관리에 대 한 자세한 내용은

+ [How to determine the appropriate page file size for 64-bit versions of Windows](https://support.microsoft.com/kb/2860880)(Windows 64비트 버전에 적절한 페이지 파일 크기를 결정하는 방법)

+ [NUMA 이해](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server의 NUMA 지원 방법](https://technet.microsoft.com/library/ms180954.aspx)

+ [소프트 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>SQL Server 최적화에 대 한 자세한 내용은

+ [인덱스 다시 구성 및 다시 작성](../../relational-databases\indexes\reorganize-and-rebuild-indexes.md)

+ [메모리 액세스에 최적화 된 테이블 소개](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [데모: 메모리 내 OLTP 성능 향상](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [데이터 압축](../../relational-databases/data-compression/data-compression.md)

+ [테이블 또는 인덱스에 압축 사용](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [테이블 또는 인덱스에서 압축 해제](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>SQL Server를 관리 하는 방법에 대 한 자세한 내용은

+ [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)

+ [리소스 관리자 소개](https://technet.microsoft.com/library/bb895232.aspx)

+ [R Services에 대한 리소스 관리](resource-governance-for-r-services.md)

+ [R에 대 한 리소스 풀을 만드는 방법](how-to-create-a-resource-pool-for-r.md)

+ [리소스 관리자 구성의 예](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Tools

+ [DISKSPD storage load generator/performance test tool](https://github.com/microsoft/diskspd)(DISKSPD 저장소 로드 생성기/성능 테스트 도구)

+ [FSUtil utility reference](https://technet.microsoft.com/library/cc753059.aspx)(FSUtil 유틸리티 참조)


## <a name="other-articles-in-this-series"></a>이 시리즈의 기타 기사

[성능-R에 대 한 튜닝 소개](sql-server-r-services-performance-tuning.md)

[R-SQL Server 구성에 대 한 성능 조정](sql-server-configuration-r-services.md)

[R-R에 대 한 성능 조정 코드 및 데이터 최적화](r-and-data-optimization-r-services.md)

[성능 튜닝-사례 연구 결과](performance-case-study-r-services.md)

