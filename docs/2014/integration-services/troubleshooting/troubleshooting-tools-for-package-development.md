---
title: 패키지 배포 문제 해결 도구 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 41dd248c-dab3-4318-b8ba-789a42d5c00c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4e1935b7ffa0acc22183f91cf5c7fe3896c9e1a3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792104"
---
# <a name="troubleshooting-tools-for-package-development"></a>패키지 배포 문제 해결 도구
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 개발하면서 패키지의 문제를 해결하는 데 사용할 수 있는 기능 및 도구를 제공합니다.  
  
## <a name="troubleshooting-design-time-validation-issues"></a>디자인 타임 유효성 검사 문제 해결  
 현재 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 패키지를 열면 모든 데이터 흐름 구성 요소와 모든 연결에 대해 차례로 유효성 검사가 실행되고, 느리거나 오프라인으로 작업에 사용할 수 없는 연결이 설정됩니다. 이로써 패키지 데이터 흐름의 유효성 검사가 지연되는 것을 줄일 수 있습니다.  
  
 패키지가 열리면 **연결 관리자** 영역에서 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **오프라인으로 작업**을 클릭하여 연결을 해제할 수도 있습니다. 이를 통해 SSIS 디자이너에서 작업 속도를 높일 수 있습니다.  
  
 오프라인으로 작업하도록 설정된 작업은 사용자가 다음 중 하나를 수행할 때까지 오프라인으로 유지됩니다.  
  
-   SSIS 디자이너의 **연결 관리자** 영역에서 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **테스트 연결**을 클릭하여 연결을 테스트합니다.  
  
     예를 들어, 패키지가 열릴 때 처음에는 연결이 오프라인으로 작업하도록 설정됩니다. 연결 문자열을 수정하여 이 문제를 해결하고 **테스트 연결** 을 클릭하여 연결을 테스트합니다.  
  
-   패키지를 다시 열거나 패키지가 들어 있는 프로젝트를 엽니다. 패키지의 모든 연결에 대해 유효성 검사가 다시 실행됩니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 유효성 검사 오류를 방지하는 데 도움이 되는 다음과 같은 추가 기능이 있습니다.  
  
-   **데이터 원본을 사용할 수 없을 때 오프라인으로 작업하도록 모든 패키지와 모든 연결을 설정합니다**. **SSIS** 메뉴에서 **오프라인으로 작업** 을 사용하도록 설정할 수 있습니다. 달리 합니다 `DelayValidation` 속성을 **오프 라인으로 작업** 옵션은 패키지를 열기 전에 사용할 수. 또한 **오프라인으로 작업** 을 설정하여 디자이너에서의 작업 속도를 높이고, 패키지의 유효성을 검사하려는 경우에만 이 옵션을 해제할 수도 있습니다.  
  
-   **런타임까지 유효하지 않은 패키지 요소에 대해 DelayValidation 속성을 구성합니다**. 디자인 타임에는 구성이 유효하지 않은 패키지 요소의 `DelayValidation`을 `True`로 설정하여 유효성 검사 오류를 방지할 수 있습니다. 예를 들어 런타임에 SQL 실행 작업을 통해 테이블이 만들어지기 전까지는 존재하지 않는 대상 테이블을 사용하는 데이터 흐름 태스크가 있을 수 있습니다. `DelayValidation` 속성은 패키지 수준 또는 패키지에 포함된 개별 태스크 및 컨테이너 수준에서 설정할 수 있습니다. 일반적으로 패키지를 배포할 때는 동일한 패키지 요소에서 이 속성을 `True`로 설정해야 런타임에 동일한 유효성 검사 오류를 방지할 수 있습니다.  
  
     `DelayValidation` 속성은 데이터 흐름 태스크에만 설정할 수 있고 개별 데이터 흐름 구성 요소에는 설정할 수 없습니다. 개별 데이터 흐름 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 속성을 `false`로 설정하면 비슷한 효과를 얻을 수 있습니다. 그러나 이 속성 값이 `false`이면 구성 요소에서 외부 데이터 원본의 메타데이터에 대한 변경 내용을 인식하지 못하게 됩니다.  
  
 유효성 검사가 발생할 때 패키지에서 사용하는 데이터베이스 개체가 잠기면 유효성 검사 프로세스가 응답하지 않을 수 있습니다. 이 경우 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너도 응답하지 않습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 연관된 세션을 닫으면 유효성 검사를 다시 시작할 수 있습니다. 또한 이 섹션에서 설명하는 설정을 사용하면 이러한 문제를 방지할 수 있습니다.  
  
