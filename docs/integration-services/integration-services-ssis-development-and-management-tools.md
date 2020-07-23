---
title: 개발 및 관리 도구 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- studio environments [Integration Services]
- tools [Integration Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, Integration Services in
- SQL Server Management Studio [Integration Services]
- SSIS, studio environments
- SQL Server Integration Services, studio environments
- tools [Integration Services], SQL Server Management Studio
ms.assetid: 4eb73e65-d9f3-4ac6-a408-abfa85afc537
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4b64d20ecb26a143c373a1073b379f0ae9debfb1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917549"
---
# <a name="integration-services-ssis-development-and-management-tools"></a>SSIS(Integration Services) 배포 및 관리 도구

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에는 패키지에 사용할 수 있는 두 가지 스튜디오가 포함되어 있습니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서는 비즈니스 솔루션에 필요한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 개발할 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 는 패키지를 만들 수 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 제공합니다.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서는 프로덕션 환경에서 패키지를 관리할 수 있습니다.  
  
## <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서는 다음 태스크를 수행할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 실행하여 원본에서 대상으로 데이터를 복사하는 기본 패키지를 만듭니다.  
  
-   복잡한 제어 흐름, 데이터 흐름, 이벤트 기반 논리 및 로깅이 포함된 패키지를 만듭니다.  
  
-   [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너의 문제 해결 및 모니터링 기능과 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 디버깅 기능을 사용하여 패키지를 테스트하고 디버깅합니다.  
  
-   패키지 및 패키지 개체의 속성을 런타임에 업데이트하는 구성을 만듭니다.  
  
-   패키지 및 종속 요소를 다른 컴퓨터에 설치할 수 있는 배포 유틸리티를 만듭니다.  
  
-   패키지의 복사본을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 데이터베이스, [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소 및 파일 시스템에 저장합니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에 대한 자세한 내용은 [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686.aspx)를 참조하세요.  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서는 패키지를 관리하고 실행 중인 패키지를 모니터링하고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체의 영향과 데이터 계보를 확인하는 데 사용되는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스를 제공합니다.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서는 다음 태스크를 수행할 수 있습니다.  
  
-   조직 요구에 맞게 패키지를 구성할 수 있는 폴더를 만듭니다.  
  
-   패키지 실행 유틸리티를 사용하여 로컬 컴퓨터에 저장된 패키지를 실행합니다.  
  
-   패키지 실행 유틸리티를 실행하여 **dtexec** 명령 프롬프트 유틸리티(dtexec.exe)를 실행할 때 사용할 명령줄을 생성합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 데이터베이스, [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 저장소 및 파일 시스템에서 패키지를 가져오고 내보냅니다.  
