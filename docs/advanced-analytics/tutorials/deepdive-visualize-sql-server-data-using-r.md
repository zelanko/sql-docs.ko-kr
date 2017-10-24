---
title: "R을 사용하여 SQL Server 데이터 시각화(데이터 과학 심층 분석) | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 023958a137515c519fe8d73e1ce1181dc7579356
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="visualize-sql-server-data-using-r"></a>R을 사용하여 SQL Server 데이터 시각화

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 의 향상된 패키지에는 확장성과 병렬 처리에 최적화된 여러 함수가 포함되어 있습니다. 일반적으로 이러한 함수 앞에는 *rx* 또는 *Rx*가 붙습니다.

이 연습에서는 **rxHistogram** 함수를 사용하여 _creditLine_ 열 값의 성별 분포를 확인합니다.

## <a name="visualize-data-using-rxhistogram"></a>RxHistogram를 사용 하 여 데이터 시각화

1. 다음 R 코드를 사용 하 여 rxHistogram 함수를 호출 하 고 수식 및 데이터 소스를 전달 합니다. 처음에 이 코드를 로컬로 실행하여 예상 결과 및 걸리는 시간을 확인할 수 있습니다.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    RxHistogram에 포함 되어 있는 rxCube 함수를 호출 하는 내부적으로 **RevoScaleR** 패키지 합니다. 계산 열 수식에 지정 된 각 변수에 대 한 열이 포함 된 단일 목록 (또는 데이터 프레임)를 출력 하는 rxCube 함수입니다.
    
2. 이제, 원격 SQL Server 컴퓨터에 계산 컨텍스트를 설정 하 고 rxHistogram를 다시 실행 합니다.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. 같은 데이터 원본을 사용하므로 결과는 정확히 같지만, 계산은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 수행됩니다.  그런 다음 결과가 로컬 워크스테이션에 반환되어 그려집니다.
   
![히스토그램 결과](media/rsql-sue-histogramresults.jpg "히스토그램 결과")

4. RxCube 함수를 호출 하 고 결과 R 그리기 함수에 전달할 수도 있습니다.  다음 예제에서는 rxCube을 사용 하 여 평균을 계산 하는 예를 들어 *fraudRisk* 의 모든 조합에 대해 *numTrans* 및 *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    그룹 평균을 계산하는 데 사용되는 그룹을 지정하려면 `F()` 표기법을 사용합니다. 이 예제에서 `F(numTrans):F(numIntlTrans)` 는 정수 값마다 하나의 수준을 사용하여 _numTrans_ 및 _numIntlTrans_ 변수의 정수를 범주 변수로 처리하도록 지정합니다.
  
    하위 및 상위 수준이 데이터 원본 *sqlFraudDS* 에 이미 추가되었으므로( *colInfo* 매개 변수 사용) 해당 수준이 히스토그램에서 자동으로 사용됩니다.
  
5. RxCube의 반환 값은 기본적으로는 *rxCube 개체*, 교차 집계를 나타냅니다. 그러나 **rxResultsDF** 함수를 사용하여 R의 표준 그리기 함수 중 하나에서 쉽게 사용할 수 있는 데이터 프레임으로 결과를 변환할 수 있습니다.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    > [!TIP]
    > 
    > RxCube 함수는 선택적 인수를 포함 하는 참고 *returnDataFrame* = TRUE, 변환할 결과 데이터 프레임을 직접 사용할 수 있습니다. 예를 들어
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
    >   
    > 그러나 이러한 rxResultsDF의 출력을 더 간단 이며 원본 열의 이름을 유지 합니다.
  
6. 사용 하 여 열 지도 만들려면 다음 코드를 실행 하는 마지막으로 `levelplot` 에서 함수는 **격자** 모든 R 배포에 포함 되어 있는 패키지입니다.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **결과**
  
    ![산점도 결과](media/rsql-sue-scatterplotresults.jpg "산점도 결과")
  
이 빠른 분석에서도 트랜잭션 수와 국제 트랜잭션 수 둘 다에서 사기 위험이 증가하는 것을 확인할 수 있습니다.

일반적으로 크로스탭와 rxCube 함수에 대 한 자세한 내용은 참조 하십시오. [데이터 요약](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries)합니다.

## <a name="next-step"></a>다음 단계

[모델 만들기](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>이전 단계

[2단원: R 스크립트 만들기 및 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)



