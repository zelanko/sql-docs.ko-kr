---
title: 겹치는 모델 및 멤버 권한(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], effective permissions
- permissions [Master Data Services], model and member overlaps
- members [Master Data Services], effective permissions
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ca57d34a3dda2880f3882d1940c6852af0729fb7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482736"
---
# <a name="overlapping-model-and-member-permissions-master-data-services"></a>겹치는 모델 및 멤버 권한(Master Data Services)
  멤버에 할당된 사용 권한과 모델 개체에 할당된 사용 권한이 겹칠 수 있습니다. 사용 권한이 겹치면 보다 제한적인 사용 권한이 적용됩니다.  
  
 멤버의 사용 권한이 해당 모델 개체와 다른 경우 다음 규칙이 적용됩니다.  
  
-   **Deny** 는 다른 모든 사용 권한을 재정의 합니다.  
  
-   **읽기 전용은** **업데이트**를 재정의 합니다.  
  
 다음 이미지는 특성 사용 권한이 멤버 권한과 다를 경우 개별 특성 값에 적용되는 사용 권한을 보여 줍니다.  
  
 ![mds_conc_security_member_overlap_table](../../2014/master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## <a name="example-1"></a>예 1  
 ![mds_conc_overlap_model_1](../../2014/master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 
  **모델** 탭의 Product 엔터티에는 **업데이트** 권한이 할당되어 있습니다. 엔터티의 모든 특성은 해당 사용 권한을 상속합니다.  
  
 
  **계층 멤버** 탭의 파생 계층에 있는 Mountain Bikes 하위 범주 노드에는 **업데이트** 권한이 할당되어 있습니다.  
  
 결과: **탐색기**에서 사용자에게는 Mountain Bikes 노드에 있는 모든 멤버의 모든 특성 값에 대한 **업데이트** 권한이 있습니다. 모든 다른 멤버와 특성은 숨겨집니다.  
  
 ![mds_conc_overlap_model_example_1](../../2014/master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## <a name="example-2"></a>예제 2  
 ![mds_conc_overlap_model_2](../../2014/master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 
  **모델** 탭의 하위 범주 특성에는 **업데이트** 권한이 할당되어 있습니다.  
  
 **계층 멤버** 탭의 파생 계층에 있는 산악 자전거 하위 범주 노드에는 **읽기** 전용 권한이 명시적으로 할당 됩니다.  
  
 결과: **탐색기**에서 사용자에 게 산악 자전거 노드의 멤버에 대 한 하위 범주 특성 값에 대 한 **읽기 전용** 권한이 있습니다. 모든 다른 멤버와 특성은 숨겨집니다.  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="example-3"></a>예제 3  
 ![mds_conc_overlap_model_3](../../2014/master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 **모델** 탭의 하위 범주 특성에는 **읽기** 전용 권한이 할당 됩니다.  
  
 
  **계층 멤버** 탭의 파생 계층에 있는 Mountain Bikes 하위 범주 노드에는 **업데이트** 권한이 명시적으로 할당됩니다.  
  
 결과: **탐색기**에서 사용자에 게는 특성 값에 대 한 **읽기 전용** 권한이 있습니다. 모든 다른 멤버와 특성은 숨겨집니다.  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services) &#40;사용 권한을 결정 하는 방법&#41;](how-permissions-are-determined-master-data-services.md)   
 [MDS(Master Data Services)&#41;&#40;겹치는 사용자 및 그룹 권한](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  
