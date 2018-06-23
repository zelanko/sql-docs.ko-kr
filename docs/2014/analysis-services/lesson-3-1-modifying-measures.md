---
title: 측정값 수정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7bd48810-15ce-45ff-862b-372d08606995
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: f95003c329dc121c3a743f1f4447a3aa8a9a506a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172291"
---
# <a name="modifying-measures"></a>측정값 수정
  **FormatString** 속성을 사용하여 측정값이 사용자에게 표시되는 방식을 제어하는 서식 설정을 정의할 수 있습니다. 이 태스크에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 통화 및 백분율 측정값에 대한 서식 속성을 지정하는 방법에 대해 설명합니다.  
  
### <a name="to-modify-the-measures-of-the-cube"></a>큐브의 측정값을 수정하려면  
  
1.  **Tutorial 큐브에 대한 큐브 디자이너의** 큐브 구조 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 탭으로 전환하고 **측정값** 창에서 **Internet Sales** 측정값 그룹을 확장한 다음 **Order Quantity**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
2.  속성 창에서 **자동 숨기기** 압정 아이콘을 클릭하여 속성 창을 열려 있게 고정합니다.  
  
     속성 창이 열려 있으면 큐브에 있는 여러 항목의 속성을 보다 쉽게 변경할 수 있습니다.  
  
3.  속성 창에서 **FormatString** 목록을 클릭하고 **#,#** 을 입력합니다.  
  
4.  **큐브 구조** 탭 도구 모음에서 왼쪽의 **측정값 표 표시** 아이콘을 클릭합니다.  
  
     표 뷰를 사용하면 동시에 여러 측정값을 선택할 수 있습니다.  
  
5.  다음 측정값을 선택합니다. CTRL 키를 누른 채 각 측정값을 클릭하면 여러 측정값을 선택할 수 있습니다.  
  
    -   **Unit Price**  
  
    -   **Extended Amount**  
  
    -   **Discount Amount**  
  
    -   **Product Standard Cost**  
  
    -   **Total Product Cost**  
  
    -   **Sales Amount**  
  
    -   **Tax Amt**  
  
    -   **Freight**  
  
6.  속성 창의 **FormatString** 목록에서 **Currency**를 선택합니다.  
  
7.  제목 표시줄 바로 아래의 속성 창 맨 위에 있는 드롭다운 목록에서 **Unit Price Discount Pct**측정값을 선택한 다음 **FormatString** 목록에서 **Percent** 를 선택합니다.  
  
8.  속성 창에서 변경 된 **이름** 속성에 대 한는 **Unit Price Discount Pct** 측정값을 `Unit Price Discount Percentage`합니다.  
  
9. 에 **측정값** 창에서 클릭 **Tax Amt** 이 측정값의 이름을 변경 하 고 `Tax Amount`합니다.  
  
10. 속성 창에서 **자동 숨기기** 아이콘을 클릭하여 속성 창을 숨긴 다음 **큐브 구조** 탭의 도구 모음에서 **측정값 트리 표시** 를 클릭합니다.  
  
11. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [Customer 차원 수정](lesson-3-2-modifying-the-customer-dimension.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 차원 정의](multidimensional-models/define-database-dimensions.md)   
 [측정값 속성 구성](multidimensional-models/configure-measure-properties.md)  
  
  