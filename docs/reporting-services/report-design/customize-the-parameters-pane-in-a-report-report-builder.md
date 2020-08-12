---
title: 보고서에서 매개 변수 창 사용자 지정(보고서 작성기) | Microsoft Docs
description: 보고서 작성기에서 매개 변수를 사용하여 페이지를 매긴 보고서를 작성할 때 매개 변수 창을 사용자 지정하는 방법을 알아봅니다.
ms.date: 06/15/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4ce9e8d5-911a-4422-928f-a8d005b79fc6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 29bd397d64280644394077a29a3420dbf43b5e6f
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796564"
---
# <a name="customize-the-parameters-pane-in-a-report-report-builder"></a>Customize the Parameters Pane in a Report (Report Builder)
  보고서 작성기에서 매개 변수를 사용하여 페이지가 매겨진 보고서의 작성하는 경우 매개 변수 창을 사용자 지정할 수 있습니다. 보고서 디자인 보기에서 매개 변수 창의 특정 열과 행에 매개 변수를 끌어 놓을 수 있습니다. 열을 추가하거나 제거하여 창 레이아웃을 변경할 수 있습니다.

 매개 변수를 창의 새 열과 행으로 끌어 놓으면 **보고서 데이터** 창에서 매개 변수 순서가 변경됩니다. **보고서 데이터** 창에서 매개 변수 순서를 변경하면 창의 매개 변수 위치가 변경됩니다. 매개 변수 순서가 중요한 이유에 대한 자세한 내용은[보고서 매개 변수의 순서 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)을 참조하세요.

## <a name="to-customize-the-parameters-pane"></a>매개 변수 창 사용자 지정

1.  **보기** 탭에서 **매개 변수** 확인란을 선택하여 매개 변수 창을 표시합니다.

     ![보기 탭에서 매개 변수 창에 액세스](../../reporting-services/report-design/media/ssrs-customparameter-accessparameterpanedesignmode.png "보기 탭에서 매개 변수 창에 액세스")

     디자인 화면의 위쪽에 창이 표시됩니다.

2.  창에 매개 변수를 추가하려면 다음 중 하나를 수행합니다.

    -   매개 변수 창의 빈 셀을 마우스 오른쪽 단추로 클릭한 후 **매개 변수 추가**를 클릭합니다.

         ![매개 변수 창에서 새 매개 변수 추가](../../reporting-services/report-design/media/ssrs-customizeparameter-addnewparameter.png "매개 변수 창에서 새 매개 변수 추가")

    -   **보고서 데이터** 창의 **매개 변수** 를 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 추가**를 클릭합니다.

3.  매개 변수를 매개 변수 창의 새로운 위치로 이동하려면 창의 다른 셀로 매개 변수를 끓어 넣습니다.

     창에서 매개 변수의 위치를 변경하면 **보고서 데이터** 창의 **매개 변수** 목록에 있는 매개 변수 순서가 자동으로 변경됩니다. 매개 변수 순서의 영향에 대한 자세한 내용은[보고서 매개 변수의 순서 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)을 참조하세요.

4.  매개 변수의 속성에 액세스하려면, 다음 중 하나를 수행합니다.

    -   매개 변수 창에서 매개 변수를 마우스 오른쪽 단추로 클릭한 후 **매개 변수 속성**을 클릭합니다.

         ![매개 변수 창에서 매개 변수 속성에 액세스](../../reporting-services/report-design/media/ssrs-customizeparameter-accessparameterproperties-composite.png "매개 변수 창에서 매개 변수 속성에 액세스")

    -   **보고서 데이터** 창에서 매개 변수를 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 속성**을 클릭합니다.

5.  창에 열과 행을 새로 추가하거나 기존 열과 행을 삭제하려면, 매개 변수 창의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 표시되는 메뉴에서 명령을 클릭합니다.

     ![매개 변수 창에 열 및 행 추가](../../reporting-services/report-design/media/ssrs-customparameter-addcolumnsrows.png "매개 변수 창에 열 및 행 추가")

    > [!IMPORTANT]
    >  매개 변수를 포함하는 행이나 열을 삭제하면 해당 매개 변수가 보고서에서 삭제됩니다.

6.  창과 보고서에서 매개 변수를 삭제하려면 다음 중 하나를 수행합니다.

    -   매개 변수 창에서 매개 변수를 마우스 오른쪽 단추로 클릭한 후  **삭제**를 클릭합니다.

         ![매개 변수 창에서 매개 변수 삭제](../../reporting-services/report-design/media/ssrs-customparameter-deleteparameter.png "매개 변수 창에서 매개 변수 삭제")

    -   **보고서 데이터** 창에서 매개 변수를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.

## <a name="hiddeninternal-parameters-during-runtime"></a>런타임 중 숨겨진/내부 매개 변수
숨겨진/내부 매개 변수가 있는 경우 런타임 중에 빈 공간으로 렌더링되는지 여부에 대한 논리는 다음과 같습니다.

   - 행 또는 열에 숨겨진/내부 매개 변수 또는 빈 셀만 있는 경우 런타임 중에 전체 행 또는 열이 렌더링되지 않습니다.
   - 그렇지 않으면 숨겨진/내부 매개 변수 또는 빈 셀이 빈 공백으로 렌더링됩니다.

예를 들어, `ReportParameter1`은 숨겨지고 나머지 매개 변수는 표시됩니다.

![숨겨진 매개 변수 예제 1](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-1.png "레이아웃 그리드에서 한 개의 매개 변수가 숨겨짐")

첫 번째 열 또는 첫 번째 행에 표시되는 매개 변수가 있기 때문에 런타임 중에 빈 공간이 생성됩니다.

![숨겨진 매개 변수 예제 1 - 런타임](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-1.png "레이아웃 그리드에 숨겨진 매개 변수가 있으면 런타임에 빈 공간이 생성됨")

동일한 예제를 사용하여 `ReportParameter3`도 숨김으로 설정하는 경우는 다음과 같습니다.

![숨겨진 매개 변수 예제 2](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-2.png "동일한 열에서 두 개의 매개 변수가 숨겨짐")

그러면 전체 열이 비어 있는 것으로 간주되기 때문에 첫 번째 열이 런타임 중에 렌더링되지 않습니다.

![숨겨진 매개 변수 예제 2 - 런타임](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-2.png "런타임에 동일한 열에서 두 개의 매개 변수가 숨겨짐")

## <a name="default-layout"></a>기본 레이아웃
SQL Server Reporting Services 2016보다 이전에 작성된 보고서의 경우 런타임 중에 2개 열과 N개 행의 기본 매개 변수 레이아웃 그리드가 사용됩니다. 기본 레이아웃을 변경하려면 Microsoft 보고서 작성기에서 보고서를 열고 보고서를 저장합니다. 보고서를 저장하면 사용자 지정된 매개 변수 레이아웃 정보가 .rdl 파일에 저장됩니다.


## <a name="see-also"></a>참고 항목
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)


