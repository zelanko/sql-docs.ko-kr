---
title: "보고서 및 그룹 변수 컬렉션 참조(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10404"
- "10083"
- sql13.rtp.rptdesigner.groupproperties.variables.f1
- sql13.rtp.rptdesigner.categorygroupproperties.variables.f1
- sql13.rtp.rptdesigner.reportproperties.variables.f1
- "10292"
- sql13.rtp.rptdesigner.seriesgroupproperties.variables.f1
- "10412"
ms.assetid: 4be5b463-3ce2-483d-a3c6-dae752cb543e
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b04a9bc443ac284afad9153f5f3196a8c9a4fc1a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="built-in-collections---report-and-group-variables-references-report-builder"></a>기본 제공 컬렉션 - 보고서 및 그룹 변수 참조(보고서 작성기)
  보고서의 식에서 두 번 이상 사용되는 복잡한 계산이 있는 경우 변수를 만들어 사용할 수 있습니다. 보고서 변수 또는 그룹 변수를 만들 수 있습니다. 변수 이름은 보고서에서 고유해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-variables"></a>보고서 변수  
 보고서 변수를 사용하여 환율이나 타임스탬프와 같이 시간에 종속되는 계산 또는 여러 번 참조되는 복잡한 계산에 대한 값을 저장할 수 있습니다. 기본적으로 보고서 변수는 한 번 계산한 후 보고서 전체의 식에 사용할 수 있습니다. 보고서 변수는 기본적으로 읽기 전용입니다. 기본값을 변경하여 보고서 변수를 읽기/쓰기 가능하도록 설정할 수 있습니다. 보고서 변수의 값은 보고서를 다시 처리할 때까지 세션 전체에서 보존됩니다.  
  
 보고서 변수를 추가하려면 **보고서 속성** 대화 상자를 열고 **변수**를 클릭한 후 이름과 값을 입력합니다. 이름은 문자로 시작하고 공백을 포함하지 않는 대/소문자를 구분하는 문자열입니다. 이름에는 문자, 숫자 또는 밑줄(_)을 포함할 수 있습니다.  
  
 식에서 변수를 참조하려면 전역 컬렉션 구문을 사용합니다(예: `=Variables!CustomTimeStamp.Value`). 디자인 화면에서 값은 입력란에 `<<Expr>>`로 표시됩니다.  
  
 다음 방법으로 보고서 변수를 사용할 수 있습니다.  
  
-   **읽기 전용으로 사용** 값을 한 번 설정하여 보고서 세션에 대해 상수를 만듭니다(예: 타임스탬프 만들기).  
  
     입력란의 식은 보고서를 읽는 사용자의 요청에 따라 계산되므로 동적 값(예: 현재 시간을 반환하는 함수인 `Now()` 를 포함하는 식)은 사용자가 **뒤로** 단추를 사용하여 앞뒤 페이지로 이동하는 경우 다른 값을 반환할 수 있습니다. 보고서 변수의 값을 `=Now()`식으로 설정하고 변수를 식에 추가하면 보고서를 처리하는 동안 내내 동일한 값이 사용되도록 할 수 있습니다.  
  
-   **읽기/쓰기로 사용** 값을 한 번 설정하고 보고서 세션 내에서 값을 직렬화합니다. 변수에 대해 읽기/쓰기 옵션을 사용하는 것이 보고서 정의의 코드 블록에서 정적 변수를 사용하는 것보다 효율적입니다.  
  
     변수의 **읽기 전용** 옵션 선택을 취소하면 변수의 Writable 속성이 **true**로 설정됩니다. 식에서 값을 업데이트하려면 SetValue 메서드(예: `=Variables!MyVariable.SetValue("123")`)를 사용합니다.  
  
    > [!NOTE]  
    >  보고서 프로세서가 변수를 초기화하는 시기 또는 변수를 업데이트하는 식을 계산하는 시기는 제어할 수 없습니다. 변수 초기화 실행 순서는 정의되어 있지 않습니다.  
  
 세션에 대한 자세한 내용은 [Previewing Reports in Report Builder](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)를 참조하십시오.  
  
## <a name="group-variables"></a>그룹 변수  
 그룹 변수를 사용하여 복잡한 식을 그룹 범위에서 한 번에 계산할 수 있습니다. 그룹 변수는 그룹 및 해당 자식 그룹의 범위 내에서만 유효합니다.  
  
 예를 들어 서로 다른 세금 범주에 속한 항목에 대한 재고 데이터를 표시하는 데이터 영역이 있고 각 범주에 대해 서로 다른 세율을 적용하려는 경우를 가정해 보겠습니다. Category에서 데이터를 그룹화하고 부모 그룹에서 *Tax* 변수를 정의합니다. 그런 다음 *ItemTax* 에 대한 그룹 변수를 각 세금 범주에 정의하고 서로 다른 각 Category 하위 그룹을 적절한 그룹 변수에 할당합니다. 예를 들어  
  
-   `[Category]`기반의 부모 그룹에 대해 *Tax* 변수를 `[Tax]`값으로 정의합니다. 범주 값은 Food와 Clothing이라고 가정하겠습니다.  
  
-   `[Subcategory]`기반의 자식 그룹에 대해 *ItemsTax* 변수를 `=Variables!Tax.Value * Sum(Fields!Price.Value)`으로 정의합니다. Food 범주의 하위 범주 값은 Beverages 및 Bread라고 가정하겠습니다. Clothing의 하위 범주 값은 Shirts 및 Hats라고 가정하겠습니다.  
  
-   자식 그룹의 행에 있는 입력란에 대해 `=Variables!ItemsTax.Value`식을 추가합니다.  
  
     입력란에는 Beverages 및 Bread에 대해 Food 세금을 사용하고 Shirts 및 Hats에 대해 Clothing 세금을 사용한 총 세금이 표시됩니다.  
  
 그룹 변수를 추가하려면 **테이블릭스 그룹 속성** 대화 상자를 열고 **변수**를 클릭하고 이름과 값을 입력합니다. 그룹 변수는 고유 그룹 값별로 한 번 계산됩니다.  
  
 식에서 변수를 참조하려면 전역 컬렉션 구문을 사용합니다(예: `=Variables!GroupDescription.Value`). 디자인 화면에서 값은 입력란에 `<<Expr>>`로 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
