---
title: 경고 (데이터베이스 디자이너) (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.warnings.f1
ms.assetid: 13f58b4d-f345-4fbc-ae2d-b3c8290a797d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90eeca203c672c21551b8aff2e24feb164d8fda5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065433"
---
# <a name="warnings-database-designer-analysis-services---multidimensional-data"></a>경고(데이터베이스 디자이너)(Analysis Services - 다차원 데이터)
  
  **경고** 탭을 사용하여 규칙을 전역적으로 확인 및 해제하고 해제된 경고의 특정 인스턴스를 확인 및 다시 설정할 수 있습니다. 
  **경고** 탭에는 **디자인 경고 규칙** 과 **해제된 경고**라는 두 개의 표가 표시됩니다.  
  
 **경고 탭을 표시하려면**  
  
1.  
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  
  **솔루션 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 편집**을 클릭한 다음 **경고** 탭을 클릭합니다.  
  
## <a name="design-warning-rules-grid"></a>디자인 경고 규칙 표  
 
  **디자인 경고 규칙** 표에는 모든 디자인 경고 규칙이 표시됩니다. 이 표는 데이터베이스에 대해 설정할 수 있는 규칙도 제어합니다. 경고 규칙을 설정하거나 해제하려면 해당 확인란을 선택하거나 선택을 취소합니다.  
  
 
  **디자인 경고 규칙** 표에는 다음과 같은 열이 있습니다.  
  
 **설명**  
 규칙의 이름을 표시합니다. 규칙은 범주별로 그룹화됩니다.  
  
 **중요도**  
 규칙에 할당된 중요도를 표시합니다.  
  
 **주석**  
 (옵션) 사용자가 경고 해제 이유에 대한 설명을 입력할 수 있습니다.  
  
## <a name="dismissed-warnings-grid"></a>해제된 경고 표  
 
  **해제된 경고** 표에는 **오류 목록**에서 해제된 특정 경고가 모두 표시됩니다. 경고를 다시 설정하려면 표에서 경고를 선택한 다음 **다시 사용**을 클릭합니다.  
  
 
  **해제된 경고** 표에는 다음과 같은 항목이 있습니다.  
  
 **Object**  
 개체 유형과 개체 이름을 나타내는 아이콘을 표시합니다.  
  
 **형식**  
 개체 유형을 표시합니다.  
  
 **설명**  
 규칙의 이름을 표시합니다.  
  
 **중요도**  
 규칙에 할당된 중요도를 표시합니다.  
  
 **주석**  
 경고를 해제할 때 입력한 설명을 표시합니다. 여기에서 설명을 추가하거나 수정할 수 있습니다.  
  
 **다시 사용**  
 선택한 경고를 다시 설정합니다.  
  
> [!NOTE]  
>  경고가 있는 개체의 경우 이 개체가 잘못된 상태이거나 프로젝트에서 수동으로 제거되면 목록에 있는 경고 옆에 오류 아이콘이 표시됩니다. 경고를 해제하려면 경고를 선택한 다음 **다시 사용**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [경고 해제 대화 상자 &#40;Analysis Services 다차원 데이터&#41;](dismiss-warning-dialog-box-analysis-services-multidimensional-data.md)   
 [일반 &#40;데이터베이스 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](general-database-designer-analysis-services-multidimensional-data.md)  
  
  
