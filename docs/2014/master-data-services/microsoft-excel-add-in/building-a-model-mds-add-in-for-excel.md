---
title: 모델 작성(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8ae26ec3-c5d5-4c4f-a810-2951a7454439
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ee3473ba16ad3a03a95065aea94888654db53187
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479341"
---
# <a name="building-a-model-mds-add-in-for-excel"></a>모델 작성(Excel용 MDS 추가 기능)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 관리자는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션에 제공되는 관리 기능 중 일부를 실행할 수 있습니다.  
  
 관리자가 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 에서 수행할 수 있는 모델 작성 태스크는 다음과 같습니다.  
  
-   엔터티 만들기. 엔터티에 대한 자세한 내용은 [엔터티&#40;Master Data Services&#41;](../entities-master-data-services.md)를 참조하세요.  
  
-   도메인 기반 특성을 포함한 모든 유형의 특성 만들기. 특성에 대한 자세한 내용은 [특성&#40;Master Data Services&#41;](../attributes-master-data-services.md) 및 [도메인 기반 특성&#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)를 참조하세요.  
  
 관리자로 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션이나 웹 서비스를 사용하여 모델을 만들어야 합니다. 그런 다음 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 를 사용하여 모델 내에 엔터티와 특성을 만들 수 있습니다. 모델 개체에 대한 자세한 내용은 [모델&#40;Master Data Services&#41;](../models-master-data-services.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 대부분의 관리 태스크는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서 수행하거나 웹 서비스를 사용하여 수행해야 합니다. 다음 표에서는 관리자가 MDS에서 태스크를 완료하는 데 사용할 수 있는 도구를 보여 줍니다.  
  
|태스크 설명|도구|항목|  
|----------------------|----------|-----------|  
|모델을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션 또는 웹 서비스|[모델 만들기&#40;Master Data Services&#41;](../create-a-model-master-data-services.md)|  
|엔터티를 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션, 웹 서비스 또는 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[엔터티 만들기&#40;Excel용 MDS 추가 기능&#41;](create-an-entity-mds-add-in-for-excel.md)|  
|도메인 기반 특성을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션, 웹 서비스 또는 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[도메인 기반 특성 만들기&#40;Excel용 MDS 추가 기능&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|특성 그룹을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션 또는 웹 서비스|[특성 그룹 만들기&#40;Master Data Services&#41;](../create-an-attribute-group-master-data-services.md)|  
|비즈니스 규칙을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션 또는 웹 서비스|[비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../create-and-publish-a-business-rule-master-data-services.md)|  
|구독 뷰를 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션 또는 웹 서비스|[MDS(Master Data Services) &#40;구독 뷰를 만듭니다&#41;](../create-a-subscription-view-to-export-data-master-data-services.md)|  
|계층을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션 또는 웹 서비스|[파생 계층 만들기&#40;Master Data Services&#41;](../create-a-derived-hierarchy-master-data-services.md)<br /><br /> [명시적 계층 만들기&#40;Master Data Services&#41;](../create-an-explicit-hierarchy-master-data-services.md)|  
|컬렉션을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션 또는 웹 서비스|[컬렉션 만들기&#40;Master Data Services&#41;](../create-a-collection-master-data-services.md)|  
|데이터의 버전을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션 또는 웹 서비스|[버전 잠금&#40;Master Data Services&#41;](../lock-a-version-master-data-services.md)|  
|모델을 배포합니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션, 웹 서비스 또는 MDSModelDeploy 도구|[MDSModelDeploy를 사용하여 모델 배포 패키지 만들기](../create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [모델&#40;Master Data Services&#41;](../models-master-data-services.md)  
  
-   [엔터티&#40;Master Data Services&#41;](../entities-master-data-services.md)  
  
-   [특성&#40;Master Data Services&#41;](../attributes-master-data-services.md)  
  
-   [도메인 기반 특성&#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)  
  
-   [특성 그룹&#40;Master Data Services&#41;](../attribute-groups-master-data-services.md)  
  
-   [비즈니스 규칙&#40;Master Data Services&#41;](../business-rules-master-data-services.md)  
  
-   [데이터 &#40;MDS(Master Data Services)&#41;내보내기](../overview-exporting-data-master-data-services.md)  
  
-   [계층&#40;Master Data Services&#41;](../hierarchies-master-data-services.md)  
  
-   [컬렉션&#40;Master Data Services&#41;](../collections-master-data-services.md)  
  
-   [버전&#40;Master Data Services&#41;](../versions-master-data-services.md)  
  
-   [보안&#40;Master Data Services&#41;](../security-master-data-services.md)  
  
-   [모델 배포&#40;Master Data Services&#41;](../deploying-models-master-data-services.md)  
  
  
