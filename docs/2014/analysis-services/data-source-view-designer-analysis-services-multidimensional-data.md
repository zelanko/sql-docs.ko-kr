---
title: 데이터 원본 뷰 디자이너 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.f1
helpviewer_keywords:
- Data Source View Designer
ms.assetid: 6f40a074-761f-440b-a999-09b755bd86ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd19f3a7f4978d2f8bcbd8e62cdf542e05437519
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175170"
---
# <a name="data-source-view-designer-analysis-services---multidimensional-data"></a>데이터 원본 뷰 디자이너(Analysis Services - 다차원 데이터)
  DSV(데이터 원본 뷰)는 다차원 모델에서 큐브 및 차원을 만들기 위해 사용되는 외부 관계형 데이터 원본에 대한 논리적 뷰입니다.

 DSV를 생성한 후에는 **에서** 데이터 원본 뷰 디자이너 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 사용하여 DSV에서 직접 작업할 수 있으므로, 기본 데이터 원본이 다차원 모델에 필요한 누락된 데이터 요소인 경우에 유용할 수 있습니다.

 
  **데이터 원본 뷰 디자이너** 를 열려면:

-   
  **솔루션 탐색기**에서 데이터 원본 뷰를 두 번 클릭합니다.

-   
  **솔루션 탐색기** 에서 데이터 원본 뷰를 마우스 오른쪽 단추로 클릭한 다음 **열기** 또는 **디자이너 보기**를 선택합니다.

 
  **데이터 원본 뷰 디자이너** 에는 도구 모음, DSV의 개체 및 관계를 나타내는 다이어그램, 테이블 및 명명된 쿼리가 알파벳 순서로 나열된 테이블 창, DSV의 특정 다이어그램을 만들고 보는 데 사용되는 다이어그램 구성 도우미 창이 포함됩니다. 테이블 또는 관계를 마우스 오른쪽 단추로 클릭하면 상황에 맞는 명령에 액세스할 수 있습니다.

 ![데이터 원본 뷰 디자이너](media/ssas-dsvdesigner.PNG "데이터 원본 뷰 디자이너")

 최소한 DSV에는 처리 중 모델 개체를 채우는 데 사용되는 관계형 데이터베이스 테이블이 표시됩니다. DSV는 일반적으로 데이터 원본 뷰 마법사를 사용해서 생성됩니다. DSV에 있는 테이블, 열 및 관계는 큐브의 측정값 및 차원의 기초가 됩니다. DSV가 생성된 다음에는 데이터 원본 뷰 디자이너를 사용하여 이를 수정할 수 있습니다.

 대부분의 Analysis Services 개발자는 생성된 DSV를 거의 수정하지 않고 있는 그대로 사용합니다. 특히 원본 데이터가 SQL Server 데이터베이스에 있는 뷰에서 온 경우에는 수정이 거의 필요하지 않습니다. 이 경우, Analysis Services DSV보다 T-SQL 뷰에서 데이터 관계 및 계산을 관리하는 것이 더 편리할 수 있습니다. 하지만 기본 데이터베이스의 소유자가 아닐 경우에는 Analysis Services에서 DSV를 수정하여 모델에 사용되는 데이터 구조를 추가로 개발할 수 있습니다.

## <a name="tasks-in-data-source-view-designer"></a>데이터 원본 뷰 디자이너의 작업
 데이터 원본 뷰 디자이너에서는 DSV를 다음과 같이 편집할 수 있습니다.

|||
|-|-|
|열 또는 테이블의 이름을 바꾸거나 새 계산 열을 만듭니다. 예를 들어 이름과 성을 새로운 전체 이름 열로 연결합니다.|[데이터 원본 뷰에서 명명 된 계산을 정의 하 여 Analysis Services &#40;&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)|
|테이블 관계 수동 추가|[데이터 원본 뷰에서 논리적 관계 정의 Analysis Services &#40;&#41;](multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)|
|T-SQL 쿼리를 기반으로 새로운 개체를 정의하기 위한 명명된 쿼리를 만듭니다.|[데이터 원본 뷰에서 명명 된 쿼리 정의 &#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)|
|기본 데이터를 탐색하여 모델 개체로 표시되는 실제 데이터 값을 봅니다.<br /><br /> 데이터 탐색을 사용하여 기본 차원 테이블 또는 쿼리에서 반환되는 데이터를 시각적으로 검사하고 복사할 수 있습니다. 데이터 탐색 시 기본적으로 샘플 개수 5000개의 최대 개수 샘플링 방법이 사용되지만 이러한 설정을 수정할 수 있습니다.|[데이터 원본 뷰에서 데이터 탐색 &#40;Analysis Services&#41;](multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)|
|DSV에 있는 테이블 및 관계의 일부 또는 전체를 다이어그램으로 작성|[데이터 원본 뷰 디자이너에서 다이어그램 사용 &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)|

## <a name="see-also"></a>참고 항목
 [다차원 모델의 데이터 원본 뷰](multidimensional-models/data-source-views-in-multidimensional-models.md) [데이터 원본 뷰에서 테이블이 나 뷰를 추가 하거나 제거 &#40;Analysis Services&#41;](multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)


