---
title: 패키지 실행 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executepackagetask.f1
helpviewer_keywords:
- Execution Package task [Integration Services]
- child packages
- parent packages [Integration Services]
ms.assetid: 042d4ec0-0668-401c-bb3a-a25fe2602eac
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 37d0edcabdb0171c8ca83c79080d59fdd8aafb76
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67284948"
---
# <a name="execute-package-task"></a>패키지 실행 태스크
  패키지 실행 태스크는 패키지가 다른 패키지를 워크플로의 일부로 실행할 수 있도록 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 엔터프라이즈 기능을 확장했습니다.  
  
 패키지 실행 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   복잡한 패키지 워크플로 분석. 이 태스크를 사용하면 워크플로를 여러 패키지로 분리하여 편리하게 읽고 테스트 및 유지 관리할 수 있습니다. 예를 들어 별모양 스키마에 데이터를 로드할 경우 별도의 패키지를 작성하여 각 차원 및 팩트 테이블을 채울 수 있습니다.  
  
-   패키지 일부 다시 사용. 다른 패키지에서 패키지 워크플로의 일부를 다시 사용할 수 있습니다. 예를 들어 다른 패키지에서 호출할 수 있는 데이터 추출 모듈을 작성할 수 있습니다. 추출 모듈을 호출하는 각 패키지는 다른 데이터 스크러빙, 필터링 또는 집계 작업을 수행할 수 있습니다.  
  
-   작업 단위 그룹화. 작업 단위는 별개의 패키지로 캡슐화되고 트랜잭션 구성 요소로 부모 패키지의 워크플로에 조인됩니다. 예를 들어 부모 패키지는 보조 패키지를 실행하고 보조 패키지의 성공 또는 실패에 따라 트랜잭션을 커밋하거나 롤백합니다.  
  
-   패키지 보안 제어. 패키지 작성자에게는 다중 패키지 솔루션의 일부에 대한 액세스 권한만 있으면 됩니다. 하나의 패키지를 여러 패키지로 분리하여 해당 패키지에만 작성자 액세스 권한을 부여할 수 있으므로 보안이 한층 강화됩니다.  
  
 다른 패키지를 실행하는 패키지를 일반적으로 부모 패키지라고 하고 부모 워크플로에서 실행하는 패키지를 자식 패키지라고 합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 실행 파일 및 배치 파일 실행과 같은 워크플로 작업을 수행하는 태스크가 포함되어 있습니다. 자세한 내용은 [Execute Process Task](execute-process-task.md)을 참조하세요.  
  
## <a name="running-packages"></a>패키지 실행  
 패키지 실행 태스크는 부모 패키지와 동일한 프로젝트에 포함된 자식 프로젝트를 실행할 수 있습니다. **ReferenceType** 속성을 **Project Reference**로 설정하고 **PackageNameFromProjectReference** 속성을 설정하여 프로젝트에서 자식 패키지를 선택할 수 있습니다.  
  
