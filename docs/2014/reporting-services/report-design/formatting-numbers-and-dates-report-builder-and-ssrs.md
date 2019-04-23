---
title: 숫자 및 날짜 서식 지정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.placeholderproperties.number.f1
- sql12.rtp.rptdesigner.serieslabelproperties.number.f1
- "10127"
- sql12.rtp.rptdesigner.axisproperties.number.f1
- "10130"
- "10286"
- sql12.rtp.rptdesigner.textboxproperties.number.f1
- "10285"
ms.assetid: 6de1a725-9f06-4708-be26-2d55e442e344
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ff184ad75c495d9f18f5e9d9e1d3aa1bdfa7132e
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59950039"
---
# <a name="formatting-numbers-and-dates-report-builder-and-ssrs"></a>숫자 및 날짜 서식 지정(보고서 작성기 및 SSRS)
  해당 데이터 영역 **속성** 대화 상자의 **숫자** 페이지에서 형식을 선택하여 데이터 영역에 있는 숫자와 날짜의 형식을 지정할 수 있습니다.  
  
 입력란 보고서 항목 안에 있는 문자열의 형식을 지정하려면 형식을 지정할 항목을 선택하고 마우스 오른쪽 단추를 클릭한 후 **입력란 속성**을 선택하고 **숫자**를 클릭합니다. 테이블 또는 행렬의 셀은 개별 입력란이기 때문에 테이블이나 행렬 데이터 영역의 개별 셀에 형식을 지정할 때도 이 방법을 사용할 수 있습니다.  
  
 차트 데이터 영역은 범주(x) 축을 따라 날짜를 표시하고 값(y) 축을 따라 값을 표시합니다. 차트에서 형식을 지정하려면 축을 마우스 오른쪽 단추로 클릭하고 **축 속성**을 선택합니다. 값 축에서는 숫자에 대한 형식만 지정할 수 있습니다. 자세한 내용은 [차트의 축 레이블 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)을 참조하세요.  
  
 계기 데이터 영역에서 형식을 지정하려면 계기의 눈금을 마우스 오른쪽 단추로 클릭하고 **방사형 눈금 속성** 또는 **선형 눈금 속성**을 선택합니다.  
  
> [!NOTE]  
>  사용하려는 일부 서식 옵션이 회색으로 표시되어 있으면 해당 서식 옵션이 데이터 원본에 설정된 필드의 데이터 형식과 호환되지 않음을 의미합니다. 예를 들어 필드에 숫자 값이 포함되어 있지만 필드의 데이터 형식이 문자열인 경우 통화 또는 10진수와 같은 숫자 데이터 서식 옵션을 적용할 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="considerations-for-formatting-numbers-and-dates"></a>숫자 및 날짜 형식 지정 시 고려 사항  
 보고서에서 숫자와 날짜의 형식을 지정하기 전에 다음을 고려합니다.  
  
-   기본적으로 클라이언트 컴퓨터의 culture 설정에 따라 숫자 형식이 지정됩니다. 형식 문자열을 사용하여 숫자 표시 방법을 지정하면 보고서를 보는 사람의 위치에 관계 없이 일관된 형식으로 숫자를 표시할 수 있습니다.  
  
-   **숫자** 페이지에서 제공되는 형식은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 표준 숫자 형식 문자열의 일부입니다. 대화 상자에 표시되지 않는 사용자 지정 형식을 사용하여 숫자나 날짜에 형식을 지정하려는 경우에는 숫자 또는 날짜에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 형식 문자열을 사용할 수 있습니다. 사용자 지정 형식 문자열에 대한 자세한 내용은 MSDN에서 [형식 지정](https://go.microsoft.com/fwlink/?LinkId=112024) 항목을 참조하십시오.  
  
-   사용자 지정 형식 문자열을 지정하면 culture별 기본 설정보다 높은 우선 순위를 가집니다. 예를 들어 숫자 1234를 1,234로 표시하기 위한 사용자 지정 형식 문자열인 "#,###"를 설정했다고 가정하겠습니다. 미국의 사용자와 유럽의 사용자는 이 형식 문자열을 다르게 해석할 수 있습니다. 사용자 지정 형식을 지정하기 전에, 선택한 형식이 해당 보고서를 보게 될 다른 culture의 사용자에게 어떤 영향을 줄지에 대해 고려하십시오.  
  
-   잘못된 형식 문자열을 지정하면 형식 지정된 텍스트는 형식 지정을 무시하는 리터럴 문자열로 해석됩니다.  
  
-   같은 입력란에 함께 포함된 숫자와 문자의 형식을 지정할 때는 숫자를 나머지 텍스트와 구분하기 위해 자리 표시자를 사용하는 것을 고려하십시오. 자세한 내용은 [텍스트 및 자리 표시자 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)를 클릭합니다. 입력란의 Format 속성에 잘못된 형식 문자열을 지정하면 형식 문자열이 무시됩니다. 차트나 계기의 Format 속성에 잘못된 형식 문자열을 지정하면 지정한 형식 문자열은 문자열로 해석되고 형식이 적용되지 않습니다.  
  
-   **범주** 에서 **통화** 를 선택하고 **값 표시 단위**를 선택한 경우 재무 형식을 사용하여 숫자를 표시하는 단위로 **천**, **백만**또는 **10억** 을 선택할 수 있습니다. 예를 들어 필드 값이 1,789,905,394인 경우 값 표시 단위로 **10억** 을 선택하고 소수 자릿수를 두 자리로 지정하면 보고서에는 1.78이 값으로 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [텍스트 및 자리 표시자 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [선, 색 및 이미지 서식 지정&#40;보고서 작성기 및 SSRS&#41;](images-report-builder-and-ssrs.md)   
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [축 레이블의 서식을 날짜 또는 통화로 지정&#40;보고서 작성기 및 SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [계기의 눈금 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)  
  
  
