---
title: 콘텐츠 형식 (데이터 마이닝) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0dcc5840467f039e78c0c4d4b75862bbf78a6a42
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725187"
---
# <a name="content-types-data-mining"></a>내용 유형(데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 마이닝 구조의 열에 대한 실제 데이터 형식과 모델에 사용된 열에 대한 논리적 내용 유형을 모두 정의할 수 있습니다.  
  
 *데이터 형식* 은 마이닝 모델을 만들 때 알고리즘이 이 열의 데이터를 처리하는 방법을 결정합니다. 열의 데이터 형식을 정의하면 열의 데이터 처리 방법 및 해당 데이터 형식에 대한 알고리즘 정보를 제공합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 각 데이터 형식은 데이터 마이닝에 대해 하나 이상의 내용 유형을 지원합니다.  
  
 *내용 유형* 은 열에 포함된 내용의 동작을 설명합니다. 예를 들어 열 내용이 요일 등의 특정 간격으로 반복되는 경우 해당 열의 내용 유형을 순환으로 지정할 수 있습니다.  
  
 일부 알고리즘의 경우 올바르게 실행되기 위해서는 특정한 데이터 형식과 특정한 내용 유형이 필요합니다. 예를 들어 Microsoft Naive Bayes 알고리즘은 연속 열을 입력으로 사용할 수 없고 연속 값을 예측할 수 없습니다. Key Sequence와 같은 일부 내용 유형은 특정 알고리즘에서만 사용됩니다. 알고리즘과 각 알고리즘이 지원하는 콘텐츠 형식 목록은 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)을 참조하세요.  
  
 다음 목록에서는 데이터 마이닝에 사용되는 내용 유형을 설명하고 각 유형을 지원하는 데이터 형식을 식별합니다.  
  
## <a name="discrete"></a>불연속  
 *Discrete* 는 열에 연속되지 않은 한정된 수의 값이 포함되어 있음을 의미합니다. 예를 들어 Gender 열은 전형적인 불연속 특성 열로서 해당 데이터가 특정 개수의 범주를 나타냅니다.  
  
 불연속 특성 열의 값은 숫자라 하더라도 순서를 의미하지 않습니다. 또한 불연속 열에 사용된 값이 숫자라 하더라도 소수 값은 계산될 수 없습니다. 불연속 숫자 데이터의 좋은 예로 전화 번호의 지역 번호가 있습니다.  
  
 **Discrete** 내용 유형은 모든 데이터 마이닝 데이터 형식에서 지원합니다.  
  
## <a name="continuous"></a>연속  
 *Continuous* 는 열에 중간 값을 허용하는 소수 자릿수의 숫자 데이터를 나타내는 값이 포함되어 있음을 의미합니다. 한정된 개수의 데이터를 나타내는 불연속 열과는 달리 연속 열은 조정 가능한 측정을 나타내며 데이터가 무한 개의 소수 값을 포함합니다. 연속 특성 열의 예로는 Temperatures 열이 있습니다.  
  
 열에 연속 숫자 데이터가 있고 데이터 배포 방법을 알고 있는 경우 값의 예상 분포를 지정하여 분석의 정확도를 향상시킬 수 있습니다. 마이닝 구조의 수준에서 열 배포를 지정합니다. 따라서 이 설정은 구조를 기반으로 하는 모든 모델에 적용됩니다. 자세한 내용은 [열 배포&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md)를 참조하세요.  
  
 합니다 **연속** 콘텐츠 형식 다음 데이터 형식에서 지원 합니다. **날짜**, **이중**, 및 **긴**합니다.  
  
## <a name="discretized"></a>불연속화됨  
 *분할* 은 제한된 개수의 가능한 값이 있도록 연속 데이터 집합의 값을 버킷에 넣는 프로세스입니다. 숫자 데이터만 분할할 수 있습니다.  
  
 따라서 *Discretized* 내용 유형은 열에 연속 열에서 파생된 값의 그룹 또는 버킷을 나타내는 값이 포함되어 있음을 나타냅니다. 버킷은 정렬된 불연속 값으로 처리됩니다.  
  
 원하는 버킷을 얻기 위해 데이터를 수동으로 분할하거나 SQL Server Analysis Services에서 제공하는 분할 메서드를 사용할 수 있습니다. 일부 알고리즘의 경우 분할을 자동으로 수행합니다. 자세한 내용은 [마이닝 모델에서 열의 불연속화 변경](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)을 참조하세요.  
  
 합니다 **Discretized** 콘텐츠 형식 다음 데이터 형식에서 지원 합니다. **날짜**, **이중**를 **Long**, 및 **텍스트**합니다.  
  
