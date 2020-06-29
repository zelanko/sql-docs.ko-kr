---
title: 값 포함 프로필 요청 옵션(데이터 프로파일링 태스크) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: ca94da82-a4c9-4e87-9cba-c2d85bd31f01
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5e39c227ede9890c1b7290a2e2dec8cdf7104a1a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438060"
---
# <a name="value-inclusion-profile-request-options-data-profiling-task"></a>값 포함 프로필 요청 옵션(데이터 프로파일링 태스크)
  **프로필 요청** 페이지의 **요청 속성** 창을 사용하여 요청 창에서 선택한 **값 포함 프로필 요청** 의 옵션을 설정할 수 있습니다. 값 포함 프로필은 두 개의 열 또는 열 집합 간에 겹치는 값을 계산합니다. 따라서 이 프로필은 열 또는 열 집합이 선택한 테이블 간의 외래 키 역할을 수행하기에 적합한지 여부도 확인할 수 있습니다. 또한 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 값 포함 프로필을 사용하여 Sales 테이블의 ProductID 열을 프로파일링하는 중 프로필이 Products 테이블의 ProductID 열에 없는 값이 열에 포함되어 있음을 검색할 수 있습니다.  
  
> [!NOTE]  
>  이 항목에서 설명하는 옵션은 **데이터 프로파일링 태스크 편집기** 의 **프로필 요청 페이지**에 나타납니다. 편집기의 이 페이지에 대한 자세한 내용은 [데이터 프로파일링 태스크 편집기&#40;프로필 요청 페이지&#41;](data-profiling-task-editor-profile-requests-page.md)를 참조하세요.  
  
 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](data-profiling-task.md)을 참조하세요. 데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 분석하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](data-profile-viewer.md)를 참조하세요.  
  
## <a name="understanding-the-selection-of-columns-for-the-inclusioncolumns-property"></a>InclusionColumns 속성에 대한 열 선택 이해  
 **값 포함 프로필 요청** 은 하위 집합의 모든 값이 상위 집합에 있는지 여부를 계산합니다. 상위 집합은 주로 조회 테이블 또는 참조 테이블입니다. 예를 들어 주소 테이블의 주 열은 하위 집합 테이블입니다. 이 열에 있는 두 개의 문자로 구성된 모든 주 코드는 상위 집합 테이블인 미국 우편 서비스 주 코드 테이블에도 있어야 합니다.  
  
 (*) 와일드카드를 하위 집합 열 또는 상위 집합 열의 값으로 사용하면 데이터 프로파일링 태스크에서 해당 측의 각 열을 다른 측에 지정된 열에 대해 비교합니다.  
  
> [!NOTE]  
>  (*)를 선택하는 경우 이 옵션으로 인해 계산이 많이 발생하여 태스크의 성능이 저하될 수 있습니다.  
  
## <a name="understanding-the-threshold-settings"></a>임계값 설정 이해  
 두 개의 다른 임계값 설정을 사용하여 값 포함 프로필 요청의 출력을 구체화할 수 있습니다.  
  
 **InclusionThresholdSetting** 에 대해 **None**이외의 값을 지정하면 다음 상황 중 하나에서만 프로필이 상위 집합에 있는 하위 집합의 포함 수준을 보고합니다.  
  
-   포함 수준이 **InclusionStrengthThreshold**에 지정된 임계값을 초과하는 경우  
  
-   포함 수준의 값이 1.0이고 **InclusionStrengthThreshold** 가 **Exact**로 설정된 경우  
  
 고유하지 않은 값으로 인해 상위 집합 열이 상위 집합 테이블에 적절한 키가 아닌 조합을 필터링하여 출력을 보다 구체화할 수 있습니다. **SupersetColumnsKeyThresholdSetting** 에 대해 **None**이외의 값을 지정하면 다음 상황 중 하나에서만 프로필이 상위 집합에 있는 하위 집합의 포함 수준을 보고합니다.  
  
-   상위 집합 테이블에서 상위 집합 열이 키로 적합한 정도를 나타내는 값이 **SupersetColumnsKeyThreshold**에 지정된 임계값을 초과하는 경우  
  
-   포함 수준의 값이 1.0이고 **SupersetColumnsKeyThreshold** 가 **Exact**로 설정된 경우  
  
