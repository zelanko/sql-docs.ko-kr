---
title: '6단원: 계산 정의 | Microsoft Docs'
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e4b4dbae844177fe121fcf1b22f4f6bf68c8584
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403885"
---
# <a name="lesson-6-defining-calculations"></a>6단원: 계산 정의
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

이 단원에서는 MDX(Multidimensional Expressions) 식 또는 스크립트에 해당하는 계산을 정의하는 방법을 배웁니다. 계산을 사용하면 계산 멤버와 명명된 집합을 정의하고 기타 스크립트 명령을 실행하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브의 기능을 확장할 수 있습니다. 예를 들어 스크립트 명령을 실행하여 하위 큐브를 정의한 다음 하위 큐브의 셀에 계산을 할당할 수 있습니다.  
  
큐브 디자이너에서 새 계산을 정의하면 큐브 디자이너의 **계산** 탭에 있는 **스크립트 구성 도우미** 창에 해당 계산이 추가되며 **계산 식** 창의 계산 폼에 특정 계산 유형에 대한 필드가 표시됩니다. 계산은 **스크립트 구성 도우미** 창에 나열된 순서대로 실행됩니다. 특정 계산을 마우스 오른쪽 단추로 클릭한 후 **위로 이동** 또는 **아래로 이동**을 선택하거나 특정 계산을 클릭한 후 **계산** 탭 도구 모음에 있는 **위로 이동** 또는 **아래로 이동** 아이콘을 사용하여 계산 순서를 다시 지정할 수 있습니다.  
  
**계산** 탭에서 새 계산을 추가하고 **계산 식** 창의 다음 보기 중 하나에서 기존 계산을 보거나 편집할 수 있습니다.  
  
-   폼 보기. 이 보기는 단일 명령에 대한 식 및 속성을 그래픽 형식으로 표시합니다. MDX 스크립트를 편집하면 폼 보기가 식 상자로 채워집니다.  
  
-   스크립트 보기. 이 보기에서는 모든 계산 스크립트가 코드 편집기에 표시되므로 계산 스크립트를 쉽게 변경할 수 있습니다. **계산 식** 창이 스크립트 보기에 표시되면 **스크립트 구성 도우미** 가 숨겨집니다. 스크립트 보기는 색 구분, 괄호 일치, 자동 완성 및 MDX 코드 영역을 제공합니다. 보다 쉬운 편집 작업을 위해 MDX 코드 영역을 확장하거나 축소할 수 있습니다.  
  
**계산 식** 창에서 이러한 보기 간 전환을 하려면 **계산** 탭 도구 모음에서 **폼 보기** 또는 **스크립트 보기** 를 클릭합니다.  
  
> [!NOTE]  
> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 계산에서 구문 오류를 검색하면 스크립트 보기에서 오류를 수정할 때까지 폼 보기가 표시되지 않습니다.  
  
비즈니스 인텔리전스 마법사를 사용하여 큐브에 특정 계산을 추가할 수도 있습니다. 예를 들어 이 마법사를 사용하여 큐브에 시간 인텔리전스를 추가할 수 있습니다. 즉, 월간 누계, 이동 평균 또는 기간별 누계와 같은 시간 관련 계산에 대한 계산 멤버를 정의할 수 있습니다. 자세한 내용은 [비즈니스 인텔리전스 마법사를 사용하여 시간 인텔리전스 계산 정의](../multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)를 참조하세요.  
  
> [!IMPORTANT]  
> **계산** 탭에서 계산 스크립트는 CALCULATE 명령으로 시작됩니다. CALCULATE 명령은 큐브의 셀 집계를 제어하므로 큐브 셀의 집계 방식을 수동으로 지정하려는 경우에만 이 명령을 편집해야 합니다.  
  
자세한 내용은 [계산](../multidimensional-models-olap-logical-cube-objects/calculations.md)및 [다차원 모델의 계산](../multidimensional-models/calculations-in-multidimensional-models.md)을 참조하세요.  
  
> [!NOTE]  
> 이 자습서의 모든 단원에 대한 완료된 프로젝트를 온라인으로 사용할 수 있습니다. 이전 단원에서 완료된 프로젝트를 시작 지점으로 사용하여 어떠한 단원으로든 이동할 수 있습니다. 이 자습서와 함께 제공되는 샘플 프로젝트를 다운로드하려면[여기를 클릭](http://go.microsoft.com/fwlink/?LinkID=221866) 하십시오.  
  
이 단원에서는 다음 태스크를 다룹니다.  
  
[계산 멤버 정의](lesson-6-1-defining-calculated-members.md)  
이 태스크에서는 계산 멤버의 정의 방법을 배웁니다.  
  
[명명된 집합 정의](lesson-6-2-defining-named-sets.md)  
이 태스크에서는 명명된 집합의 정의 방법을 배웁니다.  
  
## <a name="next-lesson"></a>다음 단원  
[7단원: 핵심 성과 지표를 정의 합니다. &#40;Kpi&#41;](lesson-7-defining-key-performance-indicators-kpis.md)  
  
## <a name="see-also"></a>관련 항목  
[Analysis Services Tutorial 시나리오](analysis-services-tutorial-scenario.md)  
[명명된 집합 만들기](../multidimensional-models/create-named-sets.md)  
[계산 멤버 만들기](../multidimensional-models/create-calculated-members.md)  
  
  
  
