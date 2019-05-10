---
title: '개요: 데이터 내보내기(Master Data Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e575aeaad1250e2795a75f525954218985cb71ac
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488100"
---
# <a name="overview-exporting-data-master-data-services"></a>개요: 데이터 내보내기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 문서에서는 구독 뷰 형식 유형 및 모델 개체에 대한 변경 내용으로 인해 뷰를 편집해야 하는 경우를 확인하는 방법을 소개합니다.  
  
 구독 뷰를 만들어 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 등의 구독 시스템으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]데이터를 내보냅니다. 구독 시스템을 사용하여 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 데이터를 확인합니다.  구독 뷰를 만드는 방법에 대한 자세한 내용은 [구독 뷰를 만들어 데이터 내보내기&#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
 뷰에 대한 자세한 내용은 [뷰](../relational-databases/views/views.md)를 참조하세요.  
  
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
|마스터 데이터 구독 뷰를 만듭니다.|[구독 뷰를 만들어 데이터 내보내기&#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|기존 구독 뷰를 삭제합니다.|[구독 뷰 삭제&#40;Master Data Services&#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [구독 뷰 형식&#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [뷰](../relational-databases/views/views.md)  
  
  
