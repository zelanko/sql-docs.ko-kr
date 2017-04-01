---
title: "자식 패키지에서 변수 및 매개 변수의 값 사용 | Microsoft Docs"
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
  - "변수 [Integration Services], 패키지 간 전달"
  - "구성 [Integration Services]"
  - "패키지 [Integration Services], 구성"
  - "변수 [Integration Services], 추가"
ms.assetid: 9b939edb-4e17-48e5-8428-855beb10049c
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# 자식 패키지에서 변수 및 매개 변수의 값 사용
  이 절차에서는 부모 변수 구성 유형을 사용하는 패키지 구성을 만드는 방법에 대해 설명합니다. 이 구성 유형을 사용하여 부모 패키지에서 실행되는 자식 패키지가 부모 변수에 액세스하도록 설정할 수 있습니다.  
  
> [!NOTE]  
>  또한 부모 패키지 변수나 매개 변수 또는 프로젝트 매개 변수를 자식 패키지 매개 변수에 매핑하도록 패키지 실행 태스크를 구성하여 값을 자식 패키지에 전달할 수 있습니다. 자세한 내용은 [Execute Package Task](../../integration-services/control-flow/execute-package-task.md)을 참조하세요.  
  
 자식 패키지에 패키지 구성을 만들기 전에 부모 패키지에 변수를 만들 필요는 없습니다. 부모 패키지에는 언제든지 변수를 추가할 수 있습니다. 단, 패키지 구성에 정확한 부모 변수의 이름을 사용해야 합니다. 그러나 부모 변수 구성을 만들려면 이 부모 변수 구성을 통해 업데이트할 수 있는 자식 패키지에 기존 변수가 있어야 합니다. 변수 추가 및 구성에 대한 자세한 내용은 [패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경](../Topic/Add,%20Delete,%20Change%20Scope%20of%20User-Defined%20Variable%20in%20a%20Package.md)을 참조하세요.  
  
 부모 변수 구성에 사용되는 부모 패키지의 변수 범위는 패키지 실행 태스크, 태스크가 있는 컨테이너 또는 패키지로 설정할 수 있습니다. 이름이 같은 여러 개의 변수가 패키지에 정의된 경우 패키지 실행 태스크 범위에 가장 가까운 변수가 사용됩니다. 패키지 실행 태스크에 가장 가까운 범위는 작업 자체입니다.  
  
### 부모 패키지에 변수를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 자식 패키지에 전달할 변수를 추가할 패키지가 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  다음 중 하나를 수행하여 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 변수 범위를 정의하십시오.  
  
    -   패키지 범위를 설정하려면 **제어 흐름** 탭의 디자인 화면에서 아무 곳이나 클릭합니다.  
  
    -   범위를 패키지 실행 태스크의 부모 컨테이너로 설정하려면 컨테이너를 클릭합니다.  
  
    -   패키지 실행 태스크의 범위를 설정하려면 태스크를 클릭합니다.  
  
4.  변수를 추가하고 구성합니다.  
  
    > [!NOTE]  
    >  변수가 저장하는 데이터와 호환 가능한 데이터 형식을 선택합니다.  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### 자식 패키지에 변수를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 부모 변수 구성을 추가할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지 범위를 설정하려면 **제어 흐름** 탭의 디자인 화면에서 아무 곳이나 클릭합니다.  
  
4.  변수를 추가하고 구성합니다.  
  
    > [!NOTE]  
    >  변수가 저장하는 데이터와 호환 가능한 데이터 형식을 선택합니다.  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### 부모 패키지 구성을 자식 패키지에 추가하려면  
  
1.  자식 패키지가 열려 있지 않은 경우에는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 자식 패키지를 엽니다.  
  
2.  **제어 흐름** 탭의 디자인 화면에서 아무 곳이나 클릭합니다.  
  
3.  **SSIS** 메뉴에서 **패키지 구성**을 클릭합니다.  
  
4.  **패키지 구성 도우미** 대화 상자에서 **패키지 구성 설정**을 선택하고 **추가**를 클릭합니다.  
  
5.  패키지 구성 마법사 시작 페이지에서 **다음**을 클릭합니다.  
  
6.  구성 유형 선택 페이지의 **구성 유형** 목록에서 **부모 패키지 변수** 를 선택하고 다음 중 하나를 수행합니다.  
  
    -   **구성 설정을 직접 지정**을 선택하고 **부모 변수** 상자에 구성에서 사용할 부모 패키지의 변수 이름을 지정합니다.  
  
        > [!IMPORTANT]  
        >  변수 이름은 대/소문자를 구분합니다.  
  
    -   **구성 위치가 환경 변수에 저장됨**을 선택한 다음 **환경 변수 목록**에서 변수 이름이 포함된 환경 변수를 선택합니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  대상 속성 선택 페이지에서 **변수** 노드, 구성할 변수의 **속성** 노드를 차례로 확장한 다음 구성에서 설정할 속성을 클릭합니다.  
  
9. **다음**을 클릭합니다.  
  
10. 마법사 완료 페이지에서 필요에 따라 기본 구성 이름을 수정하고 구성 정보를 검토합니다.  
  
11. **마침** 을 클릭하여 마법사를 완료하고 **패키지 구성 도우미** 대화 상자로 돌아갑니다.  
  
12. **패키지 구성 도우미** 대화 상자의 **구성** 상자에 새 구성이 나열됩니다.  
  
13. **닫기**를 클릭합니다.  
  
## 관련 항목:  
 [패키지 구성](../../integration-services/packages/package-configurations.md)   
 [패키지 구성 만들기](../../integration-services/packages/create-package-configurations.md)   
 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)   
 [패키지에서 변수 사용](../Topic/Use%20Variables%20in%20Packages.md)  
  
  