## <a name="troubleshooting-control-flow"></a>제어 흐름 문제 해결  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지 개발 과정에서 패키지의 제어 흐름 문제를 해결하는 데 사용할 수 있는 다음 기능 및 도구를 제공합니다.  
  
-   **태스크, 컨테이너 및 패키지에 중단점을 설정할 수 있습니다**. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너가 제공하는 그래픽 도구를 사용하여 중단점을 설정할 수 있습니다. 중단점은 패키지 수준 또는 패키지에 포함된 개별 태스크 및 컨테이너 수준에서 설정할 수 있습니다. 일부 태스크 및 컨테이너에는 중단점 설정을 위한 추가 중단 조건이 포함되어 있습니다. 예를 들어 반복되는 각 루프가 시작될 때 실행을 일시 중지하도록 For 루프 컨테이너에 중단 조건을 설정할 수 있습니다.  
  
-   **디버깅 창을 사용할 수 있습니다**. 중단점이 있는 패키지를 실행할 때 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 디버그 창에서 변수 값 및 상태 메시지에 액세스할 수 있습니다.  
  
-   **진행률 탭에서 정보를 검토할 수 있습니다**. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 실행할 때 제어 흐름에 대한 추가 정보를 제공합니다. 진행률 탭에는 태스크와 컨테이너가 실행 순서대로 나열되며 패키지 자체를 포함하여 각 태스크 및 컨테이너에 대한 시작 및 종료 시간, 경고 및 오류 메시지가 표시됩니다.  
  
 이러한 기능에 대한 자세한 내용은 [Debugging Control Flow](debugging-control-flow.md)을 참조하십시오.  
  
## <a name="troubleshooting-data-flow"></a>데이터 흐름 문제 해결  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지 개발 과정에서 패키지의 데이터 흐름 문제를 해결하는 데 사용할 수 있는 다음 기능 및 도구를 제공합니다.  
  
-   **데이터의 하위 집합만 테스트할 수 있습니다**. 데이터 세트 예제만 사용하여 패키지에 있는 데이터 흐름의 문제를 해결하려면 비율 샘플링 또는 행 샘플링 변환을 포함시켜 실행 시 인라인 데이터 예제를 만들도록 할 수 있습니다. 자세한 내용은 [Percentage Sampling Transformation](../data-flow/transformations/percentage-sampling-transformation.md) 및 [Row Sampling Transformation](../data-flow/transformations/row-sampling-transformation.md)를 참조하세요.  
  
-   **데이터 뷰어를 사용하여 데이터가 데이터 흐름을 통해 이동할 때 데이터를 모니터링할 수 있습니다**. 데이터 뷰어는 데이터가 원본, 변환 및 대상 사이를 이동할 때의 데이터 값을 표시합니다. 데이터 뷰어는 표에 데이터를 표시할 수 있습니다. 데이터를 데이터 뷰어에서 클립보드로 복사한 다음 데이터를 파일 또는 엑셀 스프레드시트로 붙여넣을 수 있습니다. 자세한 내용은 [데이터 흐름에 데이터 뷰어 추가](../add-a-data-viewer-to-a-data-flow.md)를 참조하세요.  
  
