---
title: 명시적 계층 삭제(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- explicit hierarchies, deleting
- deleting explicit hierarchies [Master Data Services]
ms.assetid: 4ce177b0-9884-47a2-9cea-212e845dd762
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 27f2da08eb5b1f9f7027d3e9747c7de8cab0ec1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478207"
---
# <a name="delete-an-explicit-hierarchy-master-data-services"></a>명시적 계층 삭제(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 명시적 계층이 더 이상 필요하지 않으면 삭제할 수 있습니다.  
  
> [!WARNING]  
>  명시적 계층을 삭제하면 해당 계층의 모든 통합 멤버도 삭제됩니다. 엔터티에 대한 모든 명시적 계층을 삭제하면 해당 엔터티의 모든 컬렉션도 삭제되며 명시적 계층과 컬렉션에 대해 엔터티를 더 이상 사용할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-delete-an-explicit-hierarchy"></a>명시적 계층을 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지의 표에서 삭제할 명시적 계층을 포함하는 엔터티에 대한 행을 선택합니다.  
  
4.  **명시적 계층**을 클릭합니다.  
  
5.  **명시적 계층 관리** 페이지에서 삭제하려는 명시적 계층을 클릭합니다.  
  
6.  **편집**을 클릭합니다.  
  
7.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [명시적 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
