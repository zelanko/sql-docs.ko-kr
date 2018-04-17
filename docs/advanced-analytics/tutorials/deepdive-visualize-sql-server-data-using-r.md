---
title: R (SQL과 R 심층 분석)를 사용 하 여 SQL Server 데이터를 시각화 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 923b8201b6948a93f0994306269c0d3338f54c2d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
#  <a name="visualize-sql-server-data-using-r-sql-and-r-deep-dive"></a>R (SQL과 R 심층 분석)를 사용 하 여 SQL Server 데이터를 시각화 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 의 향상된 패키지에는 확장성과 병렬 처리에 최적화된 여러 함수가 포함되어 있습니다. 일반적으로 이러한 함수 앞에는 **rx** 또는 **Rx**가 붙습니다.

이 연습에서는 사용는 **rxHistogram** 함수에서 값의 분포를 볼 수는 _creditLine_ 성별 열입니다.

## <a name="visualize-data-using-rxhistogram"></a>RxHistogram를 사용 하 여 데이터 시각화

1. 다음 R 코드를 사용하여 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 함수를 호출하고 수식 및 데이터 원본을 전달합니다. 처음에 이 코드를 로컬로 실행하여 예상 결과 및 걸리는 시간을 확인할 수 있습니다.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    내부적으로 **rxHistogram** 은 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 패키지에 포함된 **rxCube** 함수를 호출합니다. **rxCube** 계산 열 수식에 지정 된 각 변수에 대 한 열이 포함 된 단일 목록 (또는 데이터 프레임)을 출력 합니다.
    
2. 이제 원격 SQL Server 컴퓨터에 계산 컨텍스트를 설정 하 고 실행 **rxHistogram** 다시 합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. 같은 데이터 원본을 사용하므로 결과는 정확히 같지만, 계산은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 수행됩니다.  그런 다음 결과가 로컬 워크스테이션에 반환되어 그려집니다.
   
![히스토그램 결과](media/rsql-sue-histogramresults.jpg "히스토그램 결과")

4. 호출할 수도 있습니다는 **rxCube** 함수 및 함수를 그래프에 표시 되는 R에 결과 전달 합니다.  예를 들어 다음 예제에서는 **rxCube** 를 사용하여 *numTrans* 및 *numIntlTrans* 의 모든 조합에 대해 *fraudRisk*의 평균을 계산합니다.
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    그룹 평균을 계산하는 데 사용되는 그룹을 지정하려면 `F()` 표기법을 사용합니다. 이 예제에서는 `F(numTrans):F(numIntlTrans)` 나타냅니다 변수에 정수 `_numTrans` 및 `numIntlTrans` 각 정수 값에 대 한 수준으로 범주 변수로 처리 해야 합니다.
  
    낮은 임계값과 높은 수준의 데이터 원본에 이미 추가 된 때문에 `sqlFraudDS` (사용 하는 `colInfo` 매개 변수), 수준 히스토그램에 자동으로 사용 됩니다.
  
5. 기본 반환 값의 **rxCube** 는 *rxCube 개체*, 교차 집계를 나타냅니다. 그러나 [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) 함수를 사용하여 R의 표준 그리기 함수 중 하나에서 쉽게 사용할 수 있는 데이터 프레임으로 결과를 변환할 수 있습니다.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **rxCube** 함수는 선택적 인수를 포함 *returnDataFrame* = **TRUE**, 하는 직접 결과 데이터 프레임으로 변환 하는 데 사용할 수 없습니다. 예를 들어:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    그러나 **rxResultsDF** 출력이 훨씬 더 명확하며 원본 열의 이름을 유지합니다.
  
6. 사용 하 여 열 지도 만들려면 다음 코드를 실행 하는 마지막으로 `levelplot` 에서 함수는 **격자** 모든 R 배포에 포함 되어 있는 패키지입니다.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **결과**
  
    ![산점도 결과](media/rsql-sue-scatterplotresults.jpg "산점도 결과")
  
이 빠른 분석에서도 트랜잭션 수와 국제 트랜잭션 수 둘 다에서 사기 위험이 증가하는 것을 확인할 수 있습니다.

에 대 한 자세한 내용은 **rxCube** 함수와 크로스탭 일반적으로 참조 [RevoScaleR을 사용 하 여 데이터 요약](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)합니다.

## <a name="next-step"></a>다음 단계

[SQL Server 데이터를 사용 하 여 R 모델 만들기](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>이전 단계

[R 스크립트 만들기 및 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
