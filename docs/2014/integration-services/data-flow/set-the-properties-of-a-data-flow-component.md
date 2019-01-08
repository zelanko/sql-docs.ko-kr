---
title: 데이터 흐름 구성 요소의 속성 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9ac3714dbbd96150aa9d670e370e8a475f6a57e1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817955"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>데이터 흐름 구성 요소의 속성 설정
  원본, 대상 및 변환을 비롯한 데이터 흐름 구성 요소 속성을 설정하려면 다음 기능 중 하나를 사용합니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 제공하는 구성 요소 편집기. 이러한 편집기에는 각 데이터 흐름 구성 요소의 사용자 지정 속성만 포함됩니다.  
  
-   **속성** 창에는 각 요소에 대한 구성 요소 수준의 사용자 지정 속성뿐만 아니라 모든 데이터 흐름 요소에 공통적인 속성이 나열됩니다.  
  
-   **고급 편집기** 대화 상자에서는 각 구성 요소의 사용자 지정 속성에 액세스할 수 있습니다. 또한 **고급 편집기** 대화 상자에서는 모든 데이터 흐름 구성 요소에 공통적인 속성(입력, 출력, 오류 출력, 열 및 외부 열의 속성)에 액세스할 수 있습니다.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-a-component-editor"></a>구성 요소 편집기를 사용하여 데이터 흐름 구성 요소의 속성을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭한 후 보고 수정하려는 구성 요소 속성이 들어 있는 데이터 흐름이 포함된 데이터 흐름 태스크를 두 번 클릭합니다.  
  
4.  데이터 흐름 구성 요소를 두 번 클릭합니다.  
  
5.  구성 요소 편집기에서 속성 값을 보거나 수정한 후 편집기를 닫습니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-properties-window"></a>속성 창을 사용하여 데이터 흐름 구성 요소의 속성을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭한 후 보고 수정하려는 구성 요소 속성이 들어 있는 데이터 흐름 태스크를 두 번 클릭합니다.  
  
4.  데이터 흐름 구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  속성 값을 보거나 수정한 후 **속성** 창을 닫습니다.  
  
    > [!NOTE]  
    >  여러 속성이 읽기 전용이며 수정될 수 없습니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-advanced-editor"></a>고급 편집기를 사용하여 데이터 흐름 구성 요소의 속성을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭한 후 보거나 수정하려는 구성 요소가 들어 있는 데이터 흐름 태스크를 두 번 클릭합니다.  
  
4.  데이터 흐름 디자이너에서 데이터 흐름 구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **고급 편집기 표시**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 여러 입력을 지원하는 데이터 흐름 구성 요소에서는 **고급 편집기**를 사용할 수 없습니다.  
  
5.  **고급 편집기** 대화 상자에서 다음 단계 중 하나를 수행합니다.  
  
    -   구성 요소에서 사용하는 연결을 보고 지정하려면 **연결 관리자** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  **연결 관리자** 탭은 연결 관리자를 사용하여 파일 및 데이터베이스와 같은 데이터 원본에 연결하는 데이터 흐름 구성 요소에서만 사용할 수 있습니다.  
  
    -   구성 요소 수준의 속성을 보고 수정하려면 **구성 요소 속성** 탭을 클릭합니다.  
  
    -   외부 열과 사용 가능한 출력 간의 매핑을 보고 수정하려면 **열 매핑** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  **열 매핑** 탭은 원본 또는 대상을 보거나 편집하는 경우에만 사용할 수 있습니다.  
  
    -   사용 가능한 입력 열 목록을 보고 출력 열의 이름을 업데이트하려면 **입력 열** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  입력 열 탭은 변환 또는 대상에서 작업할 경우에만 사용할 수 있습니다. 자세한 내용은 [Integration Services Transformations](transformations/integration-services-transformations.md)을 참조하세요.  
  
    -   입력, 출력 및 오류 출력의 속성과 여기에 포함된 열의 속성을 보고 수정하려면 **입/출력 속성** 탭을 클릭합니다.  
  
        > [!NOTE]  
        >  원본에는 입력이 없습니다. 대상에는 선택적 오류 출력 외에는 출력이 없습니다.  
  
6.  속성 값을 보거나 수정합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 변환](transformations/integration-services-transformations.md)  
  
  
