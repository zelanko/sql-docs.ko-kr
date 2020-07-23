---
title: 제어 흐름 패키지 파트를 사용하여 패키지에 대해 제어 흐름 재사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.toolboxcontrolflowtemplate.f1
- sql13.dts.designer.addcopyexistingtemplate.f1
- sql13.dts.designer.addcopyexistingpackagepart.f1
- sql13.dts.designer.packagepart.general.f1
ms.assetid: 1edc91d9-1fab-4fe5-aed3-6f581fe32c18
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c86782a4ccd7ad03096ccd2723ff2867a779de16
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918316"
---
# <a name="reuse-control-flow-across-packages-by-using-control-flow-package-parts"></a>제어 흐름 패키지 파트를 사용하여 패키지에 대해 제어 흐름 재사용

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  일반적으로 사용되는 제어 흐름 태스크 또는 컨테이너를 독립 실행형 파트 파일(".dtsxp" 파일)에 저장하고 제어 흐름 패키지 파트를 사용하여 이 파일을 하나 이상의 패키지에서 여러 번 재사용합니다. 이 재사용 기능으로 인해 SSIS 패키지 디자인 및 유지 관리가 좀 더 간편해집니다.  
  
## <a name="create-a-new-control-flow-package-part"></a>새 제어 흐름 패키지 파트 만들기  
 새 제어 흐름 패키지 파트를 만들려면 솔루션 탐색기에서 **패키지 파트** 폴더를 확장합니다. **제어 흐름** 을 마우스 오른쪽 단추로 클릭하고 **새 제어 흐름 패키지 파트**를 선택합니다.  
  
 ![새 제어 흐름 템플릿 만들기](../integration-services/media/control-flow-templates-create-new.png "새 제어 흐름 템플릿 만들기")  
  
 ".dtsxp" 확장명을 가진 새 파트 파일이 **패키지 파트 | 제어 흐름** 폴더 아래에 생성됩니다. 동시에 SSIS 도구 상자에 같은 이름의 새 항목도 추가됩니다. (도구 상자 항목은 Visual Studio에서 해당 파트를 포함하는 프로젝트가 열려 있는 동안만 볼 수 있습니다.)  
  
 ![도구 상자의 제어 흐름 템플릿](../integration-services/media/control-flow-templates-in-toolbox.png "도구 상자의 제어 흐름 템플릿")  
  
## <a name="design-a-control-flow-package-part"></a>제어 흐름 패키지 파트 디자인  
 패키지 파트 편집기를 열려면 솔루션 탐색기에서 파트 파일을 두 번 클릭합니다. 패키지를 디자인하는 것처럼 파트를 디자인할 수 있습니다.  
  
 ![제어 흐름 템플릿 디자인 1단계](../integration-services/media/control-flow-template-design-step-1.png "제어 흐름 템플릿 디자인 1단계")  
  
 ![제어 흐름 템플릿 디자인 2단계](../integration-services/media/control-flow-template-design-step-2.png "제어 흐름 템플릿 디자인 2단계")  
  
 제어 흐름 패키지 파트에는 다음 제한이 적용됩니다.  
  
-   파트는 최상위 태스크 또는 컨테이너만 가질 수 있습니다. 여러 태스크 또는 컨테이너를 포함하려면 이들을 모두 단일 시퀀스 컨테이너에 넣습니다.  
  
-   파트를 디자이너에서 직접 실행하거나 디버그할 수 없습니다.  
  
## <a name="add-an-existing-control-flow-package-part-to-a-package"></a>패키지에 기존 제어 흐름 패키지 파트 추가  
 현재 Integration Services 프로젝트 또는 다른 프로젝트에 저장된 파트를 재사용할 수 있습니다.  
  
-   현재 프로젝트의 일부인 파트를 재사용하려면 파트를 도구 상자에서 끌어서 놓습니다.  
  
-   다른 프로젝트의 일부인 파트를 재사용하려면 **기존 제어 흐름 패키지 파트 추가** 명령을 사용합니다.  
  
