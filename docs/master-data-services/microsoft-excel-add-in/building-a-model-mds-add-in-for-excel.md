---
title: 모델 작성(Excel용 MDS 추가 기능) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8ae26ec3-c5d5-4c4f-a810-2951a7454439
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a6f3f669f0f1699618399bbfdccaf33f6e4c13a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092488"
---
# <a name="building-a-model-mds-add-in-for-excel"></a>모델 작성(Excel용 MDS 추가 기능)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]에서 관리자는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램에 제공되는 관리 기능 중 일부를 실행할 수 있습니다.  
  
 관리자가 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 에서 수행할 수 있는 모델 작성 태스크는 다음과 같습니다.  
  
-   엔터티 만들기. 엔터티에 대한 자세한 내용은 [엔터티&#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md)를 참조하세요.  
  
-   도메인 기반 특성을 포함한 모든 유형의 특성 만들기. 특성에 대한 자세한 내용은 [특성&#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md) 및 [도메인 기반 특성&#40;Master Data Services&#41;](../../master-data-services/domain-based-attributes-master-data-services.md)를 참조하세요.  
  
 관리자로 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션이나 웹 서비스를 사용하여 모델을 만들어야 합니다. 그런 다음 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 를 사용하여 모델 내에 엔터티와 특성을 만들 수 있습니다. 모델 개체에 대한 자세한 내용은 [모델&#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md)를 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 대부분의 관리 태스크는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서 수행하거나 웹 서비스를 사용하여 수행해야 합니다. 다음 표에서는 관리자가 MDS에서 태스크를 완료하는 데 사용할 수 있는 도구를 보여 줍니다.  
  
|태스크 설명|도구|항목|  
|----------------------|----------|-----------|  
|모델을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 또는 웹 서비스|[모델 만들기&#40;Master Data Services&#41;](../../master-data-services/create-a-model-master-data-services.md)|  
|엔터티를 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램, 웹 서비스 또는 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[엔터티 만들기&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|도메인 기반 특성을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램, 웹 서비스 또는 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[도메인 기반 특성 만들기&#40;Excel용 MDS 추가 기능&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|특성 그룹을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 또는 웹 서비스|[특성 그룹 만들기&#40;Master Data Services&#41;](../../master-data-services/create-an-attribute-group-master-data-services.md)|  
|비즈니스 규칙을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 또는 웹 서비스|[비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|구독 뷰를 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 또는 웹 서비스|[구독 뷰를 만들어 데이터 내보내기&#40;Master Data Services&#41;](../../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|계층을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 또는 웹 서비스|[파생 계층 만들기&#40;Master Data Services&#41;](../../master-data-services/create-a-derived-hierarchy-master-data-services.md)<br /><br /> [명시적 계층 만들기&#40;Master Data Services&#41;](../../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|컬렉션을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 또는 웹 서비스|[컬렉션 만들기&#40;Master Data Services&#41;](../../master-data-services/create-a-collection-master-data-services.md)|  
|데이터의 버전을 만듭니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램 또는 웹 서비스|[버전 잠금&#40;Master Data Services&#41;](../../master-data-services/lock-a-version-master-data-services.md)|  
|모델을 배포합니다.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램, 웹 서비스 또는 MDSModelDeploy 도구|[MDSModelDeploy를 사용하여 모델 배포 패키지 만들기](../../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [모델&#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md)  
  
-   [엔터티&#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md)  
  
-   [특성&#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md)  
  
-   [도메인 기반 특성&#40;Master Data Services&#41;](../../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [특성 그룹&#40;Master Data Services&#41;](../../master-data-services/attribute-groups-master-data-services.md)  
  
-   [비즈니스 규칙&#40;Master Data Services&#41;](../../master-data-services/business-rules-master-data-services.md)  
  
-   [개요: 데이터 내보내기&#40;Master Data Services&#41;](../../master-data-services/overview-exporting-data-master-data-services.md)  
  
-   [계층&#40;Master Data Services&#41;](../../master-data-services/hierarchies-master-data-services.md)  
  
-   [컬렉션&#40;Master Data Services&#41;](../../master-data-services/collections-master-data-services.md)  
  
-   [버전&#40;Master Data Services&#41;](../../master-data-services/versions-master-data-services.md)  
  
-   [보안&#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
-   [모델 배포&#40;Master Data Services&#41;](../../master-data-services/deploying-models-master-data-services.md)  
  
  
