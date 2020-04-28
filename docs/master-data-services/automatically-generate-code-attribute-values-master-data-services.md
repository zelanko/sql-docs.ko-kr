---
title: 코드 특성 값 자동 생성
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 85cfc3d3859712cdb53b7db58bb1729baca692b3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73729729"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>코드 특성 값 자동 생성(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 새 멤버를 만들 때마다 코드 값에 정수가 자동 할당되도록 하려면 엔터티의 코드 특성에 대해 값을 자동으로 생성합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](../master-data-services/administrators-master-data-services.md)를 참조 하세요.  
  
-   엔터티가 있어야 합니다. 자세한 내용은 [&#41;MDS(Master Data Services) 엔터티 &#40;만들기 ](../master-data-services/create-an-entity-master-data-services.md)를 참조 하세요.  
  
### <a name="to-automatically-generate-code-values"></a>코드 값을 자동으로 생성하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지에서 편집할 엔터티를 포함하는 모델에 대한 행을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지에서 코드를 생성할 엔터티에 해당하는 행을 선택하고 **편집**을 클릭합니다.  
  
4.  **코드 값 자동으로 만들기** 확인란을 선택합니다.  
  
5.  **시작 값** 상자에 증가를 시작할 숫자를 입력합니다. 멤버가 이미 있는 경우 가장 높은 기존 값을 기반으로 코드가 설정됩니다. 예를 들어 가장 높은 기존 코드 값이 299인 경우 다음 멤버의 코드 값은 300으로 설정됩니다.  
  
6.  **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services)&#41;&#40;자동 코드 만들기](../master-data-services/automatic-code-creation-master-data-services.md)   
 [코드 외의 특성 값 자동 생성&#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
