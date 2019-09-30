---
title: 조회 변환 전체 캐시 모드 - 캐시 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation [Integration Services]
ms.assetid: 58bc7611-5fb5-4113-9742-10959e06b94c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1ae22daf218c65bc0aa95068d6162a7b966c838c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298515"
---
# <a name="lookup-transformation-full-cache-mode---cache-connection-manager"></a>조회 변환 전체 캐시 모드 - 캐시 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  전체 캐시 모드와 캐시 연결 관리자를 사용하도록 조회 변환을 구성할 수 있습니다. 전체 캐시 모드에서 조회 변환이 실행되기 전에 참조 데이터 세트가 캐시에 로드됩니다.  
  
> [!NOTE]  
>  캐시 연결 관리자는 BLOB(Binary Large Object) 데이터 형식 DT_TEXT, DT_NTEXT 및 DT_IMAGE를 지원하지 않습니다. 참조 데이터 세트에 BLOB 데이터 형식이 있으면 패키지를 실행할 때 구성 요소가 실패합니다. **캐시 연결 관리자 편집기** 를 사용하여 열 데이터 형식을 수정할 수 있습니다. 자세한 내용은 [Cache Connection Manager Editor](../../integration-services/connection-manager/cache-connection-manager-editor.md)을 참조하세요.  
  
 조회 변환은 연결된 데이터 원본의 입력 열에 있는 데이터를 참조 데이터 세트의 열과 조인하여 조회합니다. 자세한 내용은 [Lookup Transformation](../../integration-services/data-flow/transformations/lookup-transformation.md)을(를) 참조하세요.  
  
 다음 중 하나를 사용하여 참조 데이터 세트를 생성합니다.  
  
-   캐시 파일(.caw)  
  
     기존 캐시 파일에서 데이터를 읽도록 캐시 연결 관리자를 구성합니다.  
  
-   데이터 흐름에 있는 연결된 데이터 원본  
  
     캐시 변환을 사용하여 데이터 흐름에 있는 연결된 데이터 원본의 데이터를 캐시 연결 관리자에 기록합니다. 데이터는 항상 메모리에 저장됩니다.  
  
     조회 변환을 별도의 데이터 흐름에 추가해야 합니다. 그러면 조회 변환이 실행되기 전에 캐시 변환이 캐시 연결 관리자를 채울 수 있습니다. 데이터 흐름은 같은 패키지나 두 개의 별도 패키지에 있을 수 있습니다.  
  
     데이터 흐름이 같은 패키지에 있으면 선행 제약 조건을 사용하여 데이터 흐름에 연결합니다. 그러면 조회 변환이 실행되기 전에 캐시 변환을 실행할 수 있습니다.  
  
     데이터 흐름이 별도의 패키지에 있으면 패키지 실행 태스크를 사용하여 부모 패키지에서 자식 패키지를 호출할 수 있습니다. 여러 개의 패키지 실행 태스크를 부모 패키지의 시퀀스 컨테이너 태스크에 추가하여 여러 개의 자식 패키지를 호출할 수 있습니다.  
  
 다음 방법 중 하나를 사용하여 여러 개의 조회 변환 간에 캐시에 저장된 참조 데이터 세트를 공유할 수 있습니다.  
  
-   같은 캐시 연결 관리자를 사용하도록 단일 패키지에 조회 변환 구성  
  
-   같은 캐시 파일을 사용하도록 다른 패키지에 캐시 연결 관리자 구성  
  
 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [캐시 변환](../../integration-services/data-flow/transformations/cache-transform.md)  
  
-   [캐시 연결 관리자](../../integration-services/connection-manager/cache-connection-manager.md)  
  
-   [선행 제약 조건](../../integration-services/control-flow/precedence-constraints.md)  
  
-   [패키지 실행 태스크](../../integration-services/control-flow/execute-package-task.md)  
  
