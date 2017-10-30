---
title: "모델 만들기(Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- models [Master Data Services], creating models
- creating models [Master Data Services]
ms.assetid: 9bb3b3b3-bde8-44aa-ad62-eaae21188141
caps.latest.revision: 13
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 1a32cc8f778496f5609d44c17b69623b75b8c240
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="create-a-model-master-data-services"></a>모델 만들기(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 모델 개체를 포함할 모델을 만듭니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-create-a-model"></a>모델을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **모델**을 클릭합니다.  
  
3.  **모델 관리** 페이지에서 **추가**를 클릭합니다. 오른쪽에 패널이 표시됩니다.  
  
4.  **이름** 상자에 모델의 이름을 입력합니다.  
  
5.  필요에 따라 **설명** 필드에 모델 설명을 입력합니다.  
  
6.  **로그 보존 기간(일)** 필드에서 로그 데이터 보존 옵션 중 하나를 선택합니다. 기본값인 **시스템 설정**은 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]의 시스템 설정에서 값이 상속됨을 나타냅니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
     시스템 설정을 재정의하고 트랜잭션 로그 데이터는 제거하지 않으려면 **아니요**를 선택합니다. 해당일의 로그 데이터만 보존하고 이전 날짜의 모든 로그 데이터를 자르려면 **예** 를 선택하고 **일** 필드의 값을 0으로 설정합니다. 지정된 기간(일) 동안 로그 데이터를 보존하려면 **예** 를 선택하고 **일** 필드의 값을 원하는 기간(일)으로 설정합니다.  
  
7.  또는 **모델과 이름이 같은 엔터티 만들기** 를 선택하여 모델과 이름이 같은 엔터티를 만듭니다.  
  
8.  **모델 저장**을 클릭합니다.  
  
 생성되는 각 모델에 대해 열이 8개 포함된 행이 표에 추가됩니다. 이러한 8개 열은 다음과 같습니다.  
  
-   **상태**: 모델 상태입니다. **모델 저장** 단추를 클릭하면 모델을 업데이트하는 중임을 나타내는 ![업데이트 중](../master-data-services/media/mds-model-status-updating.png "업데이트 중") 이미지가 표시됩니다. 모델을 만들거나 편집할 때 오류가 발생하면 ![오류](../master-data-services/media/mds-model-status-error.png "오류") 이미지가 표시됩니다. 오류가 발생하지 않으면 상태가 정상이며 ![확인](../master-data-services/media/mds-model-status-ok.png "확인") 이미지가 표시됩니다.  
  
-   **이름**: 모델 이름입니다.  
  
-   **설명**: 모델 설명입니다.  
  
-   **로그 보존 기간(일)**: 모델에 대 해 로그를 보존할 기간(일)입니다.  
  
-   **만든 사람**: 모델을 만든 사용자의 사용자 이름입니다.  
  
-   **만든 날짜 및 시간**: 모델을 만든 날짜와 시간입니다.  
  
-   **업데이트한 사람**: 모델을 마지막으로 업데이트한 사용자의 사용자 이름입니다.  
  
-   **업데이트한 날짜 및 시간**: 모델을 마지막으로 업데이트한 날짜와 시간입니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [모델&#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)   
 [엔터티&#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)   
 [모델 삭제&#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [모델 편집&#40;Master Data Services&#41;](../master-data-services/edit-model-master-data-services.md)   
 [트랜잭션&#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
  

