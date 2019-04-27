---
title: 부모-자식 계층의 부모 특성 속성 정의 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 2d78fa73-a13b-4e12-bbd0-43e5307f760c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 36584cce341bdbe0e13b917cbe1bcc47469d0deb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729166"
---
# <a name="defining-parent-attribute-properties-in-a-parent-child-hierarchy"></a>부모-자식 계층의 부모 특성 속성 정의
  부모-자식 계층은 두 개의 테이블 열을 기반으로 하는 차원의 계층입니다. 이 두 열은 차원의 멤버 간 계층 관계를 정의합니다. *멤버 키 열*이라는 첫 번째 열은 각 차원 멤버를 식별합니다. *부모 열*이라는 다른 하나의 열은 각 차원 멤버의 부모를 식별합니다. 부모 특성의 **NamingTemplate** 속성은 부모-자식 계층의 각 수준 이름을 지정하고 **MembersWithData** 속성은 부모 멤버의 데이터 표시 여부를 지정합니다.  
  
 자세한 내용은 [부모-자식 계층 구조](multidimensional-models/parent-child-dimension.md), [부모-자식 계층의 특성](multidimensional-models/parent-child-dimension-attributes.md)  
  
> [!NOTE]  
>  차원 마법사를 사용하여 차원을 만들면 마법사에서 부모-자식 관계가 있는 테이블을 인식하고 자동으로 부모-자식 계층을 정의합니다.  
  
 이 항목의 태스크에서는 **Employee** 차원에서 부모-자식 계층의 각 수준 이름을 정의하는 명명 템플릿을 만든 다음 모든 부모 데이터를 숨기도록 부모 특성을 구성하여 리프 수준 멤버의 판매량만 표시하는 방법에 대해 설명합니다.  
  
## <a name="browsing-the-employee-dimension"></a>Employee 차원 찾아보기  
  
1.  솔루션 탐색기의 **차원** 폴더에서 **Employee.dim** 을 두 번 클릭하여 Employee 차원에 대한 차원 디자이너를 엽니다.  
  
2.  **브라우저** 탭을 클릭하여 **계층** 목록에서 **Employees** 가 선택되어 있는지 확인한 다음 **All Employees** 멤버를 확장합니다.  
  
     **Ken J. Sánchez** 는 이 부모-자식 계층에서 최상위 관리자입니다.  
  
3.  **Ken J. Sánchez** 멤버를 선택합니다.  
  
     이 멤버의 수준 이름은 **Level 02**입니다. 수준 이름은 **All Employees** 멤버 바로 위의 **현재 수준:** 다음에 나타납니다. 다음 태스크에서는 각 수준의 보다 설명적인 이름을 정의하는 방법에 대해 설명합니다.  
  
4.  **Ken J. Sánchez**를 확장하여 이 관리자에게 보고하는 직원의 이름을 표시한 다음 **Brian S. Welcker**를 선택하여 이 수준의 이름을 표시합니다.  
  
     이 멤버의 수준 이름은 **Level 03**입니다.  
  
5.  솔루션 탐색기의 **큐브** 폴더에서 **Analysis Services Tutorial.cube** 를 두 번 클릭하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너를 엽니다.  
  
6.  **브라우저** 탭을 클릭합니다.  
  
7.  Excel 아이콘을 클릭한 다음 연결을 사용하도록 설정할지 묻는 메시지가 나타나면 **사용** 을 클릭합니다.  
  
8.  피벗 테이블 필드 목록에서 **Reseller Sales**를 확장합니다. **Reseller Sales-Sales Amount**를 값 영역으로 끌어옵니다.  
  
9. 피벗 테이블 필드 목록에서 **Employee**를 확장한 다음 **Employees** 계층을 **행** 영역으로 끌어옵니다.  
  
     Employees 계층의 모든 멤버는 피벗 테이블 보고서의 A 열에 추가됩니다.  
  
     다음 그림에서는 확장된 Employees 계층을 보여 줍니다.  
  
