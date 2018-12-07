---
title: 메시지 큐 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.messagequeuetask.f1
- sql13.dts.designer.msgqueuetask.general.f1
- sql13.dts.designer.msgqueuetask.send.f1
- sql13.dts.designer.msgqueuetask.receive.f1
- sql13.dts.designer.selectvariables.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d100819807cd669803ef698d4614373b0b997905
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52503989"
---
# <a name="message-queue-task"></a>Message Queue Task
  메시지 큐 태스크에서는 MSMQ(메시지 큐)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 간에 메시지를 보내고 받거나 사용자 지정 응용 프로그램에서 처리되는 응용 프로그램 큐에 메시지를 보낼 수 있습니다. 이러한 메시지는 단순한 텍스트, 파일 또는 변수와 해당 값의 형태로 사용될 수 있습니다.  
  
 메시지 큐 태스크를 사용하면 회사 전반의 작업을 조정할 수 있습니다. 대상이 없거나 사용 중인 경우에는 메시지를 큐에 저장하고 다음에 배달할 수 있습니다. 예를 들어 네트워크에 연결될 때 메시지를 받는 판매 영업 직원의 랩톱 컴퓨터가 오프라인인 경우 이 태스크는 메시지를 큐에 저장할 수 있습니다. 메시지 큐 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   다른 패키지가 체크 인될 때까지 태스크 실행이 지연됩니다. 예를 들어 메시지 큐 태스크는 각 소매점 사이트에서 일일 관리가 끝난 후 회사 컴퓨터에 메시지를 보냅니다. 회사 컴퓨터에서 실행되는 패키지에는 특정 소매점 사이트의 메시지를 대기 중인 메시지 큐 태스크가 있습니다. 소매점 사이트의 메시지가 도착하면 태스크가 해당 사이트의 데이터를 업로드합니다. 모든 사이트가 체크 인된 다음에는 패키지가 요약 합계를 계산합니다.  
  
-   데이터 파일을 처리 컴퓨터로 보냅니다. 예를 들어 한 식당에 있는 현금 등록기의 출력을 회사 급여 시스템에 데이터 파일 메시지로 보내서 각 웨이터의 팁에 대한 데이터를 추출할 수 있습니다.  
  
-   회사 전체에 파일을 배포합니다. 예를 들어 패키지는 메시지 큐 태스크를 사용하여 패키지 파일을 다른 컴퓨터에 보낼 수 있습니다. 대상 컴퓨터에서 실행 중인 패키지는 메시지 큐 태스크를 사용하여 패키지를 로컬로 검색하고 저장합니다.  
  
 메시지를 보내거나 받을 때 메시지 큐 태스크는 데이터 파일, 문자열, 변수에 대한 문자열 메시지 또는 변수 중 하나의 메시지 유형을 사용합니다. 변수에 대한 문자열 메시지의 메시지 유형은 메시지를 받을 때만 사용할 수 있습니다.  
  
 이 태스크는 MSMQ 연결 관리자를 사용하여 메시지 큐에 연결합니다. 자세한 내용은 [MSMQ 연결 관리자](../../integration-services/connection-manager/msmq-connection-manager.md)를 참조하세요. 메시지 큐에 대한 자세한 내용은 [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=7022)를 참조하십시오.  
  
 메시지 큐 태스크를 사용하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 설치되어 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 **설치할 구성 요소** 페이지 또는 **기능 선택** 페이지에서 선택하여 설치할 수 있는 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소의 일부 하위 집합을 설치합니다. 이러한 구성 요소는 특정 태스크에 유용하지만 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 기능은 제한됩니다. 예를 들어 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 옵션을 선택하면 패키지 디자인에 필요한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소가 설치되지만 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 설치되지 않기 때문에 메시지 큐 태스크가 작동하지 않습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 전체 설치하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 설치할 구성 요소 **페이지에서** 를 선택해야 합니다. 메시지 큐 태스크 설치 및 실행에 대한 자세한 내용은 [Integration Services 설치](../../integration-services/install-windows/install-integration-services.md)를 참조하세요.  
  
