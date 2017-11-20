---
title: "파일 시스템 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- sql13.dts.designer.filesystemtask.f1
- sql13.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System task [Integration Services]
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 63fb21cae5f8df981f243035fc7b34e53fa4d0bd
ms.contentlocale: ko-kr
ms.lasthandoff: 08/11/2017

---
# <a name="file-system-task"></a>파일 시스템 태스크
  파일 시스템 태스크는 파일 시스템의 파일 및 디렉터리에 대해 작업을 수행합니다. 예를 들어 파일 시스템 태스크를 사용하면 패키지가 디렉터리와 파일을 만들거나 이동 또는 삭제할 수 있습니다. 파일 시스템 태스크를 사용하여 파일과 디렉터리의 특성을 설정할 수도 있습니다. 예를 들어 파일 시스템 태스크는 파일에 숨김 또는 읽기 전용 특성을 설정할 수 있습니다.  
  
 모든 파일 시스템 태스크는 파일이나 디렉터리일 수 있는 원본을 사용합니다. 예를 들어 태스크에서 복사한 파일이나 삭제한 디렉터리가 원본입니다. 파일 연결 관리자를 사용하여 디렉터리 또는 파일을 가리키거나 원본 경로가 포함된 변수 이름을 제공하여 원본을 지정할 수 있습니다. 자세한 내용은 [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md) 및 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)를 참조하세요.  
  
 파일과 디렉터리를 복사 및 이동하는 작업과 파일 이름을 바꾸는 작업은 대상과 원본을 사용합니다. 대상은 파일 연결 관리자나 변수를 사용하여 지정합니다. 대상 파일과 디렉터리의 덮어쓰기를 허용하도록 파일 시스템 태스크를 구성할 수 있습니다. 지정된 이름을 가진 디렉터리가 이미 존재할 경우 실패하는 대신에 해당 디렉터리를 사용하도록 새 디렉터리를 만드는 작업을 구성할 수 있습니다.  
  
## <a name="predefined-file-system-operations"></a>미리 정의된 파일 시스템 작업  
 파일 시스템 태스크에는 미리 정의된 작업 집합이 포함되어 있습니다. 다음 표에서는 이러한 작업을 설명합니다.  
  
|연산|Description|  
|---------------|-----------------|  
|디렉터리 복사|폴더를 다른 위치에 복사합니다.|  
|파일 복사|파일을 다른 위치에 복사합니다.|  
|디렉터리 만들기|지정한 위치에 폴더를 만듭니다.|  
|디렉터리 삭제|지정한 위치의 폴더를 삭제합니다.|  
|디렉터리 내용 삭제|폴더에 있는 모든 파일과 폴더를 삭제합니다.|  
|파일 삭제|지정한 위치의 파일을 삭제합니다.|  
|디렉터리 이동|폴더를 다른 위치로 이동합니다.|  
|파일 이동|파일을 다른 위치로 이동합니다.|  
|파일 이름 바꾸기|지정한 위치의 파일 이름을 바꿉니다.|  
|특성 설정|파일과 폴더의 특성을 설정합니다. 특성에는 보관, 숨김, 보통, 읽기 전용, 시스템 등이 있습니다. 보통은 특성이 없는 것이며 다른 특성과 조합할 수 없습니다. 다른 모든 특성은 조합하여 사용할 수 있습니다.|  
  
 파일 시스템 태스크는 단일 파일 또는 디렉터리에서 작동합니다. 따라서 이 태스크는 와일드카드 문자를 사용하여 여러 파일에 대해 동일한 작업을 수행하는 것을 지원하지 않습니다. 파일 시스템 태스크가 여러 파일이나 디렉터리에 대한 작업을 반복하게 하려면 다음 단계에 따라 파일 시스템 태스크를 Foreach 루프 컨테이너에 넣으십시오.  
  
