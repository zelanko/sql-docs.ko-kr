---
title: 도메인 기반 특성 만들기(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 7b3e30dc-8f41-4a5d-8009-ae5a4426a64b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 296ace8d97269d80179d437b1033b92196d6adc5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478981"
---
# <a name="create-a-domain-based-attribute-mds-add-in-for-excel"></a>도메인 기반 특성 만들기(Excel용 MDS 추가 기능)
  
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]
  [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 관리자는 열에 있는 값을 특정 값 집합으로 제약하려는 경우 도메인 기반 특성을 만들 수 있습니다.  
  
 워크시트에 이미 있는 값이나 기존 엔터티에서 가져온 값으로 제약할 수 있습니다.  
  
> [!NOTE]  
>  목록에서 값을 선택하는 대신 제약된 열에 값을 입력하면 값이 게시될 때 **$InputStatus$** 열에 오류가 표시됩니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   
  **시스템 관리** 와 **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   모델과 엔터티가 이미 있어야 합니다.  
  
### <a name="to-perform-this-procedure"></a>이 절차를 수행하려면  
  
1.  Excel에서 제약할 열(특성)이 포함된 엔터티를 로드합니다. 자세한 내용은 [MDS에서 Excel로 데이터 로드](export-data-to-excel-from-master-data-services.md)를 참조 하세요.  
  
2.  제약할 열에서 셀을 클릭합니다.  
  
3.  
  **모델 작성** 그룹에서 **특성 속성**을 클릭합니다.  
  
4.  
  **특성 속성** 대화 상자의 **특성 유형** 목록에서 **제약된 목록(도메인 기반)** 을 선택합니다.  
  
5.  
  **특성을 채울 값** 목록에서 다음을 수행합니다.  
  
    -   워크시트의 값을 사용하려면 **선택한 열**을 선택합니다. 선택한 열의 값을 사용하여 새 엔터티와 새 준비 테이블이 만들어집니다.  
  
    -   기존 엔터티의 값을 사용하려면 엔터티 이름을 선택합니다.  
  
6.  이전 단계에서 **선택한 열을** 을 선택한 경우 **새 엔터티 이름** 상자에 새 엔터티의 이름을 입력합니다. 이 이름은 열(특성) 이름과 같을 수 있습니다.  
  
7.  **확인**을 클릭합니다. 이제 열의 각 셀에 사용자가 값을 선택할 수 있는 목록이 포함됩니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   제약된 목록에 값을 추가하거나 목록에서 값을 삭제하려면 특성의 기반이 되는 엔터티를 로드합니다. 엔터티를 로드 하는 방법에 대 한 자세한 내용은 [MDS에서 Excel로 데이터 로드](export-data-to-excel-from-master-data-services.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [도메인 기반 특성 &#40;MDS(Master Data Services)&#41;](../domain-based-attributes-master-data-services.md)   
 [엔터티 &#40;Excel용 MDS 추가 기능를 만듭니다&#41;](create-an-entity-mds-add-in-for-excel.md)   
 [모델 &#40;Excel용 MDS 추가 기능&#41;빌드](building-a-model-mds-add-in-for-excel.md)  
  
  
