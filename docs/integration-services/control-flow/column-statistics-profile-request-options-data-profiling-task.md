---
title: "열 통계 프로필 요청 옵션 (데이터 프로 파일링 태스크) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 87205984-507a-49f3-b27c-36a0075c234d
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 10b9dd217872c27b6192bde49bfaf18fbd2f511b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="column-statistics-profile-request-options-data-profiling-task"></a>열 통계 프로필 요청 옵션(데이터 프로파일링 태스크)
  **프로필 요청** 페이지의 **요청 속성** 창을 사용하여 요청 창에서 선택한 **열 통계 프로필 요청** 의 옵션을 설정할 수 있습니다. 열 통계 프로필은 숫자 열의 최소값, 최대값, 평균, 표준 편차 및 **datetime** 열에 대한 최소값, 최대값과 같은 통계를 보고합니다. 이 프로필을 사용하면 잘못된 날짜와 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 기록 날짜 열을 프로파일링하여 미래의 최대 날짜를 검색할 수 있습니다.  
  
> [!NOTE]  
>  이 항목에서 설명하는 옵션은 **데이터 프로파일링 태스크 편집기** 의 **프로필 요청 페이지**에 나타납니다. 편집기의 이 페이지에 대한 자세한 내용은 [데이터 프로파일링 태스크 편집기&#40;프로필 요청 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)를 참조하세요.  
  
 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요. 데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 분석하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요.  
  
## <a name="request-properties-options"></a>요청 속성 옵션  
 **열 통계 프로필 요청**에 대해 **요청 속성** 창에는 다음 옵션 그룹이 표시됩니다.  
  
-   **데이터**- **TableOrView** 및 **Column** 옵션이 포함되어 있습니다.  
  
-   **일반**  
  
### <a name="data-options"></a>데이터 옵션  
 **ConnectionManager**  
 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient)를 사용하여 프로파일링할 테이블이나 뷰가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 관리자를 선택합니다.  
  
 **TableOrView**  
 프로파일링할 열이 포함된 기존 테이블이나 뷰를 선택합니다.  
  
 자세한 내용은 이 항목의 "TableorView 옵션" 섹션을 참조하십시오.  
  
 **Column**  
 프로파일링할 기존 열을 선택합니다. 모든 열을 프로파일링하려면 **(\*)**를 선택합니다.  
  
 자세한 내용은 이 항목의 "열 옵션" 섹션을 참조하십시오.  
  
#### <a name="tableorview-options"></a>TableOrView 옵션  
 **스키마**  
 선택한 테이블이 속해 있는 스키마를 지정합니다. 이 옵션은 읽기 전용입니다.  
  
 **테이블**  
 선택한 테이블의 이름을 표시합니다. 이 옵션은 읽기 전용입니다.  
  
#### <a name="column-options"></a>열 옵션  
 **IsWildCard**  
 **(\*)** 와일드카드가 선택되었는지 여부를 지정합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)**를 선택한 경우 **True**로 설정됩니다. 프로파일링할 개별 열을 선택한 경우에는 **False** 로 설정됩니다. 이 옵션은 읽기 전용입니다.  
  
 **ColumnName**  
 선택한 열의 이름을 표시합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)**를 선택한 경우 비어 있습니다. 이 옵션은 읽기 전용입니다.  
  
 **StringCompareOptions**  
 이 옵션은 열 통계 프로필에 적용되지 않습니다.  
  
### <a name="general-options"></a>일반 옵션  
 **RequestID**  
 이 프로필 요청을 식별할 설명이 포함된 이름을 입력합니다. 일반적으로 자동 생성된 값은 변경하지 않아도 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 작업 편집기 &#40; 프로 파일링 일반 페이지 &#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [단일 테이블 빠른 프로필 형식 &#40; 데이터 작업 &#41; 프로 파일링](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