-   **Foreach 루프 컨테이너 구성** Foreach 루프 편집기의 **컬렉션** 페이지에서 열거자를 **Foreach File 열거자** 로 설정하고 와일드카드 식을 **파일**에 대한 열거자 구성으로 입력하십시오. Foreach 루프 편집기의 **변수 매핑** 페이지에서 파일 시스템 태스크에 파일 이름을 한 번에 한 개씩 전달하는 데 사용할 변수를 매핑합니다.  
  
-   **파일 시스템 태스크 추가 및 구성** 파일 시스템 태스크를 Foreach 루프 컨테이너에 추가합니다. 파일 시스템 태스크 편집기의 **일반** 페이지에서 **SourceVariable** 또는 **DestinationVariable** 속성을 Foreach 루프 컨테이너에 정의된 변수로 설정합니다.  
  
## <a name="custom-log-entries-available-on-the-file-system-task"></a>파일 시스템 태스크에 사용할 수 있는 사용자 지정 로그 항목  
 다음 표에서는 파일 시스템 태스크에 대한 사용자 지정 로그 항목을 설명합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**FileSystemOperation**|태스크에서 수행하는 작업을 보고합니다. 이 로그 항목은 파일 시스템 작업이 시작될 때 기록되며 원본 및 대상에 대한 정보를 포함합니다.|  
  
## <a name="configuring-the-file-system-task"></a>파일 시스템 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [파일 시스템 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/file-system-task-editor-general-page.md)  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법은 다음 항목을 참조하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
 프로그래밍 방식으로 이러한 속성을 설정하는 방법은 다음 항목을 참조하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 데이터 파일을 다운로드 및 업로드하고 서버의 디렉터리를 관리하는 태스크가 있습니다. 자세한 내용은 [FTP Task](../../integration-services/control-flow/ftp-task.md)을 참조하세요.  
  
## <a name="file-system-task-editor-general-page"></a>파일 시스템 태스크 편집기(일반 페이지)
  **파일 시스템 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 태스크가 수행하는 파일 시스템 작업을 구성할 수 있습니다.  
  
 SourceConnection 및 DestinationConnection 속성을 설정하여 원본 및 대상 연결 관리자를 지정해야 합니다. 태스크에서 원본 또는 대상으로 사용하는 파일을 가리키는 파일 연결 관리자의 이름을 입력하거나 파일 경로가 변수에 저장되어 있는 경우 변수 이름을 입력할 수 있습니다. 변수를 사용하여 파일 경로를 저장하려면 먼저 원본 연결을 위한 IsSourcePathVariable 옵션 및 대상 연결을 위한 IsDestinationPatheVariable 옵션을 **True**로 설정해야 합니다. 그런 다음 기존 시스템 또는 사용자 정의 변수를 사용하도록 선택하거나 새로운 변수를 만들 수 있습니다. **변수 추가** 대화 상자에서 변수의 범위를 구성하고 지정할 수 있습니다. 변수의 범위는 파일 시스템 태스크 또는 부모 컨테이너여야 합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)을 참조하세요.  
  
> [!NOTE]  
>  **SourceConnection** 및 **DestinationConnection** 속성에 대해 선택한 변수를 재정의하려면 **Source** 및 **Destination** 속성에 대한 식을 입력합니다. **파일 시스템 태스크 편집기** 의 **식**페이지에 식을 입력합니다. 예를 들어 태스크에서 대상으로 사용하는 파일 경로를 설정하기 위해 특정 조건에서 변수 A를 사용하고 다른 조건에서는 변수 B를 사용할 수 있습니다.  
  
> [!NOTE]  
>  파일 시스템 태스크는 단일 파일 또는 디렉터리에서 작동합니다. 따라서 이 태스크는 와일드카드 문자를 사용하여 여러 파일 또는 디렉터리에서 동일한 작업을 수행하도록 지원하지 않습니다. 파일 시스템 태스크가 여러 파일이나 디렉터리에서 작업을 반복하게 하려면 파일 시스템 태스크를 Foreach 루프 컨테이너에 넣으십시오. 자세한 내용은 [File System Task](../../integration-services/control-flow/file-system-task.md)을(를) 참조하세요.  
  
 식을 사용하여 다른 변수를 사용할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **IsDestinationPathVariable**  
 대상 경로가 변수에 저장되는지 여부를 나타냅니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|대상 경로가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **DestinationVariable**이 표시됩니다.|  
