---
title: 'SSIS 자습서: 패키지 배포 | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- deployment tutorial [Integration Services]
- deploying packages [Integration Services]
- SSIS, tutorials
- Integration Services, tutorials
- deploying packages [Integration Services], installing
- SQL Server Integration Services, tutorials
- walkthroughs [Integration Services]
- deployment utility [Integration Services]
- deploying packages [Integration Services], configurations
ms.assetid: de18468c-cff3-48f4-99ec-6863610e5886
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3752c7e0f99a62534a670743c0ee7deb3c2e07a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62899011"
---
# <a name="ssis-tutorial-deploying-packages"></a>SSIS 자습서: 패키지 배포
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 패키지를 다른 컴퓨터에 쉽게 배포할 수 있게 하는 도구를 제공합니다. 또한 이러한 배포 도구는 패키지에 필요한 구성 및 파일과 같은 모든 종속 파일을 관리합니다. 이 자습서에서는 이러한 도구를 사용하여 패키지와 패키지의 종속 파일을 대상 컴퓨터에 설치하는 방법을 배웁니다.  
  
 먼저 배포를 준비하기 위한 태스크를 수행합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 새 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 프로젝트를 만들고 기존 패키지와 데이터 파일을 프로젝트에 추가합니다. 새 패키지를 처음부터 만드는 대신에 이 자습서용으로 만들어진 완성된 패키지만 사용하여 작업합니다. 이 자습서에서 패키지의 기능을 수정하지는 않습니다. 그러나 패키지를 프로젝트에 추가한 후에 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 패키지를 열고 각 패키지의 내용을 검토하면 도움이 될 것입니다. 패키지를 검사하면 로그 파일과 같은 패키지 종속 파일과 패키지의 다른 흥미로운 기능에 대해 알 수 있습니다.  
  
 배포를 준비하면서 또한 구성을 사용하도록 패키지를 업데이트합니다. 구성은 패키지 및 패키지 개체의 속성을 런타임에 업데이트할 수 있게 만듭니다. 이 자습서에서는 구성을 사용하여 패키지가 사용하는 XML 및 XSD 파일의 위치와 로그 및 텍스트 파일의 연결 문자열을 업데이트합니다. 자세한 내용은 [패키지 구성](../../2014/integration-services/package-configurations.md) 및 [패키지 구성 만들기](../../2014/integration-services/create-package-configurations.md)를 참조하세요.  
  
 패키지가 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 성공적으로 실행되는지 확인한 후에 패키지를 설치하는 데 사용할 배포 번들을 만듭니다. 배포 번들은 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 추가한 패키지 파일 및 기타 항목, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 자동으로 포함하는 패키지 종속 파일 및 작성했던 배포 유틸리티로 구성됩니다. 자세한 내용은 [Create a Deployment Utility](../../2014/integration-services/create-a-deployment-utility.md)를 참조하세요.  
  
 그런 다음 배포 번들을 대상 컴퓨터에 복사하고 패키지 설치 마법사를 실행하여 패키지와 패키지 종속 파일을 설치합니다. 패키지는 msdb SQL Server 데이터베이스에 설치되고 지원 및 보조 파일은 파일 시스템에 설치됩니다. 배포된 패키지에서 구성이 사용되므로 새 환경에서 패키지가 성공적으로 실행될 수 있게 하는 새 값을 사용하도록 구성을 업데이트합니다.  
  
 마지막으로 패키지 실행 유틸리티를 사용하여 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 패키지를 실행합니다.  
  
 발생할 수 있는 복잡한 실제 배포 문제를 시뮬레이션하는 것이 이 자습서의 목표입니다. 그러나 패키지를 다른 컴퓨터에 배포할 수 없는 경우에도 로컬 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 있는 msdb 데이터베이스에 패키지를 설치한 다음 동일한 인스턴스에 있는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 패키지를 실행하여 이 자습서를 수행할 수 있습니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 사용할 수 있는 새 도구, 컨트롤 및 기능에 익숙해지는 가장 좋은 방법은 실제로 사용해 보는 것입니다. 이 자습서에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만든 다음 패키지 및 기타 필요한 파일을 프로젝트에 추가하는 단계를 진행합니다. 프로젝트가 완료된 후에 배포 번들을 만들고 번들을 대상 컴퓨터에 복사한 다음 패키지를 대상 컴퓨터에 설치합니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서는 기본적인 파일 시스템 작업에는 익숙하지만 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 새 기능은 많이 접해 보지 못한 사용자를 위한 것입니다. 기본를 파악 하는 데 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 이 자습서에서 사용 되는 개념에 유용할 수 있습니다이 먼저 다음을 완료 하려면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 자습서: [실행 SQL Server 가져오기 및 내보내기 마법사](import-export-data/start-the-sql-server-import-and-export-wizard.md) 고 [SSIS 자습서: 간단한 ETL 패키지 만들기](../integration-services/ssis-how-to-create-an-etl-package.md)합니다.  
  
 **원본 컴퓨터.** 배포 번들을 만들려는 컴퓨터에는 다음 구성 요소가 설치되어 있어야 합니다.  
  
-   AdventureWorks 데이터베이스가 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. 샘플 데이터베이스를 다운로드할 수 있습니다 [CodePlex](http://msftdbprodsamples.codeplex.com/releases/view/125550)합니다.  
  
-   AdventureWorks에서 테이블을 생성 및 삭제할 수 있는 권한  
  
-   예제 데이터, 완성된 패키지, 구성 및 추가 정보. 이러한 항목의 파일은 예제와 함께 설치됩니다. 예제 데이터를 찾을 수 없으면 위 절차로 돌아가 설명대로 설치를 완료하십시오.  
  
-   비즈니스 인텔리전스 개발 환경인 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]  
  
 **대상 컴퓨터.** 패키지를 배포하려는 컴퓨터에는 다음 구성 요소가 설치되어 있어야 합니다.  
  
-   AdventureWorks 데이터베이스가 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 분할된 테이블 또는 인덱스를 만들 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]입니다.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 패키지를 실행하려면 AdventureWorks에 테이블을 만들고 삭제할 수 있는 권한이 있어야 합니다.  
  
-   있어야 읽기 / 쓰기 권한 msdb의 sysssispackages 테이블에[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 시스템 데이터베이스입니다.  
  
 배포 번들을 만든 컴퓨터에 패키지를 배포하려면 해당 컴퓨터는 원본 및 대상 컴퓨터에 대한 요구 사항을 모두 충족해야 합니다.  
  
 **이 자습서에 소요되는 예상 시간:** 2시간  
  
## <a name="lessons-in-this-tutorial"></a>이 자습서의 단원  
 [1단원: 배포 번들 작성 준비](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)  
 이 단원에서는 새 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만들고 패키지 및 기타 필수 파일을 프로젝트에 추가하여 ETL 솔루션 배포를 준비합니다.  
  
 [2단원: 배포 번들 만들기](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
 이 단원에서는 배포 유틸리티를 작성하고 배포 번들에 필요한 파일이 포함되어 있는지 확인합니다.  
  
 [3단원: 패키지 설치](../integration-services/lesson-3-install-ssis-package.md)  
 이 단원에서는 배포 번들을 대상 컴퓨터에 복사하고 패키지를 설치한 다음 패키지를 실행합니다.  
  
![Integration Services 아이콘 (작은)](media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
  
