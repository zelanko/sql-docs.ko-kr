---
title: 특성 유형 변경(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4406eb225002bbf5df93f8c67385694922d7d2c7
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482761"
---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>특성 유형 변경(Excel용 MDS 추가 기능)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 관리자는 허용되는 문자 개수 또는 데이터 형식이 잘못된 경우 특성 유형을 변경할 수 있습니다.  
  
 제한된 목록(도메인 기반 특성)을 만들도록 특성 유형을 변경하려는 경우 [도메인 기반 특성 만들기&#40;Excel용 MDS 추가 기능&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)를 참조하세요.  
  
> [!NOTE]  
>  **이름** 또는 **코드** 열의 유형이나 길이는 업데이트할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 와 **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../administrators-master-data-services.md)를 참조하세요.  
  
-   기존 모델, 엔터티 및 특성이 있어야 합니다.  
  
### <a name="to-change-the-attribute-type"></a>특성 유형을 변경하려면  
  
1.  Excel에서 변경하려는 열(특성)이 포함된 엔터티를 로드합니다. 자세한 내용은 [Excel에 MDS에서 데이터 로드](export-data-to-excel-from-master-data-services.md)합니다.  
  
2.  변경할 열에서 셀을 클릭합니다.  
  
3.  **모델 작성** 그룹에서 **특성 속성**을 클릭합니다.  
  
4.  **특성 속성** 대화 상자에서 필요에 따라 설정을 업데이트합니다.  
  
5.  **확인**을 클릭합니다.  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>특성 유형을 변경하면 어떻게 됩니까?  
 특성에 종속성이 존재하여, 그러한 속성이 MDS 비즈니스 규칙에 의해 참조되거나 특성이 구독 뷰에 포함될 경우, 사용자가 특성의 데이터 형식을 변경하면, MDS에서 다음 작업이 수행됩니다.  
  
-   특성의 데이터 형식을 변경합니다.  
  
-   모든 값을 포함 하지 않는 "_old" 접미사를 사용 하 여 특성의 복사본을 생성 합니다. 이 호출 되는 **사용 되지 않는** 특성입니다.  
  
 하지만 원래 특성의 모든 기존 종속성은 변경된 특성이 아닌 더 이상 사용되지 않는 특성을 가리킵니다.  
  
 즉,  
  
-   특성의 새로운 데이터 형식에 따라 논리가 동일하지 않을 수 있기 때문에 변경된 특성을 가리키도록 비즈니스 규칙을 새로 고쳐야 합니다. 영향을 받는 각 규칙을 편집하고, 더 이상 사용되지 않는 특성(_old)에서 참조를 제거하고 업데이트된 특성을 가리키도록 식을 재작업해야 합니다.  
  
-   통합 관리 선택 구독 뷰를 열고, 뷰 행을 선택, 연필 아이콘을 클릭 하 여 편집용으로 엽니다 및 클릭 해야 하는 **저장 디스크** 아이콘 뷰 정의 새로 고쳐야 합니다. 뷰 구문을 재생성하는 데 다른 변경 사항은 필요하지 않습니다.  
  
-   특성이 포함된 준비 테이블에는 더 이상 사용되지 않는 특성 열이 테이블에 추가됩니다. 즉, 준비 코드에 영향을 줍니다. 더 이상 사용되지 않는 특성을 없애기 위해서는 비즈니스 규칙 및 구독 뷰를 업데이트한 후 삭제할 수 있습니다.  
  
 **사용 되지 않는 특성 삭제**  
  
 더 이상 사용되지 않는 특성을 삭제하려면 먼저 앞에서 설명한 것처럼 비즈니스 규칙을 수정하고 구독 뷰를 다시 생성하여 특성에 대한 모든 참조를 제거해야 합니다. 그렇지 않으면 더 이상 사용되지 않는 특성을 삭제하려고 시도할 때 시스템 관리 웹 페이지에서 개체에서 참조되기 때문에 특성을 삭제할 수 없다는 오류가 표시됩니다.  
  
 특성을 삭제 하려면 참조 [특성을 삭제 &#40;Master Data Services&#41;](../delete-an-attribute-master-data-services.md)  
  
> [!TIP]  
>  기존 데이터 및 관련 항목이 포함된 MDS 특성의 데이터 형식을 변경하는 것은 번거로운 일일 수 있습니다. 특히 엔터티에 종속된 비즈니스 규칙 또는 구독 뷰가 선언되었다면 더욱 그렇습니다. 가장 좋은 방법은 필요한 값을 저장하기에 충분히 유연한 데이터 형식으로 시작하는 것입니다. 예를 들어 문자열을 작은 크기로 시작할 수 있지만 시간이 지남에 따라 길이를 늘려야 할 수 있으므로, 최악의 시나리오를 고려하는 것입니다. 텍스트 문자열 길이가 너무 길면 부담이 될 수 있으므로(예를 들어 GUI 텍스트 상자가 너무 넓으면 화면에 맞게 표시하기 어려울 수 있음), 너무 긴 문자열 길이는 피하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [특성&#40;Master Data Services&#41;](../attributes-master-data-services.md)   
 [모델 작성&#40;Excel용 MDS 추가 기능&#41;](building-a-model-mds-add-in-for-excel.md)  
  
  
