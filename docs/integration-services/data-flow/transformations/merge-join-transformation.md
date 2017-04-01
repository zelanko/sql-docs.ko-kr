---
title: "병합 조인 변환 | Microsoft Docs"
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
  - "sql13.dts.designer.mergejointrans.f1"
helpviewer_keywords: 
  - "데이터 집합 [Integration Services]"
  - "병합 조인 변환"
  - "데이터 집합 [Integration Services], 조인"
  - "데이터 집합 조인 [Integration Services]"
  - "조인 [SQL Server], SSIS"
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
caps.latest.revision: 54
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 54
---
# 병합 조인 변환
  병합 조인 변환은 FULL, LEFT 또는 INNER 조인으로 두 개의 정렬된 데이터 집합을 조인하여 생성된 출력을 제공합니다. 예를 들어 LEFT 조인을 사용하여 제품 정보가 포함된 테이블을 제품 제조 국가/지역이 나열된 테이블과 조인할 수 있습니다. 조인 결과로 모든 제품과 제조 국가/지역이 나열된 테이블이 생성됩니다.  
  
 다음과 같은 방법으로 병합 조인 변환을 구성할 수 있습니다.  
  
-   조인이 FULL, LEFT 또는 INNER 조인인지 지정합니다.  
  
-   조인에 사용되는 열을 지정합니다.  
  
-   변환에서 Null 값을 다른 Null과 같은 값으로 처리할지를 지정합니다.  
  
    > [!NOTE]  
    >  Null 값이 같은 값으로 처리되지 않는 경우 이 변환은 SQL Server 데이터베이스 엔진과 동일한 방식으로 Null 값을 처리합니다.  
  
 이 변환에는 두 개의 입력과 하나의 출력이 있습니다. 오류 출력은 지원하지 않습니다.  
  
## 입력 요구 사항  
 병합 조인 변환에는 정렬된 데이터를 입력해야 합니다. 이러한 중요 요구 사항에 대한 자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.  
  
## 조인 요구 사항  
 병합 조인 변환을 사용하려면 조인된 열에 일치하는 메타데이터가 있어야 합니다. 예를 들어 숫자 데이터 형식의 열을 문자 데이터 형식의 열과 조인할 수는 없습니다. 데이터가 문자열 데이터 형식이면 두 번째 입력의 열 길이는 함께 병합될 첫 번째 입력의 열 길이보다 작거나 같아야 합니다.  
  
## 버퍼 스로틀  
 병합 조인 변환에서 과도한 메모리를 사용할 위험을 줄이기 위해 Microsoft에서 필요한 변경을 수행했기 때문에 더 이상 **MaxBuffersPerInput** 속성 값을 구성할 필요가 없습니다. 과도한 메모리가 사용되는 문제는 여러 병합 조인 입력에서 균일하지 않은 속도로 데이터를 생성하는 경우에 발생합니다.  
  
## 관련 작업  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 이 변환의 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [병합 조인 변환을 사용하여 데이터 집합 확장](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## 관련 항목:  
 [병합 조인 변환 편집기](../../../integration-services/data-flow/transformations/merge-join-transformation-editor.md)   
 [병합 변환](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [UNION ALL 변환](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  