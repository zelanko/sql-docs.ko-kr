---
title: 하위 보고서 및 매개 변수 추가(보고서 작성기) | Microsoft Docs
description: 하위 보고서를 추가하는 방법을 알아봅니다. 보고서 작성기에서 여러 관련 보고서의 컨테이너로 주 보고서를 만들려는 경우 하위 보고서를 사용합니다.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10093"
- sql13.rtp.rptdesigner.subreportproperties.general.f1
ms.assetid: 94f960f8-a629-4f1e-8277-c3b8f0680d98
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9131d15b8374df4b3db22946583d3349f0386e91
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462307"
---
# <a name="add-a-subreport-and-parameters-report-builder-and-ssrs"></a>하위 보고서 및 매개 변수 추가(보고서 작성기 및 SSRS)
  여러 관련 보고서의 컨테이너인 주 보고서를 만들려는 경우 하위 보고서를 보고서에 추가합니다. 하위 보고서는 다른 보고서에 대한 참조입니다. 여러 보고서에서 동일한 고객에 대한 데이터를 표시하도록 하는 등의 이유로 데이터 값을 통해 여러 보고서를 연결하려면 매개 변수가 있는 보고서(예: 특정 고객에 대한 세부 정보를 표시하는 보고서)를 하위 보고서로 디자인해야 합니다. 하위 보고서를 주 보고서에 추가할 때에는 매개 변수를 지정하여 하위 보고서에 전달할 수 있습니다.  
  
 하위 보고서를 테이블이나 행렬의 동적 행 또는 열에 추가할 수도 있습니다. 주 보고서가 처리되면 하위 보고서가 각 행에 대해 처리됩니다. 이 경우 데이터 영역 또는 중첩된 데이터 영역을 사용하여 원하는 결과를 얻을 수 있는지 생각해 보십시오.  
  
 보고서에 하위 보고서를 추가하려면 먼저 포함될 보고서 역할을 할 보고서를 만들어야 합니다. 하위 보고서를 만드는 방법은 [하위 보고서&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-subreport"></a>하위 보고서를 추가하려면  
  
1.  **삽입** 탭에서 **하위 보고서**를 클릭합니다.  
  
2.  디자인 화면에서 보고서의 한 위치를 클릭한 다음 상자를 끌어 원하는 하위 보고서 크기로 만듭니다. 또는 디자인 화면을 클릭하여 기본 크기의 하위 보고서를 만듭니다.  
  
3.  하위 보고서를 마우스 오른쪽 단추로 클릭한 다음 **하위 보고서 속성**을 클릭합니다.  
  
4.  **하위 보고서 속성** 대화 상자의 **이름** 입력란에 이름을 입력하거나 기본값을 적용합니다. 이름은 보고서 내에서 고유해야 합니다. 기본적으로 Subreport1 또는 Subreport2 등과 같은 일반 이름이 지정됩니다.  
  
5.  **이 보고서를 하위 보고서로 사용** 상자에서 **찾아보기**를 클릭하거나 보고서의 이름을 입력합니다. 하위 보고서의 경로는 자동으로 지정되므로 **찾아보기** 를 클릭하는 것이 좋습니다. 여러 가지 방법으로 보고서를 지정할 수 있습니다. 자세한 내용은 [외부 항목에 대한 경로 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)을 참조하세요.  
  
6.  (옵션) 하위 보고서가 여러 페이지에 걸쳐 있는 경우 테두리가 렌더링되지 않도록 **페이지 나누기에 테두리 생략** 에서 **예** 를 클릭합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-specify-parameters-to-pass-to-a-subreport"></a>하위 보고서에 전달할 매개 변수를 지정하려면  
  
1.  디자인 뷰에서 하위 보고서를 마우스 오른쪽 단추로 클릭한 다음 **하위 보고서 속성**을 클릭합니다.  
  
2.  **하위 보고서 속성** 대화 상자에서 **매개 변수**를 클릭합니다.  
  
3.  **추가**를 클릭합니다. 매개 변수 표에 새 행이 추가됩니다.  
  
4.  **이름** 입력란에 하위 보고서의 매개 변수 이름을 입력하거나 목록 상자에서 선택합니다. 이 이름은 쿼리 매개 변수가 아닌 하위 보고서에 있는 보고서 매개 변수의 이름과 일치해야 합니다.  
  
5.  **값** 목록 상자에서 하위 보고서에 전달할 값을 입력하거나 선택합니다. 이 값은 정적 텍스트이거나 주 보고서의 필드 또는 기타 개체를 참조하는 식일 수 있습니다.  
  
    > [!NOTE]  
    >   보고서 작성기에서는 매개 변수가 **매개 변수** 목록에 없고 하위 보고서에 기본값이 정의되어 있으면 하위 보고서가 올바르게 처리됩니다.  
    >   
    >  보고서 디자이너에서는 하위 보고서에 필요한 모든 매개 변수를 **매개 변수** 목록에 포함해야 합니다. 필요한 매개 변수가 없으면 하위 보고서가 주 보고서에 올바르게 표시되지 않습니다.  
  
6.  각 하위 보고서 매개 변수의 이름과 값을 지정하려면 3-5단계를 반복합니다.  
  
7.  하위 보고서 매개 변수를 삭제하려면 매개 변수 표에서 매개 변수를 클릭한 다음 **삭제**를 클릭합니다.  
  
8.  하위 보고서 매개 변수의 순서를 변경하려면 매개 변수를 클릭한 다음 위로 단추 또는 아래로 단추를 클릭합니다.  
  
     하위 보고서 매개 변수의 순서 변경은 하위 보고서의 처리에 아무런 영향도 주지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [하위 보고서&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)   
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)  
  
  
