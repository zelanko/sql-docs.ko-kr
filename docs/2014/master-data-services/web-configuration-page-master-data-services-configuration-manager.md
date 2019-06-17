---
title: 웹 구성 페이지(Master Data Services 구성 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 12ba4a2d03e98d5f2dac79917e23a93c0a24cdb0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481216"
---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>웹 구성 페이지(Master Data Services 구성 마법사)
  **웹 구성** 페이지를 사용하여 새 웹 사이트를 만들거나 새 웹 사이트 또는 웹 응용 프로그램을 만들 수 있습니다. [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램을 선택한 후 해당 응용 프로그램의 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스를 지정하고 Data Quality Services를 사용하도록 설정할 수 있습니다.  
  
## <a name="configure-the-web-application"></a>웹 애플리케이션 구성  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|**웹 사이트**|새 웹 사이트를 만들거나, 기본 웹 사이트를 선택하거나, 다른 사용 가능한 사이트(목록에 있는 경우)를 선택합니다. 이 목록에는 로컬 컴퓨터의 인터넷 정보 서비스(IIS)에 정의된 웹 사이트가 표시됩니다. 새 웹 사이트를 만들면 새 웹 애플리케이션이 자동으로 만들어집니다. 기본 또는 다른 기존 사이트를 선택하면 애플리케이션을 수동으로 만들어야 합니다.|  
|**웹 응용 프로그램**|구성할 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션을 선택합니다. 이 상자에는 선택한 웹 사이트의 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션만 표시됩니다.<br /><br /> 아무 항목도 표시되지 않으면 **애플리케이션 만들기** 를 클릭하여 웹 사이트를 만듭니다.|  
|**응용 프로그램 만들기**|**웹 응용 프로그램 만들기** 대화 상자를 열어 선택한 사이트에서 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 응용 프로그램을 만듭니다. 이 단추는 선택한 사이트에 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션으로 구성된 루트 웹 애플리케이션이 없는 경우에만 활성화됩니다.|  
  
## <a name="associate-application-with-database"></a>애플리케이션을 데이터베이스에 연결  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|**Select**|**서버에 연결** 대화 상자를 열어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하고 선택한 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 응용 프로그램과 연결할 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 데이터베이스를 선택합니다.|  
|**SQL Server 인스턴스**|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스를 호스팅하는 선택한 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 인스턴스의 이름을 표시합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하고 데이터베이스를 선택할 때까지 비어 있습니다.|  
|**데이터베이스 백업**|선택한 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 웹 애플리케이션과 연결된 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 데이터베이스의 이름을 표시합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하고 데이터베이스를 선택할 때까지 비어 있습니다.|  
  
## <a name="enable-dqs-integration"></a>DQS 통합 사용  
  
|컨트롤 이름|Description|  
|------------------|-----------------|  
|**Data Quality Services와의 통합 사용**|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]에서 데이터 품질 기능을 사용하도록 설정하려면 이 옵션을 선택합니다. 자세한 내용은 [MDS(Master Data Services)와 Data Quality Services의 통합 설정](install-windows/enable-data-quality-services-integration-with-master-data-services.md)을 참조하세요.|  
  
## <a name="see-also"></a>관련 항목  
 [Master Data Services에 대 한 데이터베이스 및 웹 사이트 설정](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [웹 응용 프로그램 요구 사항 &#40;Master Data Services&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [마스터 데이터 관리자 웹 애플리케이션 만들기&#40;Master Data Services&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)   
 [MDS 2014 및 "서비스를 사용할 수 없음" 오류](https://blogs.msdn.com/b/womeninanalytics/archive/2015/08/19/mds-2014-and-service-unavailable-error.aspx)  
  
  
