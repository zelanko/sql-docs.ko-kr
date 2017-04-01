---
title: "변수 창 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.variables.f1"
  - "sql13.dts.designer.variableoptionswindow.f1"
helpviewer_keywords: 
  - "변수 창 대화 상자"
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
caps.latest.revision: 53
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 52
---
# 변수 창
  **변수** 창을 사용하여 사용자 정의 변수를 생성 및 수정하고 시스템 변수를 볼 수 있습니다.  
  
 기본적으로는 **변수** 창은 **의 SSID 디자이너에 있는** 연결 관리자 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]영역 아래에 있습니다. **변수** 창이 표시되지 않는 경우 **SSIS** 메뉴에서 **변수** 를 클릭하여 창을 표시합니다.  
  
 **옵션** 대화 상자의 **키보드** 페이지에서 필요에 따라 선택한 키 조합에 View.Variables 명령을 매핑하여 **변수** 창을 표시할 수 있습니다.  
  
> [!NOTE]  
>  **Name** 및 **Namespace** 속성 값은 Unicode Standard 2.0에 정의된 대로 영문자 또는 밑줄(_)로 시작해야 합니다. 후속 문자는 Unicode Standard 2.0에 정의된 문자 또는 숫자이거나 밑줄(\_)일 수 있습니다.  
  
## 옵션  
 **변수 추가**  
 사용자 정의 변수를 추가합니다.  
  
 **변수 이동**  
 목록에서 변수를 클릭하고 **변수 이동**을 클릭하여 변수 범위를 변경합니다. **새 범위 선택** 대화 상자에서 변수 범위를 변경할 패키지나 패키지에 들어 있는 컨테이너, 태스크 또는 이벤트 처리기를 선택합니다.  
  
 변수 범위에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services/integration-services-ssis-variables.md)를 참조하세요.  
  
 **변수 삭제**  
 목록에서 변수를 선택한 다음 **변수 삭제**를 클릭합니다.  
  
 **표 옵션**  
 열 선택을 변경하고 **변수** 창에 필터를 적용할 수 있는 **가변 눈금 옵션** 대화 상자를 열려면 클릭합니다. 자세한 내용은 [가변 눈금 옵션](../integration-services/variable-grid-options.md)을 참조하세요.  
  
 **이름**  
 변수 이름을 봅니다. 사용자 정의 변수의 이름을 업데이트할 수 있습니다.  
  
 **범위**  
 변수의 범위를 봅니다. 변수 범위는 전체 패키지 범위이거나 컨테이너 또는 태스크 범위입니다. 변수 범위가 충분해야 변수 값을 읽거나 설정하는 데 필요한 모든 다른 태스크 또는 구성 요소에 변수가 표시됩니다.  
  
 변수를 클릭하고 **변수** 창에서 **변수 이동** 을 클릭하여 범위를 변경할 수 있습니다.  
  
 **데이터 형식**  
 변수의 데이터 형식을 봅니다. 사용자 정의 변수에 대한 목록에서 데이터 형식을 선택할 수 있습니다.  
  
> [!NOTE]  
>  변수에 식을 할당할 경우 데이터 형식을 변경할 수 없습니다.  
  
 **Value**  
 변수 값을 봅니다. 사용자 정의 변수에 대한 값을 업데이트할 수 있습니다. 이 값은 리터럴 또는 식일 수 있으며 값은 다중 행 문자열일 수 있습니다. 변수에 식을 할당하려면 **변수** 창의 **식** 열 옆에 있는 줄임표 단추를 클릭합니다.  
  
 **네임스페이스**  
 네임스페이스 이름을 봅니다. 사용자 정의 변수는 처음에 **User** 네임스페이스에 생성되지만 **네임스페이스** 필드에서 해당 네임스페이스 이름을 변경할 수 있습니다. 이 열을 표시하려면 **표 옵션**을 클릭합니다.  
  
 **Raise Change Event**  
 값이 변경될 때 **OnVariableValueChanged** 이벤트를 발생시킬지 여부를 나타냅니다. 사용자 정의 및 시스템 변수에 대한 값을 업데이트할 수 있습니다. 기본적으로 **변수** 창에는 이 열이 나열되지 않습니다. 이 열을 표시하려면 **표 옵션**을 클릭합니다.  
  
 **Description**  
 변수 설명을 봅니다. 사용자 정의 변수에 대한 설명을 변경할 수 있습니다. 기본적으로 **변수** 창에는 이 열이 나열되지 않습니다. 이 열을 표시하려면 **표 옵션**을 클릭합니다.  
  
 **식**  
 변수에 할당된 식을 봅니다. 식을 할당하려면 줄임표 단추를 클릭합니다.  
  
 변수에 식을 할당할 경우 해당 변수 옆에 특수 아이콘 표식이 표시됩니다. 이 특수 아이콘 표식은 식이 설정되어 있는 연결 관리자 및 태스크 옆에도 표시됩니다.  
  
## 관련 항목:  
 [Integration Services&#40;SSIS&#41; 변수](../integration-services/integration-services-ssis-variables.md)   
 [패키지에서 변수 사용](../Topic/Use%20Variables%20in%20Packages.md)   
 [Integration Services&#40;SSIS&#41; 식](../integration-services/expressions/integration-services-ssis-expressions.md)   
 [패키지 실행을 위한 덤프 파일 생성](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  