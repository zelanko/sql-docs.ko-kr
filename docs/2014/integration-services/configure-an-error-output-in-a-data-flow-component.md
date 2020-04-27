---
title: 데이터 흐름 구성 요소에서 오류 출력 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- errors [Integration Services], data flow components
- components [Integration Services], data flow
- error outputs [Integration Services]
ms.assetid: 53d7eeea-927d-4b45-8ea9-084e65ad5390
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa9df7d84a793c6825ba82b22c3b0cf567f42c3b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060822"
---
# <a name="configure-an-error-output-in-a-data-flow-component"></a>데이터 흐름 구성 요소에서 오류 출력 구성
  많은 데이터 흐름 구성 요소가 오류 출력을 지원하며 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너는 구성 요소에 따라 오류 출력을 다르게 구성할 수 있는 방법을 제공합니다. 오류 출력을 구성하는 것 외에도 오류 출력의 열을 구성할 수도 있습니다. 이 작업에는 구성 요소에서 추가한 **ErrorCode** 및 **ErrorColumn** 열의 구성이 포함됩니다.  
  
## <a name="configuring-an-error-output"></a>오류 출력 구성  
 다음 두 가지 옵션을 사용하여 오류 출력을 구성할 수 있습니다.  
  
-   **오류 출력 구성** 대화 상자를 사용합니다. 이 대화 상자를 사용하면 오류 출력을 지원하는 데이터 흐름 구성 요소의 오류 출력을 구성할 수 있습니다.  
  
-   구성 요소의 편집기 대화 상자를 사용합니다. 일부 구성 요소는 해당 편집기 대화 상자에서 직접 오류 출력을 구성할 수 있습니다. 그러나 ADO.NET 원본, 열 가져오기 변환, OLE DB 명령 변환 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 대상의 편집기 대화 상자에서는 오류 출력을 구성할 수 없습니다.  
  
 다음 절차에서는 이러한 대화 상자를 사용하여 오류 출력을 구성하는 방법을 설명합니다.  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>오류 출력 구성 대화 상자를 사용하여 오류 출력을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **데이터 흐름** 탭을 클릭합니다.  
  
4.  오류의 원본에 해당하는 구성 요소에서 빨간 색 화살표로 표시된 오류 출력을 데이터 흐름의 다른 구성 요소로 끌어다 놓습니다.  
  
5.  구성 요소 입력의 각 열에 대해 **오류 출력 구성** 대화 상자의 **오류** 및 **잘림** 열에 있는 동작을 선택합니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>구성 요소의 편집기 대화 상자를 사용하여 오류 출력을 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **데이터 흐름** 탭을 클릭합니다.  
  
4.  오류 출력을 구성할 데이터 흐름 구성 요소를 두 번 클릭한 다음 구성 요소에 따라 다음 단계 중 하나를 수행합니다.  
  
    -   **오류 출력 구성**을 클릭합니다.  
  
    -   **오류 출력**을 클릭합니다.  
  
5.  각 열에 대한 **오류** 옵션을 설정합니다.  
  
6.  각 열에 대한 **잘림** 옵션을 설정합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
## <a name="configuring-error-output-columns"></a>오류 출력 열 구성  
 오류 출력 열을 구성하려면 **고급 편집기** 대화 상자의 **입/출력 속성** 탭을 사용해야 합니다.  
  
#### <a name="to-configure-error-output-columns"></a>오류 출력 열을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **데이터 흐름** 탭을 클릭합니다.  
  
4.  구성하려는 오류 출력 열이 있는 구성 요소를 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 클릭합니다.  
  
5.  **입력 및 출력 속성** 탭을 클릭 하 고 ** \<구성 요소 이름> 오류 출력** 을 확장 한 다음 **출력 열**을 확장 합니다.  
  
6.  열을 클릭하고 속성을 업데이트합니다.  
  
    > [!NOTE]  
    >   열 목록은 구성 요소 입력 내의 열, 이전 오류 출력이 추가한 **ErrorCode** 및 **ErrorColumn** 열, 현재 구성 요소가 추가한 **ErrorCode** 및 **ErrorColumn** 열을 포함합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 오류 처리](data-flow/error-handling-in-data.md)  
  
  
