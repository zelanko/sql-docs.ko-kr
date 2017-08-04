---
title: "파생된 계층 (Master Data Services) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- derived hierarchies, creating
- creating derived hierarchies [Master Data Services]
ms.assetid: fec653c4-11cc-46a2-8dd8-b605341ebb40
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 65676239fa42e9e9f067dbd1973c005bd4198180
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-derived-hierarchy-master-data-services"></a>파생 계층 만들기(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 멤버가 올바른 수준으로 유지되는 수준 기반 계층을 원하는 경우 파생 계층을 만듭니다. 파생 계층은 모델에 있는 도메인 기반 특성 관계를 기반으로 합니다.  
  
> [!NOTE]  
>  멤버에 대한 도메인 기반 특성 값이 없으면 멤버가 파생 계층에 포함되지 않습니다. 모든 멤버에 대한 도메인 기반 특성 값을 요구하려면 [특성 값 요구&#40;Master Data Services&#41;](../master-data-services/require-attribute-values-master-data-services.md)를 참조하세요.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-create-a-derived-hierarchy"></a>파생 계층을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **파생 계층**을 클릭합니다.  
  
3.  **파생 계층 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  **추가**를 클릭합니다.  
  
5.  **파생 계층 추가** 페이지의 **파생 계층 이름** 상자에 계층의 이름을 입력합니다.  
  
    > [!TIP]  
    >  **하위 범주로 범주화할 제품**과 같이 계층의 수준을 설명하는 이름을 사용합니다.  
  
6.  **파생 계층 저장**을 클릭합니다.  
  
7.  **파생 계층 편집** 페이지의 **사용 가능한 엔터티 및 계층** 창에서 엔터티나 계층을 클릭하여 **현재 수준** 창의 **여기에 부모 놓기** 로 끌어 놓습니다.  
  
8.  계층이 완성될 때까지 엔터티나 계층을 계속 끌어 놓습니다.  
  
9. **뒤로**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [파생된 계층 &#40; Master Data services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)   
 [명시적 캡이 포함 &#40; 포함 된 파생된 계층 Master Data services&#41;](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [도메인 기반 특성 &#40; Master Data services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)  
  
  
