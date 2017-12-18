---
title: "프로그래밍 방식으로 패키지 실행 및 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 1a08c75e-ce8c-45ee-81bd-32248bbdb2b2
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6affcd02d932b1e382268f328a6e5c6abf8b177b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="running-and-managing-packages-programmatically"></a>프로그래밍 방식으로 패키지 실행 및 관리
  개발 환경 외부에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 관리 및 실행해야 하는 경우 패키지를 프로그래밍 방식으로 조작할 수 있습니다. 이 경우 다음 중 하나를 선택할 수 있습니다.  
  
-   기존 패키지를 로드하고 수정하지 않은 채로 실행합니다.  
  
-   기존 패키지를 로드하고 다시 구성(예: 다른 데이터 원본에 대해)한 다음 실행합니다.  
  
-   새 패키지를 만들고 구성 요소를 개체별 및 속성별로 구성한 다음 새 패키지를 저장 후 실행합니다.  
  
 단 몇 줄의 코드를 작성하여 클라이언트 응용 프로그램에서 기존 패키지를 로드하고 실행할 수 있습니다.  
  
 이 섹션에서는 기존 패키지를 프로그래밍 방식으로 실행하는 방법과 다른 응용 프로그램에서 데이터 흐름의 출력에 액세스하는 방법을 설명합니다. 고급 프로그래밍 옵션인 [프로그래밍 방식으로 패키지 작성](../../integration-services/building-packages-programmatically/building-packages-programmatically.md) 항목의 설명에 따라 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 프로그래밍 방식으로 한 줄씩 만들 수 있습니다.  
  
 이 섹션에서는 저장된 패키지, 실행 중인 패키지 및 패키지 역할을 관리하기 위해 프로그래밍 방식으로 수행할 수 있는 기타 관리 태스크도 설명합니다.  
  
## <a name="running-packages-on-the-integration-services-server"></a>Integration Services 서버의 패키지 실행  
 패키지를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포한 경우 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스를 사용하여 프로그래밍 방식으로 패키지를 실행할 수 있습니다. Microsoft.SqlServer.Management.IntegrationServices 어셈블리는 .NET Framework 3.5로 컴파일됩니다. .NET Framework 4.0 응용 프로그램을 빌드하는 경우 프로젝트 파일에 어셈블리 참조를 직접 추가해야 할 수 있습니다.  
  
 또한 네임스페이스를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 배포 및 관리할 수 있습니다. 네임스페이스 및 코드 조각에 대한 개요는 blogs.msdn.com에서 [SSIS 카탈로그 관리 개체 모델에 대한 이해](http://go.microsoft.com/fwlink/?LinkId=253122)블로그 항목을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
 [로컬 실행과 원격 실행의 차이점 이해](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)  
 패키지를 로컬로 실행할 때와 서버에서 실행할 때의 중요한 차이점에 대해 설명합니다.  
  
 [프로그래밍 방식으로 로컬 패키지 로드 및 실행](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
 로컬 컴퓨터의 클라이언트 응용 프로그램에서 기존 패키지를 실행하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 원격 패키지 로드 및 실행](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
 클라이언트 응용 프로그램에서 기존 패키지를 실행하고 해당 패키지가 서버에서 실행되도록 하는 방법에 대해 설명합니다.  
  
 [로컬 패키지의 출력 로드](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
 로컬 컴퓨터에서 패키지를 실행하는 방법과 DataReader 대상 및 DtsClient 네임스페이스를 사용하여 데이터 흐름의 출력을 클라이언트 응용 프로그램으로 로드하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 사용 가능 패키지 열거](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 의해 관리되는 사용 가능한 패키지를 검색하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 패키지 및 폴더 관리](../../integration-services/run-manage-packages-programmatically/managing-packages-and-folders-programmatically.md)  
 패키지 및 폴더를 만들고, 이름을 바꾸고, 삭제하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 실행 중인 패키지 관리](../../integration-services/run-manage-packages-programmatically/managing-running-packages-programmatically.md)  
 현재 실행 중인 패키지를 나열하고 해당 속성을 조사하고 실행 중인 패키지를 중지하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 패키지 역할 관리&#40;SSIS 서비스&#41;](../../integration-services/run-manage-packages-programmatically/managing-package-roles-programmatically-ssis-service.md)  
 패키지 또는 폴더에 할당된 역할에 대한 정보를 가져오거나 설정하는 방법에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)  
 미리 정의된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류 코드와 해당 심볼 이름 및 설명을 나열합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [스크립팅을 사용한 패키지 확장](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 스크립트 태스크를 사용하여 제어 흐름을 확장하는 방법과 스크립트 구성 요소를 사용하여 데이터 흐름을 확장하는 방법에 대해 설명합니다.  
  
 [사용자 지정 개체를 사용한 패키지 확장](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 여러 패키지에서 사용할 프로그램 사용자 지정 태스크, 데이터 흐름 구성 요소 및 기타 패키지 개체를 만드는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 패키지 빌드](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 프로그래밍 방식으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만들고 구성 및 저장하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
