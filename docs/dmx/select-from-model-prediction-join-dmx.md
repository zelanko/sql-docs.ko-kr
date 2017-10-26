---
title: "SELECT FROM &lt;모델&gt; PREDICTION JOIN (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICTION
- PREDICTION_JOIN
- SELECT
- join
- FROM
- PREDICTION JOIN
dev_langs:
- DMX
helpviewer_keywords:
- prediction joins [DMX]
- PREDICTION JOIN statement
- natural prediction joins [DMX]
- open query predictions
- singleton query predictions [DMX]
- SELECT FROM <model> PREDICTION JOIN statement
ms.assetid: 7ca37fec-4a50-4d79-b1d6-1c7c12176946
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7caf239374a174cc26c2bee349c1a52c805f4de4
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>SELECT FROM &lt;모델&gt; PREDICTION JOIN (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  마이닝 모델을 사용하여 외부 데이터 원본에 있는 열의 상태를 예측합니다. **PREDICTION JOIN** 문이 모델에는 원본 쿼리의 각 사례와 일치 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>인수  
 *n*  
 (선택 사항) 반환할 행의 수를 지정하는 정수입니다.  
  
 *select 식 목록*  
 열 식별자 및 식의 쉼표로 구분된 목록이며 마이닝 모델에서 파생됩니다.  
  
 *모델*  
 모델 식별자입니다.  
  
 *sub 선택*  
 포함된 select 문입니다.  
  
 *원본 데이터 쿼리*  
 원본 쿼리입니다.  
  
 *조인 매핑 목록*  
 (선택 사항) 모델의 열과 원본 쿼리의 열을 비교하는 논리 식입니다.  
  
 *조건 식*  
 (선택 사항) 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 (선택 사항) 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>주의  
 ON 절은 원본 쿼리의 열 및 마이닝 모델의 열 간의 매핑을 정의합니다. 이 매핑은 예측을 만들 때 원본 쿼리의 열을 입력으로 사용할 수 있도록 원본 쿼리의 열을 마이닝 모델의 열로 전송하는 데 사용됩니다. 열에는 \< *조인 매핑 목록*> 다음 예제와 같이 등호 (=)를 사용 하 여 관련 된:  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 ON 절에서 중첩 테이블을 바인딩하는 경우에는 중첩 열의 레코드가 속한 사례를 알고리즘이 정확히 식별할 수 있도록 키 열과 키가 아닌 열을 바인딩해야 합니다.  
  
 예측 조인에 대한 원본 쿼리는 테이블 또는 단일 쿼리일 수 있습니다.  
  
 에 있는 테이블 식을 반환 하지 않는 예측 함수를 지정할 수는 \< *select 식 목록*> 및 \< *식 조건*> 합니다.  
  
 **NATURAL PREDICTION JOIN** 자동으로 모델에서 열 이름을 일치 하는 원본 쿼리의 열 이름을 함께 매핑합니다. 사용 하는 경우 **자연 예측**, ON 절을 생략할 수 있습니다.  
  
 WHERE 조건은 예측 가능한 열이나 관련 열에만 적용할 수 있습니다.  
  
 ORDER BY 절에는 단일 열만 인수로 사용할 수 있으므로 둘 이상의 열에 따라 정렬할 수는 없습니다.  
  
## <a name="example-1-singleton-query"></a>예제 1: 단일 쿼리  
 다음 예에서는 특정 개인이 자전거를 구입할지 여부를 실시간으로 예측하는 쿼리를 만드는 방법을 보여 줍니다. 이 쿼리에서는 데이터가 테이블이나 다른 데이터 원본에 저장되지 않으며 쿼리에 직접 입력됩니다. 쿼리에 사용되는 개인의 특성은 다음과 같습니다.  
  
-   35세  
  
-   주택 소유  
  
-   자동차 두 대 소유  
  
-   동거 자녀 두 명  
  
 쿼리는 사람이 자전거를 반환 하는 테이블 형식 값의 집합을 구입 여부를 설명 하는 부울 값을 반환 TM Decision Tree 마이닝 모델 및 주체에 대 한 알려진된 특징을 사용 하는 [PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md) 예측을 만든 하는 방법을 설명 하는 함수입니다.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  PredictHistogram([Bike Buyer])  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 35 AS [Age],  
  '5-10 Miles' AS [Commute Distance],  
  '1' AS [House Owner Flag],  
  2 AS [Number Cars Owned],  
  2 AS [Total Children]) AS t  