## <a name="request-properties-options"></a>요청 속성 옵션  
 **값 포함 프로필 요청**에 대해 **요청 속성** 창에는 다음 옵션 그룹이 표시됩니다.  
  
-   **데이터**- **SubsetTableOrView**, **SupersetTableOrView**및 **InclusionColumns** 옵션이 포함되어 있습니다.  
  
-   **일반**  
  
-   **옵션**  
  
### <a name="data-options"></a>데이터 옵션  
 **ConnectionManager**  
 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient)를 사용하여 프로파일링할 테이블이나 뷰가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 관리자를 선택합니다.  
  
 **SubsetTableOrView**  
 프로파일링할 기존 테이블이나 뷰를 선택합니다.  
  
 자세한 내용은 이 항목의 "SubsetTableOrView 및 SupersetTableOrView 옵션" 섹션을 참조하십시오.  
  
 **SupersetTableOrView**  
 프로파일링할 기존 테이블이나 뷰를 선택합니다.  
  
 자세한 내용은 이 항목의 "SubsetTableOrView 및 SupersetTableOrView 옵션" 섹션을 참조하십시오.  
  
 **InclusionColumns**  
 하위 집합 및 상위 집합 테이블에서 열 또는 열 집합을 선택합니다.  
  
 자세한 내용은 이 항목의 "InclusionColumns 속성에 대한 열 선택 이해" 및 "InclusionColumns 옵션" 섹션을 참조하십시오.  
  
#### <a name="subsettableorview-and-supersettableorview-options"></a>SubsetTableOrView 및 SupersetTableOrView 옵션  
 **스키마**  
 선택한 테이블이 속해 있는 스키마를 지정합니다. 이 옵션은 읽기 전용입니다.  
  
 **TableOrView**  
 선택한 테이블의 이름을 표시합니다. 이 옵션은 읽기 전용입니다.  
  
#### <a name="inclusioncolumns-options"></a>InclusionColumns 옵션  
 **InclusionColumns**에서 프로파일링 대상으로 선택한 각 열 집합에 대해 다음 옵션이 제공됩니다.  
  
 자세한 내용은 이 항목의 앞부분에 나오는 "InclusionColumns 속성에 대한 열 선택 이해" 섹션을 참조하십시오.  
  
 **IsWildcard**  
 **(\*)** 와일드카드가 선택되었는지 여부를 지정합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)** 를 선택한 경우 **True**로 설정됩니다. 프로파일링할 개별 열을 선택한 경우에는 **False** 로 설정됩니다. 이 옵션은 읽기 전용입니다.  
  
 **ColumnName**  
 선택한 열의 이름을 표시합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)** 를 선택한 경우 비어 있습니다. 이 옵션은 읽기 전용입니다.  
  
 **StringCompareOptions**  
 문자열 값을 비교할 수 있는 옵션을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다. 이 옵션의 기본값은 **Default**입니다.  
  
> [!NOTE]  
>  **ColumnName**에 대해 **(\*)** 와일드카드를 사용하는 경우 **CompareOptions**가 읽기 전용이 되며 **Default** 설정으로 설정됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**기본값**|원본 테이블에서 열의 데이터 정렬을 기준으로 데이터를 정렬 및 비교합니다.|  
|**BinarySort**|각 문자에 대해 정의된 비트 패턴을 기준으로 데이터를 정렬 및 비교합니다. 이진 정렬 순서는 대/소문자와 악센트를 구분합니다. 이진은 가장 빠른 정렬 순서입니다.|  
|**DictionarySort**|관련된 언어 또는 알파벳에 대해 사전에 정의된 정렬 및 비교 규칙에 따라 데이터를 정렬 및 비교합니다.|  
  
 **DictionarySort**를 선택하는 경우 다음 테이블에 나열된 옵션 조합을 선택할 수도 있습니다. 이러한 추가 옵션은 기본적으로 선택되어 있지 않습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**IgnoreCase**|비교 시 대문자와 소문자를 구분할지 여부를 지정합니다. 이 옵션을 설정하면 문자열 비교 시 대/소문자가 무시됩니다. 예를 들어 "ABC"는 "abc"와 동일하게 인식됩니다.|  
