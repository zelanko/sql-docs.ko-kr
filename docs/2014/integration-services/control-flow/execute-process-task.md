---
title: 프로세스 실행 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.f1
helpviewer_keywords:
- Execute Process task [Integration Services]
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 229a5f6b5a0194f7bd815077274a4e7f97a21185
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433460"
---
# <a name="execute-process-task"></a>프로세스 실행 태스크
  프로세스 실행 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 워크플로의 일부로 애플리케이션이나 배치 파일을 실행합니다. 프로세스 실행 태스크를 사용하여 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 또는 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]와 같은 모든 표준 애플리케이션을 열 수 있지만 이 태스크는 일반적으로 데이터 원본에 대해 작동하는 비즈니스 애플리케이션이나 배치 파일을 실행하는 데 사용됩니다. 예를 들어 프로세스 실행 태스크를 사용하여 압축된 텍스트 파일을 확장할 수 있습니다. 패키지는 이 텍스트 파일을 패키지의 데이터 흐름에 대한 데이터 원본으로 사용할 수 있습니다. 예를 들어 프로세스 실행 태스크를 사용하여 일일 판매 보고서를 생성하는 사용자 지정 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 애플리케이션을 실행할 수도 있습니다. 그런 다음 이 보고서를 메일 보내기 태스크에 첨부하여 메일 그룹에 전달할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 패키지 실행과 같은 워크플로 태스크를 수행하는 기타 태스크가 있습니다. 자세한 내용은 [Execute Package Task](execute-package-task.md)를 참조하세요.  
  
## <a name="custom-log-entries-available-on-the-execute-process-task"></a>프로세스 실행 태스크에 사용할 수 있는 사용자 지정 로그 항목  
 다음 표에서는 프로세스 실행 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md) 및 [로깅할 메시지 사용자 지정](../custom-messages-for-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|태스크에서 실행하도록 구성할 프로세스에 대한 정보를 제공합니다.<br /><br /> 두 개의 로그 항목이 기록됩니다. 한 항목에는 태스크가 실행하는 실행 파일의 이름과 위치에 대한 정보가 들어 있고 다른 항목은 실행 파일의 종료를 기록합니다.|  
|`ExecuteProcessVariableRouting`|실행 파일의 입력 및 출력으로 라우팅되는 변수에 대한 정보를 제공합니다. stdin(입력), stdout(출력) 및 stderr(오류 출력)에 대한 로그 항목이 기록됩니다.|  
  
## <a name="configuration-of-the-execute-process-task"></a>프로세스 실행 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [프로세스 실행 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [프로세스 실행 태스크 편집기&#40;프로세스 페이지&#41;](../execute-process-task-editor-process-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="property-settings"></a>속성 설정  
 프로세스 실행 태스크는 사용자 지정 애플리케이션을 실행할 때 다음 방법 중 하나 또는 모두를 통해 애플리케이션에 입력을 제공합니다.  
  
-   **StandardInputVariable** 속성 설정에서 지정하는 변수. 변수에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../use-variables-in-packages.md)을 참조하세요.  
  
-   **Arguments** 속성 설정에서 지정하는 인수. 예를 들어 태스크가 Word 문서를 여는 경우 인수에서 .doc 파일의 이름을 지정할 수 있습니다.  
  
 하나의 프로세스 실행 태스크에 있는 사용자 지정 애플리케이션에 여러 인수를 전달하려면 공백으로 인수를 구분합니다. 인수는 공백을 포함할 수 없습니다. 공백을 포함하는 경우 태스크가 실행되지 않습니다. 변수 값을 인수로 전달하는 식을 사용할 수 있습니다. 다음 예에서는 식이 두 변수 값을 인수로 전달하고 공백을 사용하여 인수를 구분합니다.  
  
 `@variable1 + " " + @variable2`  
  
 여러 프로세스 실행 태스크 속성을 설정하는 식을 사용할 수 있습니다.  
  
 **Standardinputvariable** 속성을 사용 하 여 프로세스 실행 태스크에서 입력을 제공 하도록 구성 하는 경우 `Console.ReadLine` 응용 프로그램에서 메서드를 호출 하 여 입력을 읽습니다. 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스 라이브러리의 [Console.ReadLine 메서드](https://go.microsoft.com/fwlink/?LinkId=129201) 토픽을 참조하세요.  
  
 **Arguments** 속성을 사용하여 프로세스 실행 태스크에서 입력을 제공하도록 구성하는 경우 다음 단계 중 하나를 수행하여 인수를 얻습니다.  
  
-   Microsoft Visual Basic을 사용하여 애플리케이션을 작성하는 경우 `My.Application.CommandLineArgs` 속성을 설정합니다. 다음 예에서는 `My.Application.CommandLineArgs` 속성을 설정하여 두 인수를 검색합니다.  
  
    ```  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     자세한 내용은 [참조에서](https://go.microsoft.com/fwlink/?LinkId=129200)My.Application.CommandLineArgs 속성 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 항목을 참조하십시오.  
  
-   Microsoft Visual C#을 사용하여 응용 프로그램을 작성하는 경우 `Main` 메서드를 사용합니다.  
  
     자세한 내용은 C# 프로그래밍 가이드의 [명령줄 인수(C# 프로그래밍 가이드)](https://go.microsoft.com/fwlink/?LinkId=129406)항목을 참조하세요.  
  
 프로세스 실행 태스크에는 각각 애플리케이션의 표준 출력과 애플리케이션 표준 오류 출력을 사용하는 변수를 지정하는 **StandardOutputVariable** 및 **StandardErrorVariable** 속성도 있습니다.  
  
 또한 프로세스 실행 태스크를 구성하여 작업 디렉터리, 제한 시간 경과 또는 실행 파일이 성공적으로 실행되었음을 나타내는 값을 지정할 수 있습니다. 실행 파일의 반환 코드가 성공을 나타내는 값과 일치하지 않거나 지정한 위치에 실행 파일이 없을 경우 태스크가 실패하도록 구성할 수도 있습니다.  
  
## <a name="programmatic-configuration-of-the-execute-process-task"></a>프로세스 실행 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## <a name="see-also"></a>참고 항목  
 [작업 Integration Services](integration-services-tasks.md)   
 [제어 흐름](control-flow.md)  
  
  
