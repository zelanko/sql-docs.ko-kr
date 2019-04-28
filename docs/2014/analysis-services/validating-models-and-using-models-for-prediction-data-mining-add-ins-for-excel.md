---
title: 모델 유효성 검사 및 모델을 사용 하 여 예측 (데이터 마이닝 추가 기능 Excel 용) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- mining models, charting
- validation [data mining]
- mining models, testing
ms.assetid: e245ac1f-1230-48e9-9091-e70b131aa2a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a9ae056818b260ed00df9111d8b06b37378285d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62793118"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>모델 유효성 검사 및 예측용 모델 사용(Excel용 데이터 마이닝 추가 기능)
  모델 테스트 및 유효성 검사는 데이터 마이닝 프로세스에서 중요한 단계입니다. 마이닝 모델을 프로덕션 환경에 배포하기 전에 실제 데이터에 대한 마이닝 모델의 성능을 알아야 합니다.  
  
 데이터 마이닝 추가 기능에는 작성한 모델을 테스트하고 해당 모델을 사용하여 예측 및 권장 사항을 만들 수 있도록 지원하는 도구가 포함되어 있습니다.  
  
## <a name="accuracy-chart"></a>정확도 차트  
 합니다 **정확도 차트** 마법사를 통해 예측 쿼리를 만들고 리프트 차트 또는 산 점도 차트를 만들어 데이터 마이닝 모델의 성능을 평가할 수 있습니다. 리프트 차트는 한 구조에서 거의 같은 모델을 구별하여 가장 적합한 예측을 제공하는 모델을 판별하는 데 유용합니다.  
  
 [정확도 차트 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>분류표  
 합니다 **분류표** 마법사 분류 모델의 성능을 평가 하는 예측 쿼리를 만들 수 있습니다. 해당 모델로 산출한 결과는 정확한 예측과 정확하지 않은 예측을 모두 요약하는 차트로 출력됩니다. 행렬은 모델이 값을 정확하게 예측한 빈도뿐만 아니라 모델이 자주 잘못 예측한 값도 표시하기 때문에 매우 유용한 도구입니다.  
  
 [분류 행렬 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>수익 차트  
 합니다 **수익 차트** 마법사를 사용 하 여 데이터 마이닝 모델을 사용 하 여 이점을 따져보는 거짓 긍정 및 거짓 부 정의 비용 평가  
  
 이 차트 유형은 모델의 예측 정확도를 측정하고 지정한 단위와 전반적인 비용을 통합합니다.  
  
 [수익 차트 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](profit-chart-sql-server-data-mining-add-ins.md)합니다.  
  
## <a name="cross-validation"></a>교차 유효성 검사  
 교차 유효성 검사는 데이터 마이닝 커뮤니티에서 설정된 기술로 데이터 집합의 타당성과 해당 데이터 집합에 대한 마이닝 모델의 정확도를 평가합니다. 이 검사는 데이터 집합을 하위 집합으로 분할한 다음 각각의 하위 집합에 대한 모델을 반복해서 만들어 학습하고 테스트합니다.  
  
 합니다 **교차 유효성 검사** 마법사에서 데이터를 분할할 접기 수를 지정할 수 있습니다 하 고 이러한 교집합 영역 간의 차이 통계학적으로 설명 하는 교차 유효성 검사 보고서를 제공 합니다. 여기에서 모델이 모든 학습 데이터에 대해 잘 수행되고 있는지 또는 특정 하위 집합에 대해 비대칭인지 확인할 수 있습니다.  
  
 [교차 유효성 검사 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>쿼리 마법사  
 합니다 **쿼리** 마법사는 예측 쿼리를 작성할 수 있도록 대화형 도구입니다. 쿼리는 권장 사항, 미래 예측 등을 생성하는 방법입니다.  
  
 에 **쿼리** 마법사는 마법사를 통해 출력할 열을 선택 및 모델을 선택한 다음 단일 값 또는 테이블 또는 범위에서 입력된 데이터를 제공 합니다. 쿼리에 기능을 추가하여 확률 점수 및 기타 유용한 통계를 생성할 수도 있습니다.  
  
 [쿼리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>고급 쿼리 편집기  
 합니다 **고급 쿼리 편집기** 도움이 되는 대화형 대화 상자 집합을 모든 종류의 DMX 문 만드는 사용자 지정 쿼리를 실행 하는 항목을 빌드 및 모델을 삭제 하는 새 모델을 학습 또는 새 데이터 집합 만들기.  
  
 [고급 데이터 마이닝 쿼리 편집기](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 탐색 및 지우기](exploring-and-cleaning-data.md)   
 [데이터 마이닝 모델 만들기](creating-a-data-mining-model.md)   
 [마이닝 모델 배포 및 확장 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