> [!NOTE]  
>  컴퓨터의 운영 체제가 FIPS 모드에서 구성되고 태스크에서 암호화를 사용하는 경우 메시지 큐 태스크는 FIPS(Federal Information Processing Standard) 140-2와 호환되지 않습니다. 메시지 큐 태스크에서 암호화를 사용하지 않는 경우에는 태스크가 성공적으로 실행됩니다.  
  
## <a name="message-types"></a>메시지 유형  
 메시지 큐 태스크에서 제공하는 메시지 유형을 다음과 같은 방법으로 구성할 수 있습니다.  
  
-   **Data file** 메시지는 파일에 메시지가 포함되도록 지정합니다. 메시지를 받을 때 파일을 저장하고, 기존 파일을 덮어쓰고, 메시지를 받을 수 있는 태스크의 패키지를 지정하도록 태스크를 구성할 수 있습니다.  
  
-   **String** 메시지는 메시지를 문자열로 지정합니다. 메시지를 받을 때 받은 문자열을 사용자 정의 문자열과 비교하고 비교 결과에 따라 동작을 취하도록 태스크를 구성할 수 있습니다. 문자열 비교 시에는 전체 문자열 일치 및 대/소문자 구분 여부를 지정하거나 하위 문자열을 사용할 수 있습니다.  
  
-   **String message to variable** 은 원본 메시지를 대상 변수에 전송되는 문자열로 지정합니다. 전체 문자열 일치, 대/소문자 구분 또는 하위 문자열 비교를 사용하여 받은 문자열을 사용자 정의 문자열과 비교하도록 태스크를 구성할 수 있습니다. 이 메시지 유형은 태스크에서 메시지를 받는 경우에만 사용할 수 있습니다.  
  
-   **Variable** 은 메시지에 하나 이상의 변수가 포함되도록 지정합니다. 메시지에 포함된 변수 이름을 지정하도록 메시지를 구성할 수 있습니다. 메시지를 받을 때 메시지를 받아올 패키지와 메시지의 대상인 변수를 모두 지정하도록 태스크를 구성할 수 있습니다.  
  
## <a name="sending-messages"></a>메시지 보내기  
 메시지 큐 태스크에서 메시지를 보내도록 구성할 경우 메시지 큐 기술이 현재 지원하는 RC2 및 RC4 암호화 알고리즘 중 하나를 사용하여 메시지를 암호화할 수 있습니다. 이 두 암호화 알고리즘은 현재 메시지 큐 기술에서 지원하지 않는 최신 알고리즘에 비해 암호화 방식이 취약한 것으로 간주됩니다. 따라서 메시지 큐 태스크를 사용하여 메시지를 전송할 때는 암호화 요구를 신중하게 고려해야 합니다.  
  
## <a name="receiving-messages"></a>메시지 받기  
 메시지를 받을 때는 다음과 같은 방법으로 메시지 큐 태스크를 구성할 수 있습니다.  
  
-   메시지를 무시하거나 큐에서 메시지를 제거합니다.  
  
-   제한 시간을 지정합니다.  
  
-   제한 시간이 되면 오류가 발생합니다.  
  
-   메시지가 **Data file**에 저장된 경우 기존 파일을 덮어씁니다.  
  
-   메시지에서 **Data file message** 유형이 사용되는 경우 메시지 파일을 다른 파일 이름으로 저장합니다.  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>메시지 큐 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 메시지 큐 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|설명|  
|---------------|-----------------|  
|**MSMQAfterOpen**|태스크에서 메시지 큐 열기를 완료했음을 나타냅니다.|  
|**MSMQBeforeOpen**|태스크에서 메시지 큐 열기를 시작했음을 나타냅니다.|  
|**MSMQBeginReceive**|태스크에서 메시지 받기를 시작했음을 나타냅니다.|  
|**MSMQBeginSend**|태스크에서 메시지 보내기를 시작했음을 나타냅니다.|  
|**MSMQEndReceive**|태스크에서 메시지 받기를 완료했음을 나타냅니다.|  
|**MSMQEndSend**|태스크에서 메시지 보내기를 완료했음을 나타냅니다.|  
|**MSMQTaskInfo**|태스크에 대한 설명 정보를 제공합니다.|  
|**MSMQTaskTimeOut**|태스크 시간이 초과되었음을 나타냅니다.|  
  
