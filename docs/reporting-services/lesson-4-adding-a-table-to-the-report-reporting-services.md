---
title: '4단원: 보고서에 테이블 추가(Reporting Services) | Microsoft Docs'
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e925dec5eb14365a6c313349599a77ffe1d7ab13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65106013"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>4단원: 보고서에 테이블 추가(Reporting Services)

데이터 세트가 정의되면 보고서 디자인을 시작할 수 있습니다. **도구 상자** 창에서 **디자인 화면**으로 ‘보고서 개체’를 끌어다 놓아 보고서 레이아웃을 만듭니다.  보고서 개체의 몇 가지 유형은 다음과 같습니다.

- Table
- 텍스트 상자
- image
- 선
- 직사각형
- 차트
- 지도

기본 데이터 세트의 반복되는 데이터 행이 포함된 항목을 *데이터 영역*이라고 합니다. 데이터 영역을 추가한 뒤에는 데이터 영역에 필드를 추가할 수 있습니다. 기본 보고서에는 하나의 데이터 영역만 있습니다. 차트와 같은 자세한 정보를 표시하기 위해 데이터 영역을 더 추가할 수 있습니다.

## <a name="add-a-table-data-region-and-fields-to-a-report-layout"></a>보고서 레이아웃에 테이블 데이터 영역 및 필드 추가

1. 보고서 디자이너의 왼쪽 창에서 **도구 상자** 탭을 선택합니다. 마우스로 **Table** 개체를 선택하고 보고서 디자인 화면으로 끕니다. 보고서 디자이너는 디자인 화면 가운데에 세 개의 열이 있는 테이블 데이터 영역을 그립니다. **도구 상자** 탭이 표시되지 않는 경우 **보기** 메뉴 > **도구 상자**를 선택합니다.

    ![ssrs_ssdt_addtable](media/ssrs-ssdt-addtable.png)

    또한 디자인 화면에서 보고서에 테이블을 추가할 수 있습니다. 디자인 화면을 마우스 오른쪽 단추로 클릭하고 **삽입** > **테이블**을 선택합니다.

2. **보고서 데이터** 창에서 AdventureWorksDataset를 확장하여 필드를 표시합니다.

3. **보고서 데이터** 창에서 테이블의 첫 번째 열로 `[Date]` 필드를 끕니다.

    > [!IMPORTANT]
    > 필드를 첫 번째 열에 놓으면 두 가지 동작이 발생합니다. 먼저 보고서 디자이너의 데이터 셀에 ‘필드 식’이라는 필드 이름이 대괄호 안에 표시됩니다. 이 경우 `[Date]`가 표시됩니다.  두 번째로, 필드 식 바로 위의 머리글 행에 열 레이블을 추가합니다. 기본적으로 열 레이블은 필드 이름입니다. 열 레이블을 변경하려는 경우 열 레이블을 선택하고 새 값을 입력할 수 있습니다.

4. **보고서 데이터** 창에서 테이블의 두 번째 열로 `[Order]` 필드를 끕니다.

5. **보고서 데이터** 창에서 테이블의 세 번째 열로 `[Product]` 필드를 끕니다.

6. 세로 커서가 나타나고 마우스 포인터에 더하기 기호(+)가 표시될 때까지 `[Qty]` 필드를 세 번째 열의 오른쪽 가장자리로 끕니다. 마우스 단추를 놓으면 `[Qty]` 필드 식을 위한 네 번째 열이 만들어집니다.

    ![ssrs_tutorial_addcolumn](media/ssrs-tutorial-addcolumn.png)

7. 같은 방법으로 `[LineTotal]` 필드를 추가하여 다섯 번째 열을 만듭니다. 열 레이블이 “Line Total”로 추가됩니다. 보고서 디자이너가 자동으로 “LineTotal”을 두 단어로 분리하여 열 이름을 만듭니다.

다음 다이어그램은 Date, Order, Product, Qty 및 Line Total 필드가 있는 테이블 데이터 영역을 보여 줍니다.
![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

## <a name="preview-your-report"></a>보고서 미리 보기

보고서 미리 보기 기능을 사용하면 보고서 서버에 보고서를 게시하지 않고도 렌더링된 보고서를 볼 수 있으므로 보고서를 디자인하는 동안 자주 미리 보기합니다. 이런 방식으로 디자인 및 데이터 연결의 유효성을 검사하면 디자인하면서 오류와 문제를 수정할 수 있습니다.

### <a name="to-preview-a-report"></a>보고서를 미리 보려면

- **미리 보기** 탭을 선택합니다. 보고서 디자이너에서 보고서가 실행되고 **미리 보기** 뷰에 표시됩니다.

    ![ssrs_ssdt_preview](media/ssrs-ssdt-preview.png)

다음 다이어그램은 **미리 보기** 뷰에 표시된 보고서의 일부를 보여 줍니다.

   ![미리 보기, 5개의 열이 있는 테이블의 세부 정보 행](media/rs-basictabledetailspreview.png "미리 보기, 5개의 열이 있는 테이블의 세부 정보 행")

Date 및 Line Total 값을 확인합니다. 다음 단원에서는 좀 더 깔끔하게 표시되도록 서식을 지정하는 방법을 알아보겠습니다.

> [!NOTE]
> **파일** 메뉴에서 **모두 저장**을 선택하여 보고서를 저장합니다.

## <a name="next-steps"></a>다음 단계

보고서에 테이블 데이터 영역을 추가하고 데이터 영역에 필드를 추가한 다음, 보고서를 미리 보기 했습니다. 다음 단원에서는 열 머리글과 필드 식에 서식을 지정하는 방법을 알아보겠습니다. [5단원: 보고서 서식 지정 &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)에서 계속 진행하세요.
  
## <a name="see-also"></a>관련 항목:

[테이블&#40;보고서 작성기 및 SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)  
[데이터 세트 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
