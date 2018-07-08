---
title: 상호 운용성 및 공존 성 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f7face1f41fdf02f772c05427db9d45d1bd6050
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277589"
---
# <a name="interoperability-and-coexistence-integration-services"></a>상호 운용성 및 공존성(Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services(SSIS)는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 및 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services와 함께 나란히 공존할 수 있습니다.  
  
## <a name="features-and-differences"></a>기능 및 차이점  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 현재 버전과 이전 버전 간 차이점 및  
  
|기능|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|개발 환경|[SQL Server 2014 Data Tools – Visual Studio 2012 CTP 2 용 Business Intelligence](http://www.microsoft.com/download/details.aspx?id=40736)<br /><br /> [SQL Server 2014 Data Tools-Visual Studio 2013 용 Business Intelligence](http://www.microsoft.com/download/details.aspx?id=42313)|[Visual Studio 2010 용 SQL Server Data Tools](http://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools – Visual Studio 2012 용 Business Intelligence](http://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)])|  
|관리 환경|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|패키지 저장을 위한 msdb의 주 시스템 테이블|sysssispackages|sysssispackages|sysssispackages|  
|패키지 실행을 위한 주 명령 프롬프트 유틸리티|**dtexec** (dtexec.exe), 2014 버전|**dtexec** (dtexec.exe), 2012 버전|**dtexec** (dtexec.exe), 2008 버전|  
|기본 루트 파일 시스템 폴더|C:\Program Files\Microsoft SQL Server\120\DTS|C:\Program Files\Microsoft SQL Server\110\DTS|C:\Program Files\Microsoft SQL Server\100\DTS|  
|기본 루트 레지스트리 키|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>병렬 호환성 문제  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services를 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 및 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services와 함께 설치하면 다음과 같은 태스크를 수행할 수 있습니다.  
  
-   **SQL Server Data Tools에서 패키지를 디자인합니다**. 다음 도구를 사용하여 해당 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 기반으로 하는 패키지를 개발하고 유지 관리합니다.  
  
    -   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]를 기반으로 하는 패키지를 개발하고 유지 보수하려면 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 버전의 Business Intelligence Development Studio를 사용합니다.  
  
    -   사용 된 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 개발 하 고 기반으로 하는 패키지 관리 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
    -   사용 된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 개발 하 고 기반으로 하는 패키지 관리 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
-   **패키지 로드 및 실행**. 로드 하 고에서 개발 된 패키지를 실행할 수 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 하 고 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. 패키지 형식으로 영구적으로 업그레이드는 패키지를 기존 프로젝트에 추가 하는 경우는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services를 사용 합니다. 패키지 파일을 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 열면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services에서 사용하는 형식으로 패키지가 일시적으로 업그레이드됩니다. 패키지 변경 내용을 저장하면 패키지가 영구적으로 업그레이드됩니다. 한 번 형식으로 저장 하는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 사용, 패키지에서 더 이상 열 수 없습니다 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전의 Business Intelligence Development Studio 또는 해당 실행 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services 도구입니다.  
  
-   **SQL Server Management Studio에서 패키지 관리**. 인스턴스에 연결할 수 없습니다는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 합니다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다. 인스턴스에 연결할 수 없습니다는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전의는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 인스턴스에 저장된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 패키지를 관리할 수 있습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 인스턴스를 서비스에서 관리하는 위치 목록에 추가하려면 서비스 구성 파일을 수정해야 합니다. 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](../service/integration-services-service-ssis-service.md)을 참조하세요.  
  
-   **SQL Server에서 패키지 저장**. 다음 데이터베이스에 패키지를 저장할 수 있습니다.  
  
    |패키지 형식|데이터베이스|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services|인스턴스의 msdb 데이터베이스 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services|인스턴스의 msdb 데이터베이스 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services|인스턴스의 msdb 데이터베이스 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     인스턴스에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 인스턴스에서 패키지를 가져올 수 있습니다 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 인스턴스에서 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 인스턴스에 패키지를 내보낼 수는 없음 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 인스턴스에 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]합니다.  
  
     [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 인스턴스에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에서 패키지를 가져오거나 패키지를 내보낼 수 없습니다.  
  
-   **패키지 실행**. 실행할 수 있습니다 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services 및 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 사용 하 여 Integration Services 패키지를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의는 **dtexec** 유틸리티 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트입니다. 때마다를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 도구에서 개발 된 패키지를 로드 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 메모리에서이 도구에서 일시적으로 변환, 패키지에 패키지 형식으로 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 사용 합니다. 경우는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 패키지에 성공적인 변환을 방해 하는 문제는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services 도구는 이러한 문제가 해결 될 때까지 패키지를 실행할 수 없습니다. 자세한 내용은 [Upgrade Integration Services Packages](upgrade-integration-services-packages.md)를 참조하세요.  
  
  
