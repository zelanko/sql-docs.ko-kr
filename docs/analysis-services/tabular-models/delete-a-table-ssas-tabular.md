---
title: 테이블 삭제 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1d3176baca80333c8167d45e6fb3a20e85e4f19d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="delete-a-table"></a>테이블 삭제
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  모델 디자이너의 모델 작업 영역 데이터베이스에서 더 이상 필요하지 않은 테이블을 삭제할 수 있습니다. 테이블을 삭제하면 원래 원본 데이터는 영향을 받지 않고 가져와서 작업하고 있는 데이터만 삭제됩니다. 테이블의 삭제는 실행 취소할 수 없습니다.  
  
### <a name="to-delete-a-table"></a>테이블을 삭제하려면  
  
-   삭제하려는 테이블에 대해 모델 디자이너 아래쪽의 탭을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
## <a name="considerations-when-deleting-tables"></a>테이블 삭제 시 고려 사항  
  
-   테이블을 삭제하면 테이블이 있던 전체 탭이 삭제됩니다.  
  
-   해당 테이블과 연결된 측정값의 정의도 삭제됩니다.  
  
-   해당 테이블을 사용하여 계산 열을 만든 경우 해당 테이블의 열도 삭제됩니다. 다른 테이블에서 삭제된 테이블의 열을 사용하는 계산 열에서는 오류가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 열](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
