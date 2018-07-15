---
title: Integration Services (SSIS) 서버 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ea60bbdac3df4cd1130ba4afee83f882f138d33d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289399"
---
# <a name="integration-services-ssis-server"></a>Integration Services(SSIS) 서버
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 패키지를 디자인하고 테스트한 후에는 이 패키지가 포함된 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버는 `SSISDB` 데이터베이스를 호스팅하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스입니다. 데이터베이스는 패키지, 프로젝트, 매개 변수, 사용 권한, 서버 속성 및 작업 기록과 같은 개체를 저장합니다.  
  
 `SSISDB` 데이터베이스는 쿼리할 수 있는 공용 보기에 개체 정보를 표시합니다. 또한 이 데이터베이스는 개체를 관리하기 위해 호출할 수 있는 저장 프로시저를 제공합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포하려면 먼저 `SSISDB` 카탈로그를 만들어야 합니다.  
  
 SSISDB 카탈로그 기능에 대한 개요는 [SSIS 카탈로그](ssis-catalog.md)를 참조하세요.  
  
## <a name="high-availability"></a>고가용성  
 다른 사용자 데이터베이스와 같이 `SSISDB` database 데이터베이스 미러링 및 복제 지원지 않습니다. 미러링 및 복제에 대한 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
 또한 SSIS 및 AlwaysOn 가용성 그룹을 사용하여 SSISDB의 고가용성 및 해당 콘텐츠를 제공할 수도 있습니다. 자세한 내용은 blogs.msdn.com에서 Matt Masson이 게시한 [AlwaysOn을 사용하는 SSIS](http://go.microsoft.com/fwlink/?LinkId=255873)블로그를 참조하십시오.  
  
##  <a name="ssms"></a> SQL Server Management Studio의 Integration Services 서버  
 `SSISDB` 데이터베이스를 호스팅하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결하면 개체 탐색기에 다음 개체가 표시됩니다.  
  
-   **SSISDB 데이터베이스**  
  
     `SSISDB` 데이터베이스 아래에 표시 합니다 **데이터베이스** 개체 탐색기의 노드. 뷰를 쿼리하고 저장 프로시저를 호출하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버와 이 서버에 저장된 개체를 관리할 수 있습니다.  
  
-   **Integration Services 카탈로그**  
  
     **Integration Services 카탈로그** 노드 아래에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 및 환경을 위한 폴더가 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [SSIS 카탈로그 만들기](../create-the-ssis-catalog.md)  
  
-   [Integration Services 서버의 패키지 목록 보기](view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Integration Services 서버에 프로젝트 배포](../deploy-projects-to-integration-services-server.md)  
  
-   [SQL Server Management Studio를 사용하여 SSIS 서버에서 패키지 실행](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="related-content"></a>관련 내용  
 blogs.msdn.com의 블로그 항목, [AlwaysOn을 사용하는 SSIS](http://go.microsoft.com/fwlink/?LinkId=255873)  
  
  
