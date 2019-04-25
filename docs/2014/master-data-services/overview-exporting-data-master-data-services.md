---
title: 데이터 내보내기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 76a9133a013087d96f9acc102232b2340212d19f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62763826"
---
# <a name="exporting-data-master-data-services"></a>데이터 내보내기(Master Data Services)
  구독 뷰를 만들어 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터를 구독 시스템으로 내보낼 수 있습니다. 그러면 임의의 구독 시스템에서 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 게시된 데이터를 볼 수 있습니다. 뷰에 대한 자세한 내용은 [뷰](../relational-databases/views/views.md)를 참조하세요.  
  
## <a name="subscription-view-formats"></a>구독 뷰 형식  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 뷰를 만들 때 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에서 제공하는 표준 뷰 형식 집합 중에서 선택합니다. 이러한 형식을 사용하여 다음을 표시하는 뷰를 만들 수 있습니다.  
  
-   모든 리프 멤버와 해당 특성  
  
-   모든 통합 멤버와 해당 특성  
  
-   모든 컬렉션과 해당 특성  
  
-   명시적으로 컬렉션에 추가된 멤버  
  
-   부모-자식 또는 수준 형식인 파생 계층의 멤버  
  
-   부모-자식 또는 수준 형식인 엔터티에 대한 모든 명시적 계층의 멤버  
  
## <a name="subscription-views-can-become-out-of-date"></a>구독 뷰가 최신 내용을 반영하지 못할 수 있음  
 엔터티 또는 계층에 대한 구독 뷰를 만든 후 연결된 모델 개체의 변경 사항이 뷰에 자동으로 반영되지 않습니다. 또한 모델 개체에 대한 변경 사항을 반영하기 위해 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 에서 구독 뷰를 다시 생성해야 할 수 있습니다. 모델 개체가 변경될 경우 **내보내기** 페이지의 **변경됨** 열이 **True** 로 업데이트됩니다. **True** 는 구독 뷰를 편집하고 저장하여 뷰를 다시 생성해야 한다는 것을 나타냅니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|마스터 데이터 구독 뷰를 만듭니다.|[구독 뷰를 만들어 &#40;Master Data Services&#41;](create-a-subscription-view-to-export-data-master-data-services.md)|  
|기존 구독 뷰를 삭제합니다.|[구독 뷰 삭제&#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [구독 뷰 형식&#40;Master Data Services&#41;](../../2014/master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [뷰](../relational-databases/views/views.md)  
  
  
