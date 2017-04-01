---
title: "성능 사례 연구 (R 서비스) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 8
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 6
---
# 성능 사례 연구 (R 서비스)

이전 섹션에서 제공 하는 지침의 효과 보여 주기 위해 항공사 데이터 집합에서 테이블을 사용 하 여 테스트 실행 되었습니다. 

## 테스트 및 예제 데이터

각 테이블의 10m 행과 6 개의 테이블이 있습니다.

| 테이블 이름 | Description |
| ---------- | ----------- |
| _항공사_ | 사용 하 여 원래 xdf 파일에서 변환 된 *rxDataStep*합니다. |
| _airlineWithIntCol_ | *DayOfWeek* 문자열 대신 정수를 변환 합니다. 또한 추가 *rowNum* 열입니다. |
| _airlineWithIndex_ | 와 동일한 데이터는 *airlineWithIntCol* 테이블 하지만 사용 하 여 단일 클러스터형된 인덱스는 *rowNum* 열입니다. |
| _airlineWithPageComp_ | 와 동일한 데이터는 *airlineWithIndex* 테이블 하지만 페이지 압축을 사용 합니다. 또한 두 개의 열을 추가 *CRSDepHour* 및 *늦게*, 에서 계산 되 고 있는 *CRSDepTime* 및 *열*합니다. |
| _airlineWithRowComp_ | 와 동일한 데이터는 *airlineWithIndex* 테이블 하지만 행 압축을 사용 합니다. 또한 두 개의 열을 추가 *CRSDepHour* 및 *늦게* 에서 계산 되 고 있는 *CRSDepTime* 및 *열*합니다. 
| _airlineColumnar_ | 단일 클러스터형된 인덱스와 칼럼 형식 저장소입니다. 이 테이블은 정리한 csv의 데이터로 채워집니다 파일입니다. |

테스트에 사용 되는 예제 데이터에 대 한 링크 뿐 아니라이 섹션에 설명 하는 테스트를 수행 하는 데 스크립트에서 사용할 수 있는 [https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)합니다.

각 테스트가 실행 된 6 번 (차가움 실행) 첫 번째 실행의 시간 삭제 되었습니다. 필요에 따른 이상 값을 허용 하려면 나머지 5 실행에 대 한 최대 시간 삭제 되었습니다. 각 테스트의 평균 경과 된 런타임 계산 하는 데 4 개의 남은 실행의 평균을 가져왔습니다. 각 테스트 전에 R 가비지 수집이 발생 했습니다. 값 *rowsPerRead* 각 테스트 500000로 설정 되었습니다.

## 압축 및 칼럼 형식 저장소 테이블을 사용 하는 경우에 데이터 크기

다음은 압축 및 열 테이블을 사용 하 여 데이터의 크기를 줄이기 위해의 결과입니다.

| 테이블 이름 | 행 | 예약됨 | Data | index_size | 사용 안 함 | (예약 됨)를 저장 하는 % |
| ---------- | ---- | -------- | ---- | ---------- | ------ | ------------------- |
| airlineWithIndex | 10000000 | 2978816 (KB) | 2972160 (KB) | 6128 (KB) | 528 (KB) | 0 |
| airlineWithPageComp | 10000000 | 625784 (KB) | 623744 (KB) | 1352 (KB) | 데 688 (KB) | 79% |
| airlineWithRowComp | 10000000 | 1262520 (KB) | 1258880 (KB) | 2552 (KB) | 1088 (KB) | 58% |
| airlineColumnar | 9999999 | 201992 (KB) | 201624 (KB) | n/a | 368 (KB) | 93% |

## 정수 vs를 사용합니다. 수식에는 문자열

이 실험에서는 `rxLinMod` 항공사 표 사용한 (여기서 *DayOfWeek* 문자열) 및 *airlineWithIndex* (여기서 *DayOfWeek* 은 정수). 첫 번째 경우에 대 한 `colInfo` 비율 수준을 지정 하는 데 사용 되었습니다 (`Monday`, `Tuesday`, ...). 두 번째 `colInfo` 지정 되지 않았습니다. 두 경우 모두에 동일한 수식 사용 되었습니다. 사용 하는 수식은 `ArrDelay ~ CRSDepTime + DayOfWeek`합니다. 다음 결과는 정수 및 문자열을 사용 하는 이점은 명확 하 게 보여 줍니다.

| 테이블 이름 | 테스트 이름 | 평균 시간입니다. |
| ---------- | --------- | ------------ |
| 항공사 | FactorCol | 10.72 |
| airlineWithIntCol | IntCol | 3.4475 |

## 압축을 사용 하 여

이 실험에서는 `rxLinMod` 사용한는 *airlineWithIndex*, *airlineWithPageComp*, 및 *airlineWithRowComp* 테이블입니다. 동일한 수식 및 쿼리는 모든 테이블에 사용 되었습니다. 

