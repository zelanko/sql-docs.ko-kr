---
title: 열 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: baa5527f9c7eef1a2c6099dfb423347117a1f41d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="delete-a-column"></a>열 삭제 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  이 문서에서는 테이블 형식 모델 테이블에서 열을 삭제 하는 방법을 설명 합니다.  
  
## <a name="delete-a-model-table-column"></a>모델 테이블 열 삭제  
  
> [!NOTE]  
>  모델 테이블에서 열을 삭제해도 파티션 쿼리 정의에서 열이 삭제되지 않습니다. 삭제할 열이 파티션의 일부분일 경우 파티션 쿼리 정의에서 수동으로 열을 삭제해야 합니다. 파티션 쿼리 정의에서 열을 삭제하지 못하면 열이 쿼리되고 데이터가 반환되지만 작업을 처리하는 동안 모델 테이블에 채워지지는 않습니다. 자세한 내용은 참조 [파티션을](../../analysis-services/tabular-models/partitions-ssas-tabular.md)합니다.  
  
#### <a name="to-delete-a-model-table-column"></a>모델 테이블 열을 삭제하려면  
  
-   모델 디자이너에서 삭제할 열이 포함된 테이블의 열을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>테이블 속성 대화 상자를 사용하여 모델 테이블 열을 삭제하려면  
  
1.  모델 디자이너에서 삭제할 열이 포함된 테이블을 클릭하고 **테이블** 메뉴를 클릭한 다음  **테이블 속성**을 클릭합니다.  
  
2.  **열 이름 원본**에서 **모델** 을 선택합니다(*원본과 다를 경우 모델 테이블 열 이름 사용*).  
  
3.  **테이블 속성 편집** 대화 상자의 테이블 미리 보기 창에서 삭제할 열을 선택 취소한 다음 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블에 열 추가](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [파티션](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
