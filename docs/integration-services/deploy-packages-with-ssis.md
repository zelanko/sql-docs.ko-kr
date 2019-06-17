---
title: SSIS를 사용하여 패키지 배포 | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
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
ms.openlocfilehash: a6be73e7253bc0be8d8dde9766f9fcb8be0a2dfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725747"
---
# <a name="deploy-packages-with-ssis"></a>SSIS를 사용하여 패키지 배포

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 패키지를 다른 컴퓨터에 쉽게 배포할 수 있게 하는 도구를 제공합니다. 또한 이러한 배포 도구는 패키지에 필요한 구성 및 파일과 같은 모든 종속 파일을 관리합니다. 이 자습서에서는 이러한 도구를 사용하여 패키지와 패키지의 종속 파일을 대상 컴퓨터에 설치하는 방법을 배웁니다.    
    
먼저 배포를 준비하기 위한 태스크를 수행합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 새 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 프로젝트를 만들고 기존 패키지와 데이터 파일을 프로젝트에 추가합니다. 새 패키지를 처음부터 만드는 대신에 이 자습서용으로 만들어진 완성된 패키지만 사용하여 작업합니다. 이 자습서에서 패키지의 기능을 수정하지는 않습니다. 그러나 패키지를 프로젝트에 추가한 후에 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 패키지를 열고 각 패키지의 내용을 검토하면 도움이 될 것입니다. 패키지를 검사하면 로그 파일과 같은 패키지 종속 파일과 패키지의 다른 흥미로운 기능에 대해 알 수 있습니다.    
    
배포를 준비하면서 또한 구성을 사용하도록 패키지를 업데이트합니다. 구성은 패키지 및 패키지 개체의 속성을 런타임에 업데이트할 수 있게 만듭니다. 이 자습서에서는 구성을 사용하여 패키지가 사용하는 XML 및 XSD 파일의 위치와 로그 및 텍스트 파일의 연결 문자열을 업데이트합니다. 자세한 내용은 [패키지 구성](../integration-services/packages/package-configurations.md) 및 [패키지 구성 만들기](../integration-services/packages/create-package-configurations.md)를 참조하세요.    
    
패키지가 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 성공적으로 실행되는지 확인한 후에 패키지를 설치하는 데 사용할 배포 번들을 만듭니다. 배포 번들은 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 추가한 패키지 파일 및 기타 항목, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 자동으로 포함하는 패키지 종속 파일 및 작성했던 배포 유틸리티로 구성됩니다. 자세한 내용은 [Create a Deployment Utility](../integration-services/packages/create-a-deployment-utility.md)를 참조하세요.    
    
그런 다음 배포 번들을 대상 컴퓨터에 복사하고 패키지 설치 마법사를 실행하여 패키지와 패키지 종속 파일을 설치합니다. 패키지는 msdb SQL Server 데이터베이스에 설치되고 지원 및 보조 파일은 파일 시스템에 설치됩니다. 배포된 패키지에서 구성이 사용되므로 새 환경에서 패키지가 성공적으로 실행될 수 있게 하는 새 값을 사용하도록 구성을 업데이트합니다.    
    
마지막으로 패키지 실행 유틸리티를 사용하여 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 패키지를 실행합니다.    
    
발생할 수 있는 복잡한 실제 배포 문제를 시뮬레이션하는 것이 이 자습서의 목표입니다. 그러나 패키지를 다른 컴퓨터에 배포할 수 없는 경우에도 로컬 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 있는 msdb 데이터베이스에 패키지를 설치한 다음 동일한 인스턴스에 있는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 패키지를 실행하여 이 자습서를 수행할 수 있습니다.    

**이 자습서에 소요되는 예상 시간:** 2시간

