---
title: 계산 멤버 작성기 대화 상자 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.calculatedmemberbuilderdialog.f1
ms.assetid: 73b89a9f-f403-4ab8-99f7-e3ceb870c260
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8046d93f28c6d7c61899bb5f9aa3598f834c0ab3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088378"
---
# <a name="calculated-member-builder-dialog-box-analysis-services---multidimensional-data"></a>계산 멤버 작성기 대화 상자(Analysis Services - 다차원 데이터)
  
  **의** 계산 멤버 작성기 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 대화 상자를 사용하여 계산 멤버를 작성할 수 있습니다.  
  
## <a name="options"></a>옵션  
  
|용어|정의|  
|----------|----------------|  
|**이름**|계산 멤버의 이름을 입력합니다.|  
|**부모 계층**|계산 멤버를 만들 계층을 선택합니다.|  
|**부모 멤버**|수준이 두 개 이상인 부모 계층(`Measures` 차원 제외)을 선택한 경우 이 옵션이 설정됩니다. 부모 멤버를 선택 하려면 줄임표 (**...**) 단추를 클릭 합니다. 부모 멤버는 차원 구조에서 계산 멤버의 위치를 결정합니다.|  
|**식**|사용할 MDX 식을 입력합니다.|  
|**있는지**|
  **식** 에서 정의한 MDX 식을 테스트하려면 **확인**을 클릭합니다.|  
|**메타데이터**|
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 식 **에서 정의한 MDX 식에 포함시킬 수 있는 현재**개체에 대한 메타데이터를 표시합니다.<br /><br /> 선택한 항목을 마우스 오른쪽 단추로 클릭하고 **복사**를 선택하거나 선택한 항목을 **식**으로 끌어서 해당 항목에 대한 MDX 구문을 복사할 수 있습니다.|  
|**함수**|현재 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 사용 가능한 MDX 함수를 표시합니다. 나열된 항목은 MDSCHEMA_FUNCTIONS 스키마 행 집합에서 검색된 것입니다.<br /><br /> 선택한 항목을 마우스 오른쪽 단추로 클릭하고 **복사**를 선택하거나 선택한 항목을 **식**으로 끌어서 해당 항목에 대한 MDX 구문을 복사할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [MDX&#41; 참조 &#40;다차원 식](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
