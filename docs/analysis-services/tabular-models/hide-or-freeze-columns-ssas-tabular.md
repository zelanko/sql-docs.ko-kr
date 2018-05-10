---
title: 열 숨기기 또는 고정 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: adc7fa1e80e6e49dc5d740d8499df6264f3ebef7
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2018
---
# <a name="hide-or-freeze-columns"></a>열 숨기기 또는 고정 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  모델 디자이너에서 테이블에 표시하지 않으려는 열이 있는 경우 해당 열을 임시로 숨길 수 있습니다. 열을 숨기면 새 열을 추가하거나 관련 데이터 열만 사용하여 작업하기 위해 화면에서 공간을 확보할 수 있습니다. 모델 디자이너의 **열** 메뉴 및 각 열 머리글을 마우스 오른쪽 단추로 클릭했을 때 열리는 메뉴를 사용하여 열을 숨기거나 숨겨진 열을 표시할 수 있습니다. 모델의 다른 영역으로 스크롤할 때 모델의 특정 영역이 계속 표시되도록 하려면 해당 영역의 열을 고정하여 잠글 수 있습니다.  
  
> [!IMPORTANT]  
>  열을 숨기는 기능은 데이터 보안의 목적보다는 모델 디자이너 또는 보고서에 표시되는 열의 목록을 단순화하고 간소화하기 위해 사용됩니다. 데이터 보안을 위해서는 보안 역할을 정의할 수 있습니다. 역할을 통해 특정 개체에 대해서만 메타데이터와 데이터를 볼 수 있도록 제한할 수 있습니다. 자세한 내용은 참조 [역할](../../analysis-services/tabular-models/roles-ssas-tabular.md)합니다.  
  
 열을 숨길 때 모델 디자이너 또는 보고서에서 작업할 동안에만 열을 숨기는 방법도 있습니다. 모든 열을 숨기면 모델 디자이너에서 전체 테이블이 공백으로 나타납니다.  
  
> [!NOTE]  
>  숨겨야 하는 열이 많은 경우 열을 숨기거나 숨김을 해제하는 대신 큐브 뷰를 만들 수 있습니다. 큐브 뷰는 관련 데이터의 하위 집합을 보다 쉽게 사용할 수 있는 사용자 지정 데이터 뷰입니다. 자세한 내용은 참조 [만들기 큐브 뷰 및 관리](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)  
  
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
 [테이블 및 열](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [큐브 뷰](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