> [!NOTE]  
>  **ReferenceType** 옵션은 읽기 전용이며 패키지가 포함된 프로젝트가 프로젝트 배포 모델로 전환되지 않은 경우에는 **외부 참조** 로 설정됩니다. 변환에 대한 자세한 내용은 [Integration Services 서버에 프로젝트 배포](../deploy-projects-to-integration-services-server.md)를 참조하세요.  
  
 패키지 실행 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 데이터베이스에 저장된 패키지와 파일 시스템에 저장된 패키지도 실행할 수 있습니다. 이 태스크는 OLE DB 연결 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하거나 파일 연결 관리자를 사용하여 파일 시스템에 액세스합니다. 자세한 내용은 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) 및 [Flat File Connection Manager](../connection-manager/flat-file-connection-manager.md)를 참조하세요.  
  
 패키지 실행 태스크는 동일한 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 솔루션의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지와 데이터베이스 유지 관리 계획을 모두 관리할 수 있는 데이터베이스 유지 관리 계획을 실행할 수도 있습니다. 데이터베이스 유지 관리 계획은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지와 유사하지만 데이터베이스 유지 관리 태스크만 포함할 수 있으며 항상 msdb 데이터베이스에 저장됩니다.  
  
 파일 시스템에 저장된 패키지를 선택할 경우 패키지의 이름과 위치를 제공해야 합니다. 패키지 위치는 파일 시스템 어디나 가능하며 부모 패키지와 동일한 폴더에 있지 않아도 됩니다.  
  
 자식 패키지는 부모 패키지 프로세스에서 실행되거나 자체 프로세스에서 실행될 수 있습니다. 자식 패키지를 자체 프로세스에서 실행하려면 추가 메모리가 필요하지만 이런 방식으로 실행하면 유연성이 향상됩니다. 예를 들어 자식 프로세스가 실패할 경우 부모 프로세스에서 계속 실행할 수 있습니다.  
  
 또는 한 단위의 부모 패키지와 해당 자식 패키지가 함께 실행되지 못하게 하거나 다른 프로세스의 추가 오버헤드를 발생시키지 않으려는 경우도 있습니다. 예를 들어 패키지 부모 프로세스의 후속 처리가 자식 프로세스의 성공 여부에 따라 달라지는 경우 자식 프로세스가 실패하면 부모 패키지 프로세스에서 자식 패키지를 실행해야 합니다.  
  
 기본적으로 패키지 실행 태스크의 ExecuteOutOfProcess 속성은로 `False`설정 되 고 자식 패키지는 부모 패키지와 같은 프로세스에서 실행 됩니다. 이 속성을 `True`로 설정하면 하위 패키지가 개별 프로세스로 실행됩니다. 이렇게 하면 하위 패키지의 실행 속도가 느려집니다. 또한 속성을 `True`로 설정하면 도구만 설치로 패키지를 디버깅할 수 없습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치해야 합니다. 자세한 내용은 [Integration Services 설치](../install-windows/install-integration-services.md)를 참조하세요.  
  
## <a name="extending-transactions"></a>트랜잭션 확장  
 부모 패키지가 사용하는 트랜잭션은 자식 패키지로 확장될 수 있으므로 두 패키지가 수행한 작업을 모두 커밋하거나 롤백할 수 있습니다. 예를 들어 자식 패키지가 수행한 데이터베이스 삽입에 따라 부모 패키지가 수행한 데이터베이스 삽입을 커밋하거나 롤백할 수 있고 그 반대의 경우도 마찬가지로 적용됩니다. 자세한 내용은 [Inherited Transactions](../inherited-transactions.md)을 참조하세요.  
  
## <a name="propagating-logging-details"></a>로깅 세부 정보 전달  
 패키지 실행 태스크에서 실행하는 자식 패키지가 로깅을 사용하도록 구성될 수도 있고 그렇지 않을 수도 있지만 자식 패키지는 항상 로그 세부 정보를 부모 패키지로 전달합니다. 로깅을 사용하도록 패키지 실행 태스크를 구성하면 자식 패키지에서 전달된 로그 세부 정보가 기록됩니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md)을 참조하세요.  
  
## <a name="passing-values-to-child-packages"></a>자식 패키지에 값 전달  
 자식 패키지는 자신을 호출한 다른 패키지, 일반적으로 부모 패키지에서 전달된 값을 사용하는 경우가 많습니다. 부모 패키지에서 전달된 값을 사용할 경우 다음과 같은 시나리오에서 도움이 됩니다.  
  
-   큰 워크플로의 각 부분이 서로 다른 패키지에 할당됩니다. 예를 들어 한 패키지에서는 매일 데이터를 다운로드하고, 데이터를 요약하고, 요약 데이터 값을 변수에 할당하고, 데이터 추가 처리를 위해 다른 패키지로 값을 전달합니다.  
  
-   부모 패키지가 자식 패키지의 태스크를 동적으로 조정합니다. 예를 들어 부모 패키지가 현재 달의 일 수를 확인하고 이 수를 변수에 할당하면 자식 패키지가 해당 횟수만큼 태스크를 수행합니다.  
  
