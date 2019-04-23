---
title: 그룹화 창 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10033"
- sql12.rtp.rptdesigner.group.f1
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 8b4bd0b3-ec97-48f8-8bfb-82a53a2f35a1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fe230d9e3ed5259da9decc87e044005184b7d989
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59948339"
---
# <a name="grouping-pane"></a>그룹화 창
  그룹화 창에는 현재 선택한 테이블릭스 데이터 영역에 대한 행 그룹과 열 그룹이 표시됩니다. 차트 및 계기 데이터 영역은 그룹화 창에서 사용할 수 없습니다. 그룹화 창은 행 그룹 창과 열 그룹 창으로 구성되며 기본 및 고급 모드의 두 가지 모드를 제공합니다. 기본 모드에서는 행 및 열 그룹의 동적 멤버의 계층 뷰를 표시하고 고급 모드에서는 행과 열 그룹의 동적 및 정적 멤버를 모두 표시합니다. 그룹은 데이터 영역에 표시되는 보고서 데이터 세트의 명명된 데이터 세트입니다. 그룹은 정적 및 동적 멤버를 포함하는 계층으로 구성됩니다. 자세한 내용은 [그룹 이해&#40;보고서 작성기 및 SSRS&#41;](../report-design/understanding-groups-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  경우 보이지 그룹화 창에는 **보고서** 메뉴에서 클릭 **그룹화**합니다.  
  
 행과 열 그룹 영역에 있는 셀은 그룹의 정적 또는 동적 멤버일 수 있습니다. 정적 멤버는 그룹당 한 번씩 반복되며 일반적으로 레이블 또는 합계를 포함합니다. 동적 멤버는 그룹 인스턴스당 한 번씩 반복되며 일반적으로 그룹 식의 고유한 값을 포함합니다. 행 그룹 영역이나 열 그룹 영역에 있는 테이블릭스 셀을 선택하면 행 그룹 또는 열 그룹 창에서 해당 그룹 멤버가 선택됩니다. 반대로 그룹화 창에서 그룹을 선택하면 디자인 화면에서 이 그룹 멤버와 연결된 해당 셀이 선택됩니다. 테이블릭스 행 및 열 그룹 영역에 대한 자세한 내용은 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../report-design/tablix-data-region-areas-report-builder-and-ssrs.md)를 참조하세요.  
  
 그룹화 창은 다음과 같은 모드를 지원합니다.  
  
