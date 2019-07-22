---
title: 데이터 프로파일링 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataprofilingtask.f1
helpviewer_keywords:
- Data Profiling task [Integration Services], about Data Profiling task
- data profiling
- profiling data
ms.assetid: 248ce233-4342-42c5-bf26-f4387ea152cf
author: janinezhang
ms.author: janinez
ms.openlocfilehash: cafb198c7d38c3a03562d6fda39f2b9c4f3b2418
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003572"
---
# <a name="data-profiling-task"></a>데이터 프로파일링 태스크

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  데이터 프로파일링 태스크는 사용자가 데이터 원본에 익숙해지고 데이터에서 해결해야 할 문제를 식별하는 데 도움이 되는 다양한 프로필을 계산합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 내에 있는 데이터 프로파일링 태스크를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 저장된 데이터를 프로파일링하고 잠재적인 데이터 품질 문제를 식별할 수 있습니다.  
  
> [!NOTE]  
>  이 항목에서는 데이터 프로파일링 작업의 기능 및 요구 사항에 대해서만 설명합니다. 데이터 프로파일링 태스크 사용 방법에 대한 자세한 내용은 [데이터 프로파일링 태스크 및 뷰어](../../integration-services/control-flow/data-profiling-task-and-viewer.md)섹션을 참조하세요.  
  
## <a name="requirements-and-limitations"></a>요구 사항 및 제한 사항  
 데이터 프로파일링 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 저장된 데이터만 사용할 수 있습니다. 이 태스크는 타사 또는 파일 기반 데이터 원본에서는 작동하지 않습니다.  
  
 또한 데이터 프로파일링 태스크가 포함된 패키지를 실행하려면 tempdb 데이터베이스에 대해 CREATE TABLE 권한을 비롯한 읽기/쓰기 권한이 있는 계정을 사용해야 합니다.  
  
## <a name="data-profiler-viewer"></a>데이터 프로파일러 뷰어  
 이 태스크를 사용하여 데이터 프로필을 컴퓨팅하고 파일에 저장하면 독립 실행형 데이터 프로필 뷰어를 사용하여 프로필 출력을 검토할 수 있습니다. 데이터 프로필 뷰어는 드릴다운 기능도 지원하므로 프로필 출력에서 식별된 데이터 품질 문제를 파악하는 데 도움이 됩니다. 자세한 내용은 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  출력 파일에는 데이터베이스와 해당 데이터베이스에 포함된 데이터에 대한 중요 데이터가 포함될 수 있습니다. 이 파일을 보다 안전하게 보호하는 방법에 대한 제안 사항은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
>   
>  데이터 프로필 뷰어에서 사용할 수 있는 드릴다운 기능은 원래 데이터 원본에 라이브 쿼리를 보냅니다.  
  
## <a name="available-profiles"></a>사용 가능한 프로필  
 데이터 프로파일링 태스크는 8가지 데이터 프로필을 컴퓨팅할 수 있습니다. 이 중 5개는 개별 열을 분석하며, 나머지 3개는 여러 열 또는 열과 테이블 간의 관계를 분석합니다.  
  
 개별 열을 분석하는 5개 프로필은 다음과 같습니다.  
  
|개별 열을 분석하는 프로필|설명|  
|----------------------------------------------|-----------------|  
|열 길이 분포 프로필|선택한 열에 있는 문자열 값의 모든 고유 길이, 그리고 각 길이가 나타내는 테이블 내 행의 비율을 보고합니다.<br /><br /> 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 두 문자로 이루어진 미국 주 코드의 열을 프로파일링하여 두 문자보다 긴 값을 검색할 수 있습니다.|  
|열 Null 비율 프로필|선택한 열의 Null 값 비율을 보고합니다.<br /><br /> 이 프로필을 사용하면 열에 포함된 지나치게 높은 null 값 비율과 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 우편 번호 열을 프로파일링하여 허용 불가능한 수준의 누락된 코드 비율을 검색할 수 있습니다.|  
|열 패턴 프로필|문자열 열의 지정된 값 비율을 포괄하는 정규식 집합을 보고합니다.<br /><br /> 이 프로필을 사용하면 잘못된 문자열과 같은 데이터 문제를 식별할 수 있습니다. 또한 이 프로필은 앞으로 새 값의 유효성 검사에 사용할 수 있는 정규식을 제안해 줍니다. 예를 들어 미국 우편 번호 열의 패턴 프로필이 \d{5}-\d{4}, \d{5} 및 \d{9} 정규식을 생성할 수 있습니다. 다른 정규식이 발견된다면 데이터에 유효하지 않거나 잘못된 형식의 값이 포함되어 있을 가능성이 높습니다.|  
|열 통계 프로필|숫자 열의 최소값, 최대값, 평균, 표준 편차 및 **datetime** 열의 최소값, 최대값과 같은 통계를 보고합니다.<br /><br /> 이 프로필을 사용하면 잘못된 날짜와 같은 데이터 문제를 식별할 수 있습니다. 예를 들어 기록 날짜 열을 프로파일링하여 미래의 최대 날짜를 검색할 수 있습니다.|  
|열 값 분포 프로필|선택한 열에 있는 모든 고유 값, 그리고 각 값이 나타내는 테이블 내 행의 비율을 보고합니다. 또한 테이블에서 지정된 행 비율을 초과하는 값을 보고할 수도 있습니다.<br /><br /> 이 프로필을 사용하면 열에 포함된 잘못된 수의 고유 값과 같은 데이터의 문제를 식별할 수 있습니다. 예를 들어 미국의 주를 포함하는 열을 프로파일링하여 50개를 초과하는 고유 값을 검색할 수 있습니다.|  
  
 다음의 3개 프로필은 여러 열 또는 열과 테이블 간의 관계를 분석합니다.  
  
