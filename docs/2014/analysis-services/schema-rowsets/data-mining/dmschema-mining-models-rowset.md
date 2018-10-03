---
title: DMSCHEMA_MINING_MODELS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_MODELS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODELS rowset
ms.assetid: 1636f4cf-b342-4e2e-93b4-04136e2d41ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 915a4f98c319af16daff2d07667463d2ec77c50d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178103"
---
# <a name="dmschemaminingmodels-rowset"></a>DMSCHEMA_MINING_MODELS 행 집합
  현재 카탈로그의 데이터 마이닝 모델을 열거합니다. `DMSCHEMA_MINING_MODELS` 행 집합에는 각 마이닝 모델에 연결된 모델 이름, 처리 날짜 및 마이닝 알고리즘과 같은 정보가 포함됩니다.  
  
 . 합니다 `DMSCHEMA_MINING_MODELS` 스키마 행 집합은 매우 유사 합니다 [DBSCHEMA_TABLES](../ole-db/dbschema-tables-rowset.md) 스키마 행 집합 동일한 방식으로 사용할 수 있습니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DMSCHEMA_MINING_MODELS` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||카탈로그 이름입니다. 모델이 멤버인 데이터베이스 이름으로 채워집니다.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||정규화되지 않은 스키마 이름입니다. 이 열에서 지원 되지 않습니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 `NULL`합니다.|  
|`MODEL_NAME`|`DBTYPE_WSTR`||마이닝 모델 이름입니다. 이 열에는 마이닝 모델 이름이 포함되며 비어 있을 수 없습니다.|  
|`MODEL_TYPE`|`DBTYPE_WSTR`||모델 유형입니다.|  
|`MODEL_GUID`|`DBTYPE_GUID`||모델의 GUID입니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||모델에 대한 알기 쉬운 설명입니다.|  
|`MODEL_PROPID`|`DBTYPE_UI4`||모델의 속성 ID입니다. 이 열은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 지원하지 않으므로 항상 `NULL`입니다.|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||모델을 만든 날짜입니다.|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||모델 정의를 마지막으로 수정한 날짜입니다.|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`||모델에 사용된 데이터 마이닝 알고리즘의 유형을 식별하는 열거형입니다. 이 유형은 다음 값 중 하나일 수 있습니다.<br /><br /> -   `DM_SERVICETYPE_CLASSIFICATION` (1)<br />-   `DM_SERVICETYPE_SEGMENTATION`(2)<br />-   `DM_SERVICETYPE_ ASSOCIATION`(4)<br />-   `DM_SERVICETYPE_ DENSITY_ESTIMATE`(8)<br />-   `DM_SERVICETYPE_SEQUENCE`(16)|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||모델에 사용된 데이터 마이닝 알고리즘의 공급자별 이름입니다.|  
|`CREATION_STATEMENT`|`DBTYPE_WSTR`||마이닝 모델을 만드는 데 사용된 문입니다.|  
|`PREDICTION_ENTITY`|`DBTYPE_WSTR`||예측할 수 있는 마이닝 열을 나타내는 쉼표로 구분된 목록입니다.|  
|`IS_POPULATED`|`DBTYPE_BOOL`||모델이 채워졌는지 여부를 나타내는 부울 플래그입니다.<br /><br /> 모델이 채워졌으면 `TRUE`이고, 그렇지 않으면 `FALSE`입니다.|  
|`MINING_PARAMETERS`|`DBTYPE_WSTR`||모델을 만들 때 사용된 매개 변수 목록이며 쉼표로 구분되어 있습니다.|  
|`MINING_STRUCTURE`|`DBTYPE_WSTR`||모델의 기반이 되는 마이닝 구조의 ID입니다.|  
|`LAST_PROCESSED`|`DBTYPE_DBTIMESTAMP`||모델을 마지막으로 처리한 날짜입니다.|  
|`MSOLAP_IS_DRILLTHROUGH_ENABLED`|`DBTYPE_BOOL`||모델이 드릴스루를 지원하는지 여부를 나타내는 부울 플래그입니다.|  
|`FILTER`|`DBTYPE_WSTR`||마이닝 모델에 연결된 필터 식입니다.<br /><br /> NULL 또는 빈 문자열은 필터가 적용되지 않음을 나타냅니다.|  
|`TRAINING_SET_SIZE`|`DBTYPE_UIS`||구조가 처리되고 필터가 모델에 적용된 후에 마이닝 모델 학습 집합에 포함되는 사례의 수입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 `DMSCHEMA_MINING_MODELS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|(선택 사항)|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|(선택 사항)|  
|`MODEL_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`MODEL_TYPE`|`DBTYPE_WSTR`|(선택 사항)|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`|(선택 사항)|  
|`MINING_STRUCTURE`|`DBTYPE_WSTR`|(선택 사항)|  
  
 이 행 집합을 쿼리 하는 방법의 예제를 참조 하세요 [마이닝 모델을 만들려면 매개 변수 사용 쿼리](../../data-mining/query-the-parameters-used-to-create-a-mining-model.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 스키마 행 집합](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