### <a name="drag-and-drop-a-control-flow-package-part"></a>제어 흐름 패키지 파트 끌어서 놓기  
 파트를 프로젝트에 재사용하려면 다른 태스크 또는 컨테이너와 마찬가지로 파트 항목을 도구 상자에서 끌어서 놓습니다. 파트를 패키지에 여러 번 끌어서 놓으면 논리를 패키지의 여러 위치에 재사용할 수 있습니다. 이 방법을 사용하여 현재 프로젝트의 일부인 파트를 재사용합니다.  
  
 ![패키지에 제어 흐름 템플릿 추가](../integration-services/media/control-flow-templates-add-to-package.png "패키지에 제어 흐름 템플릿 추가")  
  
 ![여러 제어 흐름 템플릿이 포함된 패키지](../integration-services/media/control-flow-templates-in-package.png "여러 제어 흐름 템플릿이 포함된 패키지")  
  
 패키지를 저장하는 경우 SSIS 디자이너는 패키지에 파트 인스턴스가 하나라도 있는지 여부를 확인합니다.  
  
-   패키지가 파트 인스턴스를 포함하고 있는 경우 디자이너는 모든 파트 관련 정보를 포함하는 새 dtsx.designer 파일을 생성합니다.  
  
-   패키지가 파트를 사용하지 않는 경우 디자이너는 패키지에 대해 이전에 생성된 .dtsx.designer 파일(즉, 패키지와 같은 이름을 가진 .dtsx.designer 파일)을 삭제합니다.  
  
 ![제어 흐름 템플릿이 있는 솔루션 탐색기](../integration-services/media/control-flow-templates-in-solution-explorer.png "제어 흐름 템플릿이 있는 솔루션 탐색기")  
  
### <a name="add-a-copy-of-an-existing-control-flow-package-part-or-a-reference-to-an-existing-part"></a>기존 제어 흐름 패키지 파트 또는 기존 파트에 대한 참조의 복사본 추가  
 파일 시스템의 기존 파트의 복사본을 패키지에 추가하려면 솔루션 탐색기에서 **패키지 파트** 폴더를 확장합니다. **제어 흐름** 을 마우스 오른쪽 단추로 클릭하고 **기존 제어 흐름 패키지 파트 추가**를 선택합니다.  
  
 ![메뉴에서 새 제어 흐름 템플릿 추가](../integration-services/media/control-flow-templates-add-from-menu.png "메뉴에서 새 제어 흐름 템플릿 추가")  
  
 ![기존 템플릿 복사본 추가 대화 상자](../integration-services/media/control-flow-templates-add-copy-dialog.png "기존 템플릿 복사본 추가 대화 상자")  
  
 **옵션**  
  
 **패키지 파트 경로**  
 파트 파일에 대한 경로를 입력하거나 찾아보기 단추(...)를 클릭하고 복사하거나 참조할 파트 파일을 찾습니다.  
  
 **참조로 추가**  
 -   선택된 경우 파트는 Integration Services 프로젝트에 참조로 추가됩니다. 여러 Integration Services 프로젝트에서 파트 파일의 단일 복사본을 참조하려는 경우 이 옵션을 선택합니다.  
  
-   선택을 취소하면 파트 파일의 복사본이 프로젝트에 추가됩니다.  
  
## <a name="configure-a-control-flow-package-part"></a>제어 흐름 패키지 파트 구성  
 제어 흐름 패키지 파트를 패키지의 제어 흐름에 추가한 후 구성하려면 **패키지 파트 구성**  대화 상자를 사용합니다.  
  
#### <a name="to-open-the-package-part-configuration-dialog-box"></a>패키지 파트 구성 대화 상자를 열려면  
  
1.  파트 인스턴스를 구성하려면 제어 흐름에서 파트 인스턴스를 두 번 클릭합니다. 또는 파트 인스턴스를 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다. **패키지 파트 구성** 대화 상자가 열립니다.  
  
2.  파트 인스턴스에 대해 속성 및 연결 관리자를 구성합니다.  
  
