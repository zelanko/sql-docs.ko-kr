---
title: "열 패턴 프로필 요청 옵션 (데이터 프로 파일링 태스크) | Microsoft Docs"
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
ms.assetid: 9ccb8fc5-f65e-41a2-9511-7fa55586eb8b
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 5083458d015783a0bc82fcc328c7573eb62520c2
ms.contentlocale: ko-kr
ms.lasthandoff: 10/05/2017

---
# <a name="column-pattern-profile-request-options-data-profiling-task"></a>열 패턴 프로필 요청 옵션(데이터 프로파일링 태스크)
  **프로필 요청** 페이지의 **요청 속성** 창을 사용하여 요청 창에서 선택한 **열 패턴 프로필 요청** 의 옵션을 설정할 수 있습니다. 열 패턴 프로필은 문자열 열에서 지정된 값의 비율을 포괄하는 정규식 집합을 보고합니다. 이 프로필을 사용하면 잘못된 문자열과 같은 데이터 문제를 식별하는 데 도움이 되며 앞으로 새 값의 유효성 검사에 사용할 수 있는 정규식을 제안 받을 수 있습니다. 예를 들어 미국 우편 번호 열의 패턴 프로필이 \d{5}-\d{4}, \d{5} 및 \d{9} 정규식을 생성할 수 있습니다. 다른 정규식이 보이면 데이터에 유효하지 않거나 잘못된 형식의 값이 포함되어 있을 가능성이 높습니다.  
  