```  
  
## <a name="example-2-using-openquery"></a>예제 2: OPENQUERY 사용  
 다음 예에서는 외부 데이터 집합에 저장된 잠재 고객 목록을 사용하여 일괄 처리 예측 쿼리를 만드는 방법을 보여 줍니다. 테이블의 인스턴스에서 정의 된 데이터 원본 뷰의 일부 이므로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 쿼리 צ ְ ײ [OPENQUERY](../dmx/source-data-query-openquery.md) 데이터를 검색 합니다. 테이블의 열 이름이 마이닝 모델의 경우와 다르기 때문에 **ON** 모델의 열에는 테이블의 열을 매핑할 절을 사용 해야 합니다.  
  
 쿼리는 테이블에 있는 각 개인의 성과 이름 및 각 개인이 자전거를 구입할 가능성이 있는지 여부를 나타내는 부울 열을 반환합니다. 부울 열에서 0은 "자전거를 구입할 가능성이 낮음"을, 1은 "자전거를 구입할 가능성이 높음"을 나타냅니다. 마지막 열에는 예측된 결과에 대한 확률이 들어 있습니다.  
  
```  
SELECT  
  t.[LastName],  
  t.[FirstName],  
  [TM Decision Tree].[Bike Buyer],  
  PredictProbability([Bike Buyer])  
From  
  [TM Decision Tree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [LastName],  
      [FirstName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [Education],  
      [Occupation],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
  [TM Decision Tree].[Gender] = t.[Gender] AND  
  [TM Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM Decision Tree].[Total Children] = t.[TotalChildren] AND  
  [TM Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM Decision Tree].[Education] = t.[Education] AND  
  [TM Decision Tree].[Occupation] = t.[Occupation] AND  
  [TM Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
```  
  
 자전거를 구입할 것으로 예측된 고객만 포함되도록 데이터 집합을 제한한 다음 고객 이름에 따라 목록을 정렬하려면 위의 예에 WHERE 절과 ORDER BY 절을 추가합니다.  
  
```  
WHERE [BIKE Buyer]  
ORDER BY [LastName] ASC  
```  
  
## <a name="example-3-predicting-associations"></a>예제 3: 연결 예측  
 다음 예에서는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘을 사용하여 만든 모델로 예측을 만드는 방법을 보여 줍니다. 연결 모델에 대한 예측을 사용하여 관련 제품을 추천할 수 있습니다. 예를 들어 다음 쿼리는 함께 구입될 가능성이 가장 높은 세 가지 제품을 반환합니다.  
  
-   Mountain Bottle Cage  
  
-   Mountain Tire Tube  
  
-   Mountain-200  
  
 [Predict &#40; DMX &#41;](../dmx/predict-dmx.md) 함수는 다형성 및 모든 모델 유형과 함께 사용할 수 있습니다. value3을 함수에 대한 인수로 사용하여 쿼리가 반환하는 항목 수를 제한할 수 있습니다. **선택** NATURAL PREDICTION JOIN 절 뒤에 오는 목록에는 예측에 대 한 입력으로 사용할 값을 제공 합니다.  
  
```  
SELECT FLATTENED  
  PREDICT([Association].[v Assoc Seq Line Items], 3)  
FROM  
  [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
  UNION SELECT 'Mountain Tire Tube' AS [Model]  
  UNION SELECT 'Mountain-200' AS [Model]) AS [v Assoc Seq Line Items ]) AS t  
```  
  
 예제 결과:  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set - Mountain|  
  
 예측 가능한 특성이 들어 있는 열인 `[v Assoc Seq Line Items]`가 테이블 열이므로 중첩 테이블이 들어 있는 단일 열이 반환됩니다. 기본적으로 중첩 테이블 열의 이름은 `Expression`입니다. 공급자가 계층적 행 집합을 지원 하지 하는 경우 사용할 수 있습니다는 **FLATTENED** 결과 보다 쉽게 볼 수 있도록이 예제에 표시 된 대로 키워드입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SELECT&#40; DMX &#41;](../dmx/select-dmx.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

