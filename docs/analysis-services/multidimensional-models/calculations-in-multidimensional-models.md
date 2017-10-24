---
title: "다차원 모델의 계산 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calculations [Analysis Services], creating
- deleting calculations
- calculations [Analysis Services], scripts
- Cube Designer
- modifying scripts
- removing calculations
- calculations [Analysis Services], deleting
- scripts [Analysis Services], calculations
- cubes [Analysis Services], calculations
- solve orders [Analysis Services]
ms.assetid: c21b3459-9bef-45a2-aba5-c992eba5b66e
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 725f0ac6753947e587b6746528b6efc6d409f269
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="calculations-in-multidimensional-models"></a>다차원 모델의 계산
  큐브 디자이너의 **계산** 탭을 사용하여 계산 멤버, 명명된 집합 및 기타 MDX(Multidimensional Expression) 계산을 만들 수 있습니다.  
  
 **계산** 탭에는 다음과 같은 세 개의 창이 있습니다.  
  
-   **스크립트 구성 도우미** 창 - 큐브의 계산이 나열됩니다. 이 창을 사용하여 계산을 만들고 구성하고 선택하여 편집할 수 있습니다.  
  
-   **계산 도구** 창 - 계산을 만들 때 사용할 수 있는 메타데이터, 함수 및 템플릿을 제공합니다.  
  
-   계산 식 창 - 폼 보기와 스크립트 보기를 지원합니다.  
  
> [!NOTE]  
>  MDX 스크립팅에 대한 자세한 내용은 [Microsoft SQL Server 2005의 MDX 스크립팅 소개(Introduction to MDX Scripting in Microsoft SQL Server 2005)](http://go.microsoft.com/fwlink/?LinkId=81892)를 참조하고, Microsoft TechNet 웹 사이트의 [SQL Server 2005 - Analysis Services](http://go.microsoft.com/fwlink/?LinkId=80853) 페이지에 있는 추가 리소스 섹션을 참조하십시오. 큐브 디자인과 관련된 성능 문제에 대한 자세한 내용은 [SQL Server 2005 Analysis Services 성능 가이드(SQL Server 2005 Analysis Services Performance Guide)](http://go.microsoft.com/fwlink/?LinkId=81621)를 참조하십시오.  
  
## <a name="creating-a-new-calculation"></a>새 계산 만들기  
 새 계산을 만들려면 큐브 디자이너의 **계산** 탭에서 **큐브** 메뉴를 선택하고 만들려는 계산 유형에 따라 **새 계산 멤버**, **새 명명된 집합**또는 **새 스크립트 명령**을 클릭합니다. 도구 모음에서 해당 단추를 클릭하거나 **스크립트 구성 도우미** 창에서 아무데나 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 명령 중 하나를 클릭할 수도 있습니다. 이렇게 하면 **스크립트 구성 도우미** 창에 새 계산이 추가되고 계산 식 창의 계산 폼에 계산에 대한 필드가 표시됩니다. 새 스크립트를 만드는 경우에는 계산 식 창에 스크립트 보기가 열립니다. 세 가지 유형의 계산을 작성하는 방법은 [계산 멤버 만들기](../../analysis-services/multidimensional-models/create-calculated-members.md), [명명된 집합 만들기](../../analysis-services/multidimensional-models/create-named-sets.md)및 [할당 및 기타 스크립트 명령 정의](../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)를 참조하세요.  
  
## <a name="editing-scripts"></a>스크립트 편집  
 **계산** 탭의 계산 식 창에서 스크립트를 편집합니다. 계산 식 창에는 스크립트 보기와 폼 보기가 있습니다. 폼 보기에는 단일 명령에 대한 식과 속성이 표시됩니다. MDX 스크립트를 편집할 때는 식 상자가 전체 폼 보기를 채웁니다.  
  
 스크립트 보기에는 스크립트를 편집할 수 있는 코드 편집기가 있습니다. 계산 식 창이 스크립트 보기 상태에 있는 경우에는 **스크립트 구성 도우미** 창이 사라집니다. 스크립트 보기는 색 구분, 괄호 일치, 자동 완성 및 MDX 코드 영역을 제공합니다. 편집하기 쉽도록 MDX 코드 영역을 축소하거나 확장할 수 있습니다.  
  
 **큐브** 메뉴에서 **계산 표시 위치**를 가리킨 다음 **스크립트** 또는 **폼**을 클릭하여 폼 보기와 스크립트 보기 간에 전환할 수 있습니다. 도구 모음에서 **폼 보기** 또는 **스크립트 보기** 를 클릭하여 전환할 수도 있습니다.  
  
## <a name="changing-solve-order"></a>계산 순서 변경  
 계산은 **스크립트 구성 도우미** 창에 나열된 순서로 수행됩니다. 계산을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **위로 이동** 또는 **아래로 이동** 을 클릭하여 계산 순서를 바꿀 수 있습니다. 계산을 클릭한 다음 도구 모음에서 **위로 이동** 또는 **아래로 이동** 단추를 클릭할 수도 있습니다.  
  
 계산 셀과 계산 멤버에 대한 계산 순서를 수동으로 다시 지정할 수 있습니다. 패스 순서 및 계산 순서에 대한 자세한 내용은 [패스 순서 및 계산 순서 이해&#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)를 참조하세요.  
  
## <a name="deleting-a-calculation"></a>계산 삭제  
 기존 계산을 삭제하려면 **스크립트 구성 도우미** 창의 **계산** 탭에서 삭제할 계산을 선택하고 **편집** 메뉴에서 **삭제** 를 클릭하거나 도구 모음에서 **삭제** 아이콘을 클릭합니다. **스크립트 구성 도우미** 창에서 계산을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **삭제** 를 선택할 수도 있습니다.  
  
  

