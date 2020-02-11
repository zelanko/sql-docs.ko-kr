---
title: Excel 용 테이블 분석 도구 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- getting started
ms.assetid: 6d9d1481-18e4-4108-9efa-68152b0940c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af4c8ae7c2ba827e6110602bd21432fec4f74393
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067967"
---
# <a name="table-analysis-tools-for-excel"></a>Excel용 테이블 분석 도구
  **분석** 도구 모음의 데이터 마이닝 도구는 데이터 마이닝을 시작 하는 가장 쉬운 방법입니다. 각 도구는 자동으로 배포 및 데이터 유형을 분석하고 결과가 유효하다는 것을 증명하기 위한 매개 변수를 설정합니다. 알고리즘을 선택하거나 복잡한 매개 변수를 구성할 필요가 없습니다.  
  
 ![DM](media/dm-tabletoolsanalyze.gif "DM")  
  
 **분석** 리본에는 다음과 같은 도구가 포함 되어 있습니다.  
  
 [Excel 용 테이블 분석 도구 &#40;주요 영향 요인 분석&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 관심 있는 열 또는 출력 값을 선택한 다음 알고리즘으로 모든 입력 데이터를 분석하여 대상에 가장 많은 영향을 미친 요소를 식별합니다. 필요한 경우 두 값을 비교하는 보고서를 만들어 영향 요인이 어떻게 변경되는지 확인할 수 있습니다.  
  
 **주요 영향 요인 분석** 도구는 Microsoft naive Bayes 알고리즘을 사용 합니다.  
  
 [Excel 용 테이블 분석 도구 &#40;범주 검색&#41;](detect-categories-table-analysis-tools-for-excel.md)  
 이 도구를 사용하면 데이터 집합을 추가하고 클러스터링을 적용하여 데이터 그룹화를 찾을 수 있습니다. 유사성을 찾고 추가 분석을 위해 그룹을 만드는 데 유용 합니다.  
  
 **범주 검색** 도구는 Microsoft 클러스터링 알고리즘을 사용 합니다.  
  
 [Excel 용 테이블 분석 도구 &#40;예제로 채우기&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
 이 도구를 사용하면 누락된 값을 되돌릴 수 있습니다. 사용자는 어떤 값이 누락되었는지에 대한 예를 제공하고 해당 도구에서 표의 모든 데이터를 기반으로 패턴을 작성한 다음 데이터의 패턴을 기반으로 한 새 값을 제안합니다.  
  
 **예제로 채우기** 도구는 Microsoft 로지스틱 회귀 알고리즘을 사용 합니다.  
  
 [Excel 용 예측 &#40;테이블 분석 도구&#41;](forecast-table-analysis-tools-for-excel.md)  
 이 도구는 시간의 경과에 따라 변경되는 데이터를 가져오고 향후의 값을 예측합니다.  
  
 **예측** 도구는 Microsoft 시계열 알고리즘을 사용 합니다.  
  
 [Excel 용 테이블 분석 도구 &#40;예외 강조 표시&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
 이 도구는 데이터 테이블의 패턴을 분석 하 고 패턴에 맞지 않는 행과 값을 찾습니다. 그런 다음 모델을 검토하여 수정한 후 다시 실행하거나 향후 작업을 위해 값에 플래그를 지정합니다.  
  
 **예외 강조 표시** 도구는 Microsoft 클러스터링 알고리즘을 사용 합니다.  
  
 [Excel 용 테이블 분석 도구 &#40;목표 검색 시나리오&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
 **목표 검색** 도구에서 대상 값을 지정 하면이 도구는 해당 대상을 충족 하기 위해 변경 해야 하는 기본 요소를 식별 합니다. 예를 들어, 전화 만족도를 20% 증가시켜야 하는 경우 해당 모델을 통해 목표를 달성하기 위해 변경해야 하는 요소를 예측할 수 있습니다.  
  
 **목표 검색** 도구는 Microsoft 로지스틱 회귀 알고리즘을 사용 합니다.  
  
 [Excel 용 테이블 분석 도구 &#40;가상 시나리오&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
 **가상 분석** 도구는 **목표 검색** 도구를 보완 합니다. 이 도구를 사용하여 변경하려는 값을 입력하면 모델에서 해당 변경을 통해 원하는 결과를 얻기에 충분한지 예측합니다. 예를 들어, 모델을 통해 전화 상담원을 한 명 더 추가하면 해당 시점에서 고객 만족도를 높일 수 있는지 유추할 수 있습니다.  
  
 **가상** 도구는 Microsoft 로지스틱 회귀 알고리즘을 사용 합니다.  
  
 [Excel 용 테이블 분석 도구&#41;예측 계산기 &#40;](prediction-calculator-table-analysis-tools-for-excel.md)  
 이 도구는 대상 결과를 이끄는 요인을 분석하는 모델을 만든 다음 데이터에서 얻어낸 평가 규칙을 기반으로 새로운 입력의 결과를 예측합니다. 또한 새로운 입력을 손쉽게 평가할 수 있는 대화형 의사 결정 워크시트도 생성합니다. 오프라인에서 사용할 수 있는 평가 워크시트 인쇄 버전도 만들 수 있습니다.  
  
 **예측 계산기** 도구는 Microsoft 로지스틱 회귀 알고리즘을 사용 합니다.  
  
 [시장 바구니 분석 &#40;Table AnalysisTools for Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
 이 도구는 교차 판매 또는 상향 판매에서 사용할 수 있는 패턴을 식별합니다. 또한 자주 함께 구매하는 제품의 그룹을 식별하고 관련 제품 번들의 가격 및 비용을 기반으로 보고서를 생성하여 의사 결정도 지원합니다.  
  
 이 도구는 시장 바구니 분석으로만 제한되지 않습니다. 연결 분석에 적합한 모든 문제에 이 도구를 적용할 수 있습니다. 이러한 예로, 자주 함께 발생하는 이벤트, 진단 요소 또는 기타 일련의 잠재적 원인 및 결과를 들 수 있습니다.  
  
 시장 **바구니 분석** 도구는 Microsoft 연결 알고리즘을 사용 합니다.  
  
## <a name="requirements-for-the-table-analysis-tools-for-excel"></a>Excel용 테이블 분석 도구 요구 사항  
 Excel용 테이블 분석 도구를 사용하려면 먼저 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 연결해야 합니다. 이 연결을 통해 데이터 분석에 사용되는 Microsoft 데이터 마이닝 알고리즘에 액세스할 수 있습니다. 인스턴스에 대한 액세스 권한이 없는 경우 관리자에게 요청하여 데이터 마이닝을 시험하는 데 사용할 수 있는 인스턴스를 설정하는 것이 좋습니다. 자세한 내용은 [Excel 용 데이터 마이닝 클라이언트&#41;&#40;원본 데이터에 연결 ](connect-to-source-data-data-mining-client-for-excel.md)을 참조 하세요.  
  
 테이블 분석 도구를 사용하여 데이터 작업을 수행하려면 사용할 데이터 범위를 Excel 테이블로 변환해야 합니다.  
  
 **분석** 리본이 표시 되지 않으면 먼저 데이터 테이블 내부를 클릭 하십시오. 이 메뉴는 데이터 테이블을 선택할 때까지 활성화되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Excel 용 데이터 마이닝 클라이언트 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)   
 [Visio 데이터 마이닝 다이어그램 문제 해결 SQL Server 데이터 마이닝 추가 기능을 &#40;&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)   
 [Office용 데이터 마이닝 추가 기능에 포함된 항목](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