> [!NOTE]  
>  이 항목에서 설명하는 옵션은 **데이터 프로파일링 태스크 편집기** 의 **프로필 요청 페이지**에 나타납니다. 편집기의 이 페이지에 대한 자세한 내용은 [데이터 프로파일링 태스크 편집기&#40;프로필 요청 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)를 참조하세요.  
  
 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요. 데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 분석하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요.  
  
## <a name="understanding-the-use-of-delimiters-and-symbols"></a>구분 기호 및 기호 사용 이해  
 **열 패턴 프로필 요청**에 대한 패턴을 계산하기 전에 데이터 프로파일링 태스크에서는 데이터를 토큰화합니다. 즉, 이 태스크에서는 문자열 값을 토큰이라는 더 작은 단위로 구분합니다. 이 태스크에서는 **Delimiters** 및 **Symbols** 속성에 대해 지정하는 구분 기호 및 기호를 기반으로 문자열을 토큰으로 구분합니다.  
  
-   **Delimiters** 기본적으로 Delimiters 목록에는 공백 문자, 가로 탭 문자(\t), 줄 바꿈 문자(\n) 및 캐리지 리턴 문자(\r)가 포함됩니다. 추가 구분 기호를 지정할 수 있지만 기본 구분 기호는 제거할 수 없습니다.  
  
-   **기호** 기본적으로 목록 **기호** 문자 포함: `,.;:-"'~=&/@!?()<>[]{}|#*^%` 눈금 표시와 합니다. 예를 들어 기호가 "`()-`"인 경우 값 "(425) 123-4567"은 ["(", "425", ")", "123", "-", "4567", ")"]로 토큰화됩니다.  
  
 한 문자가 동시에 구분 기호이면서 기호일 수는 없습니다.  
  
 모든 구분 기호는 토큰화 프로세스의 일환으로 단일 공백으로 정규화됩니다. 반면 기호는 유지됩니다.  
  
## <a name="understanding-the-use-of-the-tag-table"></a>태그 테이블 사용 이해  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 만든 특수 테이블에 태그 및 관련 용어를 저장하여 관련 토큰을 단일 태그를 사용하여 그룹화할 수도 있습니다. 태그 테이블에는 이름이 하나는 "Tag"이고 다른 하나는 "Term"인 두 개의 문자열 열이 있어야 합니다. 이러한 열의 유형은 **char**, **nchar**, **varchar**또는 **nvarchar**일 수 있지만 **text** 또는 **ntext**일 수는 없습니다. 단일 테이블에서 여러 태그와 해당 용어를 결합할 수 있습니다. 열 패턴 프로필 요청은 하나의 태그 테이블만 사용할 수 있습니다. 별도의 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하여 태그 테이블에 연결할 수 있습니다. 따라서 태그 테이블은 다른 데이터베이스에 있거나 원본 데이터와 다른 서버에 있을 수 있습니다.  
  
 예를 들어 단일 태그 "Direction"을 사용하여 주소에 나타날 수 있는 값 "East", "West", "North" 및 "South"를 그룹화할 수 있습니다. 다음 테이블은 이러한 태그 테이블의 예입니다.  
  
|태그|용어|  
|---------|----------|  
|Direction|East|  
|Direction|West|  
|Direction|North|  
|Direction|South|  
  
 다른 태그를 사용하여 주소에서 "번지"의 개념을 나타내는 다른 단어를 그룹화할 수 있습니다.  
  
|태그|용어|  
|---------|----------|  
|Street|Street|  
|Street|Avenue|  
|Street|Place|  
|Street|Way|  
  
 이러한 태그의 조합을 기반으로 주소에 대한 결과 패턴은 다음과 같을 수 있습니다.  
  
 `\d+\ LookupTag=Direction \d+\p{L}+\ LookupTag=Street`  
  
> [!NOTE]  
>  태그 테이블을 사용하면 데이터 프로파일링 태스크의 성능이 저하됩니다. 태그를 11개 이상 사용하거나 태그 당 용어를 101개 이상 사용하지 마십시오.  
  
 같은 용어는 두 개 이상의 태그에 속할 수 있습니다.  
  
## <a name="request-properties-options"></a>요청 속성 옵션  
 **열 패턴 프로필 요청**에 대해 **요청 속성** 창에는 다음 옵션 그룹이 표시됩니다.  
  
-   **데이터**- **TableOrView** 및 **Column** 옵션이 포함되어 있습니다.  
  
-   **일반**  
  
-   **Options**  
  
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
 이 옵션은 열 패턴 프로필에 적용되지 않습니다.  
  
### <a name="general-options"></a>일반 옵션  
 **RequestID**  
 이 프로필 요청을 식별할 설명이 포함된 이름을 입력합니다. 일반적으로 자동 생성된 값은 변경하지 않아도 됩니다.  
  
### <a name="options"></a>옵션이 포함되어 있습니다.  
 **MaxNumberOfPatterns**  
 프로필에서 계산할 최대 패턴 수를 지정합니다. 이 옵션의 기본값은 10입니다. 최대값은 100입니다.  
  
 **PercentageDataCoverageDesired**  
 계산된 패턴에 포괄할 데이터의 비율을 지정합니다. 이 옵션의 기본값은 95%입니다.  
  
 **CaseSensitive**  
 패턴에서 대/소문자를 구분할지 여부를 나타냅니다. 이 옵션의 기본값은 **False**입니다.  
  
 **Delimiters**  
 텍스트를 토큰화할 때 단어 간 공백과 동일하게 처리할 문자를 나열합니다. 기본적으로 **Delimiters** 목록에는 공백 문자, 가로 탭 문자(\t), 줄 바꿈 문자(\n) 및 캐리지 리턴 문자(\r)가 포함됩니다. 추가 구분 기호를 지정할 수 있지만 기본 구분 기호는 제거할 수 없습니다.  
  
 자세한 내용은 이 항목의 앞부분에 나오는 "구분 기호 및 기호 사용 이해"를 참조하십시오.  
  
 **Symbols**  
 패턴의 일부로 유지할 기호를 나열합니다. 이러한 기호에는 날짜의 "/", 시간의 ":" 및 전자 메일 주소의 "@"이 포함될 수 있습니다. 기본적으로 목록 **기호** 문자 포함: `,.;:-"'~=&/@!?()<>[]{}|#*^%`합니다.  
  
 자세한 내용은 이 항목의 앞부분에 나오는 "구분 기호 및 기호 사용 이해"를 참조하십시오.  
  
 **TagTableConnectionManager**  
 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient)를 사용하여 태그 테이블이 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 관리자를 선택합니다.  
  
 자세한 내용은 이 항목의 앞부분에 나오는 "태그 테이블 사용 이해"를 참조하십시오.  
  
 **TagTableName**  
 Tag 및 Term이라는 두 개의 문자열 열이 있어야 하는 기존 태그 테이블을 선택합니다.  
  
 자세한 내용은 이 항목의 앞부분에 나오는 "태그 테이블 사용 이해"를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 프로파일링 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [단일 테이블 빠른 프로필 형식 &#40; 데이터 작업 &#41; 프로 파일링](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  