## <a name="configuration-of-the-message-queue-task"></a>메시지 큐 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 프로그래밍 방식으로 이러한 속성을 설정하는 방법은 개발자 가이드에서 **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** 클래스에 대한 설명서를 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법에 대한 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)을 참조하세요.  
  
## <a name="message-queue-task-editor-general-page"></a>메시지 큐 태스크 편집기(일반 페이지)
  **메시지 큐 태스크 편집기** 대화 상자의 **일반 페이지** 를 사용하여 메시지 큐 태스크의 이름을 지정하고 설명하며 메시지 형식을 지정하고 태스크에서 메시지를 보내거나 받을지를 나타낼 수 있습니다.  
  
### <a name="options"></a>Options  
 **이름**  
 메시지 큐 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 메시지 큐 태스크에 대한 설명을 입력합니다.  
  
 **Use2000Format**  
 2000 형식의 MSMQ(메시지 큐)를 사용할지 여부를 나타냅니다. 기본값은 **False**입니다.  
  
 **MSMQConnection**  
 기존 MSMQ 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목**: [MSMQ 연결 관리자](../../integration-services/connection-manager/msmq-connection-manager.md), [MSMQ 연결 관리자 편집기](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **메시지**  
 메시지 큐 태스크에서 메시지를 보내거나 받을지를 지정합니다. **메시지 보내기**를 선택하면 대화 상자의 왼쪽 창에 보내기 페이지가 표시되고 **메시지 받기**를 선택하면 받기 페이지가 표시됩니다. 기본적으로 이 값은 **메시지 보내기**로 설정됩니다.  
  
## <a name="message-queue-task-editor-send-page"></a>메시지 큐 태스크 편집기(보내기 페이지)
  **메시지 큐 태스크 편집기** 대화 상자의 **보내기** 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 메시지를 보내도록 메시지 큐 태스크를 구성할 수 있습니다.  
  
### <a name="options"></a>Options  
 **UseEncryption**  
 메시지 암호화 여부를 나타냅니다. 기본값은 **False**입니다.  
  
 **EncryptionAlgorithm**  
 암호화 사용을 선택한 경우 사용할 암호화 알고리즘의 이름을 지정합니다. 메시지 큐 태스크에는 RC2 및 RC4 알고리즘을 사용할 수 있습니다. 기본값은 **RC2**입니다.  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. 현재 릴리스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
> [!IMPORTANT]  
>  이러한 알고리즘은 MSMQ(메시지 큐) 기술에서 지원하는 암호화 알고리즘입니다. 이 두 암호화 알고리즘은 메시지 큐에서 현재 지원하지 않는 최신 알고리즘에 비해 암호화 방식이 취약한 것으로 간주됩니다. 따라서 메시지 큐 태스크를 사용하여 메시지를 전송할 때는 암호화 요구를 신중하게 고려해야 합니다.  
  
 **MessageType**  
 메시지 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**데이터 파일 메시지**|메시지가 파일에 저장됩니다. 이 값을 선택하면 동적 옵션 **DataFileMessage**가 표시됩니다.|  
|**변수 메시지**|메시지가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **VariableMessage**가 표시됩니다.|  
|**문자열 메시지**|메시지가 메시지 큐 태스크에 저장됩니다. 이 값을 선택하면 동적 옵션 **StringMessage**가 표시됩니다.|  
  
### <a name="messagetype-dynamic-options"></a>MessageType 동적 옵션  
  
#### <a name="messagetype--data-file-message"></a>MessageType = 데이터 파일 메시지  
 **DataFileMessage**  
 데이터 파일의 경로를 입력하거나 줄임표 **(...)** 를 클릭한 다음, 파일을 찾습니다.  
  
#### <a name="messagetype--variable-message"></a>MessageType = 변수 메시지  
 **VariableMessage**  
 변수 이름을 입력하거나 줄임표 **(...)** 를 클릭한 다음, 변수를 선택합니다. 변수는 쉼표로 구분됩니다.  
  
 **관련 항목:** 변수 선택  
  
#### <a name="messagetype--string-message"></a>MessageType = 문자열 메시지  
 **StringMessage**  
 문자열 메시지를 입력하거나 줄임표 **(...)** 를 클릭한 다음, **문자열 메시지 입력** 대화 상자에 메시지를 입력합니다.  
  
## <a name="message-queue-task-editor-receive-page"></a>메시지 큐 태스크 편집기(받기 페이지)
  **메시지 큐 태스크 편집기** 대화 상자의 **받기** 페이지를 사용하여 메시지 큐 태스크가 MSMQ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing) 메시지를 받도록 구성할 수 있습니다.  
  
