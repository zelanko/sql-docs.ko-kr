---
title: MDS(Master Data Services) |에 대 한 데이터베이스 및 웹 사이트 설정 Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 478dea9095fe22a437aecf138c22374b5a70885b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054100"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>Master Data Services에 대한 데이터베이스 및 웹 사이트 설정
  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 를 사용하여 MDS( [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] )에 대한 데이터베이스 및 웹 사이트 설정  
  
 데이터베이스 및 웹 사이트를 설정하려면 다음 작업을 완료하세요.  
  
1.  에서 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] **데이터베이스 구성** 페이지를 사용 하 여 데이터베이스를 만듭니다.  
  
     자세한 내용은 [데이터베이스 구성 페이지 &#40;Master Data Services 구성 관리자&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md) 및 [데이터베이스 만들기 마법사 &#40;Master Data Services 구성 관리자&#41;](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md)을 참조 하세요.  
  
2.  새 웹 사이트를 만들거나, 기본 웹 사이트를 선택 하거나,의 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] **웹 구성** 페이지를 사용 하 여 다른 기존 웹 사이트를 선택 합니다. 그런 다음 선택했거나 만든 웹 애플리케이션과 MDS 데이터베이스를 연결합니다.  
  
     자세한 내용은 [웹 구성 페이지 &#40;Master Data Services 구성 관리자&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) 및 웹 [사이트 만들기 대화 상자 &#40;Master Data Services 구성 관리자&#41;](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md)을 참조 하세요.  
  
3.  필드 에서 **웹 구성** 페이지를 사용 하 여 Data Quality Services와 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]의 통합을 사용 하도록 설정 합니다.  
  
     자세한 내용은 [웹 구성 페이지 &#40;Master Data Services 구성 관리자&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) 및 [MDS(Master Data Services)와 Data Quality Services 통합 사용](install-windows/enable-data-quality-services-integration-with-master-data-services.md)을 참조 하세요.  
  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 를 사용하여 MDS 데이터베이스와 연결된 웹 애플리케이션 및 서비스에 대한 설정을 지정할 수도 있습니다. 예를 들어 데이터를 로드하는 빈도나 유효성 검사 메일을 전송하는 빈도를 지정할 수 있습니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services) 데이터베이스](../../2014/master-data-services/master-data-services-database.md)   
 [마스터 데이터 관리자 웹 애플리케이션](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  
