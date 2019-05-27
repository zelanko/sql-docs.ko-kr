---
title: KPI 폼 편집기 (Kpi 탭, 큐브 디자이너) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpidefinitionpane.f1
ms.assetid: 45c6453a-bbe2-4ca5-836e-c7ef11cfcb65
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca81dda4ce34a498aa471ceed5ea86729b1df508
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079447"
---
# <a name="kpi-form-editor-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>KPI 폼 편집기(KPI 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너의 **KPI** 탭에 있는 **KPI 폼 편집기** 창을 사용하여 선택한 KPI(핵심 성과 지표)를 생성하거나 수정할 수 있습니다.  
  
> [!NOTE]  
>  이 창은 폼 보기에만 표시됩니다.  
  
## <a name="options"></a>변수  
 **이름**  
 KPI의 이름을 입력합니다.  
  
 **연결 된 측정값 그룹**  
 KPI와 관련된 측정값 그룹을 선택합니다. 클라이언트 애플리케이션에서는 이 정보를 사용하여 사용자가 이 KPI를 찾아볼 때 사용할 수 있는 차원을 확인할 수 있습니다.  
  
 **값 식**  
 KPI 값에 대한 MDX(Multidimensional Expression) 식을 보거나 편집하려면 확장합니다.  
  
 KPI 값을 반환하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 **목표 식**  
 KPI의 목표 값에 대한 MDX 식을 보거나 편집하려면 확장합니다.  
  
 KPI 실행 시 KPI의 목표 값을 반환하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 **상태**  
 **상태 그래픽** 및 **상태 식** 옵션을 보려면 확장합니다.  
  
 **상태 그래픽**  
 클라이언트 애플리케이션에서 상태 값을 그래픽 형식으로 나타내기 위해 사용할 그래픽을 선택합니다.  
  
> [!NOTE]  
>  클라이언트 애플리케이션에서 선택한 그래픽을 지원할 수도 있고 적절한 다른 항목으로 대체할 수도 있습니다.  
  
 **상태 식**  
 KPI 실행 시 KPI의 상태 값을 반환하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 이 식이-1과 1 사이의 10 진수를 반환 하는 것이 좋습니다. 값이 작으면 부정적인 추세를 나타내고 값이 크면 긍정적인 추세를 나타냅니다.  
  
> [!NOTE]  
>  1 값-1 아래의 가능 하지만 타사 클라이언트 응용 프로그램에서 올바르게 해석 하지 않을 수 있습니다.  
  
 **추세**  
 **추세 그래픽** 및 **추세 식** 옵션을 보려면 확장합니다.  
  
 **추세 그래픽**  
 클라이언트 애플리케이션에서 추세 값을 그래픽 형식으로 나타내기 위해 사용할 그래픽을 선택합니다.  
  
> [!NOTE]  
>  클라이언트 애플리케이션에서 선택한 그래픽을 지원할 수도 있고 적절한 다른 항목으로 대체할 수도 있습니다.  
  
 **추세 식**  
 KPI의 추세 값을 반환하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 추세 식은 지정한 비즈니스 컨텍스트에 맞는 모든 시간 기반 조건을 사용하여 만들 수 있습니다. 이 식이-1과 1 사이의 10 진수를 반환 하는 것이 좋습니다. 값이 작으면 시간에 따른 부정적인 추세를 나타내고 값이 크면 시간에 따른 긍정적인 추세를 나타냅니다.  
  
> [!NOTE]  
>  1 값-1 아래의 가능 하지만 타사 클라이언트 응용 프로그램에서 올바르게 해석 하지 않을 수 있습니다.  
  
 **추가 속성**  
 **표시 폴더**, **부모 KPI**, **현재 시간 멤버**, **가중치**및 **설명** 옵션을 보려면 확장합니다.  
  
 **표시 폴더**  
 클라이언트 애플리케이션에서 표시를 위해 사용할 KPI 분류를 입력합니다.  
  
 백슬래시(\\)를 사용하여 표시 폴더 내의 폴더 이름을 구분하고 세미콜론(;)을 사용하여 여러 표시 폴더를 구분할 수 있습니다. 예를 들어 `Category\Goal\Scientific;Category\Goal\Metric`과 같이 입력합니다.  
  
 **Parent KPI**  
 클라이언트 애플리케이션에서 사용할 KPI를 분류할 기존 상위 KPI를 선택합니다.  
  
> [!NOTE]  
>  이 옵션을 기존 KPI로 설정하면 **표시 폴더** 는 무시됩니다.  
  
 **현재 시간 멤버**  
 KPI의 임시 컨텍스트를 식별하는 멤버를 반환하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
> [!IMPORTANT]  
>  MDX 식은 **관련된 측정값 그룹**에서 지정한 측정값 그룹과 관련된 시간 차원 내에서 멤버의 고유 이름을 반환해야 합니다.  
  
 **Weight**  
 KPI의 가중 요인에 대한 MDX 식을 보거나 편집하려면 확장합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 **설명**  
 KPI에 대한 선택적 설명을 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Kpi &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
