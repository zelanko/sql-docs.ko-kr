---
title: 마이닝 모델을 만드는 사용 되는 매개 변수 쿼리 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df2eb8317f90a96b35fc886e2158000e0f57d09d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34014411"
---
# <a name="query-the-parameters-used-to-create-a-mining-model"></a>마이닝 모델을 만드는 데 사용한 매개 변수 쿼리
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  마이닝 모델의 컴퍼지션은 학습 사례의 영향을 받을 뿐만 아니라 모델을 만들 때 설정한 매개 변수의 영향도 받습니다. 따라서 기존 모델의 매개 변수 설정을 검색하면 모델의 동작을 보다 잘 이해할 수 있습니다. 매개 변수 검색은 해당 모델의 특정 버전을 문서화하는 데도 유용합니다.  
  
 모델을 만들 때 사용한 매개 변수를 찾으려면 마이닝 모델 스키마 행 집합 중 하나에 대한 쿼리를 만듭니다. 이러한 스키마 행 집합은 TRANSACT-SQL 구문을 사용 하 여 쉽게 쿼리할 수 있는 시스템 뷰 집합으로 노출 됩니다. 이 절차에서는 지정된 마이닝 모델을 만드는 데 사용한 매개 변수를 반환하는 쿼리를 만드는 방법에 대해 설명합니다.  
  
### <a name="to-open-a-query-window-for-a-schema-rowset-query"></a>스키마 행 집합 쿼리에 대한 쿼리 창을 열려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 쿼리할 모델이 들어 있는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 엽니다.  
  
2.  인스턴스 이름을 마우스 오른쪽 단추로 클릭하여 **새 쿼리**를 선택한 다음 **DMX**를 선택합니다.  
  
    > [!NOTE]  
    >  **MDX** 템플릿을 사용하여 데이터 마이닝 모델에 대한 쿼리를 만들 수도 있습니다.  
  
3.  인스턴스에 여러 개의 데이터베이스가 포함되어 있는 경우 도구 모음의 **사용 가능한 데이터베이스** 목록에서 쿼리할 모델을 포함하는 데이터베이스를 선택합니다.  
  
### <a name="to-return-model-parameters-for-an-existing-mining-model"></a>기존 마이닝 모델에 대한 모델 매개 변수를 반환하려면  
  
1.  DMX 쿼리 창에서 다음 텍스트를 입력하거나 붙여넣습니다.  
  
    ```  
    SELECT MINING_PARAMETERS  
    FROM $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = ''  
    ```  
  
2.  개체 탐색기에서 원하는 마이닝 모델을 선택한 다음 DMX 쿼리 창의 작은따옴표 사이로 끌어 옵니다.  
  
3.  F5 키를 누르거나 **실행**을 클릭합니다.  
  
## <a name="example"></a>예제  
 다음 코드는 [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)에서 생성한 마이닝 모델을 만드는 데 사용한 매개 변수 목록을 반환합니다. 이러한 매개 변수에는 서버의 공급자가 제공하는 마이닝 서비스에 사용되는 기본값에 대한 명시적 값이 포함됩니다.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
 이 코드 예는 클러스터링 모델에 대해 다음 매개 변수를 반환합니다.  
  
 예 결과:  
  
 MINING_PARAMETERS  
  
 CLUSTER_COUNT=10,CLUSTER_SEED=0,CLUSTERING_METHOD=1,MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_STATES=100,MINIMUM_SUPPORT=1,MODELLING_CARDINALITY=10,SAMPLE_SIZE=50000,STOPPING_TOLERANCE=10  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 쿼리 태스크 및 방법](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
