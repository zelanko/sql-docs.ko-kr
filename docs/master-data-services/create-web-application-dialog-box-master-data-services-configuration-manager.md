---
description: 웹 애플리케이션 만들기 대화 상자(Master Data Services 구성 마법사)
title: 웹 애플리케이션 만들기 대화 상자
ms.custom: seo-lt-2019
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createapp.f1
ms.assetid: e045b41a-4836-47f6-8e78-2b09494b461f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0f32becd4f98ec714102bbe38f7b15049b730508
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500666"
---
# <a name="create-web-application-dialog-box-master-data-services-configuration-manager"></a>웹 애플리케이션 만들기 대화 상자(Master Data Services 구성 마법사)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  **웹 애플리케이션 만들기** 대화 상자를 사용하여 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션을 만들 수 있습니다. 이 웹 애플리케이션은 **웹 구성** 페이지에서 선택한 사이트에 만들어집니다.  
  
## <a name="web-application"></a>웹 애플리케이션  
 웹 서버는 파일 시스템의 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **WebApplication** 폴더에서 이 웹 애플리케이션의 콘텐츠를 제공합니다. 이 위치는 설치 과정에서 지정되며 기본 경로는 *드라이브*:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication입니다.  
  
|컨트롤 이름|설명|  
|------------------|-----------------|  
|가상 경로|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션을 만들려는 가상 경로를 선택합니다. 가상 경로는 웹 애플리케이션에 액세스하는 데 사용되는 URL의 일부입니다.<br /><br /> 이 목록은 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션을 만들 수 있는 애플리케이션의 가상 경로만 표시하도록 필터링됩니다. 다른 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션 아래에는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션을 만들 수 없습니다.|  
|Alias|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션 이름을 입력하거나 기본 이름을 사용합니다. 이 이름은 웹 브라우저에서 웹 애플리케이션에 액세스하기 위한 URL에 사용됩니다.|  
  
## <a name="application-pool"></a>애플리케이션 풀  
  
|컨트롤 이름|설명|  
|------------------|-----------------|  
|**이름**|새 애플리케이션 풀의 고유 이름을 입력하거나 기본 이름을 사용합니다. [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션은 이 애플리케이션 풀에 추가됩니다.<br /><br /> 애플리케이션 풀은 한 애플리케이션 풀의 애플리케이션이 다른 애플리케이션 풀의 애플리케이션에 영향을 주지 못하도록 하는 경계를 제공합니다.|  
|**사용자 이름**|Active Directory의 도메인 및 사용자 이름을 입력합니다. 이 계정은 웹 애플리케이션이 실행되는 애플리케이션 풀의 ID입니다. 이 계정은 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스를 만들 때 서비스 계정으로 지정된 계정과 동일해야 합니다.<br /><br /> 이 계정은 데이터베이스 액세스를 위해 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 mds_exec 데이터베이스 역할에 추가됩니다. 자세한 내용은 [데이터베이스 로그인, 사용자 및 역할&#40;Master Data Services&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md)을 참조하세요. 또한 이 계정은 파일 시스템의 임시 컴파일 디렉터리인 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] MDSTempDir **에 대한 사용 권한이 부여되는**Windows 그룹인 **MDS_ServiceAccounts**에 추가됩니다. 자세한 내용은 [폴더 및 파일 사용 권한&#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md)을 참조하세요.|  
|**암호**|지정된 사용자 계정의 암호를 입력합니다.|  
|**암호 확인**|지정된 사용자 계정의 암호를 다시 입력합니다. **암호** 필드와 **암호 확인** 필드에는 같은 암호를 입력해야 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [웹 구성 페이지 &#40;Master Data Services 구성 관리자&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Master Data Services 설치 및 구성](../master-data-services/master-data-services-installation-and-configuration.md) [웹 애플리케이션 요구 사항&#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [마스터 데이터 관리자 웹 애플리케이션 만들기&#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
