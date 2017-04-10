---
title: "열 길이 분포 프로필 요청 옵션(데이터 프로파일링 태스크) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터 프로파일링 태스크 편집기"
ms.assetid: 1a4de41f-f38d-40ea-ba1b-6c0ef67ea52a
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 21
---
# 열 길이 분포 프로필 요청 옵션(데이터 프로파일링 태스크)
  **프로필 요청** 페이지의 **요청 속성** 창을 사용하여 요청 창에서 선택한 **열 길이 분포 프로필 요청** 의 옵션을 설정할 수 있습니다. 열 길이 분포 프로필은 선택한 열에 있는 문자열 값의 모든 고유 길이 및 각 길이가 나타내는 테이블 내 행의 비율을 보고합니다. 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 두 개의 문자로 구성된 미국 주 코드 열을 프로파일링하는 중 3자 이상의 값이 검색될 수 있습니다.  
  
> [!NOTE]  
>  이 항목에서 설명하는 옵션은 **데이터 프로파일링 태스크 편집기** 의 **프로필 요청 페이지**에 나타납니다. 편집기의 이 페이지에 대한 자세한 내용은 [데이터 프로파일링 태스크 편집기&#40;프로필 요청 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)를 참조하세요.  
  
 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요. 데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 분석하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요.  
  
## 요청 속성 옵션  
 **열 길이 분포 프로필 요청**에 대해 **요청 속성** 창에는 다음 옵션 그룹이 표시됩니다.  
  
-   **데이터**- **TableOrView** 및 **Column** 옵션이 포함되어 있습니다.  
  
-   **일반**  
  
-   **옵션**  
  
### 데이터 옵션  
 **ConnectionManager**  
 .NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\(SqlClient)를 사용하여 프로파일링할 테이블이나 뷰가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 기존 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 선택합니다.  
  
 **TableOrView**  
 프로파일링할 열이 포함된 기존 테이블이나 뷰를 선택합니다.  
  
 자세한 내용은 이 항목의 "TableorView 옵션" 섹션을 참조하십시오.  
  
 **열**  
 프로파일링할 기존 열을 선택합니다. 모든 열을 프로파일링하려면 **(\*)**를 선택합니다.  
  
 자세한 내용은 이 항목의 "열 옵션" 섹션을 참조하십시오.  
  
#### TableOrView 옵션  
 **스키마**  
 선택한 테이블이 속해 있는 스키마를 지정합니다. 이 옵션은 읽기 전용입니다.  
  
 **테이블**  
 선택한 테이블의 이름을 표시합니다. 이 옵션은 읽기 전용입니다.  
  
#### 열 옵션  
 **IsWildCard**  
 **(\*)** 와일드카드가 선택되었는지 여부를 지정합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)**를 선택한 경우 **True**로 설정됩니다. 프로파일링할 개별 열을 선택한 경우에는 **False** 로 설정됩니다. 이 옵션은 읽기 전용입니다.  
  
 **ColumnName**  
 선택한 열의 이름을 표시합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)**를 선택한 경우 비어 있습니다. 이 옵션은 읽기 전용입니다.  
  
 ** StringCompareOptions**  
 이 옵션은 열 길이 분포 프로필에 적용되지 않습니다.  
  
### 일반 옵션  
 **RequestID**  
 이 프로필 요청을 식별할 설명이 포함된 이름을 입력합니다. 일반적으로 자동 생성된 값은 변경하지 않아도 됩니다.  
  
### 옵션  
 **IgnoreLeadingSpaces**  
 프로필에서 문자열 값을 비교할 때 선행 공백을 무시해야 하는지 여부를 나타냅니다. 이 옵션의 기본값은 **False**입니다.  
  
 **IgnoreTrailingSpaces**  
 프로필에서 문자열 값을 비교할 때 후행 공백을 무시해야 하는지 여부를 나타냅니다. 이 옵션의 기본값은 **True**입니다.  
  
## 관련 항목:  
 [데이터 프로파일링 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [단일 테이블 빠른 프로필 형식&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  