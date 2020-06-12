---
title: 만들기-명명 된 계산 편집 대화 상자 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsveditor.createnamedcalculation.f1
helpviewer_keywords:
- Named Calculation dialog box
ms.assetid: 66fb30ae-f5c5-4bfc-80ca-8c8a3a9bb30d
author: minewiskan
ms.author: owend
ms.openlocfilehash: d6a3d94e2e003410bfdeb632d30fc0e5e3f8a0d4
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526639"
---
# <a name="create-edit-named-calculation-dialog-box-analysis-services"></a>Create-Edit Named Calculation Dialog Box (Analysis Services)
  **의** 명명된 계산 만들기/편집 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 대화 상자를 사용하여 데이터 원본 뷰에서 테이블에 대한 명명된 계산을 정의하거나 수정할 수 있습니다. 다음과 같은 방법으로 **명명된 계산 만들기/편집** 대화 상자를 표시할 수 있습니다.  
  
-   **데이터 원본 뷰 디자이너** 의 **도구 모음** 창에서 **새 명명된 계산**을 클릭합니다.  
  
-   **데이터 원본 뷰 디자이너** 의 **테이블** 또는 **다이어그램** 창에서 테이블을 마우스 오른쪽 단추로 클릭한 다음 **새 명명된 계산**을 선택합니다.  
  
-   **데이터 원본 뷰 디자이너** 의 **다이어그램** 창에서 명명된 계산의 이름을 마우스 오른쪽 단추로 클릭한 다음 **명명된 계산 편집**을 선택합니다.  
  
## <a name="options"></a>옵션  
 **열 이름**  
 명명된 계산의 이름을 입력합니다.  
  
 **설명**  
 명명된 계산에 대한 선택적 설명을 입력합니다.  
  
 **식**  
 스칼라 값을 반환하는 유효한 SQL 식을 입력합니다. 이 식은 공급자에게 전송된 다음 식으로 유효성이 검사됩니다.  
  
```  
SELECT <Table Name in Data Source>.* , <Expression> AS <Column Name> FROM <Table Name in Data Source>AS <Table Name in Data Source View>  
```  
  
 위의 식은 하위 SELECT 문을 사용하여 다른 테이블에 대한 참조를 포함할 수 있습니다. If the expression would require parentheses in a SELECT statement, the expression entered must be enclosed between parentheses.  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [데이터 원본 뷰 디자이너&#40;Analysis Services - 다차원 데이터&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
