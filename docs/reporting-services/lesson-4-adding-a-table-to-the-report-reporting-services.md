---
title: '4단원: 보고서에 테이블 추가(Reporting Services) | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 08632bb104904a20a730b0e4439d0bdef71441fb
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274475"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>4단원: 보고서에 테이블 추가(Reporting Services)
데이터 집합이 정의되면 보고서 디자인을 시작할 수 있습니다. 데이터 영역, 입력란, 이미지 및 보고서에 포함하려는 항목을 디자인 화면에 끌어다 놓는 방법으로 보고서 레이아웃을 만듭니다.  
  
기본 데이터 집합의 반복되는 데이터 행이 포함된 항목을 *데이터 영역*이라고 합니다. 기본 보고서에는 데이터 영역이 하나만 있지만 테이블 형식 보고서에 차트를 추가할 때처럼 필요한 경우에는 데이터 영역을 추가할 수 있습니다. 데이터 영역을 추가한 뒤에는 데이터 영역에 필드를 추가할 수 있습니다.  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>보고서 레이아웃에 테이블 데이터 영역과 필드를 추가하려면  
  
1.  **도구 상자**에서 **테이블**을 클릭하고 디자인 화면을 클릭하여 마우스를 끕니다. 보고서 디자이너는 디자인 화면 가운데에 세 개의 열이 있는 테이블 데이터 영역을 그립니다. **보고서 데이터** 창의 왼쪽에 **도구 상자** 가 탭으로 나타날 수 있습니다. **도구 상자**를 열려면 포인터를 **도구 상자** 탭으로 이동합니다. **도구 상자**가 표시되지 않으면 **보기** 메뉴에서 **도구 상자**를 클릭합니다.
  
     ![ssrs_ssdt_addtable](../reporting-services/media/ssrs-ssdt-addtable.png) 
  
  또한 디자인 화면에서 보고서에 테이블을 추가할 수 있습니다.  디자인 화면을 마우스 오른쪽 단추로 클릭하고 **삽입** , **테이블**을 차례로 클릭합니다.
2.  **보고서 데이터** 창에서 **AdventureWorksDataset** 데이터 집합을 확장하여 필드를 표시합니다.  
  
3.  *보고서 데이터* 창에서 **Date** 필드를 테이블의 첫 번째 열로 끕니다.  
  
    필드를 첫 번째 열에 놓으면 두 가지 동작이 발생합니다. 먼저 데이터 셀에는 *필드 식*이라는 필드 이름이 대괄호 안에 표시됩니다. 이 경우 `[Date]`와 같이 표시됩니다. 두 번째로 열 머리글 값이 자동으로 필드 식 바로 위의 머리글 행에 추가됩니다. 기본적으로 열은 필드 이름입니다. 머리글 행 텍스트를 선택한 다음 새 이름을 입력할 수 있습니다.  
  
4.  *보고서 데이터* 창에서 **Order** 필드를 테이블의 두 번째 열로 끕니다.  
  
5.  *보고서 데이터* 창에서 **Product** 필드를 테이블의 세 번째 열로 끕니다.  
  
6.  세로 커서가 나타나고 포인터가 더하기 기호(+)로 바뀔 때까지 Qty 필드를 세 번째 열의 오른쪽 가장자리로 끕니다. 마우스 단추를 놓으면 네 번째 열이 `[Qty]`에 대해 만들어집니다.  
![ssrs_tutorial_addcolumn](../reporting-services/media/ssrs-tutorial-addcolumn.png)  
  
7.  같은 방법으로 LineTotal 필드를 추가하여 다섯 번째 열을 만듭니다. 열 머리글은 Line Total입니다. 보고서 디자이너가 자동으로 LineTotal을 두 단어로 분리하여 열의 이름을 만듭니다.  
  
  
다음 다이어그램은 Date, Order, Product, Qty 및 Line Total 필드가 있는 테이블 데이터 영역을 보여 줍니다.  
![rs_BasicTableDetailsDesign](../reporting-services/media/rs-basictabledetailsdesign.png)  
  
## <a name="preview-your-report"></a>보고서 미리 보기  
보고서 미리 보기 기능을 사용하면 보고서 서버에 보고서를 게시하지 않고도 렌더링된 보고서를 볼 수 있으므로 디자인 타임에 보고서를 자주 미리 보면서 작업할 수 있습니다. 보고서를 미리 보면 디자인 및 데이터 연결에 대한 유효성 검사를 실행할 수 있으므로 보고서를 보고서 서버에 게시하기 전에 오류 및 문제를 수정할 수 있습니다.  
  
#### <a name="to-preview-a-report"></a>보고서를 미리 보려면  
  
-   미리 보기 도구 모음에서 **미리 보기** 탭을 클릭합니다. 보고서가 실행되어 미리 보기 뷰에 표시됩니다.
![ssrs_ssdt_preview](../reporting-services/media/ssrs-ssdt-preview.png)  
  
    다음 다이어그램은 미리 보기 뷰에 표시된 보고서의 일부를 보여 줍니다.  
  
    ![미리 보기, 5개의 열이 있는 테이블의 정보 행](../reporting-services/media/rs-basictabledetailspreview.png "미리 보기, 5개의 열이 있는 테이블의 정보 행")  
  
    통화(Line Total 열)의 소수점 뒤에 6자리가 있고 날짜에는 타임스탬프가 있습니다. 다음 단원에서는 이러한 서식을 수정합니다.  
  
> [!NOTE]  
> **파일** 메뉴에서 **모두 저장** 을 클릭하여 보고서를 저장합니다.  
  
## <a name="next-steps"></a>Next Steps  
보고서에 테이블 데이터 영역을 추가하고, 데이터 영역에 필드를 추가하고, 보고서를 미리 보는 방법을 배웠습니다. 다음 단원에서는 열 머리글과 날짜 및 통화 값에 서식을 지정합니다. [5단원: 보고서 서식 지정&#40;Reporting Services&#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[테이블&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