|여러 열을 분석하는 프로필|설명|  
|--------------------------------------------|-----------------|  
|후보 키 프로필|하나의 열 또는 열 집합이 선택한 테이블의 키 또는 근사 키인지 보고합니다.<br /><br /> 이 프로필을 사용하면 잠재적 키 열의 중복 값과 같은 데이터의 문제를 식별할 수 있습니다.|  
|함수 종속성 프로필|한 열(종속 열)의 값이 다른 열 또는 열 집합(결정 열)의 값에 종속되는 범위를 보고합니다.<br /><br /> 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제도 식별할 수 있습니다. 예를 들어 미국 우편 번호를 포함하는 열과 미국의 주를 포함하는 열 간의 종속성을 프로파일링할 수 있습니다. 우편 번호가 같으면 주도 동일해야 하므로 프로필에서 이러한 종속성 위반을 검색할 수 있습니다.|  
|값 포함 프로필|두 개의 열 또는 열 집합 간에 겹치는 값을 계산합니다. 이 프로필을 사용하면 열 또는 열 집합이 선택한 테이블 간의 외래 키 역할을 수행하기에 적합한지 여부를 확인할 수 있습니다.<br /><br /> 이 프로필을 사용하면 잘못된 값과 같은 데이터 문제도 식별할 수 있습니다. 예를 들어 Sales 테이블의 ProductID 열을 프로파일링하여 Products 테이블의 ProductID 열에 없는 값이 포함된 열을 검색할 수 있습니다.|  
  
## <a name="prerequisites-for-a-valid-profile"></a>유효한 프로필의 필수 구성 요소  
 프로필이 유효하려면 비어 있지 않은 테이블과 열을 선택해야 하며 열에 포함된 데이터 형식이 프로필에 적합해야 합니다.  
  
### <a name="valid-data-types"></a>유효한 데이터 형식  
 일부 프로필은 특정 데이터 형식에 대해서만 의미가 있습니다. 예를 들어 숫자 또는 **datetime** 값을 포함하는 열의 열 패턴 프로필 계산은 의미가 없습니다. 따라서 이러한 프로필은 유효하지 않게 됩니다.  
  
|프로필|유효한 데이터 형식*|  
|-------------|------------------------|  
|ColumnStatisticsProfile|숫자 형식 또는 **datetime** 형식의 열( **datetime** 열의 경우 **mean** 및 **stddev** 없음)|  
|ColumnNullRatioProfile|모든 열**|  
|ColumnValueDistributionProfile|**integer** 형식, **char** 형식 및 **datetime** 형식의 열|  
|ColumnLengthDistributionProfile|**char** 형식의 열|  
|ColumnPatternProfile|**char** 형식의 열|  
|CandidateKeyProfile|**integer** 형식, **char** 형식 및 **datetime** 형식의 열|  
|FunctionalDependencyProfile|**integer** 형식, **char** 형식 및 **datetime** 형식의 열|  
|InclusionProfile|**integer** 형식, **char** 형식 및 **datetime** 형식의 열|  
  
 \* 위의 유효한 데이터 형식 표에서 **integer**, **char**, **datetime**및 **numeric** 형식에는 다음과 같은 특정 데이터 형식이 포함됩니다.  
  
 정수 형식에는 **bit**, **tinyint**, **smallint**, **int**및 **bigint**가 포함됩니다.  
  
 문자 형식에는 **char**, **nchar**, **varchar**및 **nvarchar** 가 포함되지만 **varchar(max)** 및 **nvarchar(max)** 는 포함되지 않습니다.  
  
 날짜 및 시간 형식에는 **datetime**, **smalldatetime**및 **timestamp**가 포함됩니다.  
  
 숫자 형식에는 **integer** 형식( **bit**제외), **money**, **smallmoney**, **decimal**, **float**, **real**및 **numeric**이 포함됩니다.  
  
 \*\* **image**, **text**, **XML**, **udt**및 **variant** 형식은 열 Null 비율 프로필 이외의 프로필에 대해서는 지원되지 않습니다.  
  
### <a name="valid-tables-and-columns"></a>유효한 테이블 및 열  
 테이블 또는 열이 비어 있으면 데이터 프로파일링이 다음 동작을 수행합니다.  
  
-   선택한 테이블 또는 뷰가 비어 있으면 데이터 프로파일링 태스크가 프로필을 컴퓨팅하지 않습니다.  
  
