---
title: 큐브를 찾아볼 때 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 3819946e-d3fa-4c1d-afe3-599c938b1b2e
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2bbbf3d7badcc519f033853d19f01b090b06167f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-2-6---browsing-the-cube"></a>단원 2-6-큐브 찾아보기
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

큐브를 배포하면 큐브 디자이너의 **브라우저** 탭에 큐브 데이터가 표시되고 차원 디자이너의 **브라우저** 탭에 차원 데이터가 표시됩니다. 큐브 및 차원 데이터 검색을 통해 작업을 증분 확인할 수 있습니다. 개체가 처리된 후 속성, 관계 및 기타 개체에 대한 약간의 변경으로 원하는 결과를 얻었는지 확인할 수 있습니다. 브라우저 탭을 사용하여 큐브 데이터와 차원 데이터 모두를 확인할 수 있지만 이 탭에서는 검색하려는 개체에 따라 다른 기능을 제공합니다.  
  
차원의 경우 브라우저 탭은 리프 노드까지 모두 계층을 탐색하거나 멤버를 볼 수 있는 방법을 제공합니다. 모델에 번역을 추가한 경우 여러 다른 언어로 차원 데이터를 검색할 수 있습니다.  
  
큐브의 경우 브라우저 탭은 데이터를 탐색하는 두 가지 방법을 제공합니다. 기본 제공 MDX 쿼리 디자이너를 사용하여 다차원 데이터베이스에서 일반 행 집합을 반환하는 쿼리를 작성할 수 있습니다. 또는 Excel 바로 가기를 사용할 수 있습니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 Excel을 시작하면 이미 워크시트에 피벗 테이블이 있고 모델 작업 영역 데이터베이스에 연결이 미리 정의된 상태로 Excel이 열립니다.  
  
Excel에서는 가로 축과 세로 축을 통해 데이터의 관계를 분석하여 큐브 데이터를 대화형으로 탐색할 수 있도록 하므로 일반적으로 더 나은 검색 환경을 제공합니다. 반면 MDX 쿼리 디자이너는 단일 축으로 제한됩니다. 또한 행 집합이 일반화되므로 Excel 피벗 테이블에서 제공하는 드릴 다운을 얻지 못합니다. 이후 단원에서 큐브에 차원과 계층을 많이 추가할수록 Excel이 데이터를 검색하기에 좋은 솔루션임을 알게 됩니다.  
  
### <a name="to-browse-the-deployed-cube"></a>배포된 큐브를 찾아보려면  
  
1.  **에서 Product 차원에 대한** 차원 디자이너 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]로 전환합니다. 이렇게 하려면 솔루션 탐색기의 **차원** 노드에서 **Product** 차원을 두 번 클릭합니다.  
  
2.  **브라우저** 탭을 클릭하여 **Product Key** 특성 계층의 **All** 멤버를 표시합니다. 3단원에서는 차원을 탐색할 수 있도록 Product 차원에 대한 사용자 계층을 정의합니다.  
  
3.  **에서** 큐브 디자이너 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]로 전환합니다. 이렇게 하려면 솔루션 탐색기의 **큐브** 노드에서 **Analysis Services Tutorial** 큐브를 두 번 클릭합니다.  
  
4.  **브라우저** 탭을 선택한 다음 디자이너 도구 모음에서 **다시 연결** 아이콘을 클릭합니다.  
  
    디자이너 왼쪽 창에 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브의 개체가 표시됩니다. **브라우저** 탭의 오른쪽에는 두 개의 창이 있습니다. 위쪽 창은 **필터** 창이고 아래쪽 창은 **데이터** 창입니다. 다음 단원에서는 큐브 브라우저를 사용하여 분석을 수행합니다.  
  
## <a name="next-lesson"></a>다음 단원  
[3 단원: 측정값, 특성 및 계층 수정](../analysis-services/lesson-3-modifying-measures-attributes-and-hierarchies.md)  
  
## <a name="see-also"></a>참고 항목  
[MDX 쿼리 편집기&#40;Analysis Services - 다차원 데이터&#41;](http://msdn.microsoft.com/library/777f2c23-1c1c-4b72-9d19-48a4866551f8)  
  
  
  
