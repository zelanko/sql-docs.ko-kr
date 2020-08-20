---
description: SELECT INTO(DMX)
title: SELECT INTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e7bc85d20ab3c1c087b6352d16777b2bb7d7dcd0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500879"
---
# <a name="select-into-dmx"></a>SELECT INTO(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  기존 마이닝 모델의 마이닝 구조를 기반으로 새 마이닝 모델을 만듭니다. **SELECT INTO** 문은 스키마 및 실제 알고리즘과 관련이 없는 기타 정보를 복사 하 여 새 마이닝 모델을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT INTO <new model>   
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH[,] [FILTER(<expression>)]]  
FROM <existing model>  
```  
  
## <a name="arguments"></a>인수  
 *new model*  
 생성될 새 모델의 고유 이름입니다.  
  
 *알고리즘과*  
 공급자가 정의한 데이터 마이닝 알고리즘 이름입니다.  
  
 *매개 변수 목록*  
 (선택 사항) 알고리즘에 대해 공급자가 정의한 매개 변수의 쉼표로 구분된 목록입니다.  
  
 *expression*  
 학습 데이터에 대해 유효한 필터 조건으로 계산되는 식입니다. 필터로 사용할 수 있는 식에 대 한 자세한 내용은 [데이터 마이닝&#41;Analysis Services &#40;마이닝 모델에 대 한 필터 ](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)를 참조 하세요.  
  
 *기존 모델*  
 복사할 기존 모델의 이름입니다.  
  
## <a name="remarks"></a>설명  
 기존 모델이 학습되는 경우 새 모델은 이 문이 실행될 때 자동으로 처리됩니다. 그렇지 않은 경우 새 모델은 처리되지 않습니다.  
  
 **SELECT INTO** 문은 기존 모델의 구조가 새 모델의 알고리즘과 호환 되는 경우에만 작동 합니다. 따라서 이 문은 같은 알고리즘에 기초한 모델을 빠르게 만들고 테스트할 때 가장 유용합니다. 알고리즘 유형을 변경하는 경우 새 알고리즘은 기존 모델에 있는 각 열의 데이터 형식을 지원해야 합니다. 그렇지 않으면 모델이 처리될 때 오류가 발생합니다.  
  
 **WITH DRILLTHROUGH** 절을 사용 하면 새 마이닝 모델에서 드릴스루를 사용할 수 있습니다. 드릴스루는 모델을 만들 때만 사용할 수 있습니다.  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>예제 1: 모델의 매개 변수 변경  
 다음 예에서는 `TM_Clustering` [기본 데이터 마이닝 자습서](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)에서 만든 기존 마이닝 모델을 기반으로 새 마이닝 모델을 만듭니다. 새 모델에서는 최대 다섯 개의 클러스터가 존재하도록 CLUSTER_COUNT 매개 변수를 수정합니다. 반면 기존 모델에서는 기본값인 10이 사용됩니다.  
  
```  
SELECT * INTO [New_Clustering]  
USING [Microsoft_Clustering] (CLUSTER_COUNT = 5)   
FROM [TM Clustering]  
```  
  
## <a name="example-2-adding-a-filter-to-the-model"></a>예제 2: 모델에 필터 추가  
 다음 예에서는 기존 마이닝 모델을 기반으로 새 마이닝 모델을 만들고 모델에 필터를 추가합니다. 이 필터는 학습 데이터를 특정 지역에 거주하는 고객으로 제한합니다.  
  
```  
SELECT * INTO [Clustering Europe Region]  
USING [Microsoft_Clustering] WITH FILTER(Region='Europe')  
FROM [TM Clustering]  
```  
  
> [!NOTE]  
>  이 예와 같이 SELECT INTO 문을 사용하면 사례 테이블에 적용된 필터를 변경할 수 있지만, 원래 모델에 중첩 테이블에 대한 필터가 들어 있는 경우 중첩 테이블 필터는 이 구문을 사용하여 변경하거나 제거할 수 없습니다. 이러한 필터는 원래 모델에서 그대로 복사됩니다. 중첩 테이블에 대해 다른 필터를 사용하여 모델을 만들려면 ALTER STRTUCTURE...ADD MODEL 구문을 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