-   선택한 열의 모든 값이 Null이면 데이터 프로파일링 태스크가 열 Null 비율 프로필만 계산합니다. 열 길이 분포 프로필, 열 패턴 프로필, 열 통계 프로필 또는 열 값 분포 프로필은 컴퓨팅하지 않습니다.  
  
## <a name="features-of-the-data-profiling-task"></a>데이터 프로파일링 태스크의 기능  
 데이터 프로파일링 태스크는 다음과 같은 편리한 구성 옵션을 제공합니다.  
  
-   **와일드카드 열** 프로필 요청을 구성하는 경우 태스크는 열 이름 대신 **(\*)** 와일드카드를 허용합니다. 이 기능을 통해 구성을 간편히 수행하고 생소한 데이터의 특성을 보다 쉽게 검색할 수 있습니다. 태스크는 실행될 때 해당 데이터 형식을 가진 모든 열을 프로파일링합니다.  
  
-   **빠른 프로필** 빠른 프로필을 선택하여 신속히 태스크를 구성할 수 있습니다. 빠른 프로필은 모든 기본 프로필과 기본 설정을 사용하여 테이블 또는 뷰를 프로파일링합니다.  
  
## <a name="custom-logging-messages-available-on-the-data-profililng-task"></a>데이터 프로파일링 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 데이터 프로파일링 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|설명|  
|---------------|-----------------|  
|**DataProfilingTaskTrace**|태스크 상태에 대한 설명 정보를 제공합니다. 메시지에는 다음 정보가 포함됩니다.<br /><br /> 처리 요청 시작<br /><br /> 쿼리 시작<br /><br /> 쿼리 끝<br /><br /> 계산 요청 마침|  
  
## <a name="output-and-its-schema"></a>출력 및 스키마  
 데이터 프로파일링 태스크는 선택한 프로필을 DataProfile.xsd 스키마에 따라 구조화된 XML로 출력합니다. 이 XML을 파일 또는 패키지 변수에 저장하도록 지정할 수 있습니다. 이 스키마는 [https://schemas.microsoft.com/sqlserver/2008/DataDebugger/](https://schemas.microsoft.com/sqlserver/2008/DataDebugger/)에서 온라인으로 볼 수 있습니다. 웹 페이지에서 스키마를 로컬 복사본으로 저장할 수 있습니다. 그런 다음 Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 또는 다른 스키마 편집기, XML 편집기나 메모장과 같은 텍스트 편집기에서 스키마의 로컬 복사본을 볼 수 있습니다.  
  
 데이터 품질 정보에 대한 이 스키마는 다음과 같은 경우 유용할 수 있습니다.  
  
-   조직 내부 또는 조직 간의 데이터 품질 정보 교환  
  
-   데이터 품질 정보를 사용하는 사용자 지정 도구 빌드  
  
 대상 네임스페이스는 스키마에서 [https://schemas.microsoft.com/sqlserver/2008/DataDebugger/](https://schemas.microsoft.com/sqlserver/2008/DataDebugger/)로 식별됩니다.  
  
## <a name="output-in-the-conditional-workflow-of-a-package"></a>패키지 조건부 워크플로의 출력  
 데이터 프로파일링 구성 요소에는 데이터 프로파일링 태스크의 출력을 기반으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 워크플로에 조건부 논리를 구현하기 위한 기본 제공 기능이 없습니다. 그러나 이 논리는 스크립트 태스크를 사용하여 최소한의 프로그래밍 작업으로 손쉽게 추가할 수 있습니다. 이 코드는 XML 출력을 대상으로 XPath 쿼리를 수행한 다음 그 결과를 패키지 변수로 저장합니다. 스크립트 태스크를 후속 태스크에 연결하는 선행 제약 조건은 식을 사용하여 워크플로를 확인할 수 있습니다. 예를 들어 스크립트 태스크는 열에서 특정 임계값을 초과하는 null 값의 비율을 탐지합니다. 이 경우 패키지를 중단하면 문제가 계속되기 전에 해결할 수 있습니다.  
  
## <a name="configuration-of-the-data-profiling-task"></a>데이터 프로파일링 태스크 구성  
 데이터 프로파일링 태스크는 **데이터 프로파일링 태스크 편집기**를 사용하여 구성합니다. 이 편집기에는 다음과 같은 두 개의 페이지가 있습니다.  
  
 [일반 페이지](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)  
 **일반** 페이지에서는 출력 파일 또는 변수를 지정합니다. 또한 **빠른 프로필**을 선택하여 기본 설정으로 신속히 태스크를 구성, 프로필을 컴퓨팅할 수 있습니다. 자세한 내용은 [단일 테이블 빠른 프로필 형식&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)을 참조하세요.  
  
 [프로필 요청 페이지](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
 **프로필 요청** 페이지에서는 데이터 원본을 지정하고 컴퓨팅할 데이터 프로필을 선택 및 구성할 수 있습니다. 구성 가능한 여러 프로필에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [후보 키 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [열 길이 분포 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [열 Null 비율 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [열 패턴 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [열 통계 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [열 값 분포 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [함수 종속성 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [값 포함 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
  
