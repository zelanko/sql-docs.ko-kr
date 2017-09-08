---
title: "특성의 KeyColumn 속성 수정 | Microsoft Docs"
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
- binding attributes [Analysis Services]
- attributes [Analysis Services], binding
- key columns [Analysis Services]
ms.assetid: a2643be4-8123-4cc3-baf9-e5ec54a1669d
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fbf83ccfcec436602ce84a4fa0451102597f2e4c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---modify-the-keycolumn-property"></a>속성을 특성-KeyColumn 속성 수정
  특성의 **KeyColumns** 속성을 수정할 수 있습니다. 예를 들어 단일 키 대신 복합 키를 특성 키로 지정할 수 있습니다.  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>특성의 KeyColumns 속성을 수정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **KeyColumns** 속성을 수정할 프로젝트를 엽니다.  
  
2.  다음 절차 중 하나를 수행하여 차원 디자이너를 엽니다.  
  
    -   **솔루션 탐색기**의 **차원** 폴더에서 차원을 마우스 오른쪽 단추로 클릭한 다음 **열기** 또는 **뷰 디자이너**를 클릭합니다.  
  
         —또는—  
  
    -   큐브 디자이너에서에 **큐브 구조** 탭에서 큐브 차원을 확장 하 고는 **차원** 창을 **편집 \<차원 >**합니다.  
  
3.  **차원 구조** 탭의 **특성** 창에서 수정할 **KeyColumns** 속성이 있는 특성을 클릭합니다.  
  
4.  **속성** 창에서 **KeyColumns** 속성의 값을 클릭합니다.  
  
5.  속성 상자의 값 셀에 나타나는 찾아보기 단추 **(...)** 를 클릭합니다.  
  
     **키 열** 대화 상자가 열립니다.  
  
6.  기존 키 열을 제거하려면 **키 열** 목록에서 열을 선택한 다음 **\<** 단추를 클릭합니다.  
  
7.  키 열을 추가하려면 **사용 가능한 열** 목록에서 열을 선택한 다음 **>** 단추를 클릭합니다.  
  
    > [!NOTE]  
    >  키 열을 여러 개 정의하는 경우 해당 열이 **키 열** 목록에 표시되는 순서에 따라 표시 순서가 결정됩니다. 예를 들어 월 특성에는 월과 연도라는 두 개의 키 열이 있습니다. 목록에서 연도 열이 월 열 앞에 표시되는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 연도순으로 정렬한 다음 월순으로 정렬합니다. 월 열이 연도 열 앞에 표시되는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 월순으로 정렬한 다음 연도순으로 정렬합니다.  
  
8.  키 열의 순서를 변경하려면 열을 선택한 다음 **위로** 또는 **아래로** 단추를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [차원 특성 속성 참조](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
