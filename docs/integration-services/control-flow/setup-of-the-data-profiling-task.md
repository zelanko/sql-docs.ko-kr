---
title: 데이터 프로파일링 태스크 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], configuring
ms.assetid: fe050ca4-fe45-43d7-afa9-99478041f9a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5032c7f48bdafdab0430357c01698f5672b2f830
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727498"
---
# <a name="setup-of-the-data-profiling-task"></a>데이터 프로파일링 태스크 설정

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  원본 데이터의 프로필을 검토하기 전에 수행해야 하는 첫 번째 단계는 데이터 프로파일링 태스크를 설정하고 실행하는 것입니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 내에서 이 태스크를 만듭니다. 데이터 프로파일링 태스크를 구성하려면 데이터 프로파일링 태스크 편집기를 사용합니다. 이 편집기를 사용하면 프로필을 출력할 위치와 컴퓨팅할 프로필을 선택할 수 있습니다. 태스크를 설정한 후 패키지를 실행하여 데이터 프로필을 컴퓨팅합니다.  
  
## <a name="requirements-and-limitations"></a>요구 사항 및 제한 사항  
 데이터 프로파일링 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 저장된 데이터만 사용할 수 있습니다. 이 태스크는 타사 또는 파일 기반 데이터 원본을 사용할 수 없습니다.  
  
 또한 데이터 프로파일링 태스크가 포함된 패키지를 실행하려면 tempdb 데이터베이스에 대해 CREATE TABLE 권한을 비롯한 읽기/쓰기 권한이 있는 계정을 사용해야 합니다.  
  
## <a name="data-profiling-task-in-a-package"></a>패키지의 데이터 프로파일링 태스크  
 데이터 프로파일링 태스크는 프로필만 구성하고 계산된 프로필이 포함된 출력 파일을 만듭니다. 이 출력 파일을 검토하려면 독립 실행형 뷰어 프로그램인 데이터 프로필 뷰어를 사용해야 합니다. 출력을 별도로 검토해야 하기 때문에 다른 태스크가 포함되어 있지 않은 패키지에서 데이터 프로파일링 태스크를 사용합니다.  
  
 그러나 데이터 프로파일링 태스크를 패키지의 유일한 태스크로 사용할 필요는 없습니다. 더 복잡한 패키지의 워크플로 또는 데이터 흐름에서 데이터 프로파일링을 수행하려면 다음 방법 중 하나를 선택합니다.  
  
-   패키지의 제어 흐름에서 태스크의 출력 파일을 기반으로 하는 조건부 논리를 구현하려면 데이터 프로파일링 태스크 뒤에 스크립트 태스크를 삽입합니다. 그러면 이 스크립트 태스크를 사용하여 출력 파일을 쿼리할 수 있습니다.  
  
-   데이터가 로드되고 변환된 후 데이터 흐름에서 데이터를 프로파일링하려면 변경된 데이터를 임시로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장해야 합니다. 그러면 저장된 데이터를 프로파일링할 수 있습니다.  
  
 자세한 내용은 [패키지 워크플로에 데이터 프로파일링 태스크 포함](../../integration-services/control-flow/incorporate-a-data-profiling-task-in-package-workflow.md)을 참조하세요.  
  