| 테이블 이름 | 테스트 이름 | numTasks | 평균 시간입니다. |
| ---------- | --------- | -------- | ------------ |
| airlineWithIndex | NoCompression | 1 | 5.6775 |
| &nbsp; | &nbsp; | 4 | 5.1775 |
| airlineWithPageComp | PageCompression | 1 | 6.7875 |
| &nbsp; | &nbsp; | 4 | 5.3225 |
| airlineWithRowComp | RowCompression | 1 | 6.1325 |
| &nbsp; | &nbsp; | 4 | 5.2375 |

해당 압축만 참고 (*numTasks* 1로 설정) 하지 않는 것이 예에서 도움말 증가 압축을 처리 하는 CPU에 IO 시간 감소에 대 한 보상으로 합니다. 그러나 테스트는 실행 동시에 설정 하 여 *numTasks* 4로, 평균 시간을 줄입니다. 더 큰 데이터 집합에 대 한 압축의 효과 따라 더 두드러질 수 있습니다. 압축 효과 압축에 데이터 집합에 대해 확인 하려면 실험 필요할 수 있으므로 데이터 집합 및 값에 따라 달라 집니다.

## 변환 함수를 방지합니다.

이 실험에서는 `rxLinMod` 를 둘 다와 변환 함수를 사용 하지 않고 airlineWithIndex 테이블과 함께 사용 합니다.  

| 테스트 이름 | 평균 시간입니다. |
| --------- | ------------ |
| WithTransformation | 5.1675 |
| WithoutTransformation | 4.7 |

시간에 향상 기능입니다 (테이블에 유지 하 고 미리 계산 된 열 사용) 하는 변환 함수를 사용 하지 않을 때입니다. 더 많은 변환 되는 경우 데이터 집합은 더 큰 (> 100 M)의 공간 절약 훨씬 증가할 수 있습니다.

## 칼럼 형식 저장소를 사용 하 여

이 실험에서는 `rxLinMod` airlineWithIndex 및 airlineColumnar 테이블 된 변환을 사용 하지 않고 사용 되었습니다. 결과 열 저장소 행 저장소 보다 더 잘 수행할 수 있다는 것을 나타냅니다. 큰 데이터 집합 (> 100 M)에서 성능에 큰 차이가 없을 것입니다.  

| 테이블 이름 | 테스트 이름 |평균 시간입니다. |
| ---------- | --------- | ------------ |
| airlineWithIndex | RowStore | 4.67 |
| airlineColumnar | ColStore | 4.555 |

## 큐브 매개 변수의 효과

이 실험에서는 `rxLinMod` 항공사 표는 여기서 `DayOfWeek` 문자열로 저장 됩니다. 사용 하는 수식은 `ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime`합니다. 결과 명확 하 게 사용을 표시 하는 `cube` 성능은 매개 변수를 지원 합니다. 

| 테스트 이름 | 큐브 매개 변수 | numTasks | 평균 시간입니다. | 행이 하나씩 예측 (ArrDelay_Pred) |
| --------- | -------------- | -------- | ------------ | ------------------------------- |
| CubeArgEffect | `cube = F` | 1 | 91.0725 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 44.09 | 9.959204 |
| &nbsp; | `cube = T` | 1 | 21.1125 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 8.08 | 9.959204 |

## MaxDepth rxDTree에 미치는 영향

이 실험에서는 `rxDTree` airlineColumnar 테이블과 함께 사용 됩니다. 여러 다른 값 *maxDepth* 복잡 한 실행된 시간에 미치는 영향을 설명 하기 위해 사용 되었습니다. 깊이 증가 함에 따라 총 노드 수가 기하급수적으로 증가 하 고 경과 된 시간을 크게 증가 합니다. 이 테스트에 대 한 *numTasks* 4로 설정 되었습니다.

| 테스트 이름 | maxDepth | 평균 시간입니다. |
| --------- | -------- | ------------ |
| TreeDepthEffect | 1 | 10.1975 |
| &nbsp; | 2 | 13.2575 |
| &nbsp; | 4 | 19.27 |
| &nbsp; | 8 | 45.5775 |
| &nbsp; | 16 | 339.54 |

## 전원 옵션의 효과

이 실험에서는 `rxLinMod` Windows 전원 옵션으로 균형 조정 고성능에 설정 된 동안 airlineWithIntCol 테이블과 함께 사용 되었습니다. 모든 테스트에 대 한 *numTasks* 1로 설정 되었습니다. 테스트 6 시간, 실행 및 균형 조정된 전원 옵션을 사용 하는 경우 결과의 가변성을 보여 주기 위해 전원 옵션을 모두에서 두 번 수행 합니다. 결과는 번호가 보다 일관 되 고 고성능 전원 옵션에 대 한 빠른 지를 보여 줍니다. 

