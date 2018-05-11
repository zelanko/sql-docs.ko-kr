---
title: 비즈니스 규칙에 대해 특정 멤버 유효성 검사(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 37bf689ff457cda1717609b293661a7f4344dbc9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>비즈니스 규칙에 대해 특정 멤버 유효성 검사(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 비즈니스 규칙에 따라 멤버의 하위 집합을 업데이트하거나 유효성을 검사하려는 경우 비즈니스 규칙을 선택적으로 적용합니다.  
  
> [!NOTE]  
>  모델 버전의 모든 멤버에 비즈니스 규칙을 적용하려면 [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)를 참조하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **탐색기** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   비즈니스 규칙을 적용할 모델 개체에 대한 **업데이트** 이상의 권한이 있어야 합니다.  
  
### <a name="to-apply-business-rules-selectively"></a>비즈니스 규칙을 선택적으로 적용하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 홈페이지의 **모델** 드롭다운 목록에서 모델을 선택합니다.  
  
2.  **버전** 드롭다운 목록에서 버전을 선택합니다.  
  
3.  **탐색기** 탭을 클릭합니다.  
  
4.  메뉴 모음에서 **엔터티** 를 가리키고 규칙을 적용할 멤버를 포함하는 엔터티의 이름을 클릭합니다.  
  
5.  **규칙 적용**을 클릭합니다. 비즈니스 규칙은 표에 표시된 멤버에만 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [비즈니스 규칙에 대해 버전 유효성 검사&#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
