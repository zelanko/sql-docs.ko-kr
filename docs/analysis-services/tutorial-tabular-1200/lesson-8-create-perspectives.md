---
title: 8 단원에는 큐브 뷰 만들기 | Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f68e51be75e84226dd0b1fd3e578fa4031eda04
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403525"
---
# <a name="lesson-8-create-perspectives"></a>8단원: 큐브 뷰 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 Internet Sales 큐브 뷰를 만듭니다. 큐브 뷰는 비즈니스 또는 애플리케이션 중심의 관점에서 파악할 수 있게 해 주는 보기 가능한 모델 하위 집합을 정의합니다. 사용자가 큐브 뷰를 사용 하 여 모델에 연결 하는 경우만 해당 모델 개체 (테이블, 열, 측정값, 계층 및 Kpi) 해당 큐브 뷰에 정의 된 필드로 표시 됩니다.  
  
이 단원에서 만드는 인터넷 판매 큐브 뷰에서 DimCustomer 테이블 개체가 제외 됩니다. 뷰에서 특정 개체를 제외하는 큐브 뷰를 만들면 해당 개체가 모델에는 그대로 있지만 보고 클라이언트 필드 목록에서는 보이지 않습니다. 큐브 뷰에 포함되어 있거나 포함되어 있지 않은 계산 열 및 측정값을 계속해서 제외된 개체 데이터에서 계산할 수 있습니다.  
  
이 단원의 목표는 큐브 뷰를 만드는 방법을 설명하고 테이블 형식 모델 제작 도구를 파악하도록 돕는 데 있습니다. 나중에 추가 테이블을 포함 하도록이 모델을 확장 하는 경우에 예를 들어, 인벤토리 및 Sales 모델의 다양 한 뷰포인트를 정의 하는 추가 큐브 뷰를 만들 수 있습니다. 자세한 내용은 [큐브 뷰](../tabular-models/perspectives-ssas-tabular.md)를 참조하세요.  
  
예상이 단원을 완료 시간: **5 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 이전 단원을 완료 해야 합니다. [7단원: 핵심 성과 지표 만들기](lesson-7-create-key-performance-indicators.md)합니다.  
  
## <a name="create-perspectives"></a>큐브 뷰 만들기  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Internet Sales 큐브 뷰를 만들려면  
  
1.  클릭 합니다 **모델** 메뉴 > **큐브 뷰** > **만들기 및 관리**합니다.  
  
2.  **큐브 뷰** 대화 상자에서 **새 큐브 뷰**를 클릭합니다.  
  
3.  두 번 클릭 합니다 **새 큐브 뷰** 열 머리글을 한 다음 이름 바꾸기 **Internet Sales**합니다.  
  
4.  테이블의 모든 컴퓨터를 선택 *제외한* **DimCustomer**합니다.  
  
    ![as-tabular-lesson8-perspectives](media/as-tabular-lesson8-perspectives.png)
  
    이후 단원에서는 Excel 기능 분석을 사용 하 여이 큐브 뷰를 테스트 하는 합니다. Excel 피벗 테이블 필드 목록에는 DimCustomer 테이블을 제외한 각 테이블이 포함 됩니다.  

## <a name="whats-next"></a>다음 단계
다음 단원으로 이동 합니다. [9 단원: 계층 구조를 만들](lesson-9-create-hierarchies.md)합니다.
  
  
  
  
