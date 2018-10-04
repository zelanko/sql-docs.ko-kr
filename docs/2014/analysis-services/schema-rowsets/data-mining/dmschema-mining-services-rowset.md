---
title: DMSCHEMA_MINING_SERVICES 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_SERVICES
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICES rowset
ms.assetid: 4a672f2f-d637-4def-a572-c18556f83d34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ba6a0172207c84bb2bdb4b7e3de7acc84362b8f7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099767"
---
# <a name="dmschemaminingservices-rowset"></a>DMSCHEMA_MINING_SERVICES 행 집합
  공급자가 제공하는 각 데이터 마이닝 알고리즘에 대한 설명을 제공합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DMSCHEMA_MINING_SERVICES` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||알고리즘의 이름입니다. 이 열은 공급자별로 다릅니다.|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`||이 열에는 마이닝 서비스를 설명하는 비트맵이 포함됩니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 다음 값 중 하나를 사용 하 여이 열을 채웁니다.<br /><br /> -   `DM_SERVICETYPE_CLASSIFICATION` (`1`)<br />-   `DM_SERVICETYPE_CLUSTERING` (`2`)|  
|`SERVICE_DISPLAY_NAME`|`DBTYPE_WSTR`||알고리즘의 지역화 가능한 표시 이름입니다.|  
|`SERVICE_GUID`|`DBTYPE_GUID`||알고리즘의 GUID입니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||알고리즘에 대한 알기 쉬운 설명입니다.|  
|`PREDICTION_LIMIT`|`DBTYPE_UI4`||모델 및 알고리즘이 제공할 수 있는 최대 예측 수입니다.|  
|`SUPPORTED_DISTRIBUTION_FLAGS`|`DBTYPE_WSTR`||알고리즘에서 지원하는 통계 분포를 설명하는 쉼표로 구분된 플래그 목록입니다. 이 열에는 다음 값 중 하나 이상이 포함됩니다.<br /><br /> -   "`NORMAL`"<br />-   "`LOG NORMAL`"<br />-   "`UNIFORM`"|  
|`SUPPORTED_INPUT_CONTENT_TYPES`|`DBTYPE_WSTR`||알고리즘에서 지원하는 입력 내용 유형을 설명하는 쉼표로 구분된 플래그 목록입니다. 이 열에는 다음 값 중 하나 이상이 포함됩니다.<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-   "`DISCRETIZED`"<br />-   "`ORDERED`"<br />-"키 `SEQUENCE`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY VARIANCE`"<br />-   "`PROBABILITY STDEV`"<br />-   "`KEY TIME`"|  
|`SUPPORTED_PREDICTION_CONTENT_TYPES`|`DBTYPE_WSTR`||알고리즘에서 지원하는 예측 내용 유형을 설명하는 쉼표로 구분된 플래그 목록입니다. 이 열에는 다음 값 중 하나 이상이 포함됩니다.<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-   "`DISCRETIZED`"<br />-   "`ORDERED`"<br />-"키 `SEQUENCE` "<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY VARIANCE`"<br />-   "`PROBABILITY STDEV`"<br />-"KEY TIME"|  
|`SUPPORTED_MODELING_FLAGS`|`DBTYPE_WSTR`||알고리즘에서 지원하는 쉼표로 구분된 모델링 플래그 목록입니다. 이 열에는 다음 값 중 하나 이상이 포함됩니다.<br /><br /> -   "`MODEL_EXISTENCE_ONLY`"<br />-   "`REGRESSOR`"<br /><br /> 공급자별 플래그를 정의할 수도 있습니다.|  
|`SUPPORTED_SOURCE_QUERY`|`DBTYPE_WSTR`||-이 열은 이전 버전과 호환성을 위해 지원 됩니다.|  
|`TRAINING_COMPLEXITY`|`DBTYPE_I4`||학습 예상 소요 시간입니다.<br /><br /> -   `DM_TRAINING_COMPLEXITY_LOW` 실행 시간이 비교적 짧고 입력에 비례 하는 것을 나타냅니다.<br />-   **DM_TRAINING_COMPLEXITY_MEDIUM** 실행 시간이 길 수 있지만 입력에 일반적으로 비례 나타냅니다.<br />-   **DM_TRAINING_COMPLEXITY_HIGH** 실행 시간이 깁니다 늘어날 수 기하급수적으로 관계에서의 학습 사례 수를 나타냅니다.|  
|`PREDICTION_COMPLEXITY`|`DBTYPE_I4`||예측 예상 소요 시간입니다.<br /><br /> -   **DM_PREDICTION_COMPLEXITY_LOW** 나타내고는 실행 시간이 비교적 짧고 입력에 비례 합니다.<br />-   **DM_PREDICTION_COMPLEXITY_MEDIUM** 실행 시간이 길 수 있지만 입력에 일반적으로 비례 나타냅니다.<br />-   **DM_PREDICTION_COMPLEXITY_HIGH** 실행 시간이 깁니다 늘어날 수 기하급수적으로 관계에서의 학습 사례 수를 나타냅니다.|  
|`EXPECTED_QUALITY`|`DBTYPE_I4`||이 알고리즘을 사용하여 생성되는 모델의 예상 품질입니다.<br /><br /> -   `DM_EXPECTED_QUALITY_LOW`<br />-   `DM_EXPECTED_QUALITY_MEDIUM`<br />-   **DM_EXPECTED_QUALITY_HIGH**|  
|`SCALING`|`DBTYPE_I4`||알고리즘의 확장성입니다.<br /><br /> -   **DM_SCALING_LOW**<br />-   `DM_SCALING_MEDIUM`<br />-   **DM_SCALING_HIGH**|  
|`ALLOW_INCREMENTAL_INSERT`|`DBTYPE_BOOL`||알고리즘이 증분 학습을 지원하는지, 즉 패턴 전체를 다시 검색하지 않고 새로운 실제 데이터를 기반으로 검색된 패턴을 업데이트하는 기능을 지원하는지 여부를 나타내는 부울입니다.|  
|`ALLOW_PMML_INITIALIZATION`|`DBTYPE_BOOL`||PMML 2.1 문자열을 기반으로 마이닝 모델을 만들 수 있는지 여부를 나타내는 부울입니다.<br /><br /> `TRUE`이면 마이닝 알고리즘이 PMML 2.1 콘텐츠로부터 초기화를 지원합니다.|  
|`CONTROL`|`DBTYPE_I4`||학습이 중단되는 경우 서비스에서 제공하는 지원입니다.<br /><br /> -   `DM_CONTROL_NONE` 모델 학습에 시작 된 후 알고리즘을 취소할 수를 나타냅니다.<br />-   `DM_CONTROL_CANCEL` 모델을 학습 하기 시작 하지만 학습을 재개 하려면 다시 시작 해야 하는 알고리즘을 취소할 수 있습니다를 나타냅니다.<br />-   `DM_CONTROL_SUSPENDRESUME` 알고리즘을 취소 하 고 언제 든 지 재개할 수 있지만 학습 완료 될 때까지 결과 사용할 수 없습니다 나타냅니다.<br />-   `DM_CONTROL_SUSPENDWITHRESULT` 모든 증분 결과 얻을 수 있습니다 하 알고리즘을 취소 하 고 언제 든 지 재개할 수를 나타냅니다.|  
|`ALLOW_DUPLICATE_KEY`|`DBTYPE_BOOL`||사례에 중복 키가 포함될 수 있는지 여부를 나타내는 부울입니다.<br /><br /> `VARIANT_TRUE`이면 사례에 중복 키가 포함될 수 있습니다.|  
|`VIEWER_TYPE`|`DBTYPE_WSTR`||이 모델에 대해 권장되는 뷰어입니다.|  
|`HELP_FILE`|`DBTYPE_WSTR`||(선택 사항) 이 서비스에 대한 설명서가 있는 파일의 이름입니다.|  
|`HELP_CONTEXT`|`DBTYPE_I4`||(선택 사항) 이 서비스에 대한 도움말 컨텍스트 ID입니다.|  
|`MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL`|`DBTYPE_WSTR`||지원되는 DDL 버전입니다. 0은 DDL이 지원되지 않음을 나타냅니다.|  
|`MSOLAP_SUPPORTS_OLAP_MINING_MODELS`|`DBTYPE_BOOL`||OLAP 마이닝 모델을 만들 수 있는지 여부를 나타내는 부울입니다.<br /><br /> `TRUE`이면 OLAP 마이닝 모델을 만들 수 있습니다. `MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL`은 0이 아니어야 합니다.|  
|`MSOLAP_SUPPORTS_DATA_MINING_DIMENSIONS`|`DBTYPE_BOOL`||데이터 마이닝 차원을 만들 수 있는지 여부를 나타내는 부울입니다.<br /><br /> `TRUE`이면 데이터 마이닝 차원을 만들 수 있습니다.|  
|`MSOLAP_SUPPORTS_DRILLTHROUGH`|`DBTYPE_BOOL`||서비스가 드릴스루 기능을 지원하는지 여부를 나타내는 부울입니다.<br /><br /> `TRUE`이면 서비스가 드릴스루 기능을 지원합니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 `DMSCHEMA_MINING_SERVICES` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 스키마 행 집합](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
