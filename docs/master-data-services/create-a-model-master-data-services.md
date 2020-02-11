---
title: 모델 만들기
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], creating models
- creating models [Master Data Services]
ms.assetid: 9bb3b3b3-bde8-44aa-ad62-eaae21188141
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 730e18fca866891d62b68d321ec13e4be5da59bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73728487"
---
# <a name="create-a-model-master-data-services"></a>모델 만들기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델 개체를 포함할 모델을 만듭니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   
  **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
### <a name="to-create-a-model"></a>모델을 만들려면  
  
1.  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  
  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **모델**을 클릭합니다.  
  
3.  
  **모델 관리** 페이지에서 **추가**를 클릭합니다. 오른쪽에 패널이 표시됩니다.  
  
4.  
  **이름** 상자에 모델의 이름을 입력합니다.  
  
5.  필요에 따라 **설명** 필드에 모델 설명을 입력합니다.  
  
6.  
  **로그 보존 기간(일)** 필드에서 로그 데이터 보존 옵션 중 하나를 선택합니다. 기본값인 **시스템 설정**은 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]의 시스템 설정에서 값이 상속됨을 나타냅니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
     시스템 설정을 재정의하고 트랜잭션 로그 데이터는 제거하지 않으려면 **아니요**를 선택합니다. 해당일의 로그 데이터만 보존하고 이전 날짜의 모든 로그 데이터를 자르려면 **예**를 선택하고 **일** 필드의 값을 0으로 설정합니다. 지정된 기간(일) 동안 로그 데이터를 보존하려면 **예** 를 선택하고 **일** 필드의 값을 원하는 기간(일)으로 설정합니다.  
  
7.  또는 **모델과 이름이 같은 엔터티 만들기** 를 선택하여 모델과 이름이 같은 엔터티를 만듭니다.  
  
8.  
  **모델 저장**을 클릭합니다.  
  
 생성되는 각 모델에 대해 열이 8개 포함된 행이 표에 추가됩니다. 이러한 8개 열은 다음과 같습니다.  
  
-   **상태**: 모델 상태입니다. **모델 저장** 단추를 클릭 하면 모델이 업데이트 중임을 나타내는 ![업데이트](../master-data-services/media/mds-model-status-updating.png "Updating") 이미지가 표시 됩니다. 모델을 만들거나 편집할 때 오류가 발생 하면 ![오류](../master-data-services/media/mds-model-status-error.png "Error") 이미지가 표시 됩니다. 오류가 발생하지 않는 경우 모델은 정상 상태가 되며 ![확인](../master-data-services/media/mds-model-status-ok.png "확인") 이미지가 표시됩니다.  
  
-   **이름**: 모델 이름입니다.  
  
-   **설명**: 모델 설명입니다.  
  
-   **로그 보존 기간 (일)**: 모델에 대 한 로그가 보존 되는 일 수입니다.  
  
-   **만든 사람**: 모델을 만든 사용자의 사용자 이름입니다.  
  
-   **만든 날짜 및 시간**: 모델을 만든 날짜와 시간입니다.  
  
-   **업데이트**한 사람: 모델을 마지막으로 업데이트 한 사용자의 사용자 이름입니다.  
  
-   **업데이트 된 날짜 및 시간**: 모델을 마지막으로 업데이트 한 날짜와 시간입니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [엔터티 &#40;MDS(Master Data Services)를 만듭니다&#41;](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [모델 &#40;MDS(Master Data Services)&#41;](../master-data-services/models-master-data-services.md)   
 [엔터티 &#40;MDS(Master Data Services)&#41;](../master-data-services/entities-master-data-services.md)   
 [모델 &#40;MDS(Master Data Services) 삭제&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [모델 &#40;MDS(Master Data Services) 편집&#41;](../master-data-services/edit-model-master-data-services.md)   
 [트랜잭션 &#40;MDS(Master Data Services)&#41;](../master-data-services/transactions-master-data-services.md)  
  
  
