---
title: "Integration Services (SSIS) 개발 및 관리 도구 | Microsoft Docs"
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
  - "Studio 환경 [Integration Services]"
  - "도구 [Integration Services], Business Intelligence Development Studio"
  - "Business Intelligence Development Studio, Integration Services"
  - "SQL Server Management Studio [Integration Services]"
  - "SSIS, Studio 환경"
  - "SQL Server Integration Services, 스튜디오 환경"
  - "도구 [Integration Services], SQL Server Management Studio"
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
caps.latest.revision: 52
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 52
---
# Integration Services (SSIS) 개발 및 관리 도구
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 사용할 수 있는 두 가지 Studio가 있습니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서는 비즈니스 솔루션에 필요한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 개발할 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 는 패키지를 만들 수 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 제공합니다.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서는 프로덕션 환경에서 패키지를 관리할 수 있습니다.  
  
## SQL Server Data Tools  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서는 다음 태스크를 수행할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 실행하여 원본에서 대상으로 데이터를 복사하는 기본 패키지를 만듭니다.  
  
-   복잡한 제어 흐름, 데이터 흐름, 이벤트 기반 논리 및 로깅이 포함된 패키지를 만듭니다.  
  
-   [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너의 문제 해결 및 모니터링 기능과 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 디버깅 기능을 사용하여 패키지를 테스트하고 디버깅합니다.  
  
-   패키지 및 패키지 개체의 속성을 런타임에 업데이트하는 구성을 만듭니다.  
  
-   패키지 및 종속 요소를 다른 컴퓨터에 설치할 수 있는 배포 유틸리티를 만듭니다.  
  
-   패키지의 복사본을 저장 된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 데이터베이스, [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소 및 파일 시스템입니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 대한 자세한 내용은 [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686.aspx)를 참조하세요.  
  
## SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서는 패키지를 관리하고 실행 중인 패키지를 모니터링하고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체의 영향과 데이터 계보를 확인하는 데 사용되는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스를 제공합니다.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서는 다음 태스크를 수행할 수 있습니다.  
  
-   조직 요구에 맞게 패키지를 구성할 수 있는 폴더를 만듭니다.  
  
-   패키지 실행 유틸리티를 사용하여 로컬 컴퓨터에 저장된 패키지를 실행합니다.  
  
-   패키지 실행 유틸리티를 실행할 때 사용 하 여 명령줄 생성를 실행 하는 **dtexec** 명령 프롬프트 유틸리티 (dtexec.exe).  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 데이터베이스, [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소 및 파일 시스템에서 패키지를 가져오고 내보냅니다.  