### <a name="properties-tab"></a>속성 탭  
 **패키지 파트 구성** 대화 상자의 **속성**  탭을 사용하여 파트의 속성을 지정합니다.  
  
 ![템플릿 구성 대화 상자의 속성 탭](../integration-services/media/template-configuration-properties-tab.png "템플릿 구성 대화 상자의 속성 탭")  
  
 왼쪽 창의 트리 보기 계층에 파트 인스턴스의 모든 구성 가능 속성이 나열됩니다.  
  
-   선택을 취소한 경우 파트 인스턴스에 속성이 구성되지 않습니다. 파트 인스턴스는 제어 흐름 패키지 파트에 정의된 속성에 대한 기본값을 사용합니다.  
  
-   선택된 경우 입력하거나 선택하는 값이 기본값을 재정의합니다.  
  
 오른쪽 창의 테이블에 구성할 속성이 나열됩니다.  
  
-   **속성 경로**. 속성의 속성 경로입니다.  
  
-   **속성 유형**. 속성의 데이터 형식.  
  
-   **값**. 구성된 값입니다. 이 값은 기본값을 재정의합니다.  
  
### <a name="connection-managers-tab"></a>연결 관리자 탭  
 **패키지 파트 구성** 대화 상자의 **연결 관리자**  탭을 사용하여 파트 인스턴스에 대한 연결 관리자의 속성을 지정합니다.  
  
 ![템플릿 구성 대화 상자의 연결 관리자 탭](../integration-services/media/template-configuration-connection-managers-tab.png "템플릿 구성 대화 상자의 연결 관리자 탭")  
  
 왼쪽 창의 테이블에 제어 흐름 파트에 정의된 모든 연결 관리자가 나열됩니다. 구성하려는 연결 관리자를 선택합니다.  
  
 오른쪽 창의 목록에 선택된 연결 관리자의 속성이 나열됩니다.  
  
-   **설정**. 파트 인스턴스에 대한 속성이 구성된 경우 선택됩니다.  
  
-   **속성 이름**. 속성의 이름입니다.  
  
-   **값**. 구성된 값입니다. 이 값은 기본값을 재정의합니다.  
  
## <a name="delete-a-control-flow-part"></a>제어 흐름 파트 삭제  
 파트를 삭제하려면 솔루션 탐색기에서 파트를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 선택합니다. 삭제를 확인하려면 **확인** 을 선택하고 파트를 유지하려면 **취소** 를 선택합니다.  
  
 프로젝트에서 파트를 삭제하는 경우 해당 파트는 파일 시스템에서 영구적으로 삭제되며 복원할 수 없습니다.  
  
> [!NOTE]  
>  Integration Services 프로젝트에서 파트를 제거하지만 이 파트를 다른 프로젝트에 계속 사용하려는 경우 **삭제**  옵션 대신 **프로젝트에서 제외** 옵션을 사용합니다.  
  
## <a name="package-parts-are-a-design-time-feature-only"></a>패키지 파트는 디자인 타임 전용 기능  
 패키지 파트는 디자인 타임 전용 기능입니다. SSIS 디자이너가 파트를 만들고, 열고, 저장 및 업데이트하며 패키지의 파트 인스턴스를 추가, 구성 또는 삭제합니다. 그러나 SSIS 런타임은 파트를 인식하지 않습니다. 다음은 디자이너가 이 분리를 달성하는 방법입니다.  
  
-   디자이너는 패키지 파트 인스턴스를 해당 구성된 속성과 함께 ".dtsx.designer" 파일에 저장합니다.  
  
-   디자이너가 ".dtsx.designer" 파일을 저장할 때에는 이 파일이 참조하는 파트에서 콘텐츠를 추출하고 패키지의 파트 인스턴스를 파트의 콘텐츠로 바꿉니다.  
  
-   마지막으로 더 이상 파트 정보를 포함하지 않은 모든 콘텐츠를 ".dtsx" 패키지 파일에 다시 저장합니다. 이는 SSIS 런타임이 실행하는 파일입니다.  
  
 아래 다이어그램은 파트(".dtsxp" 파일), SSIS 디자이너 및 SSIS 런타임 간의 관계를 보여 줍니다.  
  
 ![제어 흐름 템플릿 파일 및 흐름](../integration-services/media/control-flow-templates-intro.png "제어 흐름 템플릿 파일 및 흐름")  
  
  
