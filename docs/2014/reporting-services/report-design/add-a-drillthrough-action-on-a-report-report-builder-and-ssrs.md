---
title: 보고서에 드릴스루 동작 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 153729c4-d01e-4629-b78f-0cfd5a7f83da
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a345b0ed36fde93a3bc94ff4075233c6c24728af
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106864"
---
# <a name="add-a-drillthrough-action-on-a-report-report-builder-and-ssrs"></a>보고서에 드릴스루 동작 추가(보고서 작성기 및 SSRS)
  주 보고서에서 링크를 클릭할 때 열리는 보고서를 *드릴스루 보고서*라고 합니다. 이 드릴스루 링크를 통해 드릴스루 작업을 수행할 수 있습니다.  
  
 드릴스루 보고서는 주 보고서와 같은 보고서 서버에 게시되어야 하지만 폴더는 달라도 됩니다. 입력란, 이미지 또는 차트의 데이터 요소와 같이 **동작** 속성이 있는 모든 항목에 드릴스루 링크를 추가할 수 있습니다.  
  
 드릴스루 링크를 보고서에 추가하려면 먼저 주 보고서가 연결될 드릴스루 보고서를 만들어야 합니다. 드릴스루 보고서는 일반적으로 원래 요약 보고서에 들어 있는 항목에 대한 세부 정보를 포함하며 대개 주 보고서에서 전달된 매개 변수에 기초하여 드릴스루 보고서를 필터링하는 매개 변수를 포함합니다. 드릴스루 보고서를 만드는 방법에 대한 자세한 내용은 [드릴스루 보고서&#40;보고서 작성기 및 SSRS&#41;](drillthrough-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-drillthrough-action"></a>드릴스루 동작을 추가하려면  
  
1.  디자인 뷰에서 링크를 추가하려는 입력란, 이미지 또는 차트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  항목의 **속성** 대화 상자에서 **동작**을 클릭합니다.  
  
3.  **보고서로 이동**을 선택합니다. 이 옵션에 대한 추가 섹션이 대화 상자에 나타납니다.  
  
4.  **보고서 지정**에서 **찾아보기** 를 클릭하여 이동할 보고서를 찾거나 보고서의 이름을 입력합니다. 또는 식 단추(**fx**)를 클릭하여 보고서 이름에 대한 식을 만듭니다.  
  
     드릴스루 보고서에 대한 경로 형식은 기본 모드와 SharePoint 통합 모드에서 서로 다릅니다. 보고서를 찾을 때는 올바른 형식의 경로가 제공됩니다. 자세한 내용은 [외부 항목에 대한 경로 지정&#40;보고서 작성기 및 SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)을 참조하세요.  
  
     드릴스루 보고서에 대한 매개 변수를 지정해야 하는 경우 다음 단계를 따릅니다.  
  
5.  **이러한 매개 변수를 사용하여 보고서 실행**에서 **추가**를 클릭합니다. 매개 변수 표에 새 행이 추가됩니다.  
  
    -   **이름** 입력란에서 드롭다운 목록을 클릭하거나 드릴스루 보고서에 있는 보고서 매개 변수의 이름을 입력합니다.  
  
        > [!NOTE]  
        >  매개 변수 목록에 있는 이름이 대상 보고서의 예상 매개 변수와 정확히 일치해야 합니다. 예를 들어 매개 변수 이름은 대/소문자가 일치해야 합니다. 이름이 일치하지 않거나 예상 매개 변수가 목록에 없는 경우 드릴스루 보고서가 실패합니다.  
  
    -   **값**에서 드릴스루 보고서의 매개 변수에 전달할 값을 입력하거나 선택합니다.  
  
        > [!NOTE]  
        >  보고서 매개 변수에 전달할 값을 반환하는 식을 값에 포함시킬 수 있습니다. 값 목록의 식에는 현재 보고서에 대한 필드 목록이 포함됩니다.  
  
     보고서의 매개 변수를 숨기는 방법에 대한 자세한 내용은 [보고서 매개 변수 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)를 참조하세요.  
  
6.  (옵션) 입력란의 경우 리본의 **홈** 탭에서 텍스트 색과 효과를 변경하여 텍스트가 링크임을 사용자에게 나타내는 것이 좋습니다.  
  
7.  링크를 테스트하려면 보고서를 실행하고 이 링크를 설정한 보고서 항목을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [동작 속성 대화 상자&#40;보고서 작성기 및 SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md)   
 [차트의 데이터 요소에 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [계열에 도구 설명 표시&#40;보고서 작성기 및 SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
  
