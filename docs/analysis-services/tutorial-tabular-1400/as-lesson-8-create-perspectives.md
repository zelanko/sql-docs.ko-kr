---
title: 'Analysis Services 자습서 단원 8: 큐브 뷰 만들기 | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: c74e457d29f39201601a3a62d651cce97c52fa70
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207308"
---
# <a name="create-perspectives"></a>큐브 뷰 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 인터넷 판매 큐브 뷰를 만들 수 있습니다. 큐브 뷰는 비즈니스 또는 애플리케이션 중심의 관점에서 파악할 수 있게 해 주는 보기 가능한 모델 하위 집합을 정의합니다. 사용자가 큐브 뷰를 사용 하 여 모델에 연결 하는 경우만 해당 모델 개체 (테이블, 열, 측정값, 계층 및 Kpi) 해당 큐브 뷰에 정의 된 필드로 표시 됩니다. 자세한 내용은 [큐브 뷰](../tabular-models/perspectives-ssas-tabular.md)를 참조하세요.
  
이 단원에서 만드는 인터넷 판매 큐브 뷰에서 DimCustomer 테이블 개체가 제외 됩니다. 뷰에서 특정 개체가 제외 된 큐브 뷰를 만들 때 해당 개체는 여전히 모델에 존재 합니다. 그러나 보고 클라이언트 필드 목록에 표시 되지 않습니다. 큐브 뷰에 포함되어 있거나 포함되어 있지 않은 계산 열 및 측정값을 계속해서 제외된 개체 데이터에서 계산할 수 있습니다.  
  
이 단원의 목표는 큐브 뷰를 만드는 방법을 설명하고 테이블 형식 모델 제작 도구를 파악하도록 돕는 데 있습니다. 나중에 추가 테이블을 포함 하도록이 모델을 확장 하는 경우에 예를 들어, 인벤토리 및 Sales 모델의 다양 한 뷰포인트를 정의 하는 추가 큐브 뷰를 만들 수 있습니다.  
  
예상이 단원을 완료 시간: **5분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 이전 단원을 완료 해야 합니다. [7단원: 핵심 성과 지표 만들기](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)합니다.  
  
## <a name="create-perspectives"></a>큐브 뷰 만들기  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Internet Sales 큐브 뷰를 만들려면  
  
1.  클릭 합니다 **모델** 메뉴 > **큐브 뷰** > **만들기 및 관리**합니다.  
  
2.  **큐브 뷰** 대화 상자에서 **새 큐브 뷰**를 클릭합니다.  
  
3.  두 번 클릭 합니다 **새 큐브 뷰** 열 머리글을 한 다음 이름 바꾸기 **Internet Sales**합니다.  
  
4.  모든 테이블 선택 *제외한* **DimCustomer**합니다.  
  
    ![as-lesson8-perspectives](../tutorial-tabular-1400/media/as-lesson8-perspectives.png)
  
    이후 단원에서이 큐브 뷰를 테스트 하려면 Excel 기능에서 분석을 사용 합니다. Excel 피벗 테이블 필드 목록에는 DimCustomer 테이블을 제외한 각 테이블이 포함 됩니다.  

## <a name="whats-next"></a>다음 단계

[9 단원: 계층 구조를 만들](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)합니다.
  
  
  
  
