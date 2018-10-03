---
title: 구성 된 For 루프 컨테이너 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: b9cd7ea7-b198-4a35-8b16-6acf09611ca5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2adcb3e79e3733b5fb8151bfa7f65e7bebb4d910
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126169"
---
# <a name="configure-a-for-loop-container"></a>For 루프 컨테이너 구성
  이 절차에서는 **For 루프 편집기** 대화 상자를 사용하여 For 루프 컨테이너를 구성하는 방법에 대해 설명합니다.  
  
 For Loop 컨테이너의 예는 bimonkey.com의 [실패하지 않는 SSIS 루프](http://go.microsoft.com/fwlink/?LinkId=240295) 를 참조하십시오.  
  
### <a name="to-configure-the-for-loop-container"></a>For 루프 컨테이너를 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 For 루프 컨테이너를 두 번 클릭하여 **For 루프 편집기**를 엽니다.  
  
2.  선택적으로 For 루프 컨테이너의 이름과 설명을 수정합니다.  
  
3.  선택적으로 **InitExpression** 입력란에 초기화 식을 입력합니다.  
  
4.  **EvalExpression** 입력란에 계산 식을 입력합니다.  
  
    > [!NOTE]  
    >  식은 부울로 계산되어야 합니다. 식 결과가 `false`이면 루프 실행이 중지됩니다.  
  
5.  선택적으로 **AssignExpression** 입력란에 대입 식을 입력합니다.  
  
6.  선택적으로 **식** 페이지에서 **Expressions** 를 클릭하고 For 루프 컨테이너의 속성에 대한 속성 식을 만듭니다. 자세한 내용은 [속성 식 추가 또는 변경](expressions/add-or-change-a-property-expression.md)을 참조하세요.  
  
7.  **확인** 을 클릭하여 **For 루프 편집기**를 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
 [For 루프 컨테이너](control-flow/for-loop-container.md)   
 [Integration Services&#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md)   
 [패키지에서 속성 식 사용](expressions/use-property-expressions-in-packages.md)  
  
  
