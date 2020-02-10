---
title: 명시적 계층 삭제(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 048d0c4bc88f28274dc7efd686ad075242e926ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483090"
---
# <a name="delete-an-explicit-hierarchy-master-data-services"></a>명시적 계층 삭제(Master Data Services)
  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 명시적 계층이 더 이상 필요하지 않으면 삭제할 수 있습니다.  
  
> [!WARNING]  
>  명시적 계층을 삭제하면 해당 계층의 모든 통합 멤버도 삭제됩니다. 엔터티에 대한 모든 명시적 계층을 삭제하면 해당 엔터티의 모든 컬렉션도 삭제되며 명시적 계층과 컬렉션에 대해 엔터티를 더 이상 사용할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   
  **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
### <a name="to-delete-an-explicit-hierarchy"></a>명시적 계층을 삭제하려면  
  
1.  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  
  **모델 뷰** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **엔터티**를 클릭합니다.  
  
3.  
  **엔터티 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  삭제할 명시적 계층이 포함된 엔터티의 행을 선택합니다.  
  
5.  
  **선택한 엔터티 편집**을 클릭합니다.  
  
6.  **엔터티 편집** 페이지의 **명시적 계층** 창에서 삭제 하려는 명시적 계층을 클릭 합니다.  
  
7.  **선택한 계층 삭제**를 클릭 합니다.  
  
8.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
9. 추가 확인 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [명시적 계층 &#40;MDS(Master Data Services)를 만듭니다&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [명시적 계층 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
