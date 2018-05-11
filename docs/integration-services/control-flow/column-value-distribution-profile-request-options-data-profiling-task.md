---
title: 열 값 분포 프로필 요청 옵션(데이터 프로파일링 태스크) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c1e5f5de-04f5-4d00-a9f0-55817186bdf9
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d0fb3daaeaac3afc27abfacee4c9f596baaa01e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="column-value-distribution-profile-request-options-data-profiling-task"></a>열 값 분포 프로필 요청 옵션(데이터 프로파일링 태스크)
  **프로필 요청** 페이지의 **요청 속성** 창을 사용하여 요청 창에서 선택한 **열 값 분포 프로필 요청** 의 옵션을 설정할 수 있습니다. 열 값 분포 프로필은 선택한 열에 있는 모든 고유 값 및 각 값이 나타내는 테이블 내 행의 비율을 보고합니다. 또한 프로필은 테이블에서 지정된 행 비율을 초과하는 값을 보고할 수 있습니다. 이 프로필을 사용하면 열에 포함된 잘못된 고유 값 수와 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 미국의 주가 포함된 열을 프로파일링하는 중 50개를 초과하는 고유 값이 검색될 수 있습니다.  
  
> [!NOTE]  
>  이 항목에서 설명하는 옵션은 **데이터 프로파일링 태스크 편집기** 의 **프로필 요청 페이지**에 나타납니다. 편집기의 이 페이지에 대한 자세한 내용은 [데이터 프로파일링 태스크 편집기&#40;프로필 요청 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)를 참조하세요.  
  
 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요. 데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 분석하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요.  
  
## <a name="request-properties-options"></a>요청 속성 옵션  
 **열 값 분포 프로필 요청**에 대해 **요청 속성** 창에는 다음 옵션 그룹이 표시됩니다.  
  
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
 프로파일링할 기존 열을 선택합니다. 모든 열을 프로파일링하려면 **(\*)** 를 선택합니다.  
  
 자세한 내용은 이 항목의 "열 옵션" 섹션을 참조하십시오.  
  
#### <a name="tableorview-options"></a>TableOrView 옵션  
 **스키마**  
 선택한 테이블이 속해 있는 스키마를 지정합니다. 이 옵션은 읽기 전용입니다.  
  
 **테이블**  
 선택한 테이블의 이름을 표시합니다. 이 옵션은 읽기 전용입니다.  
  
#### <a name="column-options"></a>열 옵션  
 **IsWildCard**  
 **(\*)** 와일드카드가 선택되었는지 여부를 지정합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)** 를 선택한 경우 **True**로 설정됩니다. 프로파일링할 개별 열을 선택한 경우에는 **False** 로 설정됩니다. 이 옵션은 읽기 전용입니다.  
  
 **ColumnName**  
 선택한 열의 이름을 표시합니다. 이 옵션은 모든 열을 프로파일링하도록 **(\*)** 를 선택한 경우 비어 있습니다. 이 옵션은 읽기 전용입니다.  
  
 **StringCompareOptions**  
 문자열 값을 비교할 수 있는 옵션을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다. 이 옵션의 기본값은 **Default**입니다.  
  
> [!NOTE]  
>  **ColumnName**에 대해 **(\*)** 와일드카드를 사용하는 경우 **CompareOptions**가 읽기 전용이 되며 **Default** 설정으로 설정됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Default**|원본 테이블에서 열의 데이터 정렬을 기준으로 데이터를 정렬 및 비교합니다.|  
|**BinarySort**|각 문자에 대해 정의된 비트 패턴을 기준으로 데이터를 정렬 및 비교합니다. 이진 정렬 순서는 대/소문자와 악센트를 구분합니다.  이진은 가장 빠른 정렬 순서입니다.|  
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
  
### <a name="options"></a>변수  
 **ValueDistributionOption**  
 모든 열 값에 대해 분포를 계산할 것인지 여부를 지정합니다. 이 옵션의 기본값은 **FrequentValues**입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**AllValues**|모든 열 값에 대해 분포가 계산됩니다.|  
|**FrequentValues**|빈도가 **FrequentValueThreshold**에 지정된 최소값을 초과하는 값에 대해서만 분포가 계산됩니다. **FrequentValueThreshold** 를 충족하지 않는 값은 출력 보고서에서 제외됩니다.|  
  
 **FrequentValueThreshold**  
 0-1의 값을 사용하여 임계값을 지정합니다. 이 임계값을 초과하는 열 값은 보고됩니다. **AllValues** 가 **ValueDistributionOption**으로 선택된 경우 이 옵션을 사용할 수 없습니다. 이 옵션의 기본값은 0.001입니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 프로파일링 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [단일 테이블 빠른 프로필 형식&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
