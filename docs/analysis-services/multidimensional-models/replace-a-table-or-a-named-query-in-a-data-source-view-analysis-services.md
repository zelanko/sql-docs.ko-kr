---
title: 테이블 또는 데이터 원본 뷰 (Analysis Services)에서 명명된 된 쿼리 바꾸기 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a171eafc35446f588d64c74457792912dcebe75a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services"></a>데이터 원본 뷰의 테이블 또는 명명된 쿼리 바꾸기(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  데이터 원본 뷰 디자이너에서 데이터 원본 뷰(DSV)의 테이블, 뷰 또는 명명된 쿼리를 같은 데이터 원본이나 다른 데이터 원본의 다른 테이블 또는 뷰와 바꾸거나 DSV에 정의된 명명된 쿼리와 바꿀 수 있습니다. 테이블을 바꾸는 경우 DSV의 테이블에 대한 개체 ID는 변경되지 않으므로 해당 테이블에 대한 참조를 포함하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 또는 프로젝트의 다른 모든 개체는 계속해서 이 테이블을 참조합니다. 이름 및 열 유형 일치를 기반으로 관련된 모든 관계는 유지됩니다. 반면 테이블을 삭제한 다음 추가하면 참조 및 관계가 모두 손실되며 다시 만들어야 합니다.  
  
 테이블을 다른 테이블로 바꾸려면 프로젝트 모드에서 데이터 원본 뷰 디자이너의 원본 데이터에 대한 활성 연결이 있어야 합니다.  
  
 데이터 원본 뷰의 테이블을 동일한 데이터 원본의 다른 테이블로 바꾸는 경우가 가장 많습니다. 그러나 명명된 쿼리를 테이블로 바꿀 수도 있습니다. 예를 들어 이전에 명명된 쿼리로 바꾼 테이블을 다시 테이블로 되돌릴 수 있습니다.  
  
> [!IMPORTANT]  
>  데이터 원본의 테이블 이름을 바꾸는 경우 테이블 바꾸기 단계를 수행한 다음 DSV를 새로 고치기 전에 이름을 바꾼 테이블을 DSV의 해당 테이블 원본으로 지정합니다. 바꾸기 및 이름 바꾸기 프로세스를 완료하면 DSV의 테이블, 테이블 참조 및 테이블 관계가 그대로 유지됩니다. 그렇게 하지 않으면 DSV를 새로 고칠 때 데이터 원본에서 이름을 바꾼 테이블이 삭제된 것으로 해석됩니다. 자세한 내용은 [데이터 원본 뷰에서 스키마 새로 고침&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/refresh-the-schema-in-a-data-source-view-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_nq"></a> 테이블을 명명된 쿼리로 바꾸기  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 테이블이나 명명된 쿼리를 바꿀 데이터 원본 뷰가 포함된 프로젝트를 열거나 데이터베이스에 연결합니다.  
  
2.  솔루션 탐색기에서 **데이터 원본 뷰** 폴더를 확장한 다음 해당 데이터 원본 뷰를 두 번 클릭합니다.  
  
3.  **명명된 쿼리 만들기** 대화 상자가 열립니다. **테이블** 또는 **다이어그램** 창에서 바꿀 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 바꾸기** 를 가리킨 다음 **새 명명된 쿼리로**를 클릭합니다.  
  
4.  **명명된 쿼리 만들기** 대화 상자에서 명명된 쿼리를 정의한 다음 **확인**을 클릭합니다.  
  
5.  수정된 데이터 원본 뷰를 저장합니다.  
  
## <a name="replace-a-table-or-named-query-with-a-table"></a>테이블이나 명명된 쿼리를 테이블로 바꾸기  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 테이블이나 명명된 쿼리를 바꿀 데이터 원본 뷰가 포함된 프로젝트를 열거나 데이터베이스에 연결합니다.  
  
2.  솔루션 탐색기에서 **데이터 원본 뷰** 폴더를 확장한 다음 해당 데이터 원본 뷰를 두 번 클릭합니다.  
  
3.  **다른 테이블로 테이블 바꾸기** 대화 상자가 열립니다. **테이블** 또는 **다이어그램** 창에서 바꿀 테이블이나 명명된 쿼리를 마우스 오른쪽 단추로 클릭하고 **테이블 바꾸기** 를 가리킨 다음 **다른 테이블로**를 클릭합니다.  
  
4.  **다른 테이블로 테이블 바꾸기** 대화 상자에서 다음을 수행합니다.  
  
    1.  **데이터 원본** 드롭다운 목록 상자에서 원하는 데이터 원본을 선택합니다.  
  
    2.  테이블이나 명명된 쿼리를 바꿀 테이블을 선택합니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  수정된 데이터 원본 뷰를 저장합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델의 데이터 원본 뷰](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
