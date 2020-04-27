---
title: 파생 열 변환 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- Derived Column Transformation Editor
ms.assetid: ff73923e-d245-43d8-bf24-af3bdc942e51
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4fc2701ad53cd0071be40100d168d5d5571d2958
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059566"
---
# <a name="derived-column-transformation-editor"></a>파생 열 변환 편집기
  **파생 열 변환 편집기** 대화 상자를 사용하여 새 열 또는 대체 열을 채우는 식을 만들 수 있습니다.  
  
 파생 열 변환에 대한 자세한 내용은 [Derived Column Transformation](data-flow/transformations/derived-column-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **변수 및 열**  
 사용 가능한 변수 및 열 목록에서 아래 창의 기존 테이블 행이나 목록 아래쪽의 새 행으로 변수 또는 열을 끌어 변수 또는 입력 열을 사용하는 식을 작성합니다.  
  
 **함수 및 연산자**  
 목록에서 아래 창으로 함수와 연산자를 끌어 함수 또는 연산자를 사용하여 입력 데이터와 직접 출력 데이터를 계산하는 식을 작성합니다.  
  
 **파생 열 이름**  
 파생 열의 이름을 지정합니다. 기본값은 번호가 매겨진 파생 열 목록이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 **파생 열**  
 목록에서 파생 열을 선택합니다. 파생 열을 새 출력 열로 추가할지, 아니면 기존 열의 데이터를 바꿀지를 선택합니다.  
  
 **식**  
 식을 입력하거나 사용 가능한 열, 변수, 함수 및 연산자에 대한 이전 목록에서 끌어 식을 작성합니다.  
  
 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md), [연산자&#40;SSIS 식&#41;](expressions/operators-ssis-expression.md) 및 [함수&#40;SSIS 식&#41;](expressions/functions-ssis-expression.md)  
  
 **데이터 형식**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 식을 자동으로 계산하고 데이터 형식을 적절하게 설정합니다. 이 열의 값은 읽기 전용입니다. 자세한 내용은 [Integration Services 데이터 형식](data-flow/integration-services-data-types.md)을 참조 하세요.  
  
 **길이**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 식을 자동으로 계산하고 문자열 데이터의 열 길이를 설정합니다. 이 열의 값은 읽기 전용입니다.  
  
 **정밀도**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 데이터 형식을 기반으로 숫자 데이터의 전체 자릿수를 자동으로 설정합니다. 이 열의 값은 읽기 전용입니다.  
  
 **규모**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 데이터 형식을 기반으로 숫자 데이터의 소수 자릿수를 자동으로 설정합니다. 이 열의 값은 읽기 전용입니다.  
  
 **코드 페이지**  
 새 열에 데이터를 추가하는 경우 **파생 열 변환 편집기** 대화 상자가 DT_STR 데이터 형식에 대한 코드 페이지를 자동으로 설정합니다. **코드 페이지**를 업데이트할 수 있습니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](../../2014/integration-services/configure-error-output.md) 대화 상자를 사용하여 오류 처리 방법을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [파생 열 변환을 사용하여 열 값 파생](data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
  
