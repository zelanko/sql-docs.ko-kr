---
title: 기본 선행 제약 조건을 사용 하 여 태스크 및 컨테이너 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- default precedence constraints
- containers [Integration Services], precedence constraints
ms.assetid: 8f31f15f-98ff-4c35-b41f-8b8cfd148d75
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: cf278d02e1c2eb523964ee07b039b46942c7e9de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080462"
---
# <a name="connect-tasks-and-containers-by-using-a-default-precedence-constraint"></a>기본 선행 제약 조건을 사용하여 태스크 및 컨테이너 연결
  선행 제약 조건은 두 실행 개체를 연결합니다. 실행 개체는 임의의 태스크, For 루프, Foreach 루프 또는 시퀀스 컨테이너일 수 있습니다. 이 절차에서는 선행 제약 조건에 대한 기본 동작을 설정하는 방법과 기본 선행 제약 조건을 사용하여 실행 개체를 연결하는 방법에 대해 설명합니다.  
  
## <a name="creating-default-precedence-constraints"></a>기본 선행 제약 조건 만들기  
 처음 사용할 때 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너, 선행 제약 조건의 기본값은 `Success`합니다. 다음 단계에 따라 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너를 구성하고 선행 제약 조건에 대해 다른 기본값을 사용하십시오.  
  
#### <a name="to-set-the-default-value-for-precedence-constraints"></a>선행 제약 조건에 대한 기본값을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 엽니다.  
  
2.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
3.  **옵션** 대화 상자에서 **비즈니스 인텔리전스 디자이너** 를 확장한 후 **Integration Services 디자이너**를 확장합니다.  
  
4.  **제어 흐름 자동 연결** 을 클릭하고 **기본적으로 선택한 셰이프에 새 셰이프 연결**을 선택합니다.  
  
5.  드롭다운 목록에서 **새 셰이프에 Failure 제약 조건 사용** 또는 **새 셰이프에 Completion 제약 조건 사용**을 선택합니다.  
  
6.  **확인**을 클릭합니다.  
  
#### <a name="to-create-a-default-precedence-constraint"></a>기본 선행 제약 조건을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  **제어 흐름** 탭의 디자인 화면에서 태스크 또는 컨테이너를 클릭하고 선행 제약 조건을 적용하려는 실행 개체에 해당 연결선을 끌어 옵니다.  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [선행 제약 조건](control-flow/precedence-constraints.md)   
 [바로 가기 메뉴를 사용 하 여 선행 제약 조건 값 설정](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [선행 제약 조건의 속성 설정](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [선행 제약 조건에서 식 사용](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  