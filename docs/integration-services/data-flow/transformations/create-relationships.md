---
title: 관계 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.createrelationships.f1
ms.assetid: 6ebd305f-ffd2-4a1d-b24c-e28c151b94f5
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7a7f0f3f65b1947dc22806a530fe395fbe0d7369
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-relationships"></a>관계 만들기
  **관계 만들기** 대화 상자를 사용하여 유사 항목 조회 변환 편집기, 조회 변환 편집기 및 용어 조회 변환 편집기에서 구성한 원본 열과 조회 테이블 열 간의 매핑을 편집할 수 있습니다.  
  
> [!NOTE]  
>  용어 조회 변환 편집기에서 호출하는 경우 **관계 만들기** 대화 상자는 **입력 열** 및 **조회 열** 목록만 표시합니다.  
  
 **관계 만들기** 대화 상자를 사용하는 변환에 대한 자세한 내용은 [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md), [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)및 [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **입력 열**  
 사용 가능한 입력 열 목록에서 선택합니다.  
  
 **조회 열**  
 사용 가능한 조회 열 목록에서 선택합니다.  
  
 **매핑 유형**  
 유사 항목 일치 또는 정확히 일치를 선택합니다.  
  
 유사 항목 일치를 사용하는 경우 행이 유사 항목 일치 유형이 있는 모든 열에서 충분히 유사하면 중복으로 처리됩니다. 유사 항목 일치에서 더 정확한 결과를 얻으려면 일부 열에서 유사 항목 일치 대신 정확히 일치를 사용하도록 지정합니다. 예를 들어 특정 열에 오류 또는 불일치가 없는 경우 해당 열에 정확히 일치를 지정하여 이 열에서 값이 동일한 행만 중복일 가능성이 있는 것으로 처리할 수 있습니다. 이렇게 하면 다른 열에서의 유사 항목 일치 정확도가 증가합니다.  
  
 **비교 플래그**  
 문자열 비교 옵션에 대한 자세한 내용은 [문자열 데이터 비교](../../../integration-services/data-flow/comparing-string-data.md)를 참조하세요.  
  
 **최소 유사성**  
 슬라이더를 사용하여 열 수준에서 유사성 임계값을 설정합니다. 값이 1에 가까울수록 조회 값과 원본 값이 근접하여 일치 항목으로 처리됩니다. 임계값을 높이면 고려할 레코드 수가 감소하기 때문에 비교 속도를 향상시킬 수 있습니다.  
  
 **유사성 출력 별칭**  
 선택한 열에 대한 유사성 점수를 포함하는 새 출력 열의 이름을 지정합니다. 이 값을 비워 놓으면 출력 열이 생성되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../../integration-services/integration-services-error-and-message-reference.md)   
 [유사 항목 조회 변환 편집기&#40;열 탭&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [조회 변환 편집기&#40;열 페이지&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [용어 조회 변환 편집기&#40;용어 조회 탭&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-term-lookup-tab.md)  
  
  