-   **기본.** 기본 모드를 사용하여 그룹을 추가, 편집 또는 삭제할 수 있습니다. 보고서 데이터 창에서 필드를 끌어 그룹 계층에 삽입하여 부모, 자식 및 세부 그룹을 추가할 수 있습니다. 인접 그룹을 추가하려면 **그룹 추가** 바로 가기를 사용해야 합니다. 자세한 내용은 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **고급**. **고급 모드** 를 사용하여 행 및 열 그룹의 모든 멤버를 표시하고 정적 멤버에서 속성을 설정할 수 있습니다. 그룹을 만들거나 합계를 추가하는 경우 테이블릭스 데이터 영역에서 각 보고서 페이지의 행 및 열을 렌더링하는 방법을 제어하는 속성이 자동으로 설정됩니다. 이러한 속성을 수동으로 조정하려면 테이블릭스 멤버에서 속성을 설정해야 합니다. 자세한 내용은 [보고서 페이지에서 테이블릭스 데이터 영역 표시 제어&#40;보고서 작성기 및 SSRS&#41;](../report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)를 참조하세요.  
  
## <a name="default-mode"></a>기본 모드  
 기본 모드에서는 행 그룹 창과 열 그룹 창에 모든 부모 그룹, 자식 그룹 및 인접 그룹에 대한 계층 뷰가 표시됩니다. 자식 그룹은 부모 그룹 아래 들여쓰기되어 표시됩니다. 인접 그룹은 형제 그룹과 같은 들여쓰기 수준으로 표시됩니다. 다음 그림에서는 중첩된 행 그룹 및 열 그룹이 있는 테이블릭스 데이터 영역을 보여 줍니다.  
  
 ![테이블릭스, 중첩 및 인접 행 그룹과 열 그룹](../media/rs-basictablixdesigngroupingpane.gif "테이블릭스, 중첩 및 인접 행 그룹과 열 그룹")  
  
 그룹화 창에는 해당하는 행 및 열 그룹이 표시됩니다. 다음 그림에서 행 그룹 창에는 하위 범주 기반의 그룹이 선택되어 있고 테이블릭스 데이터 영역에는 [Subcat] 그룹화 셀이 선택되어 있습니다.  
  
 ![중첩 행 및 열 그룹에 대한 그룹화 창](../media/rs-basictablixdesigngroupingpanedefaultview.gif "중첩 행 및 열 그룹에 대한 그룹화 창")  
  
 행 그룹 창에서 하위 범주 기반 그룹은 범주 기반 그룹의 자식 항목입니다. 행 그룹 창에서 국가/지역 그룹은 지리 그룹의 자식 항목입니다. 연도 그룹과 국가/지역 그룹은 인접 그룹입니다.  
  
 자세한 내용은 [테이블릭스 데이터 영역 셀, 행 및 열&#40;보고서 작성기 및 SSRS&#41;](../report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="advanced-mode"></a>고급 모드  
 고급 모드에서는 그룹의 모든 정적 및 동적 멤버를 볼 수 있습니다. 멤버를 선택하면 속성 창에 현재 선택한 **테이블릭스 멤버**에 대한 속성이 표시됩니다.  
  
> [!NOTE]  
>  **고급 모드**를 전환하려면 열 그룹 창 옆쪽에 있는 아래쪽 화살표를 마우스 오른쪽 단추로 클릭한 다음 **고급 모드**를 클릭합니다.  
  
 대부분의 경우 정적 및 동적 그룹 행과 열의 표시를 제어하는 속성은 그룹을 만들거나 합계를 추가할 때 자동으로 설정됩니다. 기본값을 편집하려면 행 또는 열 그룹 창의 그룹 멤버를 선택하고 속성 창에서 속성 값을 변경해야 합니다. 사용할 수 있는 속성은 다음과 같습니다.  
  
-   **FixedData**. Boolean입니다. 외부 행 머리글 및 열 머리글에 사용할 수 있습니다. HTML과 같은 렌더러에서 세로로 스크롤할 때 행 그룹 영역을 고정하거나 가로로 스크롤할 때 열 그룹 영역을 고정합니다.  
  
-   **HideIfNoRows**. Boolean입니다. 정적 멤버에만 사용할 수 있습니다. 설정할 경우 Hidden 및 ToggleItem은 무시합니다. 테이블릭스 데이터 영역에 데이터 행이 없는 경우 이 멤버를 숨깁니다.  
  
-   **KeepTogether**.  
  
-   `KeepWithGroup` 을 참조하세요. Boolean입니다. 정적 행 멤버에만 사용할 수 있습니다. 숨기지 않는 경우 가능하면 동적 멤버의 이전 또는 다음 형제와 함께 이 행을 표시합니다.  
  
-   **RepeatOnNewPage**. Boolean입니다. 정적 행 멤버이고 KeepWithGroup이 None이 아닌 경우에만 사용할 수 있습니다. 가능하면 KeepWithGroup에 지정된 동적 멤버의 인스턴스가 하나 이상 있는 모든 페이지에서 이 정적 행을 반복합니다.  
  
-   `Hidden` 을 참조하세요. Boolean입니다. 처음에 행 또는 열을 숨길지 여부를 나타냅니다.  
  
-   **ToggleItem.** 문자열입니다. 토글 이미지를 추가할 입력란의 이름입니다. 입력란은 동일한 그룹 범위 또는 포함 범위에 있어야 합니다.  
  
 테이블릭스 데이터 영역에서 이 동작을 제어하는 방법에 대한 자세한 내용은 [보고서 페이지에서 테이블릭스 데이터 영역 표시 제어&#40;보고서 작성기 및 SSRS&#41;](../report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)를 참조하세요.  
  
 모든 정적 멤버가 디자인 화면의 셀에 해당하는 머리글을 포함하는 것은 아닙니다. 그룹화 창에서 다음 규칙은 정적 멤버에 머리글이 있는지 여부를 나타냅니다.  
  
-   **Static** 머리글 셀이 있는 정적 멤버를 나타냅니다.  
  
-   **(Static)** 머리글 셀이 없는 정적 멤버를 나타내며, hidden static이라고도 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