__고성능__ 전원 옵션:

| 테스트 이름 | 실행 # | 경과 시간 | 평균 시간입니다. |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.57 초 | &nbsp; |
| &nbsp; | 2 | 3.45 초 | &nbsp; |
| &nbsp; | 3 | 3.45 초 | &nbsp; |
| &nbsp; | 4 | 3.55 초 | &nbsp; |
| &nbsp; | 5 | 3.55 초 | &nbsp; |
| &nbsp; | 6 | 3.45 초 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.475 |
| &nbsp; | 1 | 3.45 초 | &nbsp; |
| &nbsp; | 2 | 3.53 초 | &nbsp; |
| &nbsp; | 3 | 3.63 초 | &nbsp; |
| &nbsp; | 4 | 3.49 초 | &nbsp; |
| &nbsp; | 5 | 3.54 초 | &nbsp; |
| &nbsp; | 6 | 3.47 초 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.5075 |

__분산 된__ 전원 옵션:

| 테스트 이름 | 실행 # | 경과 시간 | 평균 시간입니다. |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.89 초 | &nbsp; |
| &nbsp; | 2 | 4.15 초 | &nbsp; |
| &nbsp; | 3 | 3.77 초 | &nbsp; |
| &nbsp; | 4 | 5 초 | &nbsp; |
| &nbsp; | 5 | 3.92 초 | &nbsp; |
| &nbsp; | 6 | 3.8 초 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.91 |
| &nbsp; | 1 | 3.82 초 | &nbsp; |
| &nbsp; | 2 | 3.84 초 | &nbsp; |
| &nbsp; | 3 | 3.86 초 | &nbsp; |
| &nbsp; | 4 | 4.07 초 | &nbsp; |
| &nbsp; | 5 | 4.86 초 | &nbsp; |
| &nbsp; | 6 | 3.75 초 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.88 |

## 저장 된 모델을 사용 하 여 예측

이 실험에서 모델을 만들고 데이터베이스에 저장 합니다. 그런 다음 저장 된 모델 데이터베이스와 메모리 (로컬 계산 컨텍스트)에 한 행 데이터 프레임을 사용 하 여 만든 예측에서 로드 됩니다. 학습 및 모델을 로드 하 고 저장을 예측 하는 데 걸리는 시간은 다음과 같습니다. 이 예측을 수행 하는 빠른 방법을 명확 하 게 합니다. 테스트 결과 모델을 저장할 시간 및 모델을 로드 하 고 예측 하는 데 걸리는 시간을 보여 줍니다. 

| 테이블 이름 | 테스트 이름 | 평균 시간 (모델을 학습) | 시간 저장/부하 모델을 |
| ---------- | --------- | ----- | ----- |
| 항공사 | SaveModel | 21.59 | 2.08 | 
| &nbsp; | LoadModelAndPredict | &nbsp; |  2.09 (예측 하는 시간 포함) |


## 성능 문제 해결

이 섹션에 사용 되는 테스트를 사용 하 여 각 실행에 대 한 출력 파일을 생성 된 *reportProgress* 매개 변수 값을 사용 하 여 테스트에 전달 되는 `3`합니다. 콘솔 출력은 출력 디렉터리에 있는 파일으로 전송 됩니다. 출력 파일 IO, 전환 시간 및 계산 시간에 소요 된 시간에 대 한 정보를 포함 합니다. 이러한 시간은 진단 및 문제 해결에 유용 합니다. 테스트 스크립트를 사용 하는 평균 시간 실행을 통해 다양 한 실행에 대 한 이러한 시간을 처리 합니다. 이러한 스크립트를 테스트 하 고 기술에서 rx 분석 함수를 사용 하 여 문제 해결에 유용할 수 있습니다 프로그램 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 예를 들어 다음은 샘플 번 실행 합니다. 관심의 주요 타이밍은 전체 읽기 (IO time) 시간 (비용 계산에 대 한 프로세스를 설정)으로 전환 하 고 있습니다.

    Running IntCol Test. Using airlineWithIntCol table.  
        run  1  took  3.66  seconds  
        run  2  took  3.44  seconds  
        run  3  took  3.44  seconds  
        run  4  took  3.44  seconds  
        run  5  took  3.45  seconds  
        run  6  took  3.75  seconds  

    Average Time:  3.4425  
                    metric   time    pct 
    1           Total time 3.4425 100.00 
    2 Overall compute time 2.8512  82.82 
    3      Total read time 2.5378  73.72 
    4      Transition time 0.5913  17.18 
    5    Total non IO time 0.3134   9.10 
 
 ## 관련 항목:
 [SQL Server R 서비스 성능 조정 가이드](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [R 서비스에 대 한 SQL Server 구성](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [R 및 데이터 최적화](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)