|**IgnoreNonSpace**|비교 시 공백 문자와 분음 기호를 구분할지 여부를 지정합니다. 이 옵션을 설정하면 비교 시 분음 기호가 무시됩니다. 예를 들어 "å"와 "a"는 동일합니다.|  
|**IgnoreKanaType**|비교 시 두 가지 형식의 일본어 가나 문자인 히라가나와 가타가나를 구분합니다. 이 옵션을 설정하면 문자열 비교 시 가나 형식이 무시됩니다.|  
|**IgnoreWidth**|비교 시 싱글바이트 문자와 동일 문자의 더블바이트 문자 표현을 구분할지 여부를 지정합니다. 이 옵션을 설정하면 문자열 비교 시 동일 문자에 대한 싱글바이트 표현과 더블바이트 표현이 동일하게 인식됩니다.|  
  
### <a name="general-options"></a>일반 옵션  
 **RequestID**  
 이 프로필 요청을 식별할 설명이 포함된 이름을 입력합니다. 일반적으로 자동 생성된 값은 변경하지 않아도 됩니다.  
  
### <a name="options"></a>옵션  
 **None**  
 프로필의 출력을 구체화하기 위한 임계값 설정을 선택합니다. 이 속성의 기본값은 **Specified**입니다. 자세한 내용은 이 항목의 앞부분에 나오는 "임계값 설정 이해" 섹션을 참조하십시오.  
  
|값|Description|  
|-----------|-----------------|  
|**없음**|임계값을 지정하지 않습니다. 키 수준은 해당 값에 관계없이 보고됩니다.|  
|**Specified**|**InclusionStrengthThreshold**에 지정된 임계값을 사용합니다. 포함 수준은 이 값이 임계값보다 큰 경우에만 보고됩니다.|  
|**Exact**|임계값을 지정하지 않습니다. 포함 수준은 하위 집합 값이 상위 집합 값에 완전히 포함된 경우에만 보고됩니다.|  
  
 **InclusionStrengthThreshold**  
 0-1의 값을 사용하여 임계값을 지정합니다. 이 임계값을 초과하는 포함 수준은 보고됩니다. 이 속성의 기본값은 0.95입니다. **Specified** 가 **InclusionThresholdSetting**으로 선택된 경우에만 이 옵션을 사용할 수 있습니다.  
  
 자세한 내용은 이 항목의 앞부분에 나오는 "임계값 설정 이해" 섹션을 참조하십시오.  
  
 **None**  
 상위 집합 임계값을 지정합니다. 이 속성의 기본값은 **Specified**입니다. 자세한 내용은 이 항목의 앞부분에 나오는 "임계값 설정 이해" 섹션을 참조하십시오.  
  
|값|Description|  
|-----------|-----------------|  
|**없음**|임계값을 지정하지 않습니다. 포함 수준은 상위 집합 열의 키 수준에 관계없이 보고됩니다.|  
|**Specified**|**SupersetColumnsKeyThreshold**에 지정된 임계값을 사용합니다. 포함 수준은 상위 집합 열의 키 수준이 임계값보다 큰 경우에만 보고됩니다.|  
|**Exact**|임계값을 지정하지 않습니다. 포함 수준은 상위 집합 열이 상위 집합 테이블의 정확한 키인 경우에만 보고됩니다.|  
  
 **SupersetColumnsKeyThreshold**  
 0-1의 값을 사용하여 임계값을 지정합니다. 이 임계값을 초과하는 포함 수준은 보고됩니다. 이 속성의 기본값은 0.95입니다. **Specified** 가 **SupersetColumnsKeyThresholdSetting**으로 선택된 경우에만 이 옵션을 사용할 수 있습니다.  
  
 자세한 내용은 이 항목의 앞부분에 나오는 "임계값 설정 이해" 섹션을 참조하십시오.  
  
 **MaxNumberOfViolations**  
 출력에 보고할 최대 포함 위반 수를 지정합니다. 이 속성의 기본값은 100입니다. **Exact** 가 **InclusionThresholdSetting**으로 선택된 경우 이 옵션을 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 프로파일링 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)   
 [단일 테이블 빠른 프로필 형식&#40;데이터 프로파일링 태스크&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
