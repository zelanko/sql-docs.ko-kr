---
title: Data Mining Extensions (DMX) 문 참조 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], statements
- statements [DMX], reference
- mining models [Analysis Services], training
- mining structures [DMX]
- mining models [Analysis Services], options
- mining structures [DMX], options
ms.assetid: 9cfa1db4-0f21-4fa3-8158-f94c48987e1b
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6eb00d13f68d8ade9866983bbaf7d9f8276ba13d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-extensions-dmx-statements"></a>Data Mining Extensions (DMX) 문
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  데이터 마이닝 모델에서 작업 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 다음과 같은 기본 작업을 수행 해야 합니다.  
  
-   마이닝 구조 및 마이닝 모델 만들기  
  
-   마이닝 구조 및 마이닝 모델 처리  
  
-   마이닝 구조 또는 마이닝 모델 삭제  
  
-   마이닝 모델 복사  
  
-   마이닝 모델 검색  
  
-   마이닝 모델로 예측  
  
 DMX(Data Mining Extensions) 문을 사용하여 이러한 태스크를 각각 프로그래밍 방식으로 수행할 수 있습니다.  
  
 마이닝 구조 및 마이닝 모델 만들기  
 사용 하 여는 [CREATE MINING STRUCTURE &#40;DMX&#41; ](../dmx/create-mining-structure-dmx.md) 문을 데이터베이스에 새 마이닝 구조를 추가 합니다. 사용할 수 있습니다는 [ALTER MINING STRUCTURE &#40;DMX&#41; ](../dmx/alter-mining-structure-dmx.md) 마이닝 구조에 마이닝 모델을 추가 하는 문입니다.  
  
 사용 하 여는 [CREATE MINING MODEL &#40;DMX&#41; ](../dmx/create-mining-model-dmx.md) 새 마이닝 모델 및 연결 된 마이닝 구조를 작성 하는 문입니다.  
  
 마이닝 구조 및 마이닝 모델 처리  
 사용 하 여는 [INSERT INTO &#40;DMX&#41; ](../dmx/insert-into-dmx.md) 마이닝 구조 및 마이닝 모델을 처리 하는 문입니다.  
  
 마이닝 구조 또는 마이닝 모델 삭제  
 사용 하 여는 [삭제 &#40;DMX&#41; ](../dmx/delete-dmx.md) 마이닝 모델 또는 마이닝 구조에서 학습된 된 모든 데이터를 제거 하는 문입니다. 사용 하 여는 [DROP MINING STRUCTURE &#40;DMX&#41; ](../dmx/drop-mining-structure-dmx.md) 또는 [DROP MINING MODEL &#40;DMX&#41; ](../dmx/drop-mining-model-dmx.md) 데이터베이스에서 마이닝 구조 또는 마이닝 모델을 완전히 제거 하는 문입니다.  
  
 마이닝 모델 복사  
 사용 하 여는 [SELECT INTO &#40;DMX&#41; ](../dmx/select-into-dmx.md) 문을 새 마이닝 모델에 기존 마이닝 모델의 구조를 복사 하 고 동일한 데이터를 새 모델을 학습 합니다.  
  
 마이닝 모델 검색  
 사용 하 여는 [선택 &#40;DMX&#41; ](../dmx/select-dmx.md) 문을 데이터 마이닝 알고리즘이 계산 하 고 모델을 학습 하는 동안 데이터 마이닝 모델에 저장 하는 정보를 검색 합니다. 과 마찬가지로 [!INCLUDE[tsql](../includes/tsql-md.md)], 기능을 확장할 SELECT 문으로 여러 절을 사용할 수 있습니다. 이러한 절에는 포함 [DISTINCT FROM \<모델 >](../dmx/select-distinct-from-model-dmx.md), [FROM \<모델 >. 경우](../dmx/select-from-model-cases-dmx.md), [FROM \<모델 >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md), [FROM \<모델 >. 콘텐츠](../dmx/select-from-model-content-dmx.md) 및 [FROM \<모델 >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)합니다.  
  
 마이닝 모델로 예측  
 사용 하 여 [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) 기존 마이닝 모델을 기반으로 하는 예측을 만들 수는 SELECT 문의 절.  
  
 가져오기 및 사용 하 여 모델을 내보낼 수도 있습니다는 [가져올 &#40;DMX&#41; ](../dmx/import-dmx.md) 및 [내보내기 &#40;DMX&#41; ](../dmx/export-dmx.md) 문입니다.  
  
 이러한 태스크는 데이터 정의 문과 데이터 조작 문이라는 두 가지 범주로 나누어집니다. 이 두 범주에 대해서는 다음 표에서 설명합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[Data Mining Extensions &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)|DDL(데이터 정의 언어)의 일부입니다. 학습을 포함하여 새 마이닝 모델을 정의하거나 데이터베이스에서 기존 마이닝 모델을 삭제하는 데 사용합니다.|  
|[Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)|DML(데이터 조작 언어)의 일부입니다. 모델을 검색하거나 예측을 만드는 등 기존 마이닝 모델로 작업하는 데 사용합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 표기 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