### <a name="options"></a>Options  
 **RemoveFromMessageQueue**  
 메시지를 받은 후 큐에서 제거할지 여부를 나타냅니다. 기본적으로 이 값은 **False**로 설정되어 있습니다.  
  
 **ErrorIfMessageTimeOut**  
 메시지 제한 시간이 초과할 경우 태스크 실패로 처리하고 오류 메시지를 표시할지 여부를 나타냅니다. 기본값은 **False**입니다.  
  
 **TimeoutAfter**  
 태스크 실패 시 오류 메시지를 표시하도록 선택하는 경우 제한 시간 오류 메시지가 표시될 때까지 기다리는 시간(초)을 지정합니다.  
  
 **MessageType**  
 메시지 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**데이터 파일 메시지**|메시지가 파일에 저장됩니다. 이 값을 선택하면 동적 옵션 **DataFileMessage**가 표시됩니다.|  
|**변수 메시지**|메시지가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **VariableMessage**가 표시됩니다.|  
|**문자열 메시지**|메시지가 메시지 큐 태스크에 저장됩니다. 이 값을 선택하면 동적 옵션 **StringMessage**가 표시됩니다.|  
|**변수에 대한 문자열 메시지**|메시지<br /><br /> 이 값을 선택하면 동적 옵션 **StringMessage**가 표시됩니다.|  
  
### <a name="messagetype-dynamic-options"></a>MessageType 동적 옵션  
  
#### <a name="messagetype--data-file-message"></a>MessageType = 데이터 파일 메시지  
 **SaveFileAs**  
 사용할 파일의 경로를 입력하거나 줄임표 단추 **(...)** 를 클릭한 다음, 파일을 찾습니다.  
  
 **Overwrite**  
 데이터 파일 메시지의 내용을 저장할 경우 기존 파일의 데이터를 덮어쓸지 여부를 나타냅니다. 기본값은 **False**입니다.  
  
 **필터**  
 필터를 메시지에 적용할지 여부를 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**필터 없음**|태스크에서 메시지를 필터링하지 않습니다. 이 값을 선택하면 동적 옵션 **IdentifierReadOnly**가 표시됩니다.|  
|**받을 패키지**|메시지는 지정한 패키지의 메시지만 받습니다. 이 값을 선택하면 동적 옵션 **Identifier**가 표시됩니다.|  
  
#### <a name="filter-dynamic-options"></a>Filter 동적 옵션  
  
##### <a name="filter--no-filter"></a>Filter = 필터 없음  
 **IdentifierReadOnly**  
 이 옵션은 읽기 전용입니다. 이전에 Filter 속성을 설정할 때 이 옵션은 비어 있거나 패키지의 GUID를 포함할 수 있습니다.  
  
##### <a name="filter--from-package"></a>Filter = 받을 패키지  
 **ID**  
 필터를 적용하도록 선택한 경우 메시지를 받을 수 있는 패키지의 고유 식별자를 입력하거나 줄임표 단추 **(...)** 를 클릭한 다음, 패키지를 지정합니다.  
  
 **관련 항목:** [패키지 선택](../../integration-services/control-flow/select-a-package.md)  
  
