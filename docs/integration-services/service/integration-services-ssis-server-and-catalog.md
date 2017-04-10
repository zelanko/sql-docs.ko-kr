---
title: "Integration Services (SSIS) 서버 및 카탈로그 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "패키지 [Integration Services], 관리"
  - "패키지 관리 [Integration Services]"
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Integration Services (SSIS) 서버 및 카탈로그
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 패키지를 디자인하고 테스트한 후에는 이 패키지가 포함된 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다.  
  
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버는의 인스턴스는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 호스트 하는 **SSISDB** 데이터베이스입니다. 데이터베이스는 패키지, 프로젝트, 매개 변수, 사용 권한, 서버 속성 및 작업 기록과 같은 개체를 저장합니다.  
  
 **SSISDB** 데이터베이스는 쿼리할 수 있는 공용 보기에 개체 정보를 표시합니다. 또한 이 데이터베이스는 개체를 관리하기 위해 호출할 수 있는 저장 프로시저를 제공합니다.  
  
 프로젝트를 배포 하기 전에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버를 만들어야 할는 **SSISDB** 카탈로그입니다.  
  
 SSISDB 카탈로그 기능 개요를 참조 하십시오. [SSIS 카탈로그](../../integration-services/service/ssis-catalog.md)합니다.  
  
## 고가용성  
 다른 사용자 데이터베이스와 같이 **SSISDB** 데이터베이스는 데이터베이스 미러링 및 복제를 지원하지 않습니다. 미러링 및 복제 하는 방법에 대 한 자세한 내용은 참조 [데이터베이스 미러링 및 #40; SQL Server 및 #41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)합니다.  
  
 함으로써 해당 내용과 SSISDB의 고가용성을 제공할 수도 있습니다 SSIS 및 Alwayson 가용성 그룹의 사용 합니다. 자세한 내용은이 블로그 Matt masson 게시물을 참조 하십시오. [무중단을 사용 하는 SSIS](http://go.microsoft.com/fwlink/?LinkId=255873), blogs.msdn.com 합니다.  
  
##  <a name="ssms"></a> SQL Server Management Studio의 Integration Services 서버  
 인스턴스에 연결 하는 경우는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 호스트 하는 **SSISDB** 데이터베이스, 개체 탐색기에서 다음 개체를 참조 하십시오:  
  
-   **SSISDB 데이터베이스**  
  
     개체 탐색기의 **데이터베이스** 노드 아래에 **SSISDB** 데이터베이스가 표시됩니다. 뷰를 쿼리하고 저장 프로시저를 호출하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버와 이 서버에 저장된 개체를 관리할 수 있습니다.  
  
-   **Integration Services 카탈로그**  
  
     **Integration Services 카탈로그** 노드 아래에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 및 환경을 위한 폴더가 있습니다.  
  
## 관련 태스크  
  
-   [SSIS 카탈로그 만들기](../../integration-services/service/create-the-ssis-catalog.md)  
  
-   [Integration Services 서버의 패키지 목록 보기](../../integration-services/service/view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Integration Services 서버에 프로젝트 배포](../../integration-services/packages/deploy-projects-to-integration-services-server.md)  
  
-   [SQL Server Management Studio를 사용하여 SSIS 서버에서 패키지 실행](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## 관련 내용  
 블로그 항목- [무중단을 사용 하는 SSIS](http://go.microsoft.com/fwlink/?LinkId=255873), blogs.msdn.com 합니다.  
  
  