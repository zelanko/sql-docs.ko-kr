---
title: "프로세스 실행 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.executeprocesstask.f1
- sql13.dts.designer.executeprocesstask.general.f1
- sql13.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process task [Integration Services]
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 76ea783edab9673a720d5b95883caffff9d9a4d7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="execute-process-task"></a>프로세스 실행 태스크
  프로세스 실행 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 워크플로의 일부로 응용 프로그램이나 배치 파일을 실행합니다. 프로세스 실행 태스크를 사용하여 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 또는 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]와 같은 모든 표준 응용 프로그램을 열 수 있지만 이 태스크는 일반적으로 데이터 원본에 대해 작동하는 비즈니스 응용 프로그램이나 배치 파일을 실행하는 데 사용됩니다. 예를 들어 프로세스 실행 태스크를 사용하여 압축된 텍스트 파일을 확장할 수 있습니다. 패키지는 이 텍스트 파일을 패키지의 데이터 흐름에 대한 데이터 원본으로 사용할 수 있습니다. 예를 들어 프로세스 실행 태스크를 사용하여 일일 판매 보고서를 생성하는 사용자 지정 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 응용 프로그램을 실행할 수도 있습니다. 그런 다음 이 보고서를 메일 보내기 태스크에 첨부하여 메일 그룹에 전달할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 패키지 실행과 같은 워크플로 태스크를 수행하는 기타 태스크가 있습니다. 자세한 내용은 [Execute Package Task](../../integration-services/control-flow/execute-package-task.md)를 참조하세요.  
  
## <a name="custom-log-entries-available-on-the-execute-process-task"></a>프로세스 실행 태스크에 사용할 수 있는 사용자 지정 로그 항목  
 다음 표에서는 프로세스 실행 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|태스크에서 실행하도록 구성할 프로세스에 대한 정보를 제공합니다.<br /><br /> 두 개의 로그 항목이 기록됩니다. 한 항목에는 태스크가 실행하는 실행 파일의 이름과 위치에 대한 정보가 들어 있고 다른 항목은 실행 파일의 종료를 기록합니다.|  
|**ExecuteProcessVariableRouting**|실행 파일의 입력 및 출력으로 라우팅되는 변수에 대한 정보를 제공합니다. stdin(입력), stdout(출력) 및 stderr(오류 출력)에 대한 로그 항목이 기록됩니다.|  
  
## <a name="configuration-of-the-execute-process-task"></a>프로세스 실행 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="property-settings"></a>속성 설정  
 프로세스 실행 태스크는 사용자 지정 응용 프로그램을 실행할 때 다음 방법 중 하나 또는 모두를 통해 응용 프로그램에 입력을 제공합니다.  
  
-   **StandardInputVariable** 속성 설정에서 지정하는 변수. 변수에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)을 참조하세요.  
  
