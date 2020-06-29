---
title: 선행 제약 조건의 속성 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Precedence Constraint Editor dialog box
- precedence constraints [Integration Services], properties
ms.assetid: d990f600-5c09-4cd5-8528-0a58d79dc9f2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 55e71b6615afc15c2963b4dbb9bfbf2790e90b3b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421545"
---
# <a name="set-the-properties-of-a-precedence-constraint"></a>선행 제약 조건의 속성 설정
  선행 제약 조건의 속성을 설정하려면 다음 도구 중 하나를 사용하면 됩니다.  
  
-   **선행 제약 조건 편집기** 를 사용할 수 있습니다.  
  
-   속성 창을 사용할 수 있습니다. 속성 창에는 **선행 제약 조건 편집기** 대화 상자에서 사용할 수 없는 선행 제약 조건을 구성하기 위한 속성이 나열됩니다. 속성 창에서는 선행 제약 조건의 설명과 이름을 제공하고 디자인 화면에서 선행 제약 조건에 표시할 주석을 구성할 수 있습니다.  
  
 다음 절차에서는 이러한 각 도구를 사용하여 선행 제약 조건의 속성을 설정하는 방법에 대해 설명합니다.  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-precedence-constraint-editor"></a>선행 제약 조건 편집기를 사용하여 선행 제약 조건의 속성을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  선행 제약 조건을 두 번 클릭합니다.  
  
     **선행 제약 조건 편집기** 가 열립니다.  
  
5.  **평가 작업** 드롭다운 목록에서 평가 작업을 선택합니다.  
  
6.  `Value`드롭다운 목록에서 선행 실행 파일의 실행 결과를 선택 합니다.  
  
7.  계산 작업에 식이 사용 되는 경우 상자에 식을 `Expression` 입력 하 고 **테스트** 를 클릭 하 여 식을 계산 합니다.  
  
    > [!NOTE]  
    >  변수 이름은 대소문자를 구분합니다.  
  
8.  제약 조건이 지정 된 실행 파일에 여러 태스크 또는 컨테이너가 연결 된 경우에는 **논리적 AND** 를 선택 하 여 모든 선행 실행 파일의 실행 결과가로 계산 되어야 하도록 지정 합니다 `true` . 단일 실행 결과만로 계산 되도록 지정 하려면 **논리적 OR** 을 선택 합니다 `true` .  
  
9. **확인** 을 클릭하여 **선행 제약 조건 편집기**를 닫습니다.  
  
10. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-properties-window"></a>속성 창을 사용하여 선행 제약 조건의 속성을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 수정할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭 합니다. **제어 흐름** 탭의 디자인 화면에서 선행 제약 조건을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다. 속성 창에서 속성 값을 수정합니다.  
  
4.  **속성** 창에서 다음과 같은 선행 제약 조건의 읽기/쓰기 속성을 설정합니다.  
  
    |읽기/쓰기 속성|구성 동작|  
    |--------------------------|--------------------------|  
    |설명|설명을 제공합니다.|  
    |EvalOp|계산 작업을 선택합니다. `Expression`, **Expressionandconstant**또는 **expressionandconstant** 작업을 선택할 경우 식을 지정할 수 있습니다.|  
    |식|계산 작업에 식이 포함된 경우 식을 제공합니다. 식은 부울로 계산되어야 합니다. 식 언어에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md)을 참조하세요.|  
    |LogicalAnd|`LogicalAnd`선행 제약 조건이 다른 선행 제약 조건과 함께 계산 되는지 여부를 지정 하려면 설정 하 고, 여러 실행 파일이 제약 조건이 있는 실행 파일에 연결 된 경우|  
    |이름|선행 제약 조건의 이름을 업데이트합니다.|  
    |ShowAnnotation|사용할 주석의 유형을 지정합니다. 주석을 사용하지 않으려면 **Never** 를 선택하고, 요청 시 주석을 사용하려면 **AsNeeded** 를 선택하고, Name 속성의 값을 사용하여 자동으로 주석을 달려면 **ConstraintName** 을 선택합니다. 또한 Description 속성의 값을 사용하여 자동으로 주석을 달려면 **ConstraintDescription** 을 선택하고, Value 및 Expression 속성의 값을 사용하여 자동으로 주석을 달려면 **ConstraintOptions** 를 선택합니다.|  
    |값|EvalOP 속성에 지정된 계산 작업에 제약 조건이 포함된 경우 제약 조건이 지정된 실행 개체의 실행 결과를 선택합니다.|  
  
5.  속성 창을 닫습니다.  
  
6.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [선행 제약 조건](control-flow/precedence-constraints.md)   
 [기본 선행 제약 조건을 사용 하 여 태스크 및 컨테이너 연결](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [바로 가기 메뉴를 사용 하 여 선행 제약 조건 값 설정](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [선행 제약 조건에서 식 사용](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