|**False**|파일 연결 관리자에서 대상 경로를 지정합니다. 이 값을 선택하면 동적 옵션 **DestinationConnection**이 표시됩니다.|  
  
 **OverwriteDestination**  
 작업이 대상 디렉터리에 있는 파일을 덮어쓸 수 있는지 여부를 지정합니다.  
  
 **이름**  
 파일 시스템 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **Description**  
 파일 시스템 태스크에 대한 설명을 입력합니다.  
  
 **연산**  
 수행할 파일 시스템 작업을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**디렉터리 복사**|디렉터리를 복사합니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다.|  
|**파일 복사**|파일을 복사합니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다.|  
|**디렉터리 만들기**|디렉터리를 만듭니다. 이 값을 선택하면 원본 및 대상 디렉터리에 대한 동적 옵션이 표시됩니다.|  
|**디렉터리 삭제**|디렉터리를 삭제합니다. 이 값을 선택하면 원본에 대한 동적 옵션이 표시됩니다.|  
|**디렉터리 내용 삭제**|디렉터리의 내용을 삭제합니다. 이 값을 선택하면 원본에 대한 동적 옵션이 표시됩니다.|  
|**파일 삭제**|파일을 삭제합니다. 이 값을 선택하면 원본에 대한 동적 옵션이 표시됩니다.|  
|**디렉터리 이동**|디렉터리를 이동합니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다.|  
|**파일 이동**|파일을 이동합니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다. 파일을 이동할 때 대상으로 제공한 디렉터리 경로에 파일 이름이 포함되지 않도록 하십시오.|  
|**파일 이름 바꾸기**|파일 이름을 바꿉니다. 이 값을 선택하면 원본 및 대상에 대한 동적 옵션이 표시됩니다. 파일 이름을 바꿀 때 대상에 대해 제공한 디렉터리 경로에 새 파일 이름을 포함시키십시오.|  
|**특성 설정**|파일 또는 디렉터리의 특성을 설정합니다. 이 값을 선택하면 원본 및 작업에 대한 동적 옵션이 표시됩니다.|  
  
 **IsSourcePathVariable**  
 대상 경로가 변수에 저장되는지 여부를 나타냅니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value||  
|-----------|-|  
|**True**|대상 경로가 변수에 저장됩니다. 이 값을 선택하면 동적 옵션 **SourceVariable**이 표시됩니다.|  
|**False**|파일 연결 관리자에서 대상 경로를 지정합니다. 이 값을 선택하면 동적 옵션 **DestinationVariable**이 표시됩니다.|  
  
### <a name="isdestinationpathvariable-dynamic-options"></a>IsDestinationPathVariable 동적 옵션  
  
#### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 목록에서 변수 이름을 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 **DestinationConnection**  
 목록에서 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="issourcepathvariable-dynamic-options"></a>IsSourcePathVariable 동적 옵션  
  
#### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 목록에서 변수 이름을 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 **SourceConnection**  
 목록에서 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md)  
  
### <a name="operation-dynamic-options"></a>Operation 동적 옵션  
  
#### <a name="operation--set-attributes"></a>Operation = 특성 설정  
 **숨김**  
 파일 또는 디렉터리의 표시 여부를 나타냅니다.  
  
 **읽기 전용**  
 파일이 읽기 전용인지 여부를 나타냅니다.  
  
 **Archive**  
 파일 또는 디렉터리가 보관될 준비가 되었는지 여부를 나타냅니다.  
  
 **시스템**  
 파일이 운영 체제 파일인지 여부를 나타냅니다.  
  
#### <a name="operation--create-directory"></a>Operation = 디렉터리 만들기  
 **UseDirectoryIfExists**  
 **디렉터리 만들기** 작업이 새 디렉터리를 만들지 않고 지정된 이름의 기존 디렉터리를 사용하는지 여부를 나타냅니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  

