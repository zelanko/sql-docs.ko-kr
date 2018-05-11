---
title: Master Data Services 데이터베이스와 웹 응용 프로그램 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ccb25672-f71d-4135-b548-f50eb45d8fa5
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c7604c76f50a9f9a05a91c877398b6f47e300629
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="associate-a-master-data-services-database-and-web-application"></a>Master Data Services 데이터베이스와 웹 응용 프로그램 연결

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램을 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스와 연결하여 웹 작업에 사용할 데이터베이스를 지정할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
-   [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 가 로컬 컴퓨터에 설치되어야 합니다. 자세한 내용은 [Master Data Services 설치](../../master-data-services/install-windows/install-master-data-services.md)를 참조하세요.  
  
-   로컬 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램이 있어야 합니다. 자세한 내용은 [마스터 데이터 관리자 웹 응용 프로그램 만들기&#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)를 참조하세요.  
  
-   로컬 또는 원격 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스가 있어야 합니다. 자세한 내용은 [Master Data Services 데이터베이스 만들기](../../master-data-services/install-windows/create-a-master-data-services-database.md)를 참조하세요.  
  
### <a name="to-associate-a-master-data-services-database-and-web-application"></a>Master Data Services 데이터베이스 및 웹 응용 프로그램을 연결하려면  
  
1.  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]를 엽니다.  
  
2.  왼쪽 창에서 **웹 구성**을 클릭합니다.  
  
3.  **웹 구성** 페이지의 **웹 응용 프로그램**아래에 있는 **웹 사이트** 목록에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램이 포함된 웹 사이트를 선택합니다.  
  
4.  **웹 응용 프로그램** 상자에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]를 호스팅하는 웹 응용 프로그램을 선택합니다.  
  
5.  **응용 프로그램을 데이터베이스에 연결**에서 **선택**을 클릭합니다. **데이터베이스에 연결** 대화 상자가 열립니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 호스팅하는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 의 인스턴스에 대한 연결 정보를 지정하고 **연결**을 클릭합니다.  
  
7.  **Master Data Services 데이터베이스** 목록에서 웹 응용 프로그램을 연결할 데이터베이스를 선택한 다음 **확인**을 클릭합니다.  
  
8.  **응용 프로그램을 데이터베이스에 연결**에서 인스턴스 및 데이터베이스 정보가 올바른지 확인한 다음 **적용**을 클릭합니다.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 웹 서비스에 대한 프로그래밍 방식의 액세스는 웹 응용 프로그램을 만들 때 자동으로 설정됩니다. 개발자가 서비스 메타데이터에 액세스하여 프로그래밍 방식의 액세스를 위한 프록시 클래스를 쉽게 생성할 수 있도록 하려면 메타데이터 게시를 사용하도록 설정합니다. 자세한 내용은 [Create Master Data Manager Web Service Proxy Classes](../../master-data-services/develop/create-master-data-manager-web-service-proxy-classes.md)를 참조하세요.  
  
-   [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]에 사용자 및 그룹을 추가합니다. [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]에 대한 액세스 권한이 사용자나 그룹에 부여되지 않은 경우 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 시스템 관리자 자격 증명을 사용하여 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 를 열어야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md) 및 [사용자 및 그룹&#40;Master Data Services&#41;](../../master-data-services/users-and-groups-master-data-services.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Master Data Services 설치](../../master-data-services/install-windows/install-master-data-services.md)   
 [웹 구성 페이지&#40;Master Data Services 구성 마법사&#41;](../../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
  
