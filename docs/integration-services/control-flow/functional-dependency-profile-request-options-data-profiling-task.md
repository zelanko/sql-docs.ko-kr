---
title: 함수 종속성 프로필 요청 옵션(데이터 프로파일링 태스크) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 6eb853aa-8016-490c-be4f-06ab8d7f5021
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8ec1e724c607a8805b9654f8ade077ab078e4eae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988197"
---
# <a name="functional-dependency-profile-request-options-data-profiling-task"></a>함수 종속성 프로필 요청 옵션(데이터 프로파일링 태스크)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **프로필 요청** 페이지의 **요청 속성** 창을 사용하여 요청 창에서 선택한 **함수 종속성 프로필 요청** 의 옵션을 설정할 수 있습니다. 함수 종속성 프로필은 한 열(종속 열)의 값이 다른 열 또는 열 집합(결정 열)의 값에 종속되는 범위를 보고합니다. 또한 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 Zip Code/Postal Code 열과 US State 열 간 종속성을 프로파일링하는 중 같은 우편 번호는 항상 같은 주여야 하는데 이 프로필이 종속성 위반을 검색할 수 있습니다.  
  
> [!NOTE]  
>  이 항목에서 설명하는 옵션은 **데이터 프로파일링 태스크 편집기** 의 **프로필 요청 페이지**에 나타납니다. 편집기의 이 페이지에 대한 자세한 내용은 [데이터 프로파일링 태스크 편집기&#40;프로필 요청 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)를 참조하세요.  
  
 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요. 데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 분석하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요.  
  
## <a name="understanding-the-selection-of-determinant-and-dependent-columns"></a>결정 열 및 종속 열 선택 이해  
 **함수 종속성 프로필 요청** 은 결정 측 열 또는 열 집합( **DeterminantColumns** 속성에 지정되어 있음)이 종속측 열( **DependentColumn** 속성에 지정되어 있음)의 값을 결정하는 정도를 계산합니다. 예를 들어 US State 열은 함수 측면에서 US Zip Code 열에 종속되어야 합니다. 즉, 우편 번호(결정 열)가 98052인 경우 주(종속 열)는 항상 Washington이어야 합니다.  
  
 결정측의 경우 **DeterminantColumns** 속성에 열 또는 열 집합을 지정할 수 있습니다. 예를 들어 열 A, B, C를 포함하는 예제 테이블의 경우 **DeterminantColumns** 속성에 대해 다음과 같이 선택합니다.  
  
-   **(\*)** 와일드카드를 선택하면 데이터 프로파일링 태스크에서 각 열을 종속성의 결정 측으로 테스트합니다.  
  
-   **(\*)** 와일드카드와 다른 열을 선택하면 데이터 프로파일링 태스크에서 각 열의 조합을 종속성의 결정 측으로 테스트합니다. 예를 들어 열 A, B, C를 포함하는 예제 테이블의 경우 **(\*)** 및 열 C를 **DeterminantColumns** 속성의 값으로 지정하면 데이터 프로파일링 태스크에서 조합 (A, C) 및 (B, C)를 종속성의 결정 측으로 테스트합니다.  
  
 종속측의 경우 **DependentColumn** 속성에 단일 열 또는 **(\*)** 와일드카드를 지정할 수 있습니다. **(\*)** 를 선택하면 데이터 프로파일링 태스크에서 각 열에 대해 결정 측 열 또는 열 집합을 테스트합니다.  
  
> [!NOTE]  
>  **(\*)** 를 선택하는 경우 이 옵션으로 인해 계산이 많이 발생하여 태스크의 성능이 저하될 수 있습니다. 그러나 태스크에서 함수 종속성에 대한 임계값을 만족하는 하위 집합을 찾으면 추가 조합을 분석하지 않습니다. 예를 들어 위에서 설명한 예제 테이블의 경우 태스크에서 열 C가 결정 열임을 확인하면 복합 후보를 계속 분석하지 않습니다.  
  
## <a name="request-properties-options"></a>요청 속성 옵션  
 **함수 종속성 프로필 요청**에 대해 **요청 속성** 창에는 다음 옵션 그룹이 표시됩니다.  
  
-   **데이터**- **DeterminantColumns** 및 **DependentColumn** 옵션이 포함되어 있습니다.  
  
-   **일반**  
  
-   **Options**  
  
### <a name="data-options"></a>데이터 옵션  
 **ConnectionManager**  
 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient)를 사용하여 프로파일링할 테이블이나 뷰가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 관리자를 선택합니다.  
  
 **TableOrView**  
 프로파일링할 기존 테이블이나 뷰를 선택합니다.  
  
 **DeterminantColumns**  
 결정 열 또는 열 집합을 선택합니다. 즉, 값이 종속 열의 값을 결정하는 열 또는 열 집합을 선택합니다.  
  
 자세한 내용은 이 항목의 "결정 열 및 종속 열 선택 이해" 및 "DeterminantColumns 및 DependentColumn 옵션" 섹션을 참조하십시오.  
  
 **DependentColumn**  
 종속 열을 선택합니다. 즉, 값이 결정 측 열 또는 열 집합의 값에 의해 결정되는 열을 선택합니다.  
  
 자세한 내용은 이 항목의 "결정 열 및 종속 열 선택 이해" 및 "DeterminantColumns 및 DependentColumn 옵션" 섹션을 참조하십시오.  
  
