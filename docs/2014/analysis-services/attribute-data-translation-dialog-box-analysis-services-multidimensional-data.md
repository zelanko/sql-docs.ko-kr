---
title: 특성 데이터 번역 대화 상자 (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dimensiondesigner.dimensionstoragesettings.f1
helpviewer_keywords:
- Attribute Data Translation dialog box
ms.assetid: bed286de-1e9b-49de-b09e-3cd076aba152
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1b8d7f28696e04045ca5ac3f11bf38d4c67f60c2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172779"
---
# <a name="attribute-data-translation-dialog-box-analysis-services---multidimensional-data"></a>특성 데이터 번역 대화 상자(Analysis Services - 다차원 데이터)
  **특성 데이터 번역** 대화 상자를 사용하여 번역 캡션 데이터가 포함된 열을 설정하고 번역된 데이터에 사용할 데이터 정렬 및 정렬 순서를 설정할 수 있습니다. 다음을 수행하여 **특성 데이터 번역** 대화 상자를 표시할 수 있습니다.  
  
-   **차원 디자이너** 의 **번역** 탭에 있는 **도구 모음** 창에서 **새 캡션 열** 또는 **캡션 열 편집**을 클릭합니다.  
  
-   **차원 디자이너** 의 **번역** 탭에서 **번역 세부 정보** 창을 마우스 오른쪽 단추로 클릭한 다음 **새 캡션 열** 또는 **캡션 열 편집**을 선택합니다.  
  
## <a name="options"></a>변수  
 **Attribute**  
 선택한 특성을 표시합니다.  
  
 **언어**  
 선택한 언어를 표시합니다.  
  
 **번역 된 캡션**  
 선택한 특성에 대해 현재 번역된 캡션을 설정합니다.  
  
 **번역 열**  
 번역 열 데이터가 저장되는 열을 설정합니다. 열은 하나만 선택할 수 있습니다. 주 차원 테이블에서 참조하는 모든 관련 테이블이 표시됩니다.  
  
 **데이터 정렬 지정자**  
 선택한 특성에 대해 데이터 정렬 지정자를 설정합니다. 기본적으로 현재 Windows 데이터 정렬이 선택됩니다. 아래쪽 화살표를 클릭하여 사용 가능한 데이터 정렬에서 선택합니다.  
  
 **이진**  
 각 문자에 대해 정의된 비트 패턴을 기준으로 데이터를 정렬 및 비교하려면 이 옵션을 선택합니다. 이진 정렬 순서는 대/소문자(소문자가 대문자 앞에 와야 함) 및 악센트를 구분합니다. 이것은 가장 빠른 정렬 순서입니다.  
  
 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 관련된 언어 또는 알파벳에 대해 사전에 정의된 정렬 및 비교 규칙을 따릅니다.  
  
> [!NOTE]  
>  이 옵션을 선택하면 **대/소문자 구분**, **악센트 구분**, **일본어 가나 구분**및 **전자/반자 구분** 옵션을 사용할 수 없습니다.  
  
 **대/소문자 구분**  
 관련된 언어 또는 알파벳에 대해 제공된 사전 규칙을 기준으로 데이터를 정렬 및 비교하고 대문자와 소문자를 구분하려면 이 옵션을 선택합니다.  
  
 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 대문자와 소문자가 동일한 것으로 간주합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 여부 소문자의 정렬 문자와 관련 된 대문자 시기를 정의 하지 않습니다 **대/소문자 구분** 선택 하지 않으면 합니다.  
  
 **악센트 구분**  
 관련된 언어 또는 알파벳에 대해 제공된 사전 규칙을 기준으로 데이터를 정렬 및 비교하고 악센트가 있는 문자와 악센트가 없는 문자를 구분하려면 이 옵션을 선택합니다. 예를 들어 'a'와 'á'는 같지 않습니다.  
  
 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 악센트가 있는 문자와 없는 문자를 동일한 것으로 간주합니다.  
  
 **일본어가 나 구분**  
 관련된 언어 또는 알파벳에 대해 제공된 사전 규칙을 기준으로 데이터를 정렬 및 비교하고 히라가나와 가타카나라는 두 가지 유형의 일본어 가나 문자를 구분하려면 이 옵션을 선택합니다.  
  
 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 히라가나와 가타카나 문자를 동일한 것으로 간주합니다.  
  
 **전자/반자 구분**  
 관련된 언어 또는 알파벳에 대해 제공된 사전 규칙을 기준으로 데이터를 정렬 및 비교하고 단일 바이트 문자(반자)와 더블바이트 문자로 표시될 때의 동일한 문자(전자)를 구분하려면 이 옵션을 선택합니다.  
  
 이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 같은 문자의 싱글바이트 표시와 더블바이트 표시를 동일한 문자로 간주합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [번역 세부 정보 &#40;번역 탭, 차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](translation-details-dimension-designer-analysis-services-multidimensional-data.md)  
  
  