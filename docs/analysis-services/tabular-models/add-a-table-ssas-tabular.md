---
title: "테이블 추가 (SSAS 테이블 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d713c432-db99-4983-acc1-52b0fdd58bd6
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 95113c2053b0e37cc4ee3d94d2baf0ed64d71d57
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="add-a-table-ssas-tabular"></a>테이블 추가(SSAS 테이블 형식)
  이 항목에서는 이전에 데이터를 모델로 가져왔던 데이터 원본의 테이블을 추가하는 방법에 대해 설명합니다. 같은 데이터 원본의 테이블을 추가하려면 기존 데이터 원본 연결을 사용합니다. 단일 데이터 원본에서 임의 개수의 테이블을 가져올 때는 항상 단일 연결을 사용하는 것이 좋습니다.  
  
### <a name="to-add-a-table-from-an-existing-data-source"></a>기존 데이터 원본의 테이블을 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **모델** 메뉴를 클릭한 다음 **기존 연결**을 클릭합니다.  
  
2.  **기존 연결** 페이지에서 추가할 테이블이 있는 데이터 원본에 대한 연결을 선택한 다음 **열기**를 클릭합니다.  
  
3.  **테이블 및 뷰 선택** 페이지에서 모델에 추가할 데이터 원본의 테이블을 선택합니다.  
  
    > [!NOTE]  
    >  **테이블 및 뷰 선택** 페이지에서는 이전에 가져온 테이블이 선택된 것으로 표시되지 않습니다.  이 연결을 사용하여 이전에 가져온 테이블을 선택했는데 해당 테이블에 다른 이름을 지정하지 않은 경우 이름에 1이 추가됩니다. 이 연결을 사용하여 이전에 가져온 테이블을 다시 선택할 필요는 없습니다.  
  
4.  필요한 경우 **미리 보기 및 필터**를 사용하여 특정 열만 선택하거나 가져올 데이터에 필터를 적용합니다.  
  
5.  **마침** 을 클릭하여 새 테이블을 가져옵니다.  
  
> [!NOTE]  
>  단일 데이터 원본에서 여러 테이블을 동시에 가져올 때는 원본에 있는 해당 테이블 간의 관계가 모델에서 자동으로 생성됩니다. 그러나 나중에 테이블을 추가할 때는 새로 추가한 테이블과 이전에 가져온 테이블 간에 모델에서 관계를 수동으로 만들어야 할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 가져오기&#40;SSAS 테이블 형식&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [테이블 삭제&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)  
  
  
