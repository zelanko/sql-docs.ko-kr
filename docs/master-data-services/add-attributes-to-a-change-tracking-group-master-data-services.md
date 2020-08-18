---
description: 변경 내용 추적 그룹에 특성 추가(Master Data Services)
title: 변경 내용 추적 그룹에 특성 추가
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 154dc5a555e97d4de56f3a40981aad71e64fe22c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491503"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>변경 내용 추적 그룹에 특성 추가(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 특성 값의 변경 내용을 추적하려는 경우 변경 내용 추적 그룹에 특성을 추가합니다.  
  
> [!NOTE]  
>  변경 내용 추적 그룹에 특성을 추가한 후에는 특성이 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 변경될 때 특성에 플래그가 지정됩니다. 변경 내용에 따라 동작을 수행할 비즈니스 규칙을 만듭니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](../master-data-services/administrators-master-data-services.md)를 참조 하세요.  
  
-   변경 내용 추적 그룹에 추가할 특성이 있어야 합니다. 자세한 내용은 [텍스트 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)를 참조하세요.  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>변경 내용 추적 그룹에 특성을 추가하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택 하 고 **엔터티**를 클릭 합니다.  
  
3.  **엔터티 관리** 페이지에서 해당 특성을 만들려는 엔터티의 행을 선택합니다.  
  
4.  **특성**을 클릭합니다.  
  
5.  **특성 관리** 페이지에서 다음 작업 중 하나를 수행합니다.  
  
    -   리프 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **리프** 를 선택합니다.  
  
    -   통합 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **통합** 을 선택합니다.  
  
    -   컬렉션용 특성의 경우 **멤버 형식** 목록 상자에서 **컬렉션** 을 선택합니다.  
  
6.  편집할 특성 행을 선택하고 **편집**을 클릭합니다.  
  
7.  **변경 내용 추적 설정** 확인란을 선택합니다.  
  
8.  **변경 내용 추적 그룹** 상자에 그룹의 번호를 입력합니다.  
  
9. **특성 저장**을 클릭합니다.  
  
     편집된 특성의 경우 표에 있는 **변경 내용 추적 그룹 설정** 열이 **예(그룹: 입력된 그룹 번호)** 로 변경됩니다.  
  
10. 그룹에 포함할 모든 특성에 대해 이 절차를 반복합니다. 그룹의 각 특성에 대해 동일한 변경 내용 추적 그룹 번호를 사용합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [특성 값 변경 기반 동작 시작&#40;Master Data Services&#41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [텍스트 특성 &#40;MDS(Master Data Services)를 만듭니다&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [도메인 기반 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