10. ![Employees 계층을 보여 주는 피벗 테이블](../../2014/tutorials/media/l4-employee-1.gif "직원 계층을 보여 주는 피벗 테이블")  
  
     Level 03의 각 관리자가 판매한 판매량도 Level 04에 표시됩니다. 각 관리자도 다른 관리자의 직원이기 때문입니다. 다음 태스크에서는 이러한 판매량을 숨기는 방법에 대해 설명합니다.  
  
## <a name="modifying-parent-attribute-properties-in-the-employee-dimension"></a>Employee 차원의 부모 특성 속성 수정  
  
1.  **Employee** 차원에 대한 차원 디자이너로 전환합니다.  
  
2.  **차원 구조** 탭을 클릭한 다음 **특성** 창에서 **Employees** 특성 계층을 선택합니다.  
  
     이 특성의 고유 아이콘이 표시됩니다. 이 아이콘은 해당 특성이 부모-자식 계층의 부모 키임을 의미합니다. 또한 속성 창에서 해당 특성의 **Usage** 속성은 **Parent**로 정의되어 있습니다. 이 속성은 차원이 디자인될 때 차원 마법사에 의해 설정되었습니다. 마법사는 부모-자식 관계를 자동으로 검색했습니다.  
  
3.  속성 창의**NamingTemplate**속성 셀에서 줄임표 단추( **...** )를 클릭합니다.  
  
     **수준 명명 템플릿** 대화 상자에서 사용자가 큐브를 찾아볼 때 표시되는 부모-자식 계층의 수준 이름을 지정하는 수준 명명 템플릿을 정의합니다.  
  
4.  두 번째 행 **\*** 행의 **이름** 열에 **Employee Level \*** 을 입력한 다음 세 번째 행을 클릭합니다.  
  
     **결과** 아래에서 순차적으로 증가하는 번호 다음에 나오는 각 수준의 이름이 "Employee Level"이 됩니다.  
  
     다음 그림에서는 **수준 명명 템플릿** 대화 상자에서 변경 내용을 보여 줍니다.  
  
     ![수준 명명 템플릿 대화 상자](../../2014/tutorials/media/l4-namingtemplate.gif "수준 명명 템플릿 대화 상자")  
  
5.  **확인**을 클릭합니다.  
  
6.  **Employees** 특성의 속성 창에 있는 **MembersWithData** 속성 셀에서 **NonLeafDataHidden** 을 선택하여 **Employees** 특성에 대해 이 값을 변경합니다.  
  
     이렇게 하면 부모-자식 계층의 리프 수준이 아닌 멤버와 관련된 데이터가 숨겨집니다.  
  
## <a name="browsing-the-employee-dimension-with-the-modified-attributes"></a>특성이 수정된 Employee 차원 찾아보기  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  배포가 성공적으로 완료되면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너로 전환한 후 **브라우저** 탭의 도구 모음에서 **다시 연결** 을 클릭합니다.  
  
3.  Excel 아이콘을 클릭한 다음 **사용**을 클릭합니다.  
  
4.  **Reseller Sales-Sales Amount** 를 값 영역으로 끌어옵니다.  
  
5.  **Employees** 계층을 행 레이블 영역으로 끌어옵니다.  
  
     다음 이미지에서는 Employees 계층의 변경 내용을 보여 줍니다. Stephen Y. Jiang은 더 이상 직원으로 나타나지 않습니다.  
  
     ![Employees 계층을 수정할](../../2014/tutorials/media/l4-employee-2.png "수정 직원 계층")  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [자동으로 특성 멤버 그룹화](../analysis-services/lesson-4-3-automatically-grouping-attribute-members.md)  
  
## <a name="see-also"></a>관련 항목  
 [부모-자식 계층](multidimensional-models/parent-child-dimension.md)   
 [부모-자식 계층의 특성](multidimensional-models/parent-child-dimension-attributes.md)  
  
  