-   자식 패키지가 부모 패키지에서 동적으로 파생된 데이터에 액세스해야 합니다. 예를 들어 부모 패키지가 테이블에서 데이터를 추출하고 행 집합을 변수에 로드하면 자식 패키지가 해당 데이터에 추가 작업을 수행합니다.  
  
 자식 패키지에 값을 전달하기 위해서는 다음과 같은 방법을 사용할 수 있습니다.  
  
-   **패키지 구성**  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 부모 패키지의 값을 자식 패키지에 전달하기 위해 구성 유형 중 하나인 부모 패키지 변수 구성을 제공합니다. 이 구성은 자식 패키지에서 작성되며 부모 패키지의 변수를 사용합니다. 이 구성은 자식 패키지의 변수나 자식 패키지의 개체 속성에 매핑됩니다. 스크립트 태스크 또는 스크립트 구성 요소가 사용하는 스크립트에서 이 변수를 사용할 수도 있습니다.  
  
-   **매개 변수**  
  
     부모 패키지 변수나 매개 변수 또는 프로젝트 매개 변수를 자식 패키지 매개 변수에 매핑하도록 패키지 실행 태스크를 구성할 수 있습니다. 프로젝트에서 프로젝트 배포 모델을 사용해야 하며 자식 패키지는 부모 패키지와 동일한 프로젝트에 포함되어 있어야 합니다. 자세한 내용은 [Execute Package Task Editor](../execute-package-task-editor.md)을 참조하세요.  
  
    > [!NOTE]  
    >  자식 패키지 매개 변수가 중요한 정보가 아니고 중요한 부모 매개 변수에 매핑된 경우 자식 패키지가 실행되지 않습니다.  
    >   
    >  다음 매핑 조건이 지원됩니다.  
    >   
    >  -   중요한 자식 패키지 매개 변수는 중요한 부모 매개 변수에 매핑됩니다.  
    > -   중요한 자식 패키지 매개 변수는 중요하지 않은 부모 매개 변수에 매핑됩니다.  
    > -   중요하지 않은 자식 패키지 매개 변수는 중요하지 않은 부모 매개 변수에 매핑됩니다.  
  
 부모 패키지 변수는 패키지 실행 태스크 범위나 패키지 등의 부모 컨테이너에서 정의할 수 있습니다. 동일한 이름을 가진 변수가 여러 개이면 패키지 실행 태스크 범위에서 정의된 변수나 범위에서 해당 태스크에 가장 가까운 변수가 사용됩니다.  
  
 자세한 내용은 [자식 패키지에서 변수 및 매개 변수의 값 사용](../use-the-values-of-variables-and-parameters-in-a-child-package.md)을 참조하세요.  
  
### <a name="accessing-parent-package-variables"></a>부모 패키지 변수 액세스  
 자식 패키지는 스크립트 태스크를 사용하여 부모 패키지 변수에 액세스할 수 있습니다. **스크립트 태스크 편집기**의 **스크립트** 페이지에 부모 패키지 변수의 이름을 입력하는 경우 변수 이름에 **User:** 를 포함하지 마십시오. 그렇지 않으면 부모 패키지를 실행할 때 자식 패키지에서 변수를 찾을 수 없습니다. 스크립트 태스크를 사용 하 여 부모 패키지 변수에 액세스 하는 방법에 대 한 자세한 내용은 [SSIS: 부모 패키지의 변수 액세스](https://andyleonard.blog/2015/08/ssis-design-pattern-access-parent-variables-from-a-child-package-in-the-ssis-catalog/)블로그 항목을 참조 하세요.  
  
## <a name="configuring-the-execute-package-task"></a>패키지 실행 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [패키지 실행 태스크 편집기](../execute-package-task-editor.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>관련 내용  

Andyleonard의 블로그 항목인 [SSIS: 부모 패키지의 변수 액세스](https://andyleonard.blog/2015/08/ssis-design-pattern-access-parent-variables-from-a-child-package-in-the-ssis-catalog/) 
  
  
