---
title: "(SSAS 테이블 형식) 열 숨기기 또는 고정 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.hideunhidecolumnsdb.f1
ms.assetid: 5407aee5-6a07-4559-a2ba-2ca00a242f02
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 875994a4c5b2f8a78d21c049236a4c95d8c38f76
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="hide-or-freeze-columns-ssas-tabular"></a>열 숨기기 또는 고정(SSAS 테이블 형식)
  모델 디자이너에서 테이블에 표시하지 않으려는 열이 있는 경우 해당 열을 임시로 숨길 수 있습니다. 열을 숨기면 새 열을 추가하거나 관련 데이터 열만 사용하여 작업하기 위해 화면에서 공간을 확보할 수 있습니다. 모델 디자이너의 **열** 메뉴 및 각 열 머리글을 마우스 오른쪽 단추로 클릭했을 때 열리는 메뉴를 사용하여 열을 숨기거나 숨겨진 열을 표시할 수 있습니다. 모델의 다른 영역으로 스크롤할 때 모델의 특정 영역이 계속 표시되도록 하려면 해당 영역의 열을 고정하여 잠글 수 있습니다.  
  
> [!IMPORTANT]  
>  열을 숨기는 기능은 데이터 보안의 목적보다는 모델 디자이너 또는 보고서에 표시되는 열의 목록을 단순화하고 간소화하기 위해 사용됩니다. 데이터 보안을 위해서는 보안 역할을 정의할 수 있습니다. 역할을 통해 특정 개체에 대해서만 메타데이터와 데이터를 볼 수 있도록 제한할 수 있습니다. 자세한 내용은 [역할&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)을 참조하세요.  
  
 열을 숨길 때 모델 디자이너 또는 보고서에서 작업할 동안에만 열을 숨기는 방법도 있습니다. 모든 열을 숨기면 모델 디자이너에서 전체 테이블이 공백으로 나타납니다.  
  
> [!NOTE]  
>  숨겨야 하는 열이 많은 경우 열을 숨기거나 숨김을 해제하는 대신 큐브 뷰를 만들 수 있습니다. 큐브 뷰는 관련 데이터의 하위 집합을 보다 쉽게 사용할 수 있는 사용자 지정 데이터 뷰입니다. 자세한 내용은 [큐브 뷰 만들기 및 관리&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)를 참조하세요.  
  
### <a name="to-hide-an-individual-column"></a>개별 열을 숨기려면  
  
1.  모델 디자이너에서 숨기려는 열이 포함된 테이블을 선택합니다.  
  
2.  열을 마우스 오른쪽 단추로 클릭하고 **열 숨기기**를 클릭한 다음 **디자이너 및 보고서에서**, **보고서에서**또는 **디자이너에서**를 클릭합니다.  
  
### <a name="to-hide-multiple-columns"></a>여러 열을 숨기려면  
  
1.  모델 디자이너에서 숨기려는 열이 포함된 테이블을 선택합니다.  
  
2.  **열** 메뉴에서 **숨기기 및 숨기기 취소**를 클릭합니다.  
  
3.  **열 숨기기 및 숨기기 취소** 대화 상자에서 숨기려는 각 열을 찾은 다음 **디자이너** 및 **보고서**중 하나 또는 둘 다 선택을 취소합니다.  
  
4.  **확인**을 클릭합니다.  
  
### <a name="to-freeze-columns"></a>열을 고정하려면  
  
1.  모델 디자이너에서 고정할 열이 포함된 테이블을 선택합니다.  
  
2.  고정할 열을 하나 이상 선택합니다.  
  
3.  **열** 메뉴에서 **고정**을 클릭합니다.  
  
    > [!NOTE]  
    >  열이 고정되면 디자이너에서 테이블의 왼쪽(또는 앞)으로 이동합니다. 나중에 열의 고정을 취소해도 다시 원래 위치로 이동하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 열&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [큐브 뷰&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [역할&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