#### <a name="determinantcolumns-and-dependentcolumn-options"></a>DeterminantColumns 및 DependentColumn 옵션  
 **DeterminantColumns** 및 **DependentColumn**에서 프로파일링 대상으로 선택한 각 열에 대해 다음 옵션이 제공됩니다.  
  
 자세한 내용은 이 항목의 앞부분에 나오는 "결정 열 및 종속 열 선택 이해" 섹션을 참조하십시오.  
  
 **IsWildCard**  
 **(\*)** 와일드카드가 선택되었는지 여부를 지정합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)** 를 선택한 경우 **True**로 설정됩니다. 프로파일링할 개별 열을 선택한 경우에는 **False** 로 설정됩니다. 이 옵션은 읽기 전용입니다.  
  
 **ColumnName**  
 선택한 열의 이름을 표시합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)** 를 선택한 경우 비어 있습니다. 이 옵션은 읽기 전용입니다.  
  
 **StringCompareOptions**  
 문자열 값을 비교할 수 있는 옵션을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다. 이 옵션의 기본값은 **Default**입니다.  
  
> [!NOTE]  
>  **ColumnName**에 대해 **(\*)** 와일드카드를 사용하는 경우 **CompareOptions**가 읽기 전용이 되며 **Default** 설정으로 설정됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|**Default**|원본 테이블에서 열의 데이터 정렬을 기준으로 데이터를 정렬 및 비교합니다.|  
|**BinarySort**|각 문자에 대해 정의된 비트 패턴을 기준으로 데이터를 정렬 및 비교합니다. 이진 정렬 순서는 대/소문자와 악센트를 구분합니다. 이진은 가장 빠른 정렬 순서입니다.|  
|**DictionarySort**|관련된 언어 또는 알파벳에 대해 사전에 정의된 정렬 및 비교 규칙에 따라 데이터를 정렬 및 비교합니다.|  
  
 **DictionarySort**를 선택하는 경우 다음 테이블에 나열된 옵션 조합을 선택할 수도 있습니다. 이러한 추가 옵션은 기본적으로 선택되어 있지 않습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**IgnoreCase**|비교 시 대문자와 소문자를 구분할지 여부를 지정합니다. 이 옵션을 설정하면 문자열 비교 시 대/소문자가 무시됩니다. 예를 들어 "ABC"는 "abc"와 동일하게 인식됩니다.|  
|**IgnoreNonSpace**|비교 시 공백 문자와 분음 기호를 구분할지 여부를 지정합니다. 이 옵션을 설정하면 비교 시 분음 기호가 무시됩니다. 예를 들어 "Ã¥"와 "a"는 동일합니다.|  
|**IgnoreKanaType**|비교 시 두 가지 형식의 일본어 가나 문자인 히라가나와 가타가나를 구분합니다. 이 옵션을 설정하면 문자열 비교 시 가나 형식이 무시됩니다.|  
|**IgnoreWidth**|비교 시 싱글바이트 문자와 동일 문자의 더블바이트 문자 표현을 구분할지 여부를 지정합니다. 이 옵션을 설정하면 문자열 비교 시 동일 문자에 대한 싱글바이트 표현과 더블바이트 표현이 동일하게 인식됩니다.|  
  
### <a name="general-options"></a>일반 옵션  
 **RequestID**  
 이 프로필 요청을 식별할 설명이 포함된 이름을 입력합니다. 일반적으로 자동 생성된 값은 변경하지 않아도 됩니다.  
  
### <a name="options"></a>옵션  
 **ThresholdSetting**  
 임계값 설정을 지정합니다. 이 속성의 기본값은 **Specified**입니다.  
  
|값|설명|  
|-----------|-----------------|  
|**없음**|임계값을 지정하지 않습니다. 함수 종속성 수준은 해당 값에 관계없이 보고됩니다.|  
|**Specified**|**FDStrengthThreshold**에 지정된 임계값을 사용합니다. 함수 종속성 수준은 이 값이 임계값보다 큰 경우에만 보고됩니다.|  
|**Exact**|임계값을 지정하지 않습니다. 함수 종속성 수준은 선택한 열 간 함수 종속성이 정확한 경우에만 보고됩니다.|  
  
 **FDStrengthThreshold**  
 0-1의 값을 사용하여 임계값을 지정합니다. 이 임계값을 초과하는 함수 종속성 수준은 보고됩니다. 이 속성의 기본값은 0.95입니다. **Specified** 가 **ThresholdSetting**으로 선택된 경우에만 이 옵션을 사용할 수 있습니다.  
  
 **MaxNumberOfViolations**  
 출력에 보고할 최대 함수 종속성 위반 수를 지정합니다. 이 속성의 기본값은 100입니다. **Exact** 가 **ThresholdSetting**으로 선택된 경우 이 옵션을 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 프로파일링 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [단일 테이블 빠른 프로필 형식&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