-   [시퀀스 컨테이너](../../integration-services/control-flow/sequence-container.md)  
  
 캐시 연결 관리자를 사용하여 전체 캐시 모드에서 조회 변환을 구현하는 방법을 보여 주는 비디오는 [방법: 전체 캐시 모드에서 조회 변환 구현(SQL Server 비디오)](https://go.microsoft.com/fwlink/?LinkId=131031)을 참조하세요.  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-in-one-package-by-using-cache-connection-manager-and-a-data-source-in-the-data-flow"></a>데이터 흐름의 데이터 원본과 캐시 연결 관리자를 사용하여 조회 변환을 한 개의 패키지에서 전체 캐시 모드로 구현하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 연 다음 하나의 패키지를 엽니다.  
  
2.  **흐름 제어** 탭에서 두 개의 데이터 흐름 태스크를 추가한 다음 녹색 연결선을 사용하여 태스크를 연결합니다.  
  
3.  첫 번째 데이터 흐름에서 캐시 변환을 추가한 다음 데이터 원본에 변환을 연결합니다.  
  
     필요한 경우 데이터 원본을 구성합니다.  
  
4.  캐시 변환을 두 번 클릭한 다음 **캐시 변환 편집기**의 **연결 관리자** 페이지에서 **새로 만들기** 를 클릭하여 새 캐시 연결 관리자를 만듭니다.  
  
5.  **캐시 연결 관리자 편집기** 대화 상자의 **열** 탭을 클릭한 다음 **인덱스 위치** 옵션을 사용하여 인덱스 열이 되는 열을 지정합니다.  
  
     비인덱스 열의 경우 인덱스 위치는 0입니다. 인덱스 열의 경우 인덱스 위치는 일련의 양수입니다.  
  
    > [!NOTE]  
    >  조회 변환은 캐시 연결 관리자를 사용하도록 구성된 경우 참조 데이터 세트의 인덱스 열만 입력 열에 매핑할 수 있습니다. 또한 모든 인덱스 열을 매핑해야 합니다. 자세한 내용은 [Cache Connection Manager Editor](../../integration-services/connection-manager/cache-connection-manager-editor.md)을 참조하세요.  
  
6.  캐시를 파일에 저장하려면 **캐시 연결 관리자 편집기**의 **일반** 탭에서 다음 옵션을 설정하여 캐시 연결 관리자를 구성합니다.  
  
    -   **파일 캐시 사용**을 선택합니다.  
  
    -   **파일 이름**에 파일 경로를 입력하거나 **찾아보기** 를 클릭하여 파일을 선택합니다.  
  
         존재하지 않는 파일의 경로를 입력하면 패키지를 실행할 때 시스템이 파일을 만듭니다.  
  
    > [!NOTE]  
    >  패키지의 보호 수준은 캐시 파일에 적용되지 않습니다. 캐시 파일에 중요한 정보가 들어 있는 경우 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더에 대한 액세스를 제한합니다. 특정 계정에 대해서만 액세스를 허용해야 합니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
7.  필요한 경우 캐시 변환을 구성합니다. 자세한 내용은 [캐시 변환 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/transformations/cache-transformation-editor-connection-manager-page.md) 및 [캐시 변환 편집기&#40;매핑 페이지&#41;](../../integration-services/data-flow/transformations/cache-transformation-editor-mappings-page.md)를 참조하세요.  
  
8.  두 번째 데이터 흐름에서 조회 변환을 추가한 후 다음 태스크를 수행하여 변환을 구성합니다.  
  
    1.  원본이나 이전 변환에서 연결선을 조회 변환으로 끌어서 조회 변환을 데이터 흐름에 연결합니다.  
  
        > [!NOTE]  
        >  조회 변환이 빈 데이터 필드가 포함된 플랫 파일에 연결되면 이러한 조회 변환의 유효성을 검사하지 못할 수 있습니다. 변환의 유효성 검사 여부는 플랫 파일의 연결 관리자가 Null 값을 유지하도록 구성되었는지 여부에 따라 결정됩니다. 조회 변환의 유효성 검사가 수행되도록 하려면 **플랫 파일 원본 편집기**의 **연결 관리자 페이지**에서 **원본의 Null 값을 데이터 흐름의 Null 값으로 유지** 옵션을 선택합니다.  
  
    2.  원본이나 이전 변환을 두 번 클릭하여 구성 요소를 구성합니다.  
  
    3.  조회 변환을 두 번 클릭한 다음 **조회 변환 편집기**의 **일반** 페이지에서 **전체 캐시**를 선택합니다.  
  
    4.  **연결 형식** 영역에서 **캐시 연결 관리자**를 선택합니다.  
  
    5.  **일치하는 항목이 없는 행 처리 방법 지정** 목록에서 오류 처리 옵션을 선택합니다.  
  
    6.  **연결** 페이지의 **캐시 연결 관리자** 목록에서 캐시 연결 관리자를 선택합니다.  
  
    7.  **열** 페이지를 클릭한 다음 **사용 가능한 입력 열** 목록에 있는 하나 이상의 열을 **사용 가능한 조회 열** 목록에 있는 열로 끌어 옵니다.  
  
        > [!NOTE]  
        >  조회 변환은 이름과 데이터 형식이 같은 열을 자동으로 매핑합니다.  
  
        > [!NOTE]  
        >  열을 매핑하려면 데이터 형식이 일치해야 합니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
    8.  **사용 가능한 조회 열** 목록에서 열을 선택합니다. 그런 다음 **조회 작업** 목록에서 조회 열의 값으로 입력 열의 값을 교체하거나 새 열에 기록할지 여부를 지정합니다.  
  
    9. 오류 출력을 구성하려면 **오류 출력** 페이지를 클릭하고 오류 처리 옵션을 설정합니다. 자세한 내용은 [조회 변환 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)를 참조하세요.  
  
    10. 변경 내용을 조회 변환에 저장하려면 **확인** 을 클릭합니다.  
  
9. 패키지를 실행합니다.  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-in-two-packages-by-using-cache-connection-manager-and-a-data-source-in-the-data-flow"></a>데이터 흐름의 데이터 원본과 캐시 연결 관리자를 사용하여 조회 변환을 두 개의 패키지에서 전체 캐시 모드로 구현하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 연 다음 두 개의 패키지를 엽니다.  
  
2.  각 페이지의 제어 흐름 탭에서 데이터 흐름 태스크를 추가합니다.  
  
3.  부모 패키지에서 데이터 흐름에 캐시 변환을 추가한 다음 변환을 데이터 원본에 연결합니다.  
  
     필요한 경우 데이터 원본을 구성합니다.  
  
4.  캐시 변환을 두 번 클릭한 다음 **캐시 변환 편집기**의 **연결 관리자** 페이지에서 **새로 만들기** 를 클릭하여 새 캐시 연결 관리자를 만듭니다.  
  
5.  **캐시 연결 관리자 편집기**의 **일반** 탭에서 다음 옵션을 설정하여 캐시를 저장하도록 캐시 연결 관리자를 구성합니다.  
  
    -   **파일 캐시 사용**을 선택합니다.  
  
    -   **파일 이름**에 파일 경로를 입력하거나 **찾아보기** 를 클릭하여 파일을 선택합니다.  
  
         존재하지 않는 파일의 경로를 입력하면 패키지를 실행할 때 시스템이 파일을 만듭니다.  
  
    > [!NOTE]  
    >  패키지의 보호 수준은 캐시 파일에 적용되지 않습니다. 캐시 파일에 중요한 정보가 들어 있는 경우 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더에 대한 액세스를 제한합니다. 특정 계정에 대해서만 액세스를 허용해야 합니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
6.  **열** 탭을 클릭한 다음 **인덱스 위치** 옵션을 사용하여 인덱스 열이 되는 열을 지정합니다.  
  
     비인덱스 열의 경우 인덱스 위치는 0입니다. 인덱스 열의 경우 인덱스 위치는 일련의 양수입니다.  
  
    > [!NOTE]  
    >  조회 변환은 캐시 연결 관리자를 사용하도록 구성된 경우 참조 데이터 세트의 인덱스 열만 입력 열에 매핑할 수 있습니다. 또한 모든 인덱스 열을 매핑해야 합니다. 자세한 내용은 [Cache Connection Manager Editor](../../integration-services/connection-manager/cache-connection-manager-editor.md)을 참조하세요.  
  
7.  필요한 경우 캐시 변환을 구성합니다. 자세한 내용은 [캐시 변환 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/transformations/cache-transformation-editor-connection-manager-page.md) 및 [캐시 변환 편집기&#40;매핑 페이지&#41;](../../integration-services/data-flow/transformations/cache-transformation-editor-mappings-page.md)를 참조하세요.  
  
8.  다음 중 하나를 수행하여 두 번째 패키지에 사용된 캐시 연결 관리자를 채웁니다.  
  
    -   부모 패키지를 실행합니다.  
  
    -   4단계에서 만든 캐시 연결 관리자를 두 번 클릭하고 **열**을 클릭하여 행을 선택한 다음 CTRL+C를 눌러 열 메타데이터를 복사합니다.  
  
9. 자식 패키지에서 **연결 관리자** 영역을 마우스 오른쪽 단추로 누르고 **새 연결**을 클릭하여 **SSIS 연결 관리자 추가** 대화 상자에서 **CACHE** 를 선택한 다음 **추가**를 클릭하여 캐시 연결 관리자를 만듭니다.  
  
     **연결 관리자** 영역은 **디자이너의**흐름 제어 **,** 데이터 흐름 **및** 이벤트 처리기 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 탭 아래에 표시됩니다.  
  
10. **캐시 연결 관리자 편집기**의 **일반** 탭에서 다음 옵션을 설정하여 캐시 파일의 데이터를 읽도록 캐시 연결 관리자를 구성합니다.  
  
    -   **파일 캐시 사용**을 선택합니다.  
  
    -   **파일 이름**에 파일 경로를 입력하거나 **찾아보기** 를 클릭하여 파일을 선택합니다.  
  
    > [!NOTE]  
    >  패키지의 보호 수준은 캐시 파일에 적용되지 않습니다. 캐시 파일에 중요한 정보가 들어 있는 경우 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더에 대한 액세스를 제한합니다. 특정 계정에 대해서만 액세스를 허용해야 합니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
11. 8단계에서 열 메타데이터를 복사했으면 **열**을 클릭하고 빈 행을 선택한 다음 Ctrl+V를 눌러 열 메타데이터를 붙여넣습니다.  
  
12. 조회 변환을 추가한 후 다음을 수행하여 변환을 구성합니다.  
  
    1.  원본이나 이전 변환에서 연결선을 조회 변환으로 끌어서 조회 변환을 데이터 흐름에 연결합니다.  
  
        > [!NOTE]  
        >  조회 변환이 빈 데이터 필드가 포함된 플랫 파일에 연결되면 이러한 조회 변환의 유효성을 검사하지 못할 수 있습니다. 변환의 유효성 검사 여부는 플랫 파일의 연결 관리자가 Null 값을 유지하도록 구성되었는지 여부에 따라 결정됩니다. 조회 변환의 유효성 검사가 수행되도록 하려면 **플랫 파일 원본 편집기**의 **연결 관리자 페이지**에서 **원본의 Null 값을 데이터 흐름의 Null 값으로 유지** 옵션을 선택합니다.  
  
    2.  원본이나 이전 변환을 두 번 클릭하여 구성 요소를 구성합니다.  
  
    3.  조회 변환을 두 번 클릭한 다음 **조회 변환 편집기** 의 **일반** 페이지에서 **전체 캐시**를 선택합니다.  
  
    4.  **연결 형식** 영역에서 **캐시 연결 관리자** 를 선택합니다.  
  
    5.  **일치하는 항목이 없는 행 처리 방법 지정** 목록에서 일치하는 항목이 없는 행에 대한 오류 처리 옵션을 선택합니다.  
  
    6.  **연결** 페이지의 **캐시 연결 관리자** 목록에서 추가한 캐시 연결 관리자를 선택합니다.  
  
    7.  **열** 페이지를 클릭한 다음 **사용 가능한 입력 열** 목록에 있는 하나 이상의 열을 **사용 가능한 조회 열** 목록에 있는 열로 끌어 옵니다.  
  
        > [!NOTE]  
        >  조회 변환은 이름과 데이터 형식이 같은 열을 자동으로 매핑합니다.  
  
        > [!NOTE]  
        >  열을 매핑하려면 데이터 형식이 일치해야 합니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
    8.  **사용 가능한 조회 열** 목록에서 열을 선택합니다. 그런 다음 **조회 작업** 목록에서 조회 열의 값으로 입력 열의 값을 교체하거나 새 열에 기록할지 여부를 지정합니다.  
  
    9. 오류 출력을 구성하려면 **오류 출력** 페이지를 클릭하고 오류 처리 옵션을 설정합니다. 자세한 내용은 [조회 변환 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)를 참조하세요.  
  
    10. 변경 내용을 조회 변환에 저장하려면 **확인** 을 클릭합니다.  
  
13. 부모 패키지를 열고 제어 흐름에 패키지 실행 태스크를 추가한 다음 자식 패키지를 호출할 태스크를 구성합니다. 자세한 내용은 [Execute Package Task](../../integration-services/control-flow/execute-package-task.md)을(를) 참조하세요.  
  
14. 패키지를 실행합니다.  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-by-using-cache-connection-manager-and-an-existing-cache-file"></a>캐시 연결 관리자와 기존 캐시 파일을 사용하여 전체 캐시 모드에서 조회 변환을 구현하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 연 다음 하나의 패키지를 엽니다.  
  
2.  **연결 관리자** 영역을 마우스 오른쪽 단추로 클릭한 다음 **새 연결**을 클릭합니다.  
  
     **연결 관리자** 영역은 **디자이너의**흐름 제어 **,** 데이터 흐름 **및** 이벤트 처리기 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 탭 아래에 표시됩니다.  
  
3.  **SSIS 연결 관리자 추가** 대화 상자에서 **CACHE**를 선택한 다음 **추가** 를 클릭하여 캐시 연결 관리자를 추가합니다.  
  
4.  캐시 연결 관리자를 두 번 클릭하여 **캐시 연결 관리자 편집기**를 엽니다.  
  
5.  **캐시 연결 관리자 편집기**의 **일반** 탭에서 다음 옵션을 설정하여 캐시를 저장하도록 캐시 연결 관리자를 구성합니다.  
  
    -   **파일 캐시 사용**을 선택합니다.  
  
    -   **파일 이름**에 파일 경로를 입력하거나 **찾아보기** 를 클릭하여 파일을 선택합니다.  
  
    > [!NOTE]  
    >  패키지의 보호 수준은 캐시 파일에 적용되지 않습니다. 캐시 파일에 중요한 정보가 들어 있는 경우 ACL(액세스 제어 목록)을 사용하여 파일 저장 위치 또는 폴더에 대한 액세스를 제한합니다. 특정 계정에 대해서만 액세스를 허용해야 합니다. 자세한 내용은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
6.  **열** 탭을 클릭한 다음 **인덱스 위치** 옵션을 사용하여 인덱스 열이 되는 열을 지정합니다.  
  
     비인덱스 열의 경우 인덱스 위치는 0입니다. 인덱스 열의 경우 인덱스 위치는 일련의 양수입니다.  
  
    > [!NOTE]  
    >  조회 변환은 캐시 연결 관리자를 사용하도록 구성된 경우 참조 데이터 세트의 인덱스 열만 입력 열에 매핑할 수 있습니다. 또한 모든 인덱스 열을 매핑해야 합니다. 자세한 내용은 [Cache Connection Manager Editor](../../integration-services/connection-manager/cache-connection-manager-editor.md)을 참조하세요.  
  
7.  **흐름 제어** 탭에서 패키지에 데이터 흐름 태스크를 추가한 다음 데이터 흐름에 조회 변환을 추가합니다.  
  
8.  다음을 수행하여 조회 변환을 구성합니다.  
  
    1.  원본이나 이전 변환에서 연결선을 조회 변환으로 끌어서 조회 변환을 데이터 흐름에 연결합니다.  
  
        > [!NOTE]  
        >  조회 변환이 빈 데이터 필드가 포함된 플랫 파일에 연결되면 이러한 조회 변환의 유효성을 검사하지 못할 수 있습니다. 변환의 유효성 검사 여부는 플랫 파일의 연결 관리자가 Null 값을 유지하도록 구성되었는지 여부에 따라 결정됩니다. 조회 변환의 유효성 검사가 수행되도록 하려면 **플랫 파일 원본 편집기**의 **연결 관리자 페이지**에서 **원본의 Null 값을 데이터 흐름의 Null 값으로 유지** 옵션을 선택합니다.  
  
    2.  원본이나 이전 변환을 두 번 클릭하여 구성 요소를 구성합니다.  
  
    3.  조회 변환을 두 번 클릭한 다음 **조회 변환 편집기**의 **일반** 페이지에서 **전체 캐시**를 선택합니다.  
  
    4.  **연결 형식** 영역에서 **캐시 연결 관리자** 를 선택합니다.  
  
    5.  **일치하는 항목이 없는 행 처리 방법 지정** 목록에서 일치하는 항목이 없는 행에 대한 오류 처리 옵션을 선택합니다.  
  
    6.  **연결** 페이지의 **캐시 연결 관리자** 목록에서 추가한 캐시 연결 관리자를 선택합니다.  
  
    7.  **열** 페이지를 클릭한 다음 **사용 가능한 입력 열** 목록에 있는 하나 이상의 열을 **사용 가능한 조회 열** 목록에 있는 열로 끌어 옵니다.  
  
        > [!NOTE]  
        >  조회 변환은 이름과 데이터 형식이 같은 열을 자동으로 매핑합니다.  
  
        > [!NOTE]  
        >  열을 매핑하려면 데이터 형식이 일치해야 합니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
    8.  **사용 가능한 조회 열** 목록에서 열을 선택합니다. 그런 다음 **조회 작업** 목록에서 조회 열의 값으로 입력 열의 값을 교체하거나 새 열에 기록할지 여부를 지정합니다.  
  
    9. 오류 출력을 구성하려면 **오류 출력** 페이지를 클릭하고 오류 처리 옵션을 설정합니다. 자세한 내용은 [조회 변환 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)를 참조하세요.  
  
    10. 변경 내용을 조회 변환에 저장하려면 **확인** 을 클릭합니다.  
  
9. 패키지를 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [OLE DB 연결 관리자를 사용하여 전체 캐시 모드에서 조회 변환 구현](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)   
 [캐시 없음 또는 부분 캐시 모드로 조회 구현](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)   
 [Integration Services 변환](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