## <a name="what-you-learn"></a>학습 내용    
[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 사용할 수 있는 새 도구, 컨트롤 및 기능에 익숙해지는 가장 좋은 방법은 실제로 사용해 보는 것입니다. 이 자습서에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만든 다음 패키지 및 기타 필요한 파일을 프로젝트에 추가하는 단계를 진행합니다. 프로젝트가 완료된 후에 배포 번들을 만들고 번들을 대상 컴퓨터에 복사한 다음 패키지를 대상 컴퓨터에 설치합니다.    
    
## <a name="prerequisites"></a>사전 요구 사항    
이 자습서는 기본적인 파일 시스템 작업에는 익숙하지만 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 새 기능은 많이 접해 보지 못한 사용자를 위한 것입니다. 이 자습서에서 사용되는 기본 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개념을 더 쉽게 이해할 수 있도록 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 자습서인 [SSIS ETL 패키지를 만드는 방법](../integration-services/ssis-how-to-create-an-etl-package.md)을 먼저 완료하는 것이 좋습니다.    
    
### <a name="on-the-source-computer"></a>원본 컴퓨터의 경우

배포 번들을 만드는 컴퓨터에는 **다음 구성 요소가 설치되어 있어야 합니다**.

- SQL Server. ([SQL Server 다운로드](https://www.microsoft.com/sql-server/sql-server-downloads)에서 SQL Server의 평가판 또는 개발자 버전을 다운로드합니다.)

- 샘플 데이터, 완성된 패키지, 구성 및 추가 정보. 샘플 데이터와 강의 패키지를 Zip 파일로 다운로드하려면 [SQL Server Integration Services 자습서 파일](https://www.microsoft.com/download/details.aspx?id=56827)을 참조하세요. Zip 파일에 있는 대부분 파일은 의도하지 않은 변경을 방지하기 위해 읽기 전용입니다. 출력을 파일에 쓰거나 변경하려면 파일 속성에서 읽기 전용 특성을 꺼야 할 수 있습니다.

-   **AdventureWorks2014** 샘플 데이터베이스. **AdventureWorks2014** 데이터베이스를 다운로드하려면 [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)에서 `AdventureWorks2014.bak`를 다운로드하고 백업을 복원하세요.  

-   AdventureWorks 데이터베이스에서 테이블을 만들고 삭제할 수 있는 권한이 있어야 합니다.
    
-   [SQL Server Data Tools(SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).    
    
### <a name="on-the-destination-computer"></a>대상 컴퓨터의 경우

패키지를 배포하려는 컴퓨터에 **다음 구성 요소가 설치되어 있어야 합니다.**    
    
- SQL Server. ([SQL Server 다운로드](https://www.microsoft.com/sql-server/sql-server-downloads)에서 SQL Server의 평가판 또는 개발자 버전을 다운로드합니다.)

- 샘플 데이터, 완성된 패키지, 구성 및 추가 정보. 샘플 데이터와 강의 패키지를 Zip 파일로 다운로드하려면 [SQL Server Integration Services 자습서 파일](https://www.microsoft.com/download/details.aspx?id=56827)을 참조하세요. Zip 파일에 있는 대부분 파일은 의도하지 않은 변경을 방지하기 위해 읽기 전용입니다. 출력을 파일에 쓰거나 변경하려면 파일 속성에서 읽기 전용 특성을 꺼야 할 수 있습니다.

-   **AdventureWorks2014** 샘플 데이터베이스. **AdventureWorks2014** 데이터베이스를 다운로드하려면 [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)에서 `AdventureWorks2014.bak`를 다운로드하고 백업을 복원하세요.  
    
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md).    
    
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. SSIS를 설치하려면 [Integration Services 설치](install-windows/install-integration-services.md)를 참조하세요.
    
-   AdventureWorks 데이터베이스에서 테이블을 만들고 삭제할 권한과 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 SSIS 패키지를 실행할 권한이 있어야 합니다.    
    
-   `sysssispackages` [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 시스템 데이터베이스의 `msdb` 테이블에 대한 읽기/쓰기 권한    
    
배포 번들을 만든 컴퓨터에 패키지를 배포하려면 해당 컴퓨터는 원본 및 대상 컴퓨터에 대한 요구 사항을 모두 충족해야 합니다.    
        
## <a name="lessons-in-this-tutorial"></a>이 자습서의 단원    
[1단원: 배포 번들 작성 준비](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)    
이 단원에서는 새 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만들고 패키지 및 기타 필수 파일을 프로젝트에 추가하여 ETL 솔루션 배포를 준비합니다.    
    
[2단원: SSIS에서 배포 번들 만들기](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)    
이 단원에서는 배포 유틸리티를 작성하고 배포 번들에 필요한 파일이 포함되어 있는지 확인합니다.    
    
[3단원: SSIS 패키지 설치](../integration-services/lesson-3-install-ssis-packages.md)    
이 단원에서는 배포 번들을 대상 컴퓨터에 복사하고 패키지를 설치한 다음 패키지를 실행합니다.    
    

