---
title: "테이블 삭제 (SSAS 테이블 형식) | Microsoft Docs"
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
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1d3437449a05b5e1f60083135e020171b3d1e916
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="delete-a-table-ssas-tabular"></a>테이블 삭제(SSAS 테이블 형식)
  모델 디자이너의 모델 작업 영역 데이터베이스에서 더 이상 필요하지 않은 테이블을 삭제할 수 있습니다. 테이블을 삭제하면 원래 원본 데이터는 영향을 받지 않고 가져와서 작업하고 있는 데이터만 삭제됩니다. 테이블의 삭제는 실행 취소할 수 없습니다.  
  
### <a name="to-delete-a-table"></a>테이블을 삭제하려면  
  
-   삭제하려는 테이블에 대해 모델 디자이너 아래쪽의 탭을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
## <a name="considerations-when-deleting-tables"></a>테이블 삭제 시 고려 사항  
  
-   테이블을 삭제하면 테이블이 있던 전체 탭이 삭제됩니다.  
  
-   해당 테이블과 연결된 측정값의 정의도 삭제됩니다.  
  
-   해당 테이블을 사용하여 계산 열을 만든 경우 해당 테이블의 열도 삭제됩니다. 다른 테이블에서 삭제된 테이블의 열을 사용하는 계산 열에서는 오류가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 열&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  

