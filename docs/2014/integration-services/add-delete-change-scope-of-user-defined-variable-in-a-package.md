---
title: 추가, 삭제, 패키지에서 사용자 정의 변수의 범위 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], adding
ms.assetid: cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: abc9f00432128750e4b61e971038bbc32dd85e86
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125703"
---
# <a name="add-delete-change-scope-of-user-defined-variable-in-a-package"></a>패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경
  다음 절차에서는 **변수** 창을 사용하여 패키지에서 사용자 정의 변수를 추가, 삭제 및 변경하는 방법에 대해 설명합니다.  
  
 변수 범위에 대 한 자세한 내용은 참조 하세요. [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md)합니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 또한 런타임에 시스템 정보를 사용할 수 있도록 하 고 패키지 및 이벤트 처리기와 같은 컨테이너에서 사용할 수 있는 시스템 변수를 제공 합니다. 시스템 변수는 삭제할 수 없습니다.  
  
### <a name="to-add-a-variable"></a>변수를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 작업하려는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  다음 중 하나를 수행하여 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 변수 범위를 정의하십시오.  
  
    -   패키지 범위를 설정하려면 **제어 흐름** 탭의 디자인 화면에서 아무 곳이나 클릭합니다.  
  
    -   이벤트 처리기의 범위를 설정하려면 **이벤트 처리기** 탭의 디자인 화면에서 실행 파일 및 이벤트 처리기를 선택합니다.  
  
    -   태스크 또는 컨테이너의 범위를 설정하려면 **제어 흐름** 탭 또는 **이벤트 처리기** 탭의 디자인 화면에서 태스크 또는 컨테이너를 클릭합니다.  
  
4.  **SSIS** 메뉴에서 **변수**를 클릭합니다. **옵션** 대화 상자의 **키보드** 페이지에서 필요에 따라 선택한 키 조합에 View.Variables 명령을 매핑하여 **변수** 창을 표시할 수 있습니다.  
  
5.  **변수** 창에서 **변수 추가** 아이콘을 클릭합니다. 새 변수가 목록에 추가됩니다.  
  
6.  필요에 따라 **표 옵션** 아이콘을 클릭하고 **가변 눈금 옵션** 대화 상자에 표시할 추가 열을 선택한 다음 **확인**을 클릭합니다.  
  
7.  필요에 따라 변수 속성을 설정합니다. 자세한 내용은 [사용자 정의 변수의 속성 설정](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)을 참조하세요.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### <a name="to-delete-a-variable"></a>변수를 삭제하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하여 엽니다.  
  
3.  **SSIS** 메뉴에서 **변수**를 클릭합니다. **옵션** 대화 상자의 **키보드** 페이지에서 필요에 따라 선택한 키 조합에 View.Variables 명령을 매핑하여 **변수** 창을 표시할 수 있습니다.  
  
4.  삭제할 변수를 선택한 다음 **변수 삭제**를 클릭합니다.  
  
     변수 창에 변수가 표시되지 않는 경우 **표 옵션** 을 클릭하고 **모든 범위의 변수 표시**를 선택합니다.  
  
5.  **변수 삭제 확인** 대화 상자에서 **예** 를 클릭하여 삭제를 확인합니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### <a name="to-change-the-scope-of-a-variable"></a>변수의 범위를 변경하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하여 엽니다.  
  
3.  **SSIS** 메뉴에서 **변수**를 클릭합니다. **옵션** 대화 상자의 **키보드** 페이지에서 필요에 따라 선택한 키 조합에 View.Variables 명령을 매핑하여 **변수** 창을 표시할 수 있습니다.  
  
4.  변수를 선택한 다음 **변수 이동**을 클릭합니다.  
  
     변수 창에 변수가 표시되지 않는 경우 **표 옵션** 을 클릭하고 **모든 범위의 변수 표시**를 선택합니다.  
  
5.  **새 범위 선택** 대화 상자에서 변수 범위를 변경할 패키지나 패키지에 들어 있는 컨테이너, 태스크 또는 이벤트 처리기를 선택합니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md)   
 [패키지에서 변수 사용](../../2014/integration-services/use-variables-in-packages.md)   
 [사용자 정의 변수의 속성 설정](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)   
 [자식 패키지에서 변수 및 매개 변수의 값 사용](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
  
