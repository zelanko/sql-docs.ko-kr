---
title: 원본 큐브 차원 (데이터 마이닝 마법사)를 선택 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.selectsourcecube.f1
ms.assetid: 556e216b-5e21-4160-967d-4c57591fbab4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdb61763a49bad7eae1a49a01633ec8f45e27642
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069227"
---
# <a name="select-the-source-cube-dimension-data-mining-wizard"></a>원본 큐브 차원 선택(데이터 마이닝 마법사)
  **원본 큐브 차원 선택** 페이지를 사용하여 분석할 사례를 포함하는 큐브의 차원을 선택할 수 있습니다. 예를 들어 인구 통계를 기반으로 하여 고객의 구매 행동을 분석하는 모델을 작성하는 경우 일반적으로 각 고객 및 성별, 위치 또는 수입과 같은 인구 통계를 나타내는 여러 특성에 대해 고유한 레코드를 포함하는 Customer 차원을 선택합니다. 마법사의 뒷부분에서는 이 사례 테이블과 관련된 테이블을 추가할 수 있습니다. 예를 들어 고객이 구매한 제품을 보여 주는 중첩 테이블을 추가할 수 있습니다.  
  
> [!NOTE]  
>  이 페이지는 마법사의 **정의 방법 선택** 페이지에서 **기존 큐브 사용** 을 선택한 경우에만 나타납니다.  
  
## <a name="options"></a>변수  
 **원본 큐브 차원 선택**  
 마이닝 구조의 원본 데이터를 제공할 큐브의 차원을 선택합니다.  
  
## <a name="choosing-a-dimension"></a>차원 선택  
 모델에 사용할 차원 하나만 선택할 수 있기 때문에 큐브 구조를 이해하고 모델에 대한 최상의 정보를 제공하는 차원을 선택하는 것이 중요합니다. 사용할 차원을 잘 모르는 경우 차원 디자이너를 사용하여 큐브를 찾고 해당 큐브의 필드 및 데이터를 검토하는 것이 유용할 수 있습니다. 자세한 내용은 [차원 디자이너에서 차원 데이터 찾아보기](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)를 참조하세요.  
  
 일반적으로 차원을 잘 모르는 경우 [차원 소개&#40;Analysis Services - 다차원 데이터&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 데이터 마이닝에 유용할 수 있는 특성 및 측정값을 포함하여 일반적으로 단일 차원에 포함되어 있는 정보 유형에 대한 자세한 내용은 [Dimension Relationships](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)를 참조하십시오.  
  
 선택하는 차원에 데이터 마이닝 모델을 작성하는 데 필요한 관련 특성이 모두 포함되어 있지는 않은 경우 차원을 수정할 필요가 있습니다. 자세한 내용은 [데이터베이스 차원 정의](multidimensional-models/define-database-dimensions.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 마법사 F1 도움말 &#40;Analysis Services-데이터 마이닝&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [데이터 마이닝 구조 만들기 &#40;데이터 마이닝 마법사&#41;](create-the-data-mining-structure-data-mining-wizard.md)   
 [사례 키 선택 &#40;데이터 마이닝 마법사&#41;](select-the-case-key-data-mining-wizard.md)  
  
  
