---
title: 용어 추출 변환 편집기 (고급 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6c783a06d5d5518639e6368f5c1eb572e60206b5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962263"
---
# <a name="term-extraction-transformation-editor-advanced-tab"></a>용어 추출 변환 편집기(고급 탭)
  **용어 추출 변환 편집기** 대화 상자의 **고급** 탭을 사용하여 빈도, 길이 및 단어 또는 구 추출 여부와 같은 추출에 대한 속성을 지정할 수 있습니다.  
  
 용어 추출 변환에 대한 자세한 내용은 [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **수식어**  
 변환에서 개별 명사만 추출하도록 지정합니다.  
  
 **명사 구**  
 변환에서 명사구만 추출하도록 지정합니다.  
  
 **명사 및 명사구**  
 변환에서 명사 및 명사구를 모두 추출하도록 지정합니다.  
  
 **빈도**  
 점수를 용어의 빈도로 지정합니다.  
  
 **TFIDF**  
 점수를 용어의 TFIDF 값으로 지정합니다. TFIDF 점수는 TF(용어 빈도)와 IDF(역 문서 빈도)의 곱으로, 용어 T의 TFIDF = (T의 빈도) * log((입력의 행 수)/(T를 포함하는 행 수))와 같이 정의됩니다.  
  
 **빈도 임계값**  
 단어 또는 구를 추출할 때까지 발생해야 하는 횟수를 지정합니다. 기본값은 2입니다.  
  
 **최대 용어 길이**  
 단어 구의 최대 길이를 지정합니다. 이 옵션은 명사구에만 영향을 줍니다. 기본 값은 12입니다.  
  
 **대/소문자 구분 용어 추출 사용**  
 추출 시 대/소문자 구분 여부를 지정합니다. 기본값은 `False`입니다.  
  
 **오류 출력 구성**  
 [오류 출력 구성](../../2014/integration-services/configure-error-output.md) 대화 상자를 사용하여 오류 발생의 원인이 되는 행에 대한 오류 처리를 지정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [용어 추출 변환 편집기 &#40;용어 추출 탭&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [용어 추출 변환 편집기 &#40;제외 탭&#41;](../../2014/integration-services/term-extraction-transformation-editor-exclusion-tab.md)   
 [용어 조회 변환](data-flow/transformations/lookup-transformation.md)  
  
  
