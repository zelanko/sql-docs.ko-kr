---
title: 텍스트 및 자리 표시자 서식 지정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql11.rtp.rptdesigner.placeholderproperties.font.f1
- "10118"
- "10135"
- sql11.rtp.rptdesigner.textboxproperties.font.f1
- "10132"
- sql11.rtp.rptdesigner.textproperties.font.f1
ms.assetid: 26a4baf2-7bc5-4634-b136-552687ffa477
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 70eb61bf1b479bb8021c09058628f25b1594b977
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287391"
---
# <a name="formatting-text-and-placeholders-report-builder-and-ssrs"></a>텍스트 및 자리 표시자 서식 지정(보고서 작성기 및 SSRS)
  입력란은 데이터 영역 안에 있는 보고서 항목 또는 개별 셀로서 텍스트, 계산 필드, 데이터베이스의 필드에 대한 포인터 또는 이 세 항목의 조합을 포함하고 있습니다. 글꼴 및 색을 혼합하고, 굵게 및 기울임꼴 스타일을 추가하고, 맞춤 및 내어쓰기와 같은 단락 스타일을 사용할 수 있습니다. 또한 입력란 전체의 형식을 지정하거나 입력란 내에 있는 특정 텍스트, 숫자, 식 또는 필드의 형식을 지정할 수 있습니다.  
  
 글꼴, 크기, 색 및 효과는 모두 보고서의 가독성에 영향을 줍니다. 입력란 또는 데이터 영역에 있는 텍스트에 글꼴, 글꼴 스타일, 글꼴 크기 및 밑줄 효과를 적용할 수 있습니다. 기본적으로 Arial, 10포인트 및 검정의 보고서 글꼴이 사용됩니다. **입력란** 및 **입력란 속성** 대화 상자를 사용하여 보고서가 렌더링될 때 텍스트가 표시되는 방법을 지정할 수 있습니다.  
  
 ![rs_MixedFormatText](../media/rs-mixedformattext.gif "rs_MixedFormatText")  
  
 이 그림에서 입력란 자체에 테두리가 있으며 모든 텍스트는 동일한 입력란에 있지만 텍스트의 서식이 다양합니다.  
  
 빠르게 시작하려면 [자습서: 텍스트 서식 지정&#40;보고서 작성기&#41;](../tutorial-format-text-report-builder.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-placeholder-text-in-a-text-box"></a>입력란에 자리 표시자 텍스트 만들기  
 입력란 안에 단순 또는 복합 식이 정의되어 있는 경우 이 식의 최종 UI 표현을 *자리 표시자*라고 합니다. 수에 관계없이 단일 입력란 내의 자리 표시자 또는 텍스트 구역에 색, 글꼴, 동작 및 기타 작동을 정의할 수 있습니다.  
  
 자리 표시자의 값은 항상 단순 또는 복합 식입니다. 다음 방법 중 하나로 식을 만들어서 입력란에 자리 표시자를 추가할 수 있습니다.  
  
-   **보고서 데이터** 창에서 필드를 끌어다 입력란 안에 놓습니다. 보고서 본문이 아닌 다른 곳으로 식을 끌면 자리 표시자를 포함하는 새 입력란이 생성됩니다. 끌어다 놓은 필드에 해당하는 필드 식이 이 자리 표시자의 값이 됩니다.  
  
-   입력란의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 **자리 표시자 삽입**을 선택합니다. **자리 표시자 속성** 대화 상자에서 식을 자리 표시자의 값으로 지정할 수 있습니다. 자세한 내용은 [자리 표시자 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](../placeholder-properties-dialog-box-general-report-builder-and-ssrs.md)을 참조하세요.  
  
-   입력란에 단순 또는 복합 식을 입력합니다. 예를 들어 입력란에 **Name: [Name]** 을 입력하면 **[Name]** 텍스트가 `=Fields!Name.Value`식을 나타내는 자리 표시자로 표시됩니다.  
  
-   등호(=)로 시작하는 식을 빈 입력란에 입력합니다. 포커스를 입력란 바깥으로 이동하면 최종 식이 편집 가능한 자리 표시자로 변환됩니다. 입력란이 비어 있지 않거나 입력란에서 등호가 첫 문자가 아닌 곳에 삽입되어 있는 경우에는 등호가 문자열 리터럴로 취급되어 자리 표시자가 생성되지 않습니다. 단순 및 복합 식을 정의하는 방법에 대한 자세한 내용은 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="formatting-placeholders-and-static-text-in-a-text-box"></a>입력란에서 자리 표시자 및 정적 텍스트 서식 지정  
 **자리 표시자 속성** 대화 상자를 사용하여 자리 표시자의 서식을 지정할 수 있습니다. 전체 자리 표시자의 서식만 지정할 수 있고, 자리 표시자의 구역을 서식 지정할 수는 없습니다. 기본 식을 보려면 자리 표시자 위에 포인터를 잠시 올려 놓으면 됩니다. 자리 표시자를 두 번 클릭하거나, 자리 표시자를 마우스 오른쪽 단추로 클릭하고 **자리 표시자 속성**을 선택하여 기본 식을 변경할 수 있습니다. **자리 표시자 속성** 대화 상자의 **일반** 에서 **레이블** 속성을 사용하여 UI 레이블을 지정할 수도 있습니다. 자리 표시자의 디자인 타임에 표시된 텍스트가 이 UI 레이블이 됩니다.  
  
 ![rs_MixedTextnPlaceholder](../media/rs-mixedtextnplaceholder.gif "rs_MixedTextnPlaceholder")  
  
 이 그림에서 목록의 입력란에는 굵은 서식이 있는 레이블과 서식 없는 자리 표시자가 둘 다 포함되어 있습니다.  
  
 자리 표시자 텍스트와 달리 입력란에서 개별 텍스트를 맞추고, 한 입력란에 여러 단락을 사용하고, 텍스트 하위 집합에 다른 동작을 정의할 수 있습니다.  
  
 단일 입력란 내의 텍스트 하위 집합에 색, 글꼴, 동작 및 기타 작동을 정의하여 보고서에 있는 텍스트의 편지 병합 또는 템플릿을 만들 수 있습니다. 한 입력란에 여러 단락을 사용할 수도 있습니다. 예를 들어 두 개의 텍스트 단락이 있는 경우 입력란에서 Enter 키를 눌러 단락을 분리할 수 있습니다. 개별 텍스트 문자열에 대한 맞춤 값을 설정할 수도 있습니다. 입력란에서 개별 텍스트의 동작을 정의할 수도 있습니다. 이렇게 하면 입력란에 포함된 텍스트 문자열에 대한 하이퍼링크를 추가하려는 경우에 유용할 수 있습니다.  
  
> [!NOTE]  
>  입력란에 정의된 동작은 입력란의 개별 텍스트에 대해 정의된 동작보다 우선 순위가 높습니다.  
  
 혼합 서식에 대한 자세한 내용은 [입력란의 텍스트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](format-text-in-a-text-box-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="aligning-horizontal-text-using-general"></a>일반을 사용하여 가로 텍스트 맞춤  
 **입력란 속성** 대화 상자의 **맞춤** 에서 텍스트를 가로로 어떻게 맞출 것인지를 지정할 수 있습니다. 맞춤 값을 지정하지 않는 경우 맞춤의 기본값은 **기본값**입니다. 즉, 자리 표시자 값의 필드 유형에 따라 텍스트를 맞춥니다. 문자열이 아닌 값(즉, 숫자가 아닌 값)으로 계산되는 식을 지정하면 텍스트를 오른쪽에 맞춥니다. 식이 문자열 값(예: 숫자)으로 평가되면 텍스트를 왼쪽에 맞춥니다.  
  
## <a name="see-also"></a>관련 항목  
 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [계기의 눈금 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [자리 표시자 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](../placeholder-properties-dialog-box-general-report-builder-and-ssrs.md)   
 [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)   
 [입력란&#40;보고서 작성기 및 SSRS&#41;](text-boxes-report-builder-and-ssrs.md)  
  
  
