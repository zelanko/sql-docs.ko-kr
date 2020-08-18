---
description: DMX(Data Mining Extensions) 문 참조
title: DMX (데이터 마이닝 확장) 문 참조 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ce95adec18bd17dce45fdc988b6db92d66383c74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414099"
---
# <a name="data-mining-extensions-dmx-statements"></a>DMX(Data Mining Extensions) 문
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  에서 데이터 마이닝 모델을 사용 하 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 경우 다음과 같은 기본 작업을 수행 해야 합니다.  
  
-   마이닝 구조 및 마이닝 모델 만들기  
  
-   마이닝 구조 및 마이닝 모델 처리  
  
-   마이닝 구조 또는 마이닝 모델 삭제  
  
-   마이닝 모델 복사  
  
-   마이닝 모델 검색  
  
-   마이닝 모델로 예측  
  
 DMX(Data Mining Extensions) 문을 사용하여 이러한 태스크를 각각 프로그래밍 방식으로 수행할 수 있습니다.  
  
 마이닝 구조 및 마이닝 모델 만들기  
 [CREATE 마이닝 structure &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md) 문을 사용 하 여 데이터베이스에 새 마이닝 구조를 추가할 수 있습니다. 그런 다음 [ALTER 마이닝 structure &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) 문을 사용 하 여 마이닝 구조에 마이닝 모델을 추가할 수 있습니다.  
  
 [CREATE 마이닝 model &#40;DMX&#41;](../dmx/create-mining-model-dmx.md) 문을 사용 하 여 새 마이닝 모델 및 연결 된 마이닝 구조를 작성할 수 있습니다.  
  
 마이닝 구조 및 마이닝 모델 처리  
 [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) 문을 사용 하 여 마이닝 구조 및 마이닝 모델을 처리 합니다.  
  
 마이닝 구조 또는 마이닝 모델 삭제  
 [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) 문을 사용 하 여 마이닝 모델 또는 마이닝 구조에서 학습 된 모든 데이터를 제거할 수 있습니다. 데이터베이스에서 마이닝 구조 또는 마이닝 모델을 완전히 제거 하려면 [dmx &#40;dmx&#41;](../dmx/drop-mining-structure-dmx.md) 또는 [drop 마이닝 모델 &#40;dmx&#41;](../dmx/drop-mining-model-dmx.md) 문을 사용 합니다.  
  
 마이닝 모델 복사  
 [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md) 문을 사용 하 여 기존 마이닝 모델의 구조를 새 마이닝 모델로 복사 하 고 동일한 데이터를 사용 하 여 새 모델을 학습 합니다.  
  
 마이닝 모델 검색  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md) 문을 사용 하 여 모델 학습 중 데이터 마이닝 알고리즘에서 계산 하 고 데이터 마이닝 모델에 저장 하는 정보를 찾아볼 수 있습니다. 와 마찬가지로 [!INCLUDE[tsql](../includes/tsql-md.md)] SELECT 문에 여러 절을 사용 하 여 해당 기능을 확장할 수 있습니다. 이러한 절에는의 [ \<model> 고유한 ](../dmx/select-distinct-from-model-dmx.md)가 포함 됩니다 [ \<model> . ](../dmx/select-from-model-cases-dmx.md)의 사례 [ \<model> . ](../dmx/select-from-model-sample-cases-dmx.md)에서 SAMPLE_CASES [ \<model> 합니다. 콘텐츠](../dmx/select-from-model-content-dmx.md) 및 [의 \<model> DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md).  
  
 마이닝 모델로 예측  
 SELECT 문의 [예측 조인](../dmx/select-from-model-prediction-join-dmx.md) 절을 사용 하 여 기존 마이닝 모델을 기반으로 하는 예측을 만들 수 있습니다.  
  
 [&#40;dmx&#41;가져오기](../dmx/import-dmx.md) 및 [내보내기 &#40;dmx&#41;](../dmx/export-dmx.md) 문을 사용 하 여 모델을 가져오고 내보낼 수도 있습니다.  
  
 이러한 태스크는 데이터 정의 문과 데이터 조작 문이라는 두 가지 범주로 나누어집니다. 이 두 범주에 대해서는 다음 표에서 설명합니다.  
  
|항목|설명|  
|-----------|-----------------|  
|[DMX&#40;Data Mining Extensions&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)|DDL(데이터 정의 언어)의 일부입니다. 학습을 포함하여 새 마이닝 모델을 정의하거나 데이터베이스에서 기존 마이닝 모델을 삭제하는 데 사용합니다.|  
|[데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)|DML(데이터 조작 언어)의 일부입니다. 모델을 검색하거나 예측을 만드는 등 기존 마이닝 모델로 작업하는 데 사용합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
