---
title: (기본 데이터 마이닝 자습서) 구조에 대 한 테스트 데이터 집합 지정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 75cd508f-b126-418b-848d-3c4c3e6c303f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 21eaa86fb1ff594e8b9d2b779b787276ee13ab4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62720102"
---
# <a name="specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial"></a>구조에 대한 테스트 데이터 집합 지정(기본 데이터 마이닝 자습서)
  데이터 마이닝 마법사의 마지막 화면에서 데이터를 테스트 집합과 학습 집합으로 나눕니다. 그런 다음 구조에 이름을 지정하고 모델에 드릴스루를 사용합니다.  
  
## <a name="specifying-a-testing-set"></a>학습 집합 지정  
 마이닝 구조를 만들 때 학습 집합과 테스트 집합으로 데이터를 분리하면 나중에 만드는 마이닝 모델의 정확도를 쉽게 평가할 수 있습니다. 테스트 집합에 대 한 자세한 내용은 참조 하세요. [학습 및 테스트 데이터 집합](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md)합니다.  
  
#### <a name="to-specify-the-testing-set"></a>테스트 집합을 지정하려면  
  
1.  에 **테스트 집합 만들기** 페이지에 대 한 **테스트용 데이터 비율**의 기본값을 그대로 둡니다 `30`합니다.  
  
2.  에 대 한 **테스트 데이터 집합 내 사례의 최대 수**, 형식 `1000`합니다.  
  
3.  **다음**을 클릭합니다.  
  
## <a name="specifying-drillthrough"></a>드릴스루 지정  
 모델 및 구조에 드릴스루를 설정할 수 있습니다. 이 대화 상자에서 확인란을 선택하여 명명된 모델에 대한 드릴스루를 사용하도록 설정할 수 있습니다. 모델을 처리한 후에는 모델을 만드는 데 사용된 학습 데이터에서 자세한 정보를 검색할 수 있습니다.  
  
 기본 마이닝 구조도 드릴스루를 허용하도록 구성한 경우 마이닝 모델에 포함되지 않은 열을 비롯하여 모델 사례 및 마이닝 구조 모두의 세부 정보를 검색할 수 있습니다. 자세한 내용은 [드릴스루 쿼리&#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)를 참조하세요.  
  
#### <a name="to-name-the-model-and-structure-and-specify-drillthrough"></a>모델 및 구조에 이름을 지정하고 드릴스루를 지정하려면  
  
1.  에 **마법사 완료** 페이지에서 **마이닝 구조 이름**, 형식 `Targeted Mailing`합니다.  
  
2.  **마이닝 모델 이름**, 형식 `TM_Decision_Tree`합니다.  
  
3.  선택 된 **드릴스루 허용** 확인란 합니다.  
  
4.  검토 합니다 **미리 보기** 창입니다. 으로 선택한 열에 **키**를 **입력** 하거나 **예측 가능** 표시 됩니다. 선택한 다른 열(예: AddressLine1)은 모델 작성에 사용되지 않지만 기존 구조에 사용할 수 있으며 모델이 처리 및 배포된 후에 쿼리할 수 있습니다.  
  
5.  **마침**을 클릭합니다.  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [데이터 형식 및 내용 유형 지정 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>다음 단원  
 [3단원: 모델 추가 및 처리](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 모델에 드릴스루 사용](../../2014/analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)   
 [드릴스루 쿼리&#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [학습 데이터 지정 &#40;데이터 마이닝 마법사&#41;](../../2014/analysis-services/specify-the-training-data-data-mining-wizard.md)  
  
  
