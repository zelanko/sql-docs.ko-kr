---
title: 지정 된 학습 데이터 (데이터 마이닝 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.specifytrainingdata.f1
ms.assetid: cb04deeb-0f89-4bba-b3f1-efccada16825
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c06fb99f8e2104e17d9f6d5f8016b3149ab62c76
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62745853"
---
# <a name="specify-the-training-data-data-mining-wizard"></a>학습 데이터 지정(데이터 마이닝 마법사)
  **학습 데이터 지정** 페이지를 사용하여 마이닝 구조에 포함할 열을 확인할 수 있습니다. 모든 모델에서 열을 사용하지 않는 경우에도 열을 선택하여 구조에 포함할 수 있습니다. 예를 들어 마이닝 모델에서 열로 드릴스루하려는 경우 모델이 아닌 구조에 열을 포함할 수 있습니다.  
  
 구조에 포함되는 각 테이블에 적어도 하나의 키 열이 필요합니다. 키로 선택하는 열은 테이블이 사례 테이블인지 중첩 테이블인지에 따라 달라집니다. 중첩 테이블인 경우 키는 관계형 외래 키가 아니라 주로 예측 열이 되기도 합니다. 중첩 키에 대한 자세한 내용은 [중첩 테이블&#40;Analysis Services - 데이터 마이닝&#41;](data-mining/nested-tables-analysis-services-data-mining.md)을 참조하세요.  
  
> [!NOTE]  
>  다른 마이닝 알고리즘은 키를 다르게 사용합니다. 다른 종류의 키에 대한 자세한 내용은 [콘텐츠 형식&#40;데이터 마이닝&#41;](data-mining/content-types-data-mining.md)을 참조하세요.  
  
 **참조 항목:** [마이닝 구조 &#40;Analysis Services-데이터 마이닝&#41;](data-mining/mining-structures-analysis-services-data-mining.md)를 [마이닝 모델 열](data-mining/mining-model-columns.md)합니다 [데이터 마이닝 마법사 &#40;&#40;analysis Services-데이터 마이닝&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [ 관계형 마이닝 구조 만들기](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>변수  
 **테이블/열**  
 마법사의 이전 페이지에서 선택한 테이블 및 열을 표시합니다.  
  
 **\<확인란 >**  
 마이닝 구조에 포함할 열을 선택합니다.  
  
 데이터 원본에 중첩 테이블 또는 여러 뷰가 포함된 경우 열 목록을 확장하여 중첩 테이블을 볼 수 있습니다.  
  
 **Key**  
 열을 데이터의 고유 식별자로 사용하려면 선택합니다.  
  
 사례 테이블에서 키는 일반적으로 고유 식별자입니다.  
  
 중첩 테이블에서 **키** 는 연결된 사례의 컨텍스트에 있는 행 식별자를 나타냅니다.  
  
 **Input**  
 열을 예측 생성 시 사용하려면 선택합니다.  
  
> [!NOTE]  
>  이 열은 마이닝 모델과 마이닝 구조를 함께 만드는 경우에만 사용할 수 있습니다.  
  
 **예측 가능한**  
 추가 입력을 기반으로 테이블 또는 열을 예측하도록 하려면 선택합니다.  
  
 중첩 테이블을 예측 가능으로 표시하면 전체 중첩 테이블이 예측 가능하게 됩니다. 중첩 테이블에 입력 또는 예측 가능으로 표시된 열이 없으면 중첩 테이블이 마이닝 구조에는 나타나지만 모델에서 무시됩니다.  
  
 **참고** 이 열은 마이닝 모델과 마이닝 구조를 함께 만드는 경우에만 사용할 수 있습니다.  
  
 **Suggest**  
 Entropy를 기반으로 데이터 샘플을 분석하여 선택한 **예측 가능** 열에 가장 밀접히 관련되어 있는 입력 열을 식별하는 **관련 열 제안** 대화 상자를 열려면 클릭합니다. 이 분석은 OLAP 원본을 기반으로 하는 중첩 테이블 열 또는 마이닝 구조에도 적용됩니다.  
  
 **참고** 이 열은 마이닝 모델과 마이닝 구조를 함께 만드는 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 마법사 F1 도움말 &#40;Analysis Services-데이터 마이닝&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [관련된 열 제안 &#40;데이터 마이닝 마법사&#41;](suggest-related-columns-data-mining-wizard.md)   
 [테이블 유형 지정 &#40;데이터 마이닝 마법사&#41;](specify-table-types-data-mining-wizard.md)   
 [열 내용 및 데이터 형식 지정 &#40;데이터 마이닝 마법사&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
