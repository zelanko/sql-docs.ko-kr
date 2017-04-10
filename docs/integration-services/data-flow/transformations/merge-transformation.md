---
title: "병합 변환 | Microsoft Docs"
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
  - "sql13.dts.designer.mergetrans.f1"
helpviewer_keywords: 
  - "데이터 집합 병합 [Integration Services]"
  - "데이터 병합 [Integration Services]"
  - "병합 변환"
  - "데이터 집합 결합"
  - "데이터 집합 [Integration Services], 병합"
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# 병합 변환
  병합 변환은 두 개의 정렬된 데이터 집합을 단일 데이터 집합으로 결합합니다. 각 데이터 집합의 행은 해당 키 열의 값을 기반으로 출력에 삽입됩니다.  
  
 데이터 흐름에 병합 변환을 포함하면 다음 태스크를 수행할 수 있습니다.  
  
-   테이블 및 파일과 같은 데이터 원본 두 개의 데이터 병합  
  
-   병합 변환을 중첩하여 복잡한 데이터 집합 만들기  
  
-   데이터 오류를 수정한 후 행 다시 병합  
  
 병합 변환은 UNION ALL 변환과 유사합니다. 다음과 같은 경우 병합 변환 대신 UNION ALL 변환을 사용합니다.  
  
-   변환 입력이 정렬되지 않는 경우  
  
-   결합된 출력을 정렬할 필요가 없는 경우  
  
-   변환에 둘 이상의 입력이 있는 경우  
  
## 입력 요구 사항  
 병합 변환에는 정렬된 데이터를 입력해야 합니다. 이러한 중요 요구 사항에 대한 자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.  
  
 또한 병합 변환에 입력한 병합된 열에는 일치하는 메타데이터가 있어야 합니다. 예를 들어 숫자 데이터 형식의 열을 문자 데이터 형식의 열과 병합할 수는 없습니다. 데이터가 문자열 데이터 형식이면 두 번째 입력의 열 길이는 함께 병합될 첫 번째 입력의 열 길이보다 작거나 같아야 합니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 병합 변환용 사용자 인터페이스는 동일한 메타데이터가 있는 열을 자동으로 매핑합니다. 그런 다음 호환 가능한 데이터 형식의 다른 열을 수동으로 매핑할 수 있습니다.  
  
 이 변환에는 두 개의 입력과 하나의 출력이 있습니다. 오류 출력은 지원하지 않습니다.  
  
## 병합 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **병합 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Merge Transformation Editor](../../../integration-services/data-flow/transformations/merge-transformation-editor.md)를 참조하십시오.  
  
 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [공용 속성](../Topic/Common%20Properties.md)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## 관련 작업  
 속성을 설정하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## 관련 항목:  
 [병합 조인 변환](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [UNION ALL 변환](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  