## <a name="key"></a>Key  
 *Key* 내용 유형은 열이 행을 고유하게 식별함을 의미합니다. 사례 테이블에서 키 열은 일반적으로 숫자 또는 텍스트 식별자입니다. 내용 유형을 **key** 로 설정하면 열을 분석에 사용해서는 안 되고 레코드 추적용으로만 사용해야 함을 나타냅니다.  
  
 중첩 테이블에도 키가 있지만 중첩 테이블 키의 사용법은 약간 다릅니다. 열이 분석하려는 특성일 경우 중첩 테이블에서 내용 유형을 **key** 로 설정하십시오. 중첩 테이블 키의 값은 각 사례에 대해 고유해야 하지만 사례 집합 전체에서는 중복될 수 있습니다.  
  
 예를 들어 고객이 구매한 제품을 분석하는 경우 사례 테이블의 **CustomerID** 열에 대해 내용 유형을 Key로 설정한 다음 중첩 테이블의 **PurchasedProducts** 열에 대해 내용 유형을 다시 Key로 설정할 수 있습니다.  
  
> [!NOTE]  
>  중첩 테이블은 Analysis Services 데이터 원본 뷰로 정의된 외부 데이터 원본의 데이터를 사용하는 경우에만 사용할 수 있습니다.  
  
 이 내용 유형은 데이터 형식에서 사용할 수 있습니다. **날짜**, **이중**를 **Long**, 및 **텍스트**합니다.  
  
## <a name="key-sequence"></a>키 시퀀스  
 *Key Sequence* 내용 유형은 시퀀스 클러스터링 모델에서만 사용할 수 있습니다. 내용 유형을 **key sequence**로 설정할 경우 이는 이벤트 시퀀스를 표시하는 값이 열에 포함되어 있음을 나타냅니다. 이러한 값은 정렬되지만 간격은 달라도 됩니다.  
  
 이 내용 유형은 데이터 형식에서 사용할 수 있습니다. **이중**, **긴**를 **텍스트**, 및 **날짜**합니다.  
  
## <a name="key-time"></a>Key Time  
 *Key Time* 내용 유형은 시계열 모델에서만 사용할 수 있습니다. 내용 유형을 **key time**으로 설정할 경우 이는 값이 정렬되고 시간 단위를 가리킴을 나타냅니다.  
  
 이 내용 유형은 데이터 형식에서 사용할 수 있습니다. **이중**, **긴**, 및 **날짜**합니다.  
  
## <a name="table"></a>Table  
 *Table* 내용 유형은 열에 행과 열이 각각 한 개 이상인 다른 데이터 테이블이 포함되어 있음을 나타냅니다. 이 열은 사례 테이블의 특정 행에 대해 여러 값을 포함할 수 있는데 이러한 값은 모두 부모 사례 레코드와 관련되어 있습니다. 예를 들어 주 사례 테이블에 고객 목록이 포함되어 있는 경우 중첩 테이블을 포함하는 열이 여러 개 있을 수 있습니다. 예를 들어 **ProductsPurchased** 열의 중첩 테이블에는 이 고객이 과거에 구매한 제품이 나열되며 **Hobbies** 열에는 고객의 관심 사항이 나열됩니다.  
  
 이 열의 데이터 형식은 항상 **Table**입니다.  
  
## <a name="cyclical"></a>Cyclical  
 *Cyclical* 내용 유형은 열에 정렬된 순환 집합을 나타내는 값이 포함되어 있음을 나타냅니다. 예를 들어 각 주의 번호가 매겨진 날짜들은 제7일 다음에 제1일이 오는 순환 정렬 집합입니다.  
  
 순환 열은 내용 유형 면에서 정렬 및 불연속 등 두 가지 모두로 인식됩니다.  
  
 이 내용 유형은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 모든 데이터 마이닝 데이터 형식에서 지원합니다. 그러나 대부분의 알고리즘은 순환 값을 불연속 값으로 처리하며 특수한 처리를 수행하지 않습니다.  
  
## <a name="ordered"></a>Ordered  
 *Ordered* 내용 유형도 열에 시퀀스 또는 순서를 정의하는 값이 포함되어 있음을 나타냅니다. 그러나 이 내용 유형에서는 정렬에 사용되는 값이 집합 내에 있는 값 간의 거리 또는 크기 관계를 의미하는 것은 아닙니다. 예를 들어 정렬된 특성 열에 1부터 5까지 범위의 기술 수준에 대한 정보가 포함된 경우 기술 수준 간의 거리를 나타내는 정보는 포함되어 있지 않으므로 기술 수준 5가 기술 수준 1보다 반드시 5배 우수한 것은 아닙니다.  
  
 정렬된 특성 열은 내용 유형 면에서 불연속으로 인식됩니다.  
  
 이 내용 유형은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 모든 데이터 마이닝 데이터 형식에서 지원합니다. 그러나 대부분의 알고리즘은 정렬된 값을 불연속 값으로 처리하며 특수한 처리를 수행하지 않습니다.  
  
## <a name="classified"></a>Classified  
 모든 모델에서 일반적으로 사용되는 위의 내용 유형 외에도 일부 데이터 형식에 대해 분류된 열을 사용하여 내용 유형을 정의할 수 있습니다. 분류된 열에 대한 자세한 내용은 [분류된 열&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/classified-columns-data-mining.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [콘텐츠 형식&#40;DMX&#41;](../../dmx/content-types-dmx.md)   
 [데이터 형식&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/data-types-data-mining.md)   
 [데이터 형식&#40;DMX&#41;](../../dmx/data-types-dmx.md)   
 [마이닝 구조 속성 변경](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)   
 [마이닝 구조 열](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
