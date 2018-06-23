---
title: 예측 (중급 데이터 마이닝 자습서)에 대 한 추가 데이터 원본 뷰 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2665040a-1291-4064-ba01-f458637dda57
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3c355f9755e4dfd2ddd1fcc3f65e1b34857709ca
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312221"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>예측할 데이터 원본 뷰 추가(중급 데이터 마이닝 자습서)
  이 태스크에서 예측 시나리오에 사용할 데이터 원본 뷰를 추가합니다. 예측 모델을 사용하려면 데이터에 시계열의 단계를 식별하는 데 사용할 수 있는 열이 있어야 합니다. 여러 데이터 계열을 분석하려는 경우 모든 계열이 같은 날짜 또는 시간 단계에서 종료해야 합니다.  
  
### <a name="to-add-a-data-source-view"></a>데이터 원본 뷰를 추가하려면  
  
1.  솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **데이터 원본 뷰**를 선택한 후 **새 데이터 원본 뷰**합니다.  
  
2.  **데이터 원본 뷰 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **데이터 원본을 선택** 페이지의 **관계형 데이터 원본**, 선택는 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터 원본. **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  이 데이터 원본이 없을 경우에 데이터 원본을 만드는 단계를 찾을 수 있습니다는 [기본 데이터 마이닝 자습서](../../2014/tutorials/basic-data-mining-tutorial.md)합니다.  
  
4.  에 **테이블 및 뷰 선택** 페이지 vTimeSeries (dbo) 테이블을 선택 하 고 데이터 원본 뷰에 추가 하려면 오른쪽 화살표를 클릭 합니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  에 **마법사 완료** 데이터 원본 뷰의 이름이 기본적으로 페이지 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]합니다. 이름을 변경한 **SalesByRegion**, 클릭 하 고 **마침**합니다.  
  
     데이터 원본 뷰 디자이너가 열리면서 및 **SalesByRegion** 데이터 원본 뷰가 나타납니다.  
  
## <a name="working-with-the-data-source-view"></a>데이터 원본 뷰 작업  
 데이터 원본 뷰를 만든 후 다음과 같은 방법으로 데이터를 탐색할 수 있습니다.  
  
-   디자이너에서 vTimeSeries 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 탐색** 를 표에 선택한 테이블을 엽니다.  
  
-   클릭 **샘플링 옵션** 다음 사용 하 여는 **데이터 탐색 옵션** 샘플링 방법을 변경 하려면 대화 상자. 클릭 **새로 고침** 새 옵션 설정을 사용 하 여 테이블에 데이터를 로드 합니다. 예를 들어 처음 n 개의 행을 선택 하거나, 샘플에 출력할 행 수를 지정할 수 있습니다.  
  
-   VTimeSeries 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성** 테이블에 새 이름을 할당할 수 있습니다. 데이터 원본 뷰에서 개별 열을 선택하고 열 속성을 수정할 수도 있습니다.  
  
-   데이터 원본 뷰 디자인 영역 안을 클릭하여 새 쿼리를 만들고 쿼리에 이름을 할당하거나, 테이블 간의 관계를 만들거나, 디자인 영역의 레이아웃을 변경합니다.  
  
-   테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **새 명명 된 계산** 집계를 포함 하 여 파생된 열을 만들려고 합니다. 이 뷰의 데이터 원본에서 새 테이블과 뷰를 추가할 수도 있습니다.  
  
 다음 태스크에서는 시계열 데이터를 탐색하고 시계열 식별자로 사용할 최상의 열을 결정합니다. 시계열 데이터의 간격을 처리하는 방법도 배웁니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [모델 시계열에 대 한 요구 사항을 이해 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 시계열 알고리즘](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  