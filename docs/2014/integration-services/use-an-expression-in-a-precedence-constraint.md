---
title: 선행 제약 조건에서 식을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence constraints [Integration Services], adding expressions
- expressions [Integration Services], adding
ms.assetid: 601038bb-3b17-42ac-b09d-5b3a82fb6564
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0b2491a03e0d0121f3aa3b31f354f71b36088e5d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766126"
---
# <a name="use-an-expression-in-a-precedence-constraint"></a>선행 제약 조건에서 식 사용
  이 절차에서는 **선행 제약 조건 편집기** 대화 상자를 사용하여 선행 제약 조건에 식을 추가하는 방법에 대해 설명합니다. 선행 제약 조건에 식을 추가하려면 패키지에 태스크 또는 컨테이너와 같은 실행 개체가 적어도 두 개 이상 포함되어야 하며 선행 제약 조건에 의해 연결되어 있어야 합니다.  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>선행 제약 조건에 식을 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  **제어 흐름** 탭의 디자인 화면에서 선행 제약 조건을 두 번 클릭합니다. **선행 제약 조건 편집기** 가 열립니다.  
  
5.  **평가 작업**목록에서 **식**, **식 및 제약 조건** 또는 **식 또는 제약 조건** 을 선택합니다.  
  
6.  **실행** 텍스트 상자에 표현식을 입력하거나 Expression Builder를 실행하여 실행을 만듭니다.  
  
7.  식 구문의 유효성을 검사하려면 **테스트**를 클릭합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [선행 제약 조건](control-flow/precedence-constraints.md)   
 [기본 선행 제약 조건을 사용하여 태스크 및 컨테이너 연결](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [바로 가기 메뉴를 사용 하 여 선행 제약 조건 값 설정](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [선행 제약 조건의 속성 설정](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [Integration Services&#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md)  
  
  