-   **오류 출력을 지원하는 데이터 흐름 구성 요소에 오류 출력을 구성할 수 있습니다**. 여러 데이터 흐름 원본, 변환 및 대상은 오류 출력을 지원합니다. 데이터 흐름 구성 요소의 오류 출력을 구성하면 오류가 있는 데이터를 다른 대상으로 보낼 수 있습니다. 예를 들어 오류가 있거나 잘린 데이터를 별개의 텍스트 파일로 캡처할 수 있습니다. 오류 출력에 데이터 뷰어를 연결하고 오류 데이터만 검사할 수도 있습니다. 디자인 타임에 오류 출력을 통해 문제가 있는 데이터 값을 캡처하면 실제 데이터를 효과적으로 다루는 패키지를 개발하는 데 도움이 됩니다. 그러나 다른 문제 해결 도구 및 기능이 디자인 타임에만 유용한 것과 달리 오류 출력은 프로덕션 환경에서도 유용할 수 있습니다. 자세한 내용은 [데이터 오류 처리](../data-flow/error-handling-in-data.md)를 참조하세요.  
  
-   **처리되는 행 개수를 캡처할 수 있습니다**. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지를 실행할 때 경로를 통해 전달한 행 개수는 데이터 흐름 디자이너에 표시됩니다. 데이터가 경로를 통해 이동하는 동안 이 개수는 주기적으로 업데이트됩니다. 또한 행 개수 변환을 데이터 흐름에 추가하여 변수에서 마지막 행 개수를 캡처할 수 있습니다. 자세한 내용은 [Row Count Transformation](../data-flow/transformations/row-count-transformation.md)을(를) 참조하세요.  
  
-   **진행률 탭에서 정보를 검토할 수 있습니다**. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 실행할 때 데이터 흐름에 대한 추가 정보를 제공합니다. 진행률 탭에는 데이터 흐름 구성 요소가 실행 순서대로 나열되며 패키지의 각 단계에 대한 진행률이 백분율로 표시되고 대상에 기록된 행 개수도 표시됩니다.  
  
 이러한 기능에 대한 자세한 내용은 [Debugging Data Flow](debugging-data-flow.md)을 참조하십시오.  
  
## <a name="troubleshooting-scripts"></a>스크립트 문제 해결  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA(Tools for Applications)는 스크립트 태스크 및 스크립트 구성 요소가 사용하는 스크립트를 작성하는 개발 환경입니다. VSTA는 패키지 개발 과정에서 스크립트 문제를 해결하는 데 사용할 수 있는 다음 기능 및 도구를 제공합니다.  
  
-   **스크립트 태스크의 스크립트에 중단점을 설정할 수 있습니다.** VSTA는 스크립트 태스크의 스크립트에 대해서만 디버깅을 지원합니다. 스크립트 태스크에서 설정한 중단점은 패키지와 패키지의 태스크 및 컨테이너에서 설정한 중단점과 통합되므로 모든 패키지 요소를 완벽하게 디버깅할 수 있습니다.  
  
    > [!NOTE]  
    >  스크립트 태스크가 여러 개 포함된 패키지를 디버깅할 경우 한 개의 스크립트 태스크에서만 디버거가 중단점에 도달하며 다른 스크립트 태스크에서는 중단점이 무시됩니다. 스크립트 태스크가 Foreach 루프 또는 For 루프 컨테이너의 일부일 경우 디버거는 루프의 첫 번째 반복 뒤에 있는 스크립트 태스크의 중단점을 무시합니다.  
  
 자세한 내용은 [Debugging Script](debugging-script.md)을(를) 참조하세요. 스크립트 구성 요소를 디버깅 하는 방법에 대 한 제안 사항이 있는 경우 참조 [코딩 and Debugging the Script Component] (.. / extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md 합니다.  
  
## <a name="troubleshooting-errors-without-a-description"></a>설명이 없는 오류 문제 해결  
 패키지 개발 과정에서 설명이 없는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류 번호가 발생할 경우 [Integration Services 오류 및 메시지 참조](../integration-services-error-and-message-reference.md)에서 해당 설명을 찾을 수 있습니다. 이 목록에는 현재 문제 해결 정보는 들어 있지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [패키지 실행 문제 해결 도구](troubleshooting-tools-for-package-execution.md)   
 [데이터 흐름 성능 기능](../data-flow/data-flow-performance-features.md)  
  
  