-   **Arguments** 속성 설정에서 지정하는 인수. 예를 들어 태스크가 Word 문서를 여는 경우 인수에서 .doc 파일의 이름을 지정할 수 있습니다.  
  
 하나의 프로세스 실행 태스크에 있는 사용자 지정 응용 프로그램에 여러 인수를 전달하려면 공백으로 인수를 구분합니다. 인수는 공백을 포함할 수 없습니다. 공백을 포함하는 경우 태스크가 실행되지 않습니다. 변수 값을 인수로 전달하는 식을 사용할 수 있습니다. 다음 예에서는 식이 두 변수 값을 인수로 전달하고 공백을 사용하여 인수를 구분합니다.  
  
 `@variable1 + " " + @variable2`  
  
 여러 프로세스 실행 태스크 속성을 설정하는 식을 사용할 수 있습니다.  
  
 **StandardInputVariable** 속성을 사용하여 프로세스 실행 태스크에서 입력을 제공하도록 구성하는 경우 응용 프로그램에서 **Console.ReadLine** 메서드를 호출하여 입력을 읽습니다. 자세한 내용은 [Console.ReadLine 메서드](http://go.microsoft.com/fwlink/?LinkId=129201)클래스 라이브러리의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 항목을 참조하세요.  
  
 **Arguments** 속성을 사용하여 프로세스 실행 태스크에서 입력을 제공하도록 구성하는 경우 다음 단계 중 하나를 수행하여 인수를 얻습니다.  
  
-   Microsoft Visual Basic을 사용하여 응용 프로그램을 작성하는 경우 **My.Application.CommandLineArgs** 속성을 설정합니다. 다음 예에서는 **My.Application.CommandLineArgs** 속성을 설정하여 두 인수를 검색합니다.  
  
    ```vb  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     자세한 내용은 [참조에서](http://go.microsoft.com/fwlink/?LinkId=129200)My.Application.CommandLineArgs 속성 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 항목을 참조하십시오.  
  
-   Microsoft Visual C#을 사용하여 응용 프로그램을 작성하는 경우 **Main** 메서드를 사용합니다.  
  
     자세한 내용은 C# 프로그래밍 가이드의 [명령줄 인수(C# 프로그래밍 가이드)](http://go.microsoft.com/fwlink/?LinkId=129406)항목을 참조하세요.  
  
 프로세스 실행 태스크에는 각각 응용 프로그램의 표준 출력과 응용 프로그램 표준 오류 출력을 사용하는 변수를 지정하는 **StandardOutputVariable** 및 **StandardErrorVariable** 속성도 있습니다.  
  
 또한 프로세스 실행 태스크를 구성하여 작업 디렉터리, 제한 시간 경과 또는 실행 파일이 성공적으로 실행되었음을 나타내는 값을 지정할 수 있습니다. 실행 파일의 반환 코드가 성공을 나타내는 값과 일치하지 않거나 지정한 위치에 실행 파일이 없을 경우 태스크가 실패하도록 구성할 수도 있습니다.  
  
## <a name="programmatic-configuration-of-the-execute-process-task"></a>프로세스 실행 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## <a name="execute-process-task-editor-general-page"></a>프로세스 실행 태스크 편집기(일반 페이지)
  **프로세스 실행 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 프로세스 실행 태스크를 명명 및 설명할 수 있습니다.  
  
### <a name="options"></a>변수  
 **이름**  
 프로세스 실행 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 프로세스 실행 태스크에 대한 설명을 입력합니다.  
  
## <a name="execute-process-task-editor-process-page"></a>프로세스 실행 태스크 편집기(프로세스 페이지)
  **프로세스 실행 태스크 편집기** 대화 상자의 **프로세스** 페이지를 사용하여 프로세스 실행 옵션을 구성할 수 있습니다. 이러한 옵션에는 실행할 실행 파일, 해당 위치, 명령 프롬프트 인수, 입력 제공 및 출력 캡처 변수가 포함됩니다.  
  
### <a name="options"></a>변수  
 **RequireFullFileName**  
 지정한 위치에 실행 파일이 없는 경우 태스크 실패 여부를 나타냅니다.  
  
 **실행 파일**  
 실행할 실행 파일 이름을 입력합니다.  
  
 **인수**  
 명령 프롬프트 인수를 제공합니다.  
  
 **WorkingDirectory**  
 실행 파일이 들어 있는 폴더의 경로를 입력하거나 찾아보기 단추 **(...)** 를 클릭하고 해당 폴더를 찾습니다.  
  
 **StandardInputVariable**  
 프로세스에 입력을 제공할 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **StandardOutputVariable**  
 프로세스 출력을 캡처할 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **StandardErrorVariable**  
 프로세서의 오류 출력을 캡처할 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 프로세스 종료 코드가 **SuccessValue**에 지정한 값과 다른 경우 태스크 실패 여부를 나타냅니다.  
  
 **SuccessValue**  
 성공을 표시하기 위해 실행 파일에서 반환하는 값을 지정합니다. 기본적으로 이 값은 **0**으로 설정됩니다.  
  
 **TimeOut**  
 프로세스가 실행될 수 있는 시간(초)을 지정합니다. 값 **0** 은 제한 시간 값이 사용되지 않으며 프로세스가 완료되거나 오류가 발생할 때까지 실행됨을 나타냅니다.  
  
 **TerminateProcessAfterTimeOut**  
 **TimeOut** 옵션에 지정한 제한 시간 후의 프로세스 강제 종료 여부를 나타냅니다. 이 옵션은 **TimeOut** 이 **0**이 아닌 경우에만 사용할 수 있습니다.  
  
 **WindowStyle**  
 프로세스를 실행할 창 스타일을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  
