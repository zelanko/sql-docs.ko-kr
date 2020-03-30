---
title: 데이터 프로파일링 태스크 편집기(일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.general.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: eec15906-d757-4079-b2f6-aca4e52b3b4c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 46eb7c7f0834f864aba8e3951f4caf9092f5bb7b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294197"
---
# <a name="data-profiling-task-editor-general-page"></a>데이터 프로파일링 태스크 편집기(일반 페이지)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **데이터 프로파일링 태스크 편집기** 의 **일반** 페이지를 사용하여 다음 옵션을 구성할 수 있습니다.  
  
-   프로필 출력의 대상을 지정합니다.  
  
-   기본 설정을 사용하여 단일 테이블 또는 뷰를 프로파일링하는 태스크를 단순화합니다.  
  
 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요. 데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 분석하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요.  
  
 **데이터 프로파일링 태스크 편집기의 일반 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 데이터 프로파일링 태스크가 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **제어 흐름** 탭에서 데이터 프로파일링 태스크를 두 번 클릭합니다.  
  
3.  **데이터 프로파일링 태스크 편집기**에서 **일반**을 클릭합니다.  
  
## <a name="data-profiling-options"></a>데이터 프로파일링 옵션  
 **Timeout**  
 데이터 프로파일링 태스크가 시간 초과되어 실행이 중지되는 시간(초)을 지정합니다. 기본값은 0으로 제한 시간이 없음을 나타냅니다.  
  
## <a name="destination-options"></a>대상 옵션  
  
> [!IMPORTANT]  
>  출력 파일에는 데이터베이스와 해당 데이터베이스에 포함된 데이터에 대한 중요 데이터가 포함될 수 있습니다. 이 파일을 보다 안전하게 보호하는 방법에 대한 제안 사항은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
 **DestinationType**  
 데이터 프로필 출력을 파일이나 변수에 저장할 것인지 여부를 지정합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**FileConnection**|파일 연결 관리자에서 지정한 위치에 있는 파일에 프로필 출력을 저장합니다.<br /><br /> 참고: **Destination** 옵션에서 사용할 파일 연결 관리자를 지정합니다.|  
|**변수**|프로필 출력을 패키지 변수에 저장합니다.<br /><br /> 참고: **Destination** 옵션에서 사용할 패키지 변수를 지정합니다.|  
  
 **대상**  
 데이터 프로필 출력을 포함할 파일 연결 관리자 또는 패키지 변수를 지정합니다.  
  
-   **DestinationType** 옵션이 **FileConnection**으로 설정된 경우 **Destination** 옵션에 사용 가능한 파일 연결 관리자가 표시됩니다. 이러한 연결 관리자 중 하나를 선택하거나 \<새 파일 연결>을 선택하여 새 파일 연결 관리자를 만듭니다.  
  
-   **DestinationType** 옵션이 **Variable**로 설정된 경우 **Destination** 옵션에 사용 가능한 패키지 변수가 **Destination** 목록으로 표시합니다. 이러한 변수 중 하나를 선택하거나 \<새 변수>를 선택하여 새 변수를 만듭니다.  
  
 **OverwriteDestination**  
 출력 파일이 이미 있는 경우 덮어쓸 것인지 여부를 지정합니다. 기본값은 **False**입니다. 이 속성의 값은 DestinationType 옵션이 FileConnection으로 설정된 경우에만 사용됩니다. DestinationType 옵션이 Variable로 설정된 경우 태스크에서는 변수의 이전 값을 항상 덮어씁니다.  
  
> [!IMPORTANT]  
>  출력 파일 이름을 바꾸거나 **OverwriteDestination** 속성의 값을 **True**로 변경하지 않고 데이터 프로파일링 태스크를 두 번 이상 실행하려고 하면 출력 파일이 이미 있다는 메시지와 함께 태스크가 실패합니다.  
  
## <a name="other-options"></a>다른 옵션  
 **빠른 프로필**  
 **단일 테이블 빠른 프로필 형식**을 표시합니다. 이 형식은 기본 설정을 사용하여 단일 테이블 또는 뷰를 프로파일링하는 태스크를 단순화합니다. 자세한 내용은 [단일 테이블 빠른 프로필 형식&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)을 참조하세요.  
  
 **프로필 뷰어 열기**  
 데이터 프로필 뷰어를 엽니다. 독립 실행형 데이터 프로필 뷰어에는 데이터 프로파일링 태스크의 데이터 프로필 출력이 표시됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 내에서 데이터 프로파일링 태스크를 실행하고 데이터 프로필을 계산한 후에 이러한 프로필 출력을 볼 수 있습니다.  
  
> [!NOTE]  
>  또한 *\<드라이브>* :\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn 폴더에서 DataProfileViewer.exe를 실행하여 데이터 프로필 뷰어를 열 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [단일 테이블 빠른 프로필 형식&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)   
 [데이터 프로파일링 태스크 편집기&#40;프로필 요청 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
  
  
