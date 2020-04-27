---
title: '4단원: 보고서에 테이블 추가(Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3bb152b749041451cdb3a3294c24d8b172c49a99
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108446"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>4단원: 보고서에 테이블 추가(Reporting Services)
  데이터 세트가 정의되면 보고서 디자인을 시작할 수 있습니다. 데이터 영역, 입력란, 이미지 및 보고서에 포함하려는 항목을 디자인 화면에 끌어다 놓는 방법으로 보고서 레이아웃을 만듭니다.  
  
 기본 데이터 세트의 반복되는 데이터 행이 포함된 항목을 *데이터 영역*이라고 합니다. 기본 보고서에는 데이터 영역이 하나만 있지만 테이블 형식 보고서에 차트를 추가할 때처럼 필요한 경우에는 데이터 영역을 추가할 수 있습니다. 데이터 영역을 추가한 뒤에는 데이터 영역에 필드를 추가할 수 있습니다.  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>보고서 레이아웃에 테이블 데이터 영역과 필드를 추가하려면  
  
1.  **도구 상자**에서 **테이블**을 클릭하고 디자인 화면을 클릭하여 마우스를 끕니다. 보고서 디자이너는 디자인 화면 가운데에 세 개의 열이 있는 테이블 데이터 영역을 그립니다.  
  
    > [!NOTE]  
    >  **보고서 데이터** 창의 왼쪽에 **도구 상자** 가 탭으로 나타날 수 있습니다. **도구 상자**를 열려면 포인터를 **도구 상자** 탭 위로 이동 합니다. **도구 상자가** 표시 되지 않으면 **보기** 메뉴에서 **도구 상자**를 클릭 합니다.  
  
2.  **보고서 데이터** 창에서 **AdventureWorksDataset** 데이터 집합을 확장 하 여 필드를 표시 합니다.  
  
3.  보고서 데이터 창에서 **Date** 필드를 테이블의 첫 번째 열로 끕니다.  
  
     필드를 첫 번째 열에 놓으면 두 가지 동작이 발생합니다. 먼저 데이터 셀에는 *필드 식*이라는 필드 이름이 대괄호 안에 표시됩니다. 이 경우 `[Date]`와 같이 표시됩니다. 두 번째로 열 머리글 값이 자동으로 필드 식 바로 위의 머리글 행에 추가됩니다. 기본적으로 열은 필드 이름입니다. 머리글 행 텍스트를 선택한 다음 새 이름을 입력할 수 있습니다.  
  
4.  보고서 데이터 창에서 **Order** 필드를 테이블의 두 번째 열로 끕니다.  
  
5.  보고서 데이터 창에서 **Product** 필드를 테이블의 세 번째 열로 끕니다.  
  
6.  세로 커서가 나타나고 포인터가 더하기 기호(+)로 바뀔 때까지 Qty 필드를 세 번째 열의 오른쪽 가장자리로 끕니다. 마우스 단추를 놓으면 네 번째 열이 `[Qty]`에 대해 만들어집니다.  
  
7.  같은 방법으로 LineTotal 필드를 추가하여 다섯 번째 열을 만듭니다.  
  
    > [!NOTE]  
    >  열 머리글은 Line Total입니다. 보고서 디자이너가 자동으로 LineTotal을 두 단어로 분리하여 열의 이름을 만듭니다.  
  
     다음 다이어그램은 Date, Order, Product, Qty 및 Line Total 필드가 있는 테이블 데이터 영역을 보여 줍니다.  
  
     ![디자인, 머리글 행과 정보 행이 있는 테이블](../../2014/tutorials/media/rs-basictabledetailsdesign.gif "디자인, 머리글 행과 정보 행이 있는 테이블")  
  
## <a name="preview-your-report"></a>보고서 미리 보기  
 보고서 미리 보기 기능을 사용하면 보고서 서버에 보고서를 게시하지 않고도 렌더링된 보고서를 볼 수 있으므로 디자인 타임에 보고서를 자주 미리 보면서 작업할 수 있습니다. 보고서를 미리 보면 디자인 및 데이터 연결에 대한 유효성 검사를 실행할 수 있으므로 보고서를 보고서 서버에 게시하기 전에 오류 및 문제를 수정할 수 있습니다.  
  
#### <a name="to-preview-a-report"></a>보고서를 미리 보려면  
  
-   **미리 보기** 탭을 클릭 합니다. 보고서 디자이너 보고서를 실행 하 고 미리 보기 보기에 표시 합니다.  
  
     다음 다이어그램은 미리 보기 뷰에 표시된 보고서의 일부를 보여 줍니다.  
  
     ![미리 보기, 5개의 열이 있는 테이블의 정보 행](../../2014/tutorials/media/rs-basictabledetailspreview.gif "미리 보기, 5개의 열이 있는 테이블의 정보 행")  
  
     통화(Line Total 열)의 소수점 뒤에 6자리가 있고 날짜에는 타임스탬프가 있습니다. 다음 단원에서는 이러한 서식을 수정합니다.  
  
> [!NOTE]  
>  **파일** 메뉴에서 **모두 저장** 을 클릭하여 보고서를 저장합니다.  
  
## <a name="next-steps"></a>다음 단계  
 보고서에 테이블 데이터 영역을 추가하고, 데이터 영역에 필드를 추가하고, 보고서를 미리 보는 방법을 배웠습니다. 다음 단원에서는 열 머리글과 날짜 및 통화 값에 서식을 지정합니다. [5단원: 보고서 서식 지정&#40;Reporting Services&#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 &#40;보고서 작성기 및 SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)   
 [데이터 세트 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
