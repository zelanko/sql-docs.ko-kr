---
title: 특성 순서 변경
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 835a032c-e37c-4f35-8ab0-5e4ae25c2e9b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a62ad36e17fd25a922615ed4d7b8a49c12a14adf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73728616"
---
# <a name="change-the-order-of-attributes"></a>특성 순서 변경

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 특성의 순서를 변경할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   
  **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
### <a name="to-change-the-order-of-an-attribute"></a>특성 순서를 변경하려면  
  
1.  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  
  **모델 관리** 페이지의 표에서 모델을 선택하고 **엔터티**를 클릭합니다.  
  
3.  
  **엔터티 관리** 페이지에서 해당 특성을 만들려는 엔터티의 행을 선택합니다.  
  
4.  
  **특성**을 클릭합니다.  
  
5.  
  **특성 관리** 페이지에서 다음 작업 중 하나를 수행합니다.  
  
    -   리프 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **리프** 를 선택합니다.  
  
    -   통합 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **통합** 을 선택합니다.  
  
    -   컬렉션용 특성의 경우 **멤버 형식** 목록 상자에서 **컬렉션** 을 선택합니다.  
  
6.  순서를 변경하려는 특성의 행을 선택합니다.  
  
    > [!NOTE]  
    >  이름 또는 코드 특성의 순서는 변경할 수 없습니다.  
  
7.  
  **위로 이동** 또는 **아래로 이동**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [특성 &#40;MDS(Master Data Services)&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
