---
title: "Integration Services 서비스(SSIS 서비스) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 서비스, Integration Services 서비스 정보"
  - "SQL Server Integration Services 서비스"
  - "서비스 [Integration Services], Integration Services 서비스 정보"
  - "서비스 [Integration Services]"
  - "SQL Server Integration Services, 서비스"
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
caps.latest.revision: 61
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Integration Services 서비스(SSIS 서비스)
  이 섹션의 항목에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. 이 서비스는 Integration Services 패키지를 생성, 저장 및 실행하는 데 필요하지 않습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 는 이전 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 버전과의 호환성을 위한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]서비스를 지원합니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 프로젝트 배포 모델을 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포한 프로젝트의 **SSISDB** 데이터베이스에 개체, 설정 및 작업 데이터를 저장합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터베이스 엔진의 인스턴스인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버는 데이터베이스를 호스팅합니다. 데이터베이스에 대한 자세한 내용은 [SSIS 카탈로그](../../integration-services/service/ssis-catalog.md)를 참조하세요. 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포하는 방법에 대한 자세한 내용은 [Integration Services 서버에 프로젝트 배포](../../integration-services/packages/deploy-projects-to-integration-services-server.md)를 참조하세요.  
  
## 관리 기능  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 관리를 위한 Windows 서비스입니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서만 사용할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 다음 관리 기능을 제공합니다.  
  
-   원격 및 로컬에 저장된 패키지 시작  
  
-   원격 및 로컬로 실행 중인 패키지 중지  
  
-   원격 및 로컬로 실행 중인 패키지 모니터링  
  
-   패키지 가져오기 및 내보내기  
  
-   패키지 저장소 관리  
  
-   저장소 폴더 사용자 지정  
  
-   서비스가 중지될 때 실행 중인 패키지 중지  
  
-   Windows 이벤트 로그 보기  
  
-   여러 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결  
  
## Integration Services 서비스 시작 유형  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구성 요소를 설치할 때 함께 설치됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 기본적으로 시작되며 서비스의 시작 유형은 자동으로 설정됩니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소에 저장된 패키지를 모니터링하려면 서비스가 실행되고 있어야 합니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 msdb 데이터베이스 또는 파일 시스템 내의 지정된 폴더일 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 디자인 및 실행만 하려는 경우에는 필요하지 않습니다. 하지만 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 패키지를 나열하고 모니터링하려면 이 서비스가 필요합니다.  
  
## 관련 작업  
  
-   [Integration Services 서비스 속성 설정](../../integration-services/service/set-the-properties-of-the-integration-services-service.md)  
  
-   [Integration Services 서비스의 뷰 이벤트](../../integration-services/service/view-events-for-the-integration-services-service.md)  
  
  