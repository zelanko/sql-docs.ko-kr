---
title: 단일 테이블 빠른 프로필 형식(데이터 프로파일링 태스크) | Microsoft Docs
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
f1_keywords:
- sql13.dts.designer.dataprofilingtask.quickprofile.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: d2fac9ce-730e-474e-961a-69406b633778
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5c4314afd154ff063d960f77ba282b7cf3f28b08
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="single-table-quick-profile-form-data-profiling-task"></a>단일 테이블 빠른 프로필 형식(데이터 프로파일링 태스크)
  **단일 테이블 빠른 프로필 형식** 을 사용하여 데이터 프로파일링 태스크를 구성하고 기본 설정으로 단일 테이블이나 뷰를 빠르게 프로파일링할 수 있습니다.  
  
 데이터 프로파일링 태스크를 사용하는 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 설정](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)을 참조하세요. 데이터 프로필 뷰어를 사용하여 데이터 프로파일링 태스크의 출력을 분석하는 방법에 대한 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요.  
  
## <a name="options"></a>변수  
 **대량 삽입 태스크 편집기**  
 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient)를 사용하여 프로파일링할 테이블이나 뷰가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 관리자를 선택합니다.  
  
 **테이블 또는 뷰**  
 선택한 연결 관리자에서 연결할 데이터베이스의 기존 테이블 또는 뷰를 선택합니다.  
  
 **계산**  
 계산할 프로필을 선택합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**열 Null 비율 프로필**|선택한 테이블 또는 뷰에서 적용 가능한 모든 열의 기본 설정을 사용하여 열 Null 비율 프로필을 계산합니다.<br /><br /> 이 프로필은 선택한 열에 있는 Null 값의 비율을 보고합니다. 이 프로필을 사용하면 예기치 않게 높은 열 내 Null 값의 비율과 같은 데이터 문제를 식별할 수 있습니다. 이 프로필의 설정에 대한 자세한 내용은 [열 Null 비율 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)을 참조하세요.|  
|**열 통계 프로필**|선택한 테이블 또는 뷰에서 적용 가능한 모든 열의 기본 설정을 사용하여 열 통계 프로필을 계산합니다.<br /><br /> 이 프로필은 숫자 열의 최소값, 최대값, 평균, 표준 편차 및 **datetime** 열의 최소값, 최대값과 같은 통계를 보고합니다. 이 프로필을 사용하면 잘못된 날짜와 같은 데이터 문제를 식별할 수 있습니다. 이 프로필의 설정에 대한 자세한 내용은 [열 통계 프로필 요청&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)을 참조하세요.|  
|**열 값 분포 프로필**|선택한 테이블 또는 뷰에서 적용 가능한 모든 열의 기본 설정을 사용하여 열 값 분포 프로필을 계산합니다.<br /><br /> 이 프로필은 선택한 열에 있는 모든 고유 값 및 각 값이 나타내는 테이블 내 행의 비율을 보고합니다. 또한 이 프로필은 테이블에서 지정된 행 비율을 초과하는 값을 보고할 수 있습니다. 이 프로필을 사용하면 열에 포함된 잘못된 고유 값 수와 같은 데이터 문제를 식별할 수 있습니다. 이 프로필에 대한 자세한 내용은 [열 값 분포 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)을 참조하세요.|  
|**열 길이 분포 프로필**|선택한 테이블 또는 뷰에서 적용 가능한 모든 열의 기본 설정을 사용하여 열 길이 분포 프로필을 계산합니다.<br /><br /> 이 프로필은 선택한 열에 있는 문자열 값의 모든 고유 길이 및 각 길이가 나타내는 테이블 내 행의 비율을 보고합니다. 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제를 식별할 수 있습니다. 이 프로필의 설정에 대한 자세한 내용은 [열 길이 분포 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)을 참조하세요.|  
|**열 패턴 프로필**|선택한 테이블 또는 뷰에서 적용 가능한 모든 열의 기본 설정을 사용하여 열 패턴 프로필을 계산합니다.<br /><br /> 이 프로필은 문자열 열의 값을 포괄하는 정규식 집합을 보고합니다. 이 프로필을 사용하면 잘못된 문자열과 같은 데이터 문제를 식별할 수 있습니다. 또한 이 프로필은 앞으로 새 값의 유효성 검사에 사용할 수 있는 정규식을 제안해 줍니다. 이 프로필의 설정에 대한 자세한 내용은 [열 패턴 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)을 참조하세요.|  
|**후보 키 프로필**|**최대 N 열 키**에 지정한 열 수까지 포함하는 열 조합에 대해 후보 키 프로필을 계산합니다.<br /><br /> 이 프로필은 열 또는 열 집합이 선택한 테이블에 대해 키 역할을 수행하기에 적합한지 여부를 보고합니다. 또한 이 프로필을 사용하면 잠재적 키 열의 중복 값과 같은 데이터 문제를 식별할 수 있습니다. 이 프로필의 설정에 대한 자세한 내용은 [후보 키 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)을 참조하세요.|  
|**최대 N 열 키**|가능한 조합에서, 테이블 또는 뷰에 대한 키로 테스트할 최대 열 수를 선택합니다. 기본값은 1입니다. 최대값은 1000입니다. 예를 들어 3을 선택하면 열 하나에서 세 개까지의 키 조합을 테스트합니다.|  
|**함수 종속성 프로필**|**최대 N 한정사로 사용되는 열**에 지정된 열 수까지 포함하는 결정 열 조합에 대해 함수 종속성 프로필을 계산합니다.<br /><br /> 이 프로필은 한 열(종속 열)의 값이 다른 열 또는 열 집합(결정 열)의 값에 종속되는 범위를 보고합니다. 또한 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제를 식별할 수 있습니다. 이 프로필의 설정에 대한 자세한 내용은 [함수 종속성 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)을 참조하세요.|  
|**최대 N 한정사로 사용되는 열**|가능한 조합에서, 결정 열로 테스트할 최대 열 수를 선택합니다. 기본값은 1입니다. 최대값은 1000입니다. 예를 들어 2를 선택하면 단일 열 또는 두 열 조합이 다른(종속) 열에 대한 결정 열인 조합을 테스트합니다.|  
  
> [!NOTE]  
>  값 포함 프로필 형식은 **단일 테이블 빠른 프로필 형식**에서 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 프로파일링 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [데이터 프로파일링 태스크 편집기&#40;프로필 요청 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
  
  
