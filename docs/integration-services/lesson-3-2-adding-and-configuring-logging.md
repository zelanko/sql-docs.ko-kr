---
title: '2단계: 로깅 추가 및 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 80d2eb1ec30b4729deb4891c451fc5967bec9d54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65722069"
---
# <a name="lesson-3-2-add-and-configure-logging"></a>3-2단원: 로깅 추가 및 구성

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이 태스크에서는 Lesson 3.dtsx 패키지의 데이터 흐름에 로깅을 사용하도록 설정합니다. 그런 다음, PipelineExecutionPlan 및 PipelineExecuteTrees 이벤트를 로그하도록 텍스트 파일 로그 공급자를 구성합니다. 텍스트 파일 로그 공급자는 보고 전송하기 쉬운 로그를 만듭니다. 이러한 로그 파일은 단순하기 때문에 패키지의 기본 테스트 단계에서 유용합니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너의 **로그 이벤트** 창에서 로그 항목을 볼 수도 있습니다.  
  
## <a name="add-logging-to-the-package"></a>패키지에 로깅 추가  
  
1.  **SSIS** 메뉴에서 **로깅**을 선택합니다.  
  
2.  **SSIS 로그 구성** 대화 상자의 **컨테이너** 창에서 최상위 개체가 선택되어 있는지 확인합니다. 이 개체는 3단원 패키지를 나타냅니다.
  
3.  **공급자 및 로그** 탭의 **공급자 유형** 상자에서 **텍스트 파일용 SSIS 로그 공급자**를 선택한 다음, **추가**를 선택합니다.  
  
    Integration Services는 기본 이름이 **텍스트 파일용 SSIS 로그 공급자**인 새 텍스트 파일 로그 공급자를 패키지에 추가합니다. 이제 새 로그 공급자를 구성할 수 있습니다.  
  
4.  **이름** 열에 **3단원 로그 파일**을 입력합니다.  
  
5.  **설명**을 수정할 수도 있습니다.  
  
6.  **구성** 열에서 **\<새 연결>** 을 선택하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]가 로그 정보를 기록하는 위치를 지정합니다.  
  
    **파일 연결 관리자 편집기** 대화 상자의 **사용 유형**에서 **파일 만들기**를 선택한 다음, **찾아보기**를 선택합니다. 기본적으로 **파일 선택** 대화 상자에 프로젝트 폴더가 열리지만 임의의 위치에 로그 정보를 저장할 수도 있습니다.  
  
7.  **파일 선택** 대화 상자의 **파일 이름** 상자에 **TutorialLog.log**를 입력하고 **열기**를 선택합니다.
  
8.  **확인**을 선택하여 **파일 연결 관리자 편집기** 대화 상자를 닫습니다.  
  
9. **컨테이너** 창에서 패키지 컨테이너 계층의 모든 노드를 확장한 다음 **Extract Sample Currency Data** 확인란을 포함한 모든 확인란의 선택을 취소합니다. 이제 **Extract Sample Currency Data** 의 확인란을 선택하여 이 노드에 대한 이벤트만 가져옵니다.  
  
    > [!NOTE]  
    > **Extract Sample Currency Data** 확인란이 선택되지 않고 흐리게 표시되어 있는 경우에는 태스크에서 부모 컨테이너의 로그 설정을 사용하여 해당 작업과 관련된 로그 이벤트를 활성화할 수 없습니다. 이 인스턴스를 해결하려면 부모 확인란의 선택을 취소합니다.
  
10. **자세히** 탭의 **이벤트** 열에서 **PipelineExecutionPlan** 및 **PipelineExecutionTrees** 이벤트를 선택합니다.  
  
11. **고급**을 선택하여 로그 공급자가 각 이벤트의 로그에 기록하는 세부 사항을 검토합니다. 기본적으로 지정된 이벤트에 대해 모든 정보 범주가 자동으로 선택됩니다.  
  
12. **기본**을 선택하여 정보 범주를 숨깁니다.  
  
13. **공급자 및 로그** 탭의 **이름** 열에서 **Lesson 3 Log File**을 선택합니다. 패키지의 로그 공급자를 만든 후에는 로그 공급자를 삭제하고 다시 만들지 않아도 선택적으로 로그 공급자를 선택 취소하여 로깅을 해제할 수 있습니다.  
  
14. **확인**을 선택합니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동  
[3단계: 3단원 패키지 테스트](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