#### <a name="messagetype--variable-message"></a>MessageType = 변수 메시지  
 **Assert**  
 필터를 메시지에 적용할지 여부를 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**필터 없음**|태스크에서 메시지를 필터링하지 않습니다. 이 값을 선택하면 동적 옵션 **IdentifierReadOnly**가 표시됩니다.|  
|**받을 패키지**|메시지는 지정한 패키지의 메시지만 받습니다. 이 값을 선택하면 동적 옵션 **Identifier**가 표시됩니다.|  
  
 **변수**  
 변수 이름을 입력하거나 \<**새 변수...**>를 클릭한 다음, 새 변수를 구성합니다.  
  
 **관련 항목:** [변수 추가](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="filter-dynamic-options"></a>Filter 동적 옵션  
  
##### <a name="filter--no-filter"></a>Filter = 필터 없음  
 **IdentifierReadOnly**  
 이 옵션은 비어 있습니다.  
  
##### <a name="filter--from-package"></a>Filter = 받을 패키지  
 **ID**  
 필터를 적용하도록 선택한 경우 메시지를 받을 수 있는 패키지의 고유 식별자를 입력하거나 줄임표 단추 **(...)** 를 클릭한 다음, 패키지를 지정합니다.  
  
 **관련 항목:** [패키지 선택](../../integration-services/control-flow/select-a-package.md)  
  
#### <a name="messagetype--string-message"></a>MessageType = 문자열 메시지  
 **Compare**  
 필터를 메시지에 적용할지 여부를 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|메시지를 비교하지 않습니다.|  
|**정확히 일치**|메시지가 **CompareString** 옵션의 문자열과 정확히 일치해야 합니다.|  
|**대/소문자 무시**|메시지가 **CompareString** 옵션의 문자열과 일치해야 하지만 비교 시 대/소문자를 무시합니다.|  
|**포함**|메시지가 **CompareString** 옵션의 문자열을 포함해야 합니다.|  
  
 **CompareString**  
 **Compare** 옵션을 **없음**으로 설정한 경우가 아니면 메시지를 비교할 문자열을 제공합니다.  
  
#### <a name="messagetype--string-message-to-variable"></a>MessageType = 변수에 대한 문자열 메시지  
 **Compare**  
 필터를 메시지에 적용할지 여부를 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|메시지를 비교하지 않습니다.|  
|**정확히 일치**|메시지가 **CompareString** 옵션의 문자열과 정확히 일치해야 합니다.|  
|**대/소문자 무시**|메시지가 **CompareString** 옵션의 문자열과 일치해야 하지만 비교 시 대/소문자를 무시합니다.|  
|**포함**|메시지가 **CompareString** 옵션의 문자열을 포함해야 합니다.|  
  
 **CompareString**  
 **Compare** 옵션을 **없음**으로 설정한 경우가 아니면 메시지를 비교할 문자열을 제공합니다.  
  
 **변수**  
 받은 메시지를 보관할 변수의 이름을 입력하거나 \<**새 변수...**>를 클릭한 다음, 새 변수를 구성합니다.  
  
 **관련 항목:** [변수 추가](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="select-variables"></a>변수 선택
  **변수 선택** 대화 상자를 사용하여 메시지 큐 태스크의 메시지 보내기 작업에 사용할 변수를 지정할 수 있습니다. **사용 가능한 변수** 목록에는 메시지 큐 태스크 또는 해당 부모 컨테이너의 범위에 있는 시스템 및 사용자 정의 변수가 포함되어 있습니다. 이 태스크에서는 **선택한 변수** 목록의 변수를 사용합니다.  
  
### <a name="options"></a>Options  
 **사용 가능한 변수**  
 변수를 하나 이상 선택합니다.  
  
 **선택한 변수**  
 변수를 하나 이상 선택합니다.  
  
 **오른쪽 화살표**  
 선택한 변수를 **선택한 변수** 목록으로 이동합니다.  
  
 **왼쪽 화살표**  
 선택한 변수를 **사용 가능한 변수** 목록으로 다시 이동합니다.  
  
 **새 변수**  
 새 변수를 만듭니다.  
  
 **관련 항목:** [변수 추가](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
## <a name="see-also"></a>참고 항목  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  
