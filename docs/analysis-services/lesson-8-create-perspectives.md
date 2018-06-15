---
title: 9 단원 뷰를 만듭니다. | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e917e817768571e1959ae6163743ecdad0409af
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019790"
---
# <a name="lesson-8-create-perspectives"></a>8단원: 큐브 뷰 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 Internet Sales 큐브 뷰를 만듭니다. 큐브 뷰는 비즈니스 또는 응용 프로그램 중심의 관점에서 파악할 수 있게 해 주는 보기 가능한 모델 하위 집합을 정의합니다. 사용자가 큐브 뷰를 사용 하 여 모델에 연결, 모델 개체만 (테이블, 열, 측정값, 계층 및 Kpi) 해당 큐브 뷰에 정의 된 필드로 표시 됩니다.  
  
이 단원에서 만드는 Internet Sales 큐브 뷰는 DimCustomer 테이블 개체가 제외 됩니다. 뷰에서 특정 개체를 제외하는 큐브 뷰를 만들면 해당 개체가 모델에는 그대로 있지만 보고 클라이언트 필드 목록에서는 보이지 않습니다. 큐브 뷰에 포함되어 있거나 포함되어 있지 않은 계산 열 및 측정값을 계속해서 제외된 개체 데이터에서 계산할 수 있습니다.  
  
이 단원의 목표는 큐브 뷰를 만드는 방법을 설명하고 테이블 형식 모델 제작 도구를 파악하도록 돕는 데 있습니다. 나중에 추가 테이블을 포함 하도록이 모델을 확장 하는 경우에 다양 한 뷰포인트 모델의 예를 들어: Inventory 및 Sales를 정의 하려면 큐브 뷰를 추가로 만들 수 있습니다. 자세한 내용은 [큐브 뷰](../analysis-services/tabular-models/perspectives-ssas-tabular.md)를 참조하세요.  
  
이 단원에 소요되는 예상 시간: **5분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [7 단원: 핵심 성과 지표 만들기](../analysis-services/lesson-7-create-key-performance-indicators.md)합니다.  
  
## <a name="create-perspectives"></a>큐브 뷰 만들기  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Internet Sales 큐브 뷰를 만들려면  
  
1.  클릭는 **모델** 메뉴 > **큐브 뷰** > **만들기 및 관리**합니다.  
  
2.  **큐브 뷰** 대화 상자에서 **새 큐브 뷰**를 클릭합니다.  
  
3.  두 번 클릭 하 고 **새 큐브 뷰** 열 머리글을 다음 이름 바꾸기 **인터넷 판매**합니다.  
  
4.  테이블의 모든 선택 *제외 하 고* **DimCustomer**합니다.  
  
    ![로-테이블 형식-lesson8-큐브 뷰](../analysis-services/media/as-tabular-lesson8-perspectives.png)
  
    이후 단원에서 Excel 기능 분석을 사용 하 여이 큐브 뷰를 테스트 합니다. Excel 피벗 테이블 필드 목록 DimCustomer 테이블을 제외한 각 테이블이 포함 됩니다.  

## <a name="whats-next"></a>다음 단계
다음 단원으로 이동: [9 단원: 계층 구조 만들기](../analysis-services/lesson-9-create-hierarchies.md)합니다.
  
  
  
  
