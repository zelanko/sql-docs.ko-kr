---
title: 키 열 대화 상자 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.dataitemCollection.f1
helpviewer_keywords:
- DataItem Collection dialog box
ms.assetid: 585f27f2-d5eb-4516-b29a-2084010b7d51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26eb85c97c970f9fe1cfaf63ca9861c2be0b4695
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079470"
---
# <a name="key-columns-dialog-box-analysis-services---multidimensional-data"></a>키 열 대화 상자(Analysis Services - 다차원 데이터)
  
  **키 열** 대화 상자를 사용하여 특성의 **KeyColumns** 속성을 변경할 수 있습니다. 자세한 내용은 [특성의 KeyColumn 속성 수정](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)을 참조하세요.  
  
 **키 열 대화 상자를 표시하려면**  
  
-   
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 특성을 선택하고 **속성** 창에서 해당 특성의**KeyColumns**속성과 연관된 줄임표 단추( **...** )를 클릭합니다.  
  
## <a name="options"></a>옵션  
 **원본 테이블**  
 키 열을 선택할 원본 테이블을 선택합니다. 원본 테이블은 데이터 원본 뷰의 모든 테이블 목록에서 선택할 수 있습니다.  
  
 **사용 가능한 열**  
 키 열로 사용할 열을 선택합니다. 지정된 **원본 테이블** 의 열 목록에서 아직 키 열로 선택하지 않은 열을 선택할 수 있습니다.  
  
 선택한 열을 **키 열** 목록에 추가하려면 **>** 단추를 클릭합니다.  
  
 **키 열**  
 선택한 키 열의 순서를 정의합니다. 키 열의 순서는 올바른 복합 키를 정의하는 데 중요합니다. 키 열의 목록을 정렬하거나 다시 정렬하려면 열을 선택한 다음 **위로** 또는 **아래로** 단추를 클릭합니다.  
  
 
  **키 열** 목록에서 열을 제거하려면 열을 선택하고 **\<** 단추를 클릭합니다.  
  
 **위로**  
 
  **키 열** 에서 선택한 열을 한 위치 위로 이동하려면 클릭합니다.  
  
> [!NOTE]  
>  이 옵션은 목록에 둘 이상의 열이 있고 열을 선택한 경우에만 사용할 수 있습니다.  
  
 **드롭다운**  
 
  **키 열** 에서 선택한 열을 한 위치 아래로 이동하려면 클릭합니다.  
  
> [!NOTE]  
>  이 옵션은 목록에 둘 이상의 열이 있고 열을 선택한 경우에만 사용할 수 있습니다.  
  
 **>**  
 
  **키 열**에 나열된 열의 끝에 새 열을 추가하려면 클릭합니다.  
  
 **<**  
 선택한 열을 **키 열**에 나열된 열에서 제거하려면 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
