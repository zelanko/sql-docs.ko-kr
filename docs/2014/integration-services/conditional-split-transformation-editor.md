---
title: 조건부 분할 변환 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split Transformation Editor
ms.assetid: c30e1633-537a-4837-9991-6203c6f2a21e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 920ec41ae30d53853cfb757fb7fc33610953dc86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060891"
---
# <a name="conditional-split-transformation-editor"></a>조건부 분할 변환 편집기
  
  **조건부 분할 변환 편집기** 대화 상자를 사용하여 식을 만들고, 식을 평가하는 순서를 설정하고, 조건부 분할 출력의 이름을 지정할 수 있습니다. 이 대화 상자에는 식을 작성할 때 사용할 수 있는 수치 연산, 문자열 및 날짜/시간 함수와 연산자가 포함되어 있습니다. True로 평가하는 첫 번째 조건에 따라 행을 전송할 출력이 결정됩니다.  
  
> [!NOTE]  
>  조건부 분할 변환에서는 각 입력 행을 하나의 출력에만 전송합니다. 여러 조건을 입력하는 경우 조건부 분할 변환에서는 각 행을 조건이 True가 되는 첫 번째 출력으로 전송하고 해당 행에 대한 다른 조건은 무시합니다. 여러 조건을 연속적으로 평가해야 하는 경우 조건부 분할 변환을 데이터 흐름에서 연결해야 합니다.  
  
 조건부 분할 변환에 대한 자세한 내용은 [조건부 분할 변환](data-flow/transformations/conditional-split-transformation.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **주문**  
 행을 선택하고 오른쪽의 화살표 키를 사용하여 식을 평가하는 순서를 변경합니다.  
  
 **출력 이름**  
 출력 이름을 입력합니다. 기본값은 번호가 매겨진 사례 목록이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 **조건**  
 식을 입력하거나 사용 가능한 열, 변수, 함수 및 연산자 목록에서 끌어 식을 작성합니다.  
  
 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
 **관련 항목:** Ssis[&#41; 식](expressions/integration-services-ssis-expressions.md), [연산자 &#40;ssis 식&#41;](expressions/operators-ssis-expression.md)및 [함수 &#40;ssis 식](expressions/functions-ssis-expression.md)&#41;&#40;Integration Services    
  
 **기본 출력 이름**  
 기본 출력의 이름을 입력하거나 기본값을 사용합니다.  
  
 **오류 출력 구성**  
 
  [오류 출력 구성](../../2014/integration-services/configure-error-output.md) 대화 상자를 사용하여 오류 처리 방법을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [조건부 분할 변환을 사용하여 데이터 세트 분할](data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
