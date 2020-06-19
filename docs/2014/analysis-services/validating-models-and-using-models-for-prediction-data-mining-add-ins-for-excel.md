---
title: 모델 유효성 검사 및 예측을 위한 모델 사용 (Excel 용 데이터 마이닝 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- mining models, charting
- validation [data mining]
- mining models, testing
ms.assetid: e245ac1f-1230-48e9-9091-e70b131aa2a8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 00048ea3c5f344a90e93799a92b4d48c07325482
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938164"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>모델 유효성 검사 및 예측용 모델 사용(Excel용 데이터 마이닝 추가 기능)
  모델 테스트 및 유효성 검사는 데이터 마이닝 프로세스에서 중요한 단계입니다. 마이닝 모델을 프로덕션 환경에 배포하기 전에 실제 데이터에 대한 마이닝 모델의 성능을 알아야 합니다.  
  
 데이터 마이닝 추가 기능에는 작성한 모델을 테스트하고 해당 모델을 사용하여 예측 및 권장 사항을 만들 수 있도록 지원하는 도구가 포함되어 있습니다.  
  
## <a name="accuracy-chart"></a>정확도 차트  
 **정확도 차트** 마법사를 사용 하 여 리프트 차트나 산 점도 차트를 만들어 예측 쿼리를 만들고 데이터 마이닝 모델의 성능을 평가할 수 있습니다. 리프트 차트는 한 구조에서 거의 같은 모델을 구별하여 가장 적합한 예측을 제공하는 모델을 판별하는 데 유용합니다.  
  
 [정확도 차트 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>분류표  
 분류표 **마법사를** 사용 하면 예측 쿼리를 만들어 분류 모델의 성능을 평가할 수 있습니다. 해당 모델로 산출한 결과는 정확한 예측과 정확하지 않은 예측을 모두 요약하는 차트로 출력됩니다. 행렬은 모델이 값을 정확하게 예측한 빈도뿐만 아니라 모델이 자주 잘못 예측한 값도 표시하기 때문에 매우 유용한 도구입니다.  
  
 [분류표는 데이터 마이닝 추가 기능을 SQL Server &#40;&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>수익 차트  
 **수익 차트** 마법사를 사용 하면 데이터 마이닝 모델을 사용 하 여 얻을 수 있는 이점을 비교 하 고 거짓 긍정 및 거짓 네거티브의 비용을 평가할 수 있습니다.  
  
 이 차트 유형은 모델의 예측 정확도를 측정하고 지정한 단위와 전반적인 비용을 통합합니다.  
  
 [수익 차트는&#41;SQL Server 데이터 마이닝 추가 기능을 &#40;](profit-chart-sql-server-data-mining-add-ins.md)합니다.  
  
## <a name="cross-validation"></a>교차 유효성 검사  
 교차 유효성 검사는 데이터 마이닝 커뮤니티에서 설정된 기술로 데이터 집합의 타당성과 해당 데이터 집합에 대한 마이닝 모델의 정확도를 평가합니다. 이 검사는 데이터 집합을 하위 집합으로 분할한 다음 각각의 하위 집합에 대한 모델을 반복해서 만들어 학습하고 테스트합니다.  
  
 **교차 유효성 검사** 마법사를 사용 하면 데이터를 나눌 접기 수를 지정한 다음 이러한 교차 섹션 간의 차이점을 통계적으로 설명 하는 교차 유효성 검사 보고서를 제공할 수 있습니다. 여기에서 모델이 모든 학습 데이터에 대해 잘 수행되고 있는지 또는 특정 하위 집합에 대해 비대칭인지 확인할 수 있습니다.  
  
 [교차 유효성 검사는 데이터 마이닝 추가 기능 SQL Server &#40;&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>쿼리 마법사  
 **쿼리** 마법사는 예측 쿼리를 작성 하는 데 도움이 되는 대화형 도구입니다. 쿼리는 권장 사항, 미래 예측 등을 생성하는 방법입니다.  
  
 **쿼리** 마법사에서 모델을 선택한 다음 입력 데이터를 단일 값 이나 테이블이 나 범위에서 제공 하 고 마법사를 사용 하 여 출력할 열을 선택할 수 있습니다. 쿼리에 기능을 추가하여 확률 점수 및 기타 유용한 통계를 생성할 수도 있습니다.  
  
 [쿼리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>고급 쿼리 편집기  
 **고급 쿼리 편집기** 는 모든 종류의 DMX 문을 작성 하는 데 도움이 되는 대화 상자의 대화형 대화 상자 집합으로, 새 모델을 만들고 학습 하거나 모델을 삭제 하거나 새 데이터 집합을 만들기 위해 사용자 지정 쿼리 실행에서 수행할 수 있습니다.  
  
 [고급 데이터 마이닝 쿼리 편집기](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 탐색 및 정리](exploring-and-cleaning-data.md)   
 [데이터 마이닝 모델 만들기](creating-a-data-mining-model.md)   
 [Excel 용 데이터 마이닝 추가 기능 &#40;마이닝 모델 배포 및 확장&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
