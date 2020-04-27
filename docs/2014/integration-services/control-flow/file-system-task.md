---
title: 파일 시스템 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.f1
helpviewer_keywords:
- File System task [Integration Services]
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c9a2244c5e6cddbc53ccd3aaec7faaaa3836a923
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62831748"
---
# <a name="file-system-task"></a>파일 시스템 태스크
  파일 시스템 태스크는 파일 시스템의 파일 및 디렉터리에 대해 작업을 수행합니다. 예를 들어 파일 시스템 태스크를 사용하면 패키지가 디렉터리와 파일을 만들거나 이동 또는 삭제할 수 있습니다. 파일 시스템 태스크를 사용하여 파일과 디렉터리의 특성을 설정할 수도 있습니다. 예를 들어 파일 시스템 태스크는 파일에 숨김 또는 읽기 전용 특성을 설정할 수 있습니다.  
  
 모든 파일 시스템 태스크는 파일이나 디렉터리일 수 있는 원본을 사용합니다. 예를 들어 태스크에서 복사한 파일이나 삭제한 디렉터리가 원본입니다. 파일 연결 관리자를 사용하여 디렉터리 또는 파일을 가리키거나 원본 경로가 포함된 변수 이름을 제공하여 원본을 지정할 수 있습니다. 자세한 내용은 [파일 연결 관리자](../connection-manager/file-connection-manager.md) 및 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md)를 참조하세요.  
  
 파일과 디렉터리를 복사 및 이동하는 작업과 파일 이름을 바꾸는 작업은 대상과 원본을 사용합니다. 대상은 파일 연결 관리자나 변수를 사용하여 지정합니다. 대상 파일과 디렉터리의 덮어쓰기를 허용하도록 파일 시스템 태스크를 구성할 수 있습니다. 지정된 이름을 가진 디렉터리가 이미 존재할 경우 실패하는 대신에 해당 디렉터리를 사용하도록 새 디렉터리를 만드는 작업을 구성할 수 있습니다.  
  
## <a name="predefined-file-system-operations"></a>미리 정의된 파일 시스템 작업  
 파일 시스템 태스크에는 미리 정의된 작업 집합이 포함되어 있습니다. 다음 표에서는 이러한 작업을 설명합니다.  
  
|작업(Operation)|Description|  
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
 다음 표에서는 파일 시스템 태스크에 대한 사용자 지정 로그 항목을 설명합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md) 및 [로깅할 메시지 사용자 지정](../custom-messages-for-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`FileSystemOperation`|태스크에서 수행하는 작업을 보고합니다. 이 로그 항목은 파일 시스템 작업이 시작될 때 기록되며 원본 및 대상에 대한 정보를 포함합니다.|  
  
## <a name="configuring-the-file-system-task"></a>파일 시스템 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [파일 시스템 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법은 다음 항목을 참조하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
 프로그래밍 방식으로 이러한 속성을 설정하는 방법은 다음 항목을 참조하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 데이터 파일을 다운로드 및 업로드하고 서버의 디렉터리를 관리하는 태스크가 있습니다. 자세한 내용은 [FTP Task](ftp-task.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [작업 Integration Services](integration-services-tasks.md)   
 [제어 흐름](control-flow.md)  
  
  