## <a name="setup-of-the-task-output"></a>태스크 출력 설정  
 패키지에 데이터 프로파일링 태스크를 삽입한 후에는 태스크에서 컴퓨팅할 프로필의 출력을 설정해야 합니다. 프로필의 출력을 설정하려면 데이터 프로파일링 태스크 편집기의 **일반** 페이지를 사용합니다. **일반** 페이지는 출력의 대상을 지정하는 기능뿐만 아니라 빠른 데이터 프로파일링을 수행하는 기능을 제공합니다. **빠른 프로필**을 선택하면 데이터 프로파일링 태스크가 일부 또는 전체 기본 프로필과 해당 기본 설정을 사용하여 테이블 또는 뷰를 프로파일링합니다.  
  
 자세한 내용은 [데이터 프로파일링 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md) 및 [단일 테이블 빠른 프로필 형식&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  출력 파일에는 데이터베이스와 해당 데이터베이스에 포함된 데이터에 대한 중요 데이터가 포함될 수 있습니다. 이 파일을 보다 안전하게 보호하는 방법에 대한 제안 사항은 [패키지에서 사용되는 파일 액세스](../../integration-services/security/security-overview-integration-services.md#files)를 참조하세요.  
  
## <a name="selection-and-configuration-of-the-profiles-to-be-computed"></a>계산할 프로필 선택 및 구성  
 출력 파일을 설정한 후에는 컴퓨팅할 데이터 프로필을 선택해야 합니다. 데이터 프로파일링 태스크는 8가지 데이터 프로필을 컴퓨팅할 수 있습니다. 이 중 5개는 개별 열을 분석하며, 나머지 3개는 여러 열 또는 열과 테이블 간의 관계를 분석합니다. 단일 데이터 프로파일링 태스크에서 여러 테이블 또는 뷰에 있는 여러 열이나 열 조합에 대해 여러 프로필을 컴퓨팅할 수 있습니다.  
  
 다음 표에서는 이러한 각 프로필이 계산하는 보고서와 해당 프로필이 유효한 데이터 형식을 설명합니다.  
  
|컴퓨팅 대상|식별에 도움이 되는 값|사용할 프로필|  
|----------------|-------------------------|----------------------|  
|선택한 열에 있는 문자열 값의 모든 고유 길이 및 각 길이가 나타내는 테이블 내 행의 비율|**유효하지 않은 문자열 값** - 예를 들어 미국의 주 코드에 대해 두 개의 문자를 사용해야 하는 열을 프로파일링하는 중에 두 문자보다 긴 값을 검색할 수 있습니다.|**열 길이 분포** - 다음 문자 데이터 형식 중 하나가 포함된 열에 대해 유효합니다.<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**|  
|문자열 열에서 지정된 값의 비율을 포괄하는 정규식 집합<br /><br /> 또한 앞으로 새 값의 유효성 검사에 사용할 수 있는 정규식 검색을 위해|**유효하지 않거나 올바른 형식이 아닌 문자열 값** - 예를 들어 우편 번호 열의 패턴 프로필은 \d{5}-\d{4}, \d{5} 및 \d{9} 같은 정규식을 생성할 수 있습니다. 출력에 다른 정규식이 포함된 경우 데이터에 유효하지 않거나 잘못된 형식의 값이 포함되어 있는 것입니다.|**열 패턴 프로필** - 다음 문자 데이터 형식 중 하나가 포함된 열에 대해 유효합니다.<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**|  
|선택한 열 내 Null 값의 비율|**예기치 않게 높은 열 내 Null 값의 비율** - 예를 들어 미국 우편 번호를 포함해야 하는 열을 프로파일링하는 중 예기치 않게 높은 비율의 누락된 우편 번호를 검색할 수 있습니다.|**열 Null 비율** - 다음 데이터 형식 중 하나가 포함된 열에 대해 유효합니다.<br /><br /> **image**<br /><br /> **text**<br /><br /> **xml**<br /><br /> 사용자 정의 형식<br /><br /> 변형 유형|  
|숫자 열에 대한 최소값, 최대값, 평균값, 표준 편차 및 **datetime** 열에 대한 최소값/최대값과 같은 통계|**유효하지 않은 숫자 값 및 날짜** - 예를 들어 기록 날짜 열을 프로파일링하는 중 미래의 최대 날짜를 검색할 수 있습니다.|**열 통계 프로필** - 다음 데이터 형식 중 하나가 포함된 열에 대해 유효합니다.<br /><br /> 숫자 데이터 형식:<br /><br /> 정수 형식(제외: **bit**<br /><br /> **money**<br /><br /> **smallmoney**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **real**<br /><br /> **numeric**<br /><br /> 날짜 및 시간 데이터 형식:<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> 참고: 날짜 및 시간 데이터 유형이 포함된 열의 경우 프로필이 최소값 및 최대값만 계산합니다.|  
|선택한 열에 있는 모든 고유 값 및 각 값이 나타내는 테이블 내 행의 비율 또는 테이블에서 지정된 비율을 초과하는 값|**열에 포함된 잘못된 수의 고유 값** - 예를 들어 미국의 주가 포함된 열을 프로파일링하는 중 50개를 초과하는 고유 값을 검색할 수 있습니다.|**열 값 분포** - 다음 데이터 형식 중 하나가 포함된 열에 대해 유효합니다.<br /><br /> 숫자 데이터 형식:<br /><br /> 정수 형식(제외: **bit**<br /><br /> **money**<br /><br /> **smallmoney**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **real**<br /><br /> **numeric**<br /><br /> 문자 데이터 형식:<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**<br /><br /> 날짜 및 시간 데이터 형식:<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**|  
|열 또는 열 집합이 선택한 테이블에 대해 키인지, 아니면 근사 키인지 여부|**잠재적 키 열의 중복 값** - 예를 들어 Customers 테이블의 Name 및 Address 열을 프로파일링하는 중 이름과 주소의 조합이 고유해야 하는 중복 값을 검색할 수 있습니다.|**후보 키** - 열 또는 열 집합이 선택한 테이블에 대한 키 역할을 수행하기에 적합한지 여부를 보고하는 여러 열 프로필입니다. 다음 데이터 형식 중 하나가 지정된 열에 대해 유효합니다.<br /><br /> 정수 데이터 형식:<br /><br /> **bit**<br /><br /> **tinyint**<br /><br /> **smallint**<br /><br /> **ssNoversion**<br /><br /> **bigint**<br /><br /> 문자 데이터 형식:<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**<br /><br /> 날짜 및 시간 데이터 형식:<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**|  
|한 열(종속 열)의 값이 다른 열 또는 열 집합(결정 열)의 값에 종속되는 범위|**종속 열에서 유효하지 않은 값** - 예를 들어 미국의 우편 번호가 포함된 열과 미국의 주가 포함된 열 간 종속성을 프로파일링하는 중 같은 우편 번호는 항상 같은 주여야 하는데 프로필이 종속성 위반을 검색할 수 있습니다.|**함수 종속성** - 다음 데이터 형식 중 하나가 포함된 열에 대해 유효합니다.<br /><br /> 정수 데이터 형식:<br /><br /> **bit**<br /><br /> **tinyint**<br /><br /> **smallint**<br /><br /> **ssNoversion**<br /><br /> **bigint**<br /><br /> 문자 데이터 형식:<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**<br /><br /> 날짜 및 시간 데이터 형식:<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**|  
|열 또는 열 집합이 선택한 테이블 간의 외래 키 역할을 수행하기에 적합한지 여부<br /><br /> 즉, 이 프로필은 두 개의 열 또는 열 집합 간에 겹치는 값을 보고합니다.|**유효하지 않은 값** - 예를 들어 Sales 테이블의 ProductID 열을 프로파일링하는 중 프로필이 Products 테이블의 ProductID 열에 없는 값이 열에 포함되어 있음을 검색할 수 있습니다.|**값 포함** - 다음 데이터 형식 중 하나가 포함된 열에 대해 유효합니다.<br /><br /> 정수 데이터 형식:<br /><br /> **bit**<br /><br /> **tinyint**<br /><br /> **smallint**<br /><br /> **ssNoversion**<br /><br /> **bigint**<br /><br /> 문자 데이터 형식:<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**<br /><br /> 날짜 및 시간 데이터 형식:<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**|  
  
 컴퓨팅할 프로필을 선택하려면 데이터 프로파일링 태스크 편집기의 **프로필 요청** 페이지를 사용합니다. 자세한 내용은 [데이터 프로파일링 태스크 편집기&#40;프로필 요청 페이지&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)를 참조하세요.  
  
 **프로필 요청** 페이지에서 데이터 원본을 지정하고 데이터 프로필도 구성합니다. 태스크를 구성할 때 다음 정보를 고려하십시오.  
  
-   구성을 단순화하고 익숙지 않은 데이터의 특징을 더욱 쉽게 파악하기 위해 개별 열 이름 대신 와일드카드 **(\*)** 를 사용할 수 있습니다. 이 와일드카드를 사용하면 태스크에서 적절한 데이터 형식이 포함된 모든 열을 프로파일링하기 때문에 처리 속도가 느려질 수 있습니다.  
  
-   선택한 테이블 또는 뷰가 비어 있으면 데이터 프로파일링 태스크가 프로필을 컴퓨팅하지 않습니다.  
  
-   선택한 열의 모든 값이 Null이면 데이터 프로파일링 태스크가 열 Null 비율 프로필만 계산합니다. 이 태스크는 빈 열에 대한 열 길이 분포 프로필, 열 패턴 프로필, 열 통계 프로필 또는 열 값 분포 프로필을 컴퓨팅하지 않습니다.  
  
 사용 가능한 데이터 프로필 각각에는 고유한 구성 옵션이 있습니다. 이러한 옵션에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [후보 키 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [열 길이 분포 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [열 Null 비율 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [열 패턴 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [열 통계 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [열 값 분포 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [함수 종속성 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [값 포함 프로필 요청 옵션&#40;데이터 프로파일링 태스크&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="execution-of-the-package-that-contains-the-data-profiling-task"></a>데이터 프로파일링 태스크가 포함된 패키지 실행  
 데이터 프로파일링 태스크를 설정한 후 이 태스크를 실행할 수 있습니다. 그러면 이 태스크에서 데이터 프로필을 계산하여 이 정보를 XML 형식으로 파일 또는 패키지 변수에 출력합니다. 이 XML의 구조는 DataProfile.xsd 스키마를 따릅니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 또는 다른 스키마 편집기, XML 편집기, 메모장과 같은 텍스트 편집기에서 이 스키마를 열 수 있습니다. 데이터 품질 정보에 대한 이 스키마는 다음과 같은 용도로 사용할 경우 유용할 수 있습니다.  
  
-   조직 내부 또는 조직 간의 데이터 품질 정보 교환  
  
-   데이터 품질 정보를 사용하는 사용자 지정 도구 빌드  
  
 대상 네임스페이스는 스키마에서 [https://schemas.microsoft.com/sqlserver/2008/DataDebugger/](https://schemas.microsoft.com/sqlserver/2008/DataDebugger/)로 식별됩니다.  
  
## <a name="next-step"></a>다음 단계  
 [데이터 프로필 뷰어](../../integration-services/control-flow/data-profile-viewer.md)  
  
  
