---
title: 데이터 프로파일링 태스크 편집기(프로필 요청 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.profilerequests.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c72acb3d-380e-436e-8041-ed364eddfabd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e3f98e88428c25c3ecf2af415c942c30a18e9cf1
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273378"
---
# <a name="data-profiling-task-editor-profile-requests-page"></a>데이터 프로파일링 태스크 편집기(프로필 요청 페이지)
  **데이터 프로파일링 태스크 편집기** 의 **프로필 요청 페이지** 를 사용하여 계산할 프로필을 선택하고 구성할 수 있습니다. 단일 데이터 프로파일링 태스크에서 여러 테이블 또는 뷰에 있는 여러 열이나 열 조합에 대해 여러 프로필을 계산할 수 있습니다.  
  
 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요. 데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 분석하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요.  
  
 **데이터 프로파일링 태스크 편집기의 프로필 요청 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 데이터 프로파일링 태스크가 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **제어 흐름** 탭에서 데이터 프로파일링 태스크를 두 번 클릭합니다.  
  
3.  **데이터 프로파일링 태스크 편집기**에서 **프로필 요청**을 클릭합니다.  
  
## <a name="using-the-requests-pane"></a>요청 창 사용  
 요청 창은 페이지의 맨 위에 나타나는 창입니다. 이 창에는 현재 데이터 프로파일링 태스크에 대해 구성된 모든 프로필이 나열됩니다. 구성된 프로필이 없는 경우 요청 창이 비어 있게 됩니다. 새 프로필을 추가하려면 **프로필 유형** 열에서 빈 영역을 클릭하고 목록에서 프로필 유형을 선택합니다. 프로필을 구성하려면 요청 창에서 프로필을 선택한 다음 **요청 속성** 창에서 프로필의 속성을 설정합니다.  
  
### <a name="requests-pane-options"></a>요청 창 옵션  
 요청 창에는 다음 옵션이 있습니다.  
  
 **보기**  
 태스크에 대해 구성된 모든 프로필을 볼지, 아니면 프로필 중 하나만 볼지를 선택합니다.  
  
 요청 창의 열은 선택하는 **뷰** 에 따라 변경됩니다. 이러한 각 열에 대한 자세한 내용은 다음 섹션인 "요청 창 열"을 참조하세요.  
  
### <a name="requests-pane-columns"></a>요청 창 열  
 요청 창에 표시되는 열은 선택한 **뷰** 에 따라 다음과 같이 달라집니다.  
  
-   **모든 요청**을 보려고 선택하면 요청 창에 **프로필 유형**과 **요청 ID**라는 두 개의 열이 포함됩니다.  
  
-   5개의 열 프로필 중 하나를 보려고 선택하면 요청 창에 **프로필 유형**, **테이블 또는 뷰**, **열** 및 **요청 ID**라는 4개의 열이 포함됩니다.  
  
-   후보 키 프로필을 보려고 선택하면 요청 창에 **프로필 유형**, **테이블 또는 뷰**, **키 열** 및 **요청 ID**라는 4개의 열이 포함됩니다.  
  
-   함수 종속성 프로필을 보려고 선택하면 요청 창에 **프로필 유형**, **테이블 또는 뷰**, **결정 열**, **종속 열** 및 **요청 ID**라는 5개의 열이 포함됩니다.  
  
-   값 포함 프로필을 보려고 선택하면 요청 창에 **프로필 유형**, **하위 집합측 테이블 또는 뷰**, **상위 집합측 테이블 또는 뷰**, **하위 집합측 열**, **상위 집합측 열** 및 **요청 ID**라는 6개의 열이 포함됩니다.  
  
 다음 섹션에서는 이러한 각 열에 대해 설명합니다.  
  
#### <a name="columns-common-to-all-views"></a>모든 뷰에 공통된 열  
 **프로필 유형**  
 다음 옵션에서 데이터 프로필을 선택합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**후보 키 프로필 요청**|후보 키 프로필을 계산합니다.<br /><br /> 이 프로필은 열 또는 열 집합이 선택한 테이블에 대해 키인지, 아니면 근사 키인지를 보고합니다. 또한 이 프로필을 사용하면 잠재적 키 열의 중복 값과 같은 데이터 문제를 식별할 수 있습니다.|  
|**열 길이 분포 프로필 요청**|열 길이 분포 프로필을 계산합니다.<br /><br /> 열 길이 분포 프로필은 선택한 열에 있는 문자열 값의 모든 고유 길이 및 각 길이가 나타내는 테이블 내 행의 비율을 보고합니다. 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 두 개의 문자로 구성된 미국 주 코드 열을 프로파일링하는 중 3자 이상의 값이 검색될 수 있습니다.|  
|**열 Null 비율 프로필 요청**|열 Null 비율 프로필을 계산합니다.<br /><br /> 열 Null 비율 프로필은 선택한 열 내 Null 값의 비율을 보고합니다. 이 프로필을 사용하면 예기치 않게 높은 열 내 Null 값의 비율과 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 우편 번호 열을 프로파일링하여 허용 불가능한 수준의 누락된 코드 비율을 검색할 수 있습니다.|  
|**열 패턴 프로필 요청**|열 패턴 프로필을 계산합니다.<br /><br /> 열 패턴 프로필은 문자열 열에서 지정된 값의 비율을 포괄하는 정규식 집합을 보고합니다. 이 프로필을 사용하면 잘못된 문자열과 같은 데이터 문제를 식별할 수 있습니다. 또한 이 프로필은 앞으로 새 값의 유효성 검사에 사용할 수 있는 정규식을 제안해 줍니다. 예를 들어 우편 번호 열의 패턴 프로필은 \d{5}-\d{4}, \d{5} 및 \d{9} 정규식을 생성할 수 있습니다. 다른 정규식이 발견된다면 데이터에 유효하지 않거나 잘못된 형식의 값이 포함되어 있을 가능성이 높습니다.|  
|**열 통계 프로필 요청**|선택한 테이블 또는 뷰에서 적용 가능한 모든 열의 기본 설정을 사용하여 열 통계 프로필을 계산하려면 이 옵션을 선택합니다.<br /><br /> 열 통계 프로필은 숫자 열에 대한 최소값, 최대값, 평균값, 표준 편차 및 **datetime** 열에 대한 최소값/최대값과 같은 통계를 보고합니다. 이 프로필을 사용하면 잘못된 날짜와 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 기록 날짜 열을 프로파일링하여 미래의 최대 날짜를 검색할 수 있습니다.|  
|**열 값 분포 프로필 요청**|열 값 분포 프로필을 계산합니다.<br /><br /> 열 값 분포 프로필은 선택한 열에 있는 모든 고유 값 및 각 값이 나타내는 테이블 내 행의 비율을 보고합니다. 또한 이 프로필은 테이블에서 지정된 비율을 초과하는 값을 보고할 수 있습니다. 이 프로필을 사용하면 열에 포함된 잘못된 고유 값 수와 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 미국의 주가 포함된 열을 프로파일링하는 중 50개를 초과하는 고유 값이 검색될 수 있습니다.|  
|**함수 종속성 프로필 요청**|함수 종속성 프로필을 계산합니다.<br /><br /> 함수 종속성 프로필은 한 열(종속 열)의 값이 다른 열 또는 열 집합(결정 열)의 값에 종속되는 범위를 보고합니다. 또한 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 미국 우편 번호 열과 미국 주 열 간 종속성을 프로파일링하는 중 우편 번호가 같으면 주도 동일해야 하므로 프로필에서 이러한 종속성 위반을 검색할 수 있습니다.|  
|**값 포함 프로필 요청**|값 포함 프로필을 계산합니다.<br /><br /> 값 포함 프로필은 두 개의 열 또는 열 집합 간에 겹치는 값을 계산합니다. 이 프로필은 열 또는 열 집합이 선택한 테이블 간의 외래 키 역할을 수행하기에 적합한지 여부도 확인합니다. 또한 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 Sales 테이블의 ProductID 열을 프로파일링하여 Products 테이블의 ProductID 열에 없는 값이 포함된 열을 검색할 수 있습니다.|  
  
 **RequestID**  
 요청의 식별자를 표시합니다. 일반적으로 자동 생성된 값은 변경하지 않아도 됩니다.  
  
#### <a name="columns-common-to-all-individual-profiles"></a>모든 개별 프로필에 공통된 열  
 **연결 관리자**  
 원본 데이터베이스에 연결되는 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 표시합니다.  
  
 **요청 ID**  
 요청의 식별자를 표시합니다. 일반적으로 자동 생성된 값은 변경하지 않아도 됩니다.  
  
#### <a name="columns-common-to-the-five-individual-column-profiles"></a>5개의 개별 열 프로필에 공통된 열  
 **테이블 또는 뷰**  
 선택한 열이 포함된 테이블 또는 뷰를 표시합니다.  
  
 **열**  
 프로파일링하기 위해 선택한 열을 표시합니다.  
  
#### <a name="columns-specific-to-the-candidate-key-profile"></a>후보 키 프로필 관련 열  
 **테이블 또는 뷰**  
 선택한 열이 포함된 테이블 또는 뷰를 표시합니다.  
  
 **키 열**  
 프로파일링하기 위해 선택한 열을 표시합니다.  
  
#### <a name="columns-specific-to-the-functional-dependency-profile"></a>함수 종속성 프로필 관련 열  
 **테이블 또는 뷰**  
 선택한 열이 포함된 테이블 또는 뷰를 표시합니다.  
  
 **결정 열**  
 프로파일링하기 위해 선택한 열을 결정 열로 표시합니다. 미국 우편 번호가 미국의 주를 결정하는 예에서는 Zip Code 열이 결정 열입니다.  
  
 **Dependent column**  
 프로파일링하기 위해 선택한 열을 종속 열로 표시합니다. 미국 우편 번호가 미국의 주를 결정하는 예에서는 State 열이 종속 열입니다.  
  
#### <a name="columns-specific-to-the-value-inclusion-profile"></a>값 포함 프로필 관련 열  
 **하위 집합측 테이블 또는 뷰**  
 하위 집합측 열로 선택한 열이 포함된 테이블 또는 뷰를 표시합니다.  
  
 **상위 집합측 테이블 또는 뷰**  
 상위 집합측 열로 선택한 열이 포함된 테이블 또는 뷰를 표시합니다.  
  
 **하위 집합측 열**  
 프로파일링하기 위해 선택한 열을 하위 집합측 열로 표시합니다. US State 열의 값이 두 개의 문자로 구성된 미국 주 코드가 포함된 참조 테이블에 있는지 확인하는 예에서는 원본 테이블의 State 열이 하위 집합 열입니다.  
  
 **상위 집합측 열**  
 프로파일링하기 위해 선택한 열을 상위 집합측 열로 표시합니다. US State 열의 값이 두 개의 문자로 구성된 미국 주 코드가 포함된 참조 테이블에 있는지 확인하는 예에서는 참조 테이블의 주 코드 열이 상위 집합 열입니다.  
  
## <a name="using-the-request-properties-pane"></a>요청 속성 창 사용  
 **요청 속성** 창은 요청 창 아래에 나타납니다. 이 창에는 요청 창에서 선택한 프로필의 옵션이 표시됩니다.  
  
> [!NOTE]  
>  **프로필 유형**을 선택한 후에 **요청 속성** 창의 프로필 요청에 대한 속성을 확인하려면 **요청 ID** 필드를 선택해야 합니다.  
  
 이러한 옵션은 선택한 프로필에 따라 달라집니다. 개별 프로필 유형 옵션에 대한 자세한 내용은 다음 항목을 참조하세요.  
  
-   [후보 키 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [열 Null 비율 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [열 통계 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [열 값 분포 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [열 길이 분포 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [열 패턴 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [함수 종속성 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [값 포함 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 프로파일링 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [단일 테이블 빠른 프로필 형식&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
