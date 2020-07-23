---
title: Integration Services(SSIS) 서버 및 카탈로그 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 37acf59a44c561e43f6c1dc6dbcb4f26cd06918e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922631"
---
# <a name="integration-services-ssis-server-and-catalog"></a>Integration Services(SSIS) 서버 및 카탈로그

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 패키지를 디자인하고 테스트한 후에는 이 패키지가 포함된 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다.  
  
 개체 탐색기의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 데이터베이스를 호스팅하는 **ssDEnoversion** 인스턴스입니다. 데이터베이스는 패키지, 프로젝트, 매개 변수, 사용 권한, 서버 속성 및 작업 기록과 같은 개체를 저장합니다.  
  
 **SSISDB** 데이터베이스는 쿼리할 수 있는 공용 보기에 개체 정보를 표시합니다. 또한 이 데이터베이스는 개체를 관리하기 위해 호출할 수 있는 저장 프로시저를 제공합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포하려면 먼저 **SSISDB** 카탈로그를 만들어야 합니다.  
  
 SSISDB 카탈로그 기능에 대한 개요는 [SSIS 카탈로그](../../integration-services/catalog/ssis-catalog.md)를 참조하세요.  
  
## <a name="high-availability"></a>고가용성  
 다른 사용자 데이터베이스와 마찬가지로, **SSISDB** 데이터베이스는 데이터베이스 미러링 및 복제를 지원합니다. 미러링 및 복제에 대한 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
 또한 SSIS 및 Always On 가용성 그룹을 사용하여 SSISDB의 고가용성 및 해당 콘텐츠를 제공할 수도 있습니다. 자세한 내용은 [SSIS 카탈로그에 대한 Always On(SSISDB)](ssis-catalog.md#always-on-for-ssis-catalog-ssisdb)을 참조하세요. blogs.msdn.com에서 Matt Masson이 게시한 [Always On을 사용하는 SSIS](https://go.microsoft.com/fwlink/?LinkId=255873) 블로그도 참조하세요.  
  
##  <a name="integration-services-server-in-sql-server-management-studio"></a><a name="ssms"></a> SQL Server Management Studio의 Integration Services 서버  
 **SSISDB** 데이터베이스를 호스트하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결할 때 개체 탐색기에 다음 개체가 표시됩니다.  
  
-   **SSISDB 데이터베이스**  
  
     개체 탐색기의 **데이터베이스** 노드 아래에 **SSISDB** 데이터베이스가 표시됩니다. 뷰를 쿼리하고 저장 프로시저를 호출하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버와 이 서버에 저장된 개체를 관리할 수 있습니다.  
  
-   **Integration Services 카탈로그**  
  
     **Integration Services 카탈로그** 노드 아래에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 및 환경을 위한 폴더가 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [Integration Services 서버의 패키지 목록 보기](../../integration-services/catalog/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Integration Services(SSIS) 프로젝트 및 패키지 배포](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
-   [Integration Services(SSIS) 패키지 실행](../../integration-services/packages/run-integration-services-ssis-packages.md)  
  
## <a name="related-content"></a>관련 내용  
 blogs.msdn.com의 블로그 항목, [Always On을 사용하는 SSIS](https://go.microsoft.com/fwlink/?LinkId=255873)  
  
  
