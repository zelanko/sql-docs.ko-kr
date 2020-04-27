---
title: 파일 시스템 태스크 편집기 (일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System Task Editor
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 594b87b3e2d58ffe60bd3c31324811a66038c82b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058810"
---
# <a name="file-system-task-editor-general-page"></a>파일 시스템 태스크 편집기(일반 페이지)
  **파일 시스템 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 태스크가 수행하는 파일 시스템 작업을 구성할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [File System Task](control-flow/file-system-task.md)를 참조하십시오.  
  
 SourceConnection 및 DestinationConnection 속성을 설정하여 원본 및 대상 연결 관리자를 지정해야 합니다. 태스크에서 원본 또는 대상으로 사용하는 파일을 가리키는 파일 연결 관리자의 이름을 입력하거나 파일 경로가 변수에 저장되어 있는 경우 변수 이름을 입력할 수 있습니다. 변수를 사용하여 파일 경로를 저장하려면 먼저 원본 연결을 위한 IsSourcePathVariable 옵션 및 대상 연결을 위한 IsDestinationPatheVariable 옵션을 **True**로 설정해야 합니다. 그런 다음 기존 시스템 또는 사용자 정의 변수를 사용하도록 선택하거나 새로운 변수를 만들 수 있습니다. **변수 추가** 대화 상자에서 변수의 범위를 구성하고 지정할 수 있습니다. 변수의 범위는 파일 시스템 태스크 또는 부모 컨테이너여야 합니다. 자세한 내용은 [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../../2014/integration-services/use-variables-in-packages.md)을 참조 하세요.  
  
> [!NOTE]  
>  `SourceConnection` 및 `DestinationConnection` 속성에 대해 선택한 변수를 재정의 하려면 **Source** 및 **Destination** 속성에 대 한 식을 입력 합니다. **파일 시스템 태스크 편집기** 의 **식**페이지에 식을 입력합니다. 예를 들어 태스크에서 대상으로 사용하는 파일 경로를 설정하기 위해 특정 조건에서 변수 A를 사용하고 다른 조건에서는 변수 B를 사용할 수 있습니다.  
  
> [!NOTE]  
>  파일 시스템 태스크는 단일 파일 또는 디렉터리에서 작동합니다. 따라서 이 태스크는 와일드카드 문자를 사용하여 여러 파일 또는 디렉터리에서 동일한 작업을 수행하도록 지원하지 않습니다. 파일 시스템 태스크가 여러 파일이나 디렉터리에서 작업을 반복하게 하려면 파일 시스템 태스크를 Foreach 루프 컨테이너에 넣으십시오. 자세한 내용은 [File System Task](control-flow/file-system-task.md)을(를) 참조하세요.  
  
 식을 사용하여 다른 변수를 사용할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **IsDestinationPathVariable**  
 대상 경로가 변수에 저장되는지 여부를 나타냅니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**True**|대상 경로가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **DestinationVariable**이 표시됩니다.|  
|**허위**|파일 연결 관리자에서 대상 경로를 지정합니다. 이 값을 선택 하면 동적 옵션가 `DestinationConnection`표시 됩니다.|  
  
 **OverwriteDestination**  
 작업이 대상 디렉터리에 있는 파일을 덮어쓸 수 있는지 여부를 지정합니다.  
  
 **이름**  
 파일 시스템 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 파일 시스템 태스크에 대한 설명을 입력합니다.  
  
 **연산**  
 수행할 파일 시스템 작업을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**디렉터리 복사**|디렉터리를 복사합니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다.|  
|**파일 복사**|파일을 복사합니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다.|  
|**디렉터리 만들기**|디렉터리 만들기 이 값을 선택하면 원본 및 대상 디렉터리에 대한 동적 옵션이 표시됩니다.|  
|**디렉터리 삭제**|디렉터리를 삭제합니다. 이 값을 선택하면 원본에 대한 동적 옵션이 표시됩니다.|  
|**디렉터리 내용 삭제**|디렉터리의 내용을 삭제합니다. 이 값을 선택하면 원본에 대한 동적 옵션이 표시됩니다.|  
|**파일 삭제**|파일을 삭제합니다. 이 값을 선택하면 원본에 대한 동적 옵션이 표시됩니다.|  
|**디렉터리 이동**|디렉터리를 이동합니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다.|  
|**파일 이동**|파일을 이동합니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다.<br /><br /> 참고: 파일을 이동할 때 대상으로 제공한 디렉터리 경로에 파일 이름을 포함 하지 마십시오.|  
|**파일 이름 바꾸기**|파일 이름을 바꿉니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다.<br /><br /> 참고: 파일 이름을 바꿀 때 대상에 대해 제공한 디렉터리 경로에 새 파일 이름을 포함 합니다.|  
|**특성 설정**|파일 또는 디렉터리의 특성을 설정합니다. 이 값을 선택하면 원본 및 작업에 대한 동적 옵션이 표시됩니다.|  
  
 `IsSourcePathVariable`  
 대상 경로가 변수에 저장되는지 여부를 나타냅니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값||  
|-----------|-|  
|**True**|대상 경로가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **SourceVariable**이 표시됩니다.|  
|**허위**|파일 연결 관리자에서 대상 경로를 지정합니다. 이 값을 선택하면 동적 옵션 **DestinationVariable**이 표시됩니다.|  
  
## <a name="isdestinationpathvariable-dynamic-options"></a>IsDestinationPathVariable 동적 옵션  
  
### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 목록에서 변수 이름을 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 `DestinationConnection`  
 목록에서 파일 연결 관리자를 선택 하거나 \< **새 연결** ...>을 클릭 하 여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="issourcepathvariable-dynamic-options"></a>IsSourcePathVariable 동적 옵션  
  
### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 목록에서 변수 이름을 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 `SourceConnection`  
 목록에서 파일 연결 관리자를 선택 하거나 \< **새 연결** ...>을 클릭 하 여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="operation-dynamic-options"></a>Operation 동적 옵션  
  
### <a name="operation--set-attributes"></a>Operation = 특성 설정  
 **은선제거**  
 파일 또는 디렉터리의 표시 여부를 나타냅니다.  
  
 **ReadOnly**  
 파일이 읽기 전용인지 여부를 나타냅니다.  
  
 **아카이브**  
 파일 또는 디렉터리가 보관될 준비가 되었는지 여부를 나타냅니다.  
  
 **시스템**  
 파일이 운영 체제 파일인지 여부를 나타냅니다.  
  
### <a name="operation--create-directory"></a>Operation = 디렉터리 만들기  
 `UseDirectoryIfExists`  
 **디렉터리 만들기** 작업이 새 디렉터리를 만들지 않고 지정된 이름의 기존 디렉터리를 사용하는지 여부를 나타냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [식 페이지](expressions/expressions-page.md)  
  
  
