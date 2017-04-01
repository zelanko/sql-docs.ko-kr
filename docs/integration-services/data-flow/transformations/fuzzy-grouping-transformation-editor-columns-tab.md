---
title: "유사 항목 그룹화 변환 편집기(열 탭) | Microsoft Docs"
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
  - "sql13.dts.designer.fuzzygroupingtransformation.columns.f1"
helpviewer_keywords: 
  - "유사 항목 그룹화 변환 편집기"
ms.assetid: 24f4539f-2a9f-4acd-acc7-06228a07f7df
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# 유사 항목 그룹화 변환 편집기(열 탭)
  **유사 항목 그룹화 변환 편집기** 대화 상자의 **열** 탭을 사용하여 중복 값을 가진 행을 그룹화하는 데 사용할 열을 지정할 수 있습니다.  
  
 유사 항목 그룹화 변환에 대한 자세한 내용은 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)을 참조하십시오.  
  
## 옵션  
 **사용 가능한 입력 열**  
 중복 값을 가진 행을 그룹화하는 데 사용할 입력 열을 이 목록에서 선택합니다.  
  
 **이름**  
 사용 가능한 입력 열 이름을 표시합니다.  
  
 **통과**  
 입력 열을 변환의 출력에 포함할지 여부를 선택합니다. 그룹화에 사용되는 모든 열이 자동으로 출력에 복사됩니다. 이 열을 선택하여 추가 열을 포함할 수 있습니다.  
  
 **입력 열**  
 **사용 가능한 입력 열** 목록에서 이전에 선택한 입력 열 중 하나를 선택합니다.  
  
 **출력 별칭**  
 해당 출력 열을 설명하는 이름을 입력합니다. 기본적으로 출력 열 이름은 입력 열 이름과 같습니다.  
  
 **그룹 출력 별칭**  
 그룹화된 중복의 정식 값이 포함될 열을 설명하는 이름을 입력합니다. 이 출력 열의 기본 이름은 입력 열 이름에 _clean이 추가된 것입니다.  
  
 **일치 유형**  
 유사 항목 일치 또는 정확히 일치를 선택합니다. 유사 항목 일치 유형에서 모든 열이 충분히 유사할 경우 중복 행으로 간주됩니다. 또한 특정 열에 대해 정확히 일치를 지정하면 정확히 일치 열에 동일한 값이 포함된 행만 중복 가능한 것으로 간주됩니다. 따라서 특정 열에 확실하게 오류 없음이나 불일치가 포함되어 있으면 해당 열에 대해 정확히 일치를 지정하여 다른 열에 대한 유사 항목 일치의 정확도를 높일 수 있습니다.  
  
 **최소 유사성**  
 슬라이더를 사용하여 조인 수준에서 유사성 임계값을 설정합니다. 값이 1에 가까울수록 조회 값과 원본 값이 근접하여 일치 항목으로 처리됩니다. 임계값을 높이면 고려할 레코드 수가 감소하기 때문에 비교 속도를 향상시킬 수 있습니다.  
  
 **유사성 출력 별칭**  
 선택한 조인에 대한 유사성 점수가 포함된 새 출력 열의 이름을 지정합니다. 이 값을 비워 놓으면 출력 열이 생성되지 않습니다.  
  
 **숫자**  
 열 데이터 비교 시 선행 및 후행 숫자의 의미를 지정합니다. 예를 들어 선행 숫자가 의미가 있을 경우 "123 Main Street"는 "456 Main Street"와 그룹화되지 않습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Neither**|선행 및 후행 숫자 모두 의미가 없습니다.|  
|**Leading**|선행 숫자만 의미가 있습니다.|  
|**Trailing**|후행 숫자만 의미가 있습니다.|  
|**LeadingAndTrailing**|선행 및 후행 숫자 모두 의미가 있습니다.|  
  
 **비교 플래그**  
 문자열 비교 옵션에 대한 자세한 내용은 [문자열 데이터 비교](../../../integration-services/data-flow/comparing-string-data.md)를 참조하세요.  
  
## 관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../../integration-services/integration-services-error-and-message-reference.md)   
 [유사 항목 그룹화 변환을 사용하여 유사한 데이터 행 식별](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  