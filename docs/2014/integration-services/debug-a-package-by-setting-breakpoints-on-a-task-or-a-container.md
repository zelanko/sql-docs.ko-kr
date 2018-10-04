---
title: 태스크 또는 컨테이너에 중단점을 설정 하 여 패키지 디버깅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], breakpoints
- breakpoints [Integration Services]
- tasks [Integration Services], breakpoints
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff0f1ef3f7baff1c39b3d338f47eb5eddde286e7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098183"
---
# <a name="debug-a-package-by-setting-breakpoints-on-a-task-or-a-container"></a>태스크 또는 컨테이너에 중단점을 설정하여 패키지 디버깅
  이 절차에서는 패키지, 태스크, For 루프 컨테이너, Foreach 루프 컨테이너 또는 시퀀스 컨테이너에 중단점을 설정하는 방법을 설명합니다.  
  
### <a name="to-set-breakpoints-in-a-package-a-task-or-a-container"></a>패키지, 태스크 또는 컨테이너에 중단점을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  중단점을 설정할 패키지를 두 번 클릭합니다.  
  
3.  SSIS 디자이너에서 다음을 수행합니다.  
  
    -   패키지 개체에 중단점을 설정하려면 **제어 흐름** 탭을 클릭하고 디자인 화면에 아무 곳에 커서를 놓고 마우스 오른쪽 단추를 클릭한 다음 **중단점 편집**을 클릭합니다.  
  
    -   패키지 제어 흐름에 중단점을 설정하려면 **제어 흐름** 탭을 클릭하고 태스크, For 루프 컨테이너, Foreach 루프 컨테이너 또는 시퀀스 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **중단점 편집**을 클릭합니다.  
  
    -   이벤트 처리기에 중단점을 설정하려면 **이벤트 처리기** 탭을 클릭하고 태스크, For 루프 컨테이너, Foreach 루프 컨테이너 또는 시퀀스 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **중단점 편집**을 클릭합니다.  
  
4.  **중단점 설정 \<컨테이너 이름>** 대화 상자에서 활성화할 중단점을 선택합니다.  
  
5.  필요에 따라 각 중단점의 적중 횟수 형식 및 적중 횟수를 수정합니다.  
  
6.  패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [패키지 개발용 문제 해결 도구](troubleshooting/troubleshooting-tools-for-package-development.md)   
 [스크립트 태스크 및 스크립트 구성 요소에서 중단점을 설정 하 여 스크립트 디버깅](data-flow/transformations/script-component.md)   
 [스크립트 태스크 코딩 및 디버깅](control-flow/script-task.md)   
 [스크립트 구성 요소 코딩 및 디버깅](extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
