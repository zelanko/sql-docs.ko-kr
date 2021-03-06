---
title: 마스터 데이터 관리자 웹 응용 프로그램 만들기
description: 마스터 데이터 관리자 웹 응용 프로그램은 사용자가 마스터 데이터를 사용 하 고 관리자가 MDS를 구성 하 고 관리 하는 데 사용할 수 있는 인터페이스를 제공 합니다.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 241d46d7-8008-47f6-bebd-0dfff1cc856a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1f7504244f658af94cccb42bead95de60b2c409e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882112"
---
# <a name="create-a-master-data-manager-web-application-master-data-services"></a>마스터 데이터 관리자 웹 응용 프로그램 만들기 (MDS(Master Data Services))

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션은 마스터 데이터 작업을 하는 사용자 및 MDS를 구성하고 관리하는 관리자를 위한 인터페이스를 제공합니다.  
  
 웹 애플리케이션은 항상 웹 사이트에 포함되어야 합니다. 웹 애플리케이션을 만들려면 다음 중 하나를 수행해야 합니다.  
  
-   기본 웹 사이트를 사용하고 웹 애플리케이션을 만듭니다.  
  
-   기존 웹 사이트를 사용하고 웹 애플리케이션을 만듭니다. 또는  
  
-   웹 애플리케이션을 자동으로 만드는 새 웹 사이트를 만듭니다.  
  
 웹 애플리케이션을 만든 후 이를 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스에 연결합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
-   웹 애플리케이션을 호스트하는 컴퓨터의 요구 사항에 대한 자세한 내용은 [웹 애플리케이션 요구 사항&#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)을 참조하세요.  
  
## <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>새 웹 사이트에서 마스터 데이터 관리자 웹 애플리케이션을 만들려면  
 새 웹 사이트를 만들면 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션이 루트 웹 애플리케이션입니다. 또한 웹 애플리케이션이 새 애플리케이션 풀에 추가됩니다.  
  
> [!NOTE]  
>  이 절차를 따르는 경우 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션의 가상 경로 및 별칭을 지정할 수 없습니다. [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]에 대한 가상 경로 및 별칭을 지정하려면 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션으로 이미 구성되지 않은 기존 웹 사이트에서 웹 애플리케이션을 만들어야 합니다.  
  
 또한 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 에서는 HTTP 바인딩만 사용하여 사이트를 만드는 것이 지원됩니다. HTTPS 바인딩을 추가하려면 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 에서 새 사이트 및 애플리케이션을 만듭니다. 자세한 내용은 [마스터 데이터 관리자 웹 애플리케이션의 보안 설정](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md) 을 참조하세요.  
  
#### <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>새 웹 사이트에서 마스터 데이터 관리자 웹 애플리케이션을 만들려면  
  
1.  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]를 엽니다.  
  
2.  왼쪽 창에서 **웹 구성**을 클릭합니다.  
  
3.  **웹 구성** 페이지의 웹 사이트 목록에서 **새 웹 사이트 만들기**를 선택합니다.  
  
4.  **웹 사이트 만들기** 대화 상자에서 새 웹 사이트에 대한 정보를 지정합니다. 대화 상자의 UI(사용자 인터페이스) 옵션에 대한 자세한 내용은 [웹 사이트 만들기 대화 상자&#40;Master Data Services 구성 관리자&#41;](../../master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md)를 참조하세요.  
  
5.  **확인**을 클릭합니다.  
  
## <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>기존 웹 사이트에서 마스터 데이터 관리자 웹 애플리케이션을 만들려면  
 기존 웹 사이트에서 웹 애플리케이션을 만드는 경우 웹 애플리케이션의 가상 경로 및 별칭을 선택할 수 있습니다. 이 웹 애플리케이션은 새 애플리케이션 풀에 추가됩니다.  
  
#### <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>기존 웹 사이트에서 마스터 데이터 관리자 웹 애플리케이션을 만들려면  
  
1.  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]를 엽니다.  
  
2.  왼쪽 창에서 **웹 구성**을 클릭합니다.  
  
3.  **웹 구성** 페이지의 **웹 사이트** 목록에서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션을 만들려는 웹 사이트를 선택합니다.  
  
4.  **애플리케이션 만들기**를 클릭합니다.  
  
5.  **웹 애플리케이션 만들기** 대화 상자에서 새 웹 애플리케이션에 대한 정보를 지정합니다. 대화 상자의 UI(사용자 인터페이스) 옵션에 대한 자세한 내용은 [웹 애플리케이션 만들기 대화 상자&#40;Master Data Services 구성 관리자&#41;](../../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md)를 참조하세요.  
  
6.  **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   웹 애플리케이션을 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스와 연결합니다. 자세한 내용은 [Master Data Services 데이터베이스와 웹 애플리케이션 연결](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md)을 참조하세요.  
  
-   또는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] TLS (Transport Layer Security) SSL(Secure Sockets Layer)를 사용 하 여 콘텐츠를 암호화 하려는 경우 HTTPS 바인딩을 사용 하도록 웹 응용 프로그램을 호스트 하는 웹 사이트를 구성할 수 있습니다 (SSL (Transport Layer Security)). IIS 관리자와 같은 인터넷 정보 서비스 (IIS) 도구를 사용 하 여 웹 서버에 대 한 서버 인증서를 구성 하 고 사이트에 대 한 HTTPS 바인딩과 TLS 설정을 구성 해야 합니다. 자세한 내용은 [Secure a Master Data Manager Web Application](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services) 설치](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
