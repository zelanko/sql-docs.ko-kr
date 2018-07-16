---
title: Excel (SQL Server 데이터 마이닝 추가 기능) 용 데이터 마이닝 클라이언트 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Data Mining Client
- wizards
- getting started
ms.assetid: e075e2de-11cc-4f71-9603-0b161bca8a24
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78a71f5fed5bfcc46742f8554ff69329c3a30b0d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257509"
---
# <a name="data-mining-client-for-excel-sql-server-data-mining-add-ins"></a>Excel용 데이터 마이닝 클라이언트(SQL Server 데이터 마이닝 추가 기능)
  Excel용 데이터 마이닝 클라이언트는 데이터 정리부터 모델 작성 및 예측 쿼리에 이르는 일반적인 데이터 마이닝 작업을 수행할 수 있는 도구 집합입니다. Excel 테이블 또는 범위에서 데이터를 사용하거나 외부 데이터 원본에 액세스할 수 있습니다.  
  
 ![DM](media/dm-tabletools.gif "DM")  
  
-   [데이터 작업](#bkmk_Data)  
  
     Excel에 데이터를 로드하고 데이터를 정리하며 이상값을 확인하고 통계 요약을 만듭니다. 또한 여러 종류의 샘플링을 수행하고 데이터를 프로파일링하고 외부 데이터를 사용하여 모델을 테스트할 수 있습니다. 데이터 마이닝 클라이언트는 복잡한 스크립트 또는 ETL 프로세스 없이 분석용 데이터를 준비하는 가장 쉬운 방법입니다.  
  
-   [모델을 작성 하 고 분석](#bkmk_Model)  
  
     이러한 도구는 클러스터링(K-means 및 EM), 연결 분석, 시계열 분석 및 의사 결정 트리를 포함하여 잘 알려지고 실험적으로 테스트된 데이터 마이닝 알고리즘에 대한 인터페이스를 제공합니다. 각 마법사에 대한 고급 모델링 옵션을 사용하면 Naïve Bayes, 신경망 등의 다른 알고리즘을 선택하고 클러스터 시드 또는 초기 샘플링 크기와 같은 동작을 사용자 지정할 수 있습니다.  
  
     모든 데이터 마이닝 알고리즘은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 인스턴스에 호스팅되어 복잡한 모델을 작성하는 데 더욱 강력한 기능을 제공합니다.  
  
-   [테스트, 쿼리 및 모델 유효성 검사](#bkmk_Validate)  
  
     데이터 마이닝 클라이언트는 리프트 차트 및 교차 유효성 검사를 비롯하여 모델 테스트를 위한 업계 표준 도구를 제공합니다. 제공되는 마법사를 사용하면 데이터 집합의 유효성과 정확성을 쉽게 테스트할 수 있습니다. 쿼리 마법사는 예측 및 평가에 모델을 사용하기 위해 쿼리를 만듭니다.  
  
-   [모델 보기](#bkmk_ViewModels)  
  
     대부분의 도구에서 생성된 차트는 직접 Excel에 저장될 수 있습니다. 사용 된 [Excel에서 모델 찾아보기 &#40;SQL Server 데이터 마이닝 추가 기능&#41; ](browsing-models-in-excel-sql-server-data-mining-add-ins.md) 모델을 탐색 하는 도구입니다.  
  
-   [관리, 문서화 및 배포](#bkmk_UsageMgmt)  
  
     Excel용 데이터 마이닝 클라이언트는 서버에 대한 활성 연결을 유지하므로 서버에 데이터 마이닝 모델을 저장하여 향후 테스트에 사용하거나 확장성을 높이기 위해 프로덕션 서버에 배포하는 데 사용됩니다.  
  
##  <a name="bkmk_Data"></a> 데이터 작업  
 **데이터 준비** 그룹은 데이터 마이닝 작업 준비 시 데이터를 검토하고 지울 수 있는 다음과 같은 마법사를 포함합니다. 또한 대부분의 마법사를 사용하면 데이터를 학습 및 테스트 집합으로 손쉽게 분리할 수 있습니다.  
  
 [데이터 탐색 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 모델 작성 및 저장 시 추가 기능은 다음과 같은 데이터 연결을 지원합니다.  
  
-   모델 저장 및 처리를 위해 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버에 연결합니다.  
  
-   외부 데이터 원본에 대한 선택적 연결. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 원본으로 정의할 수 있는 데이터 형식을 사용하여 모델을 작성하거나 이미 Excel에 있는 데이터를 사용할 수 있습니다.  
  
 [데이터 탐색 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 **데이터 탐색** 마법사를 사용하면 한 번에 한 개씩 선택한 열에 대한 분포 및 값을 그래프로 표시하여 데이터 테이블에 있는 데이터 형식 및 양을 파악할 수 있습니다.  
  
 [샘플 데이터 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](sample-data-sql-server-data-mining-add-ins.md)  
 모델을 학습하고 테스트하기 위해 적합한 종류의 데이터를 만드는 것은 데이터 마이닝에서 중요한 부분이지만 적합한 도구 없이는 힘든 작업입니다. **데이터 샘플링** 마법사를 사용하면 모델에 사용할 데이터를 모델 작성용 그룹과 모델 테스트용 그룹의 두 그룹으로 쉽게 나눌 수 있습니다. 무작위 샘플링 또는 초과 샘플링을 사용할 수 있습니다.  
  
 [예측 계산기 &#40;Excel 용 테이블 분석 도구&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 **이상값 제거** 마법사는 이상값을 식별하여 적절히 처리할 수 있는 몇 가지 도구를 제공합니다. 이것은 값의 분포와 이상값 및 다른 데이터와의 관계를 보여주며 이상값을 제거하거나 변경할지를 결정할 수 있도록 도와줍니다.  
  
 [예측 계산기 &#40;Excel 용 테이블 분석 도구&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 **레이블 재지정** 마법사를 사용하면 분석 결과를 보다 쉽게 이해할 수 있도록 새 데이터 레이블을 만들 수 있습니다. 예를 들어 데이터 범위의 이름을 보다 설명적인 이름으로 바꾸거나 목록에서 대표값을 선택할 수 있습니다.  
  
##  <a name="bkmk_Model"></a> 모델을 작성 하 고 분석  
 도구 모음의 **데이터 모델링** 섹션에 있는 옵션을 사용하여 데이터에서 패턴을 파생시키고 특성을 기반으로 데이터 행을 그룹화하거나 연결을 탐색할 수 있습니다. 이 도구 리본의 마법사는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 사용할 수 있는 강력한 데이터 마이닝 알고리즘에 기반을 두고 있습니다. 이러한 마법사는 Excel용 테이블 분석 도구에 있는 유사 도구와는 달리 알고리즘의 동작을 사용자 지정하고 다양한 데이터 원본을 사용할 수 있도록 해줍니다.  
  
 [분류 마법사 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
 **분류** 마법사를 사용하면 Excel 테이블, Excel 범위 또는 외부 데이터 원본의 기존 데이터를 기반으로 분류 모델을 만들 수 있습니다. 분류 모델을 사용하면 유사성을 나타내는 데이터의 패턴을 추출하여 값 그룹에 따라 예측할 수 있습니다. 예를 들어 수입 또는 지출 패턴을 기반으로 위험을 예측하는 데 분류 모델을 사용할 수 있습니다.  
  
 **분류**  마법사는 다음 Microsoft 데이터 마이닝 알고리즘의 사용을 지원합니다. 즉, 의사 결정 트리 알고리즘, 로지스틱 회귀, Naïve Bayes, 신경망입니다.  
  
 [추정 마법사 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
 **추정** 마법사로 추정 모델을 만들 수 있습니다. 추정 마법사는 데이터 패턴을 추출하고 이 패턴을 사용하여 통화, 판매액, 날짜 또는 시간 등의 숫자 결과를 예측합니다.  
  
 **추정** 마법사는 다음과 같은 Microsoft 데이터 마이닝 알고리즘을 사용합니다. 즉, 의사 결정 트리, 선형 회귀, 로지스틱 회귀, 신경망입니다.  
  
 [주요 영향 요인 분석 &#40;Excel 용 테이블 분석 도구&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 클러스터 마법사를 사용하면 클러스터링 모델을 만들 수 있습니다. 클러스터링 모델은 비슷한 특성을 공유하는 행 그룹을 검색합니다. 이 마법사는 모든 종류의 데이터에서 패턴을 탐색하는 데 유용합니다.  
  
 **클러스터** 마법사는 k-means 및 EM을 포함하는 Microsoft 클러스터링 알고리즘을 사용합니다.  
  
 [연결 마법사 &#40;Excel 용 데이터 마이닝 클라이언트&#41;](associate-wizard-data-mining-client-for-excel.md)  
 **연결** 마법사를 사용하면 Microsoft 연결 규칙 알고리즘을 통해 데이터 마이닝 모델을 만들어 자주 동시 발생하는 항목 또는 이벤트를 검색할 수 있습니다. 이러한 연결 모델은 특히 권장 사항을 만드는 데 유용합니다.  
  
 **연결** 마법사는 Microsoft 연결 규칙 알고리즘을 사용합니다.  
  
 [예측 마법사 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
 **예측** 마법사를 사용하면 시계열의 값을 예측할 수 있습니다. 일반적으로 예측에 사용하는 데이터에는 날짜 스탬프 또는 시퀀스 ID의 몇 가지 시계열 종류가 포함되어 있으며 미래 값을 예측하기 위한 패턴을 유추하는 데 사용합니다.  
  
 **예측** 마법사는 Microsoft 시계열 알고리즘을 사용합니다.  
  
 [고급 모델링 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
 데이터 마이닝에 대해 잘 알고 계십니까? **고급** 데이터 모델링 옵션을 사용하면 사용자 지정 데이터 구조를 만들고 기타 도구 및 마법사에 포함되지 않은 사용자 지정 기능을 사용하여 모델을 작성할 수 있습니다.  
  
##  <a name="bkmk_Validate"></a> 테스트, 쿼리 및 모델 유효성 검사  
 **정확성 및 유효성 검사** 도구 모음에서 이 마법사를 통해 산업 표준 테스트를 사용하여 모델의 정확성을 확인하고 모델을 만들기 위한 데이터 집합의 실행 가능성을 평가합니다.  
  
 [주요 영향 요인 분석 &#40;Excel 용 테이블 분석 도구&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 리프트 차트 또는 산점도 차트를 생성하여 데이터 마이닝 모델의 성능을 평가합니다.  
  
 [분류 행렬 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
 모델이 수행한 정확한 예측 및 부정확한 예측을 요약하는 차트를 만들어 분류 모델의 성능을 평가할 수 있도록 지원합니다.  
  
 [수익 차트 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
 예측을 기반으로 조치를 취하는 비용과 이점과 함께 예측의 정확도를 차트로 만들어 데이터 마이닝 모델의 영향을 파악할 수 있습니다.  
  
 [교차 유효성 검사 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
 모델의 안정성을 파악할 수 있도록 데이터 집합의 여러 하위 집합에서 모델의 정확도를 요약하는 보고서를 만듭니다.  
  
 또한 Excel 테이블의 데이터를 서버에 저장된 마이닝 모델에 대한 예측 쿼리의 입력으로 사용할 수 있습니다.  
  
 [쿼리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](query-sql-server-data-mining-add-ins.md)  
 **쿼리** 마법사를 사용하면 기존의 데이터 마이닝 모델에 대한 예측을 만들 수 있습니다.  
  
 [고급 데이터 마이닝 쿼리 편집기](advanced-data-mining-query-editor.md)  
 이 도구는 고급 사용자를 위해 DMX에 대한 끌어서 놓기 인터페이스를 제공합니다. 구문에 대한 걱정 없이 손쉽게 예측 쿼리 또는 새로운 모델을 만들 수 있습니다.  
  
##  <a name="bkmk_ViewModels"></a> 모델 보기  
 만든 모델은 탐색을 위해 자동으로 열립니다. 그러나 서버에서 모델을 탐색하고 새로운 시각화를 생성할 수도 있습니다. 사용 된 [Visio 셰이프](viewing-data-mining-models-in-visio-data-mining-add-ins.md) 모델 다이어그램을 사용자 지정 가능한 캔버스로 내보낼 합니다.  
  
 [Excel에서 모델 찾아보기 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
 각 모델 유형에 맞게 사용자 지정된 대화형 그래프를 사용하여 만들어진 모델을 확인합니다.  
  
 [마이닝 모델 문서화 &#40;Excel 용 데이터 마이닝 추가 기능&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)  
 이 마법사는 모델에 대한 데이터 집합 및 메타데이터 통계 요약을 제공하여 조사 및 해석을 지원하는 보고서를 만듭니다.  
  
##  <a name="bkmk_UsageMgmt"></a> 관리, 문서화 및 배포  
 이러한 도구를 사용하면 데이터 마이닝 서버에 연결할 뿐만 아니라 모델 관리 및 내보내기, 데이터 마이닝 활동 모니터링을 수행할 수 있습니다.  
  
 [모델 관리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](manage-models-sql-server-data-mining-add-ins.md)  
 필요한 권한이 있는 경우 Excel을 벗어나지 않고도 기존 마이닝 모델 및 구조를 삭제, 수정, 이름 변경 또는 처리할 수 있습니다.  
  
 [추적 &#40;Excel 용 데이터 마이닝 클라이언트&#41;](trace-data-mining-client-for-excel.md)  
 클릭 **추적** Excel 클라이언트 간의 상호 작용을 지속적으로 캡처하여 볼 수 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서버. 모든 작업은 DMX 또는 XMLA 문으로 저장되므로 데이터 마이닝 세션의 문제를 해결하거나 나중에 사용하기 위해 정보를 저장할 수 있습니다.  
  
 [데이터 마이닝 서버에 연결](connect-to-a-data-mining-server.md)  
 Excel을 데이터 마이닝 클라이언트로 사용하려면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 연결해야 합니다. 이를 통해 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 엔진에 액세스할 수 있습니다. 사용 권한이 있는 경우에는 연결을 통해 발견한 모든 패턴을 저장하고 기존 데이터 마이닝 개체를 수정할 수 있습니다.  
  
 합니다 **연결** 인스턴스에 연결 관리 마법사를 제공 하는 도구 모음 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다. 데이터 마이닝 도구와 알고리즘을 사용하려면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결을 정의해야 합니다. 추가 기능을 설치할 때 연결을 만들거나 나중에 추가할 수 있습니다.  
  
 **시작**  
 클릭 합니다 **Getting Started** 인스턴스에 연결을 만드는 과정을 단계별로 안내 하는 구성 마법사를 시작 하는 단추 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 데이터 마이닝을 수행 하는 데 필요한 사용 권한을 취득 합니다.  
  
 **도움말**  
 **도움말** 드롭다운 메뉴는 설치를 완료하고 데이터 마이닝을 시작하는 데 도움이 되는 온라인 도움말, 웹 사이트 및 구성 마법사에 대한 링크를 제공합니다.  
  
 또한 도움말 페이지는 추가 기능, 추가 비디오 및 샘플에 대한 도움말을 포함하여 온라인 리소스로 연결됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Excel 용 테이블 분석 도구](table-analysis-tools-for-excel.md)   
 [Visio 데이터 마이닝 다이어그램 문제 해결 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
