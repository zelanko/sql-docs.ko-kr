---
title: "DQS 정리 변환 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터 수정"
  - "데이터 수정"
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# DQS 정리 변환
  DQS 정리 변환은 DQS(Data Quality Services)를 통해, 데이터 원본 또는 유사한 데이터 원본에 대해 만든 승인된 규칙을 적용하여 연결된 데이터 원본에서 데이터를 수정합니다. 데이터 수정 규칙에 대한 자세한 내용은 [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)을 참조하십시오. DQS에 대한 자세한 내용은 [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)을 참조하십시오.  
  
 데이터를 수정해야 할지 여부를 확인하기 위해 DQS 정리 변환은 다음과 같은 조건이 충족되는 경우 입력 열의 데이터를 처리합니다.  
  
-   데이터 수정을 위해 열이 선택됩니다.  
  
-   열 데이터 형식에 데이터 수정이 지원됩니다.  
  
-   열은 호환 가능한 데이터 형식의 도메인에 매핑됩니다.  
  
 변환에는 행 수준 오류를 처리하기 위해 구성할 수 있는 오류 출력이 포함됩니다. 오류 출력을 구성하려면 **DQS 정리 변환 편집기**를 사용합니다.  
  
 데이터 흐름에 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) 을 포함하여 중복된 것으로 간주되는 데이터 행을 식별할 수 있습니다.  
  
## 데이터 품질 프로젝트 및 값  
 DQS 정리 변환으로 데이터를 처리하면 Data Quality 서버에 정리 프로젝트가 생성됩니다. Data Quality 클라이언트를 사용하여 프로젝트를 관리합니다. 또한 Data Quality 클라이언트를 사용하여 프로젝트 값을 DQS 기술 자료 도메인으로 가져올 수 있습니다. 값만 도메인(또는 연결된 도메인)으로 가져올 수 있으며, DQS 정리 변환은 해당 도메인을 사용하도록 구성되었습니다.  
  
## 관련 작업  
  
-   [데이터 품질 클라이언트에서 Integration Services 프로젝트 열기](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [도메인으로 정리 프로젝트 값 가져오기](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [데이터 원본에 데이터 품질 규칙 적용](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## 관련 내용  
  
-   [데이터 품질 프로젝트 열기, 잠금 해제, 이름 바꾸기 및 삭제](https://msdn.microsoft.com/library/hh510417.aspx)  
  
-   social.technet.microsoft.com의 문서, [복합 도메인을 사용하여 복합 데이터 정리](http://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)  
  
  