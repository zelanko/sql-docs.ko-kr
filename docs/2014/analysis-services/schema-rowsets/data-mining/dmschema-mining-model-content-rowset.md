---
title: DMSCHEMA_MINING_MODEL_CONTENT 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_MODEL_CONTENT
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT rowset
ms.assetid: 1e85d9e7-3b74-42ac-b94e-f52f76d8a25d
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 76724967936008e52cb43f7af02bbb7a833475d0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165454"
---
# <a name="dmschemaminingmodelcontent-rowset"></a>DMSCHEMA_MINING_MODEL_CONTENT 행 집합
  클라이언트 응용 프로그램에서 데이터 마이닝 모델의 내용을 찾아볼 수 있습니다. 클라이언트 응용 프로그램에서는 이 항목의 마지막에 설명된 특수 트리 작업 제한을 사용하여 마이닝 모델의 내용을 탐색할 수 있습니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DMSCHEMA_MINING_MODEL_CONTENT` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||카탈로그 이름입니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 이 열을 모델이 멤버인 데이터베이스의 이름으로 채웁니다.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||정규화되지 않은 스키마 이름입니다. 이 열은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 지원하지 않으므로 항상 `VT_NULL`입니다.|  
|`MODEL_NAME`|`DBTYPE_WSTR`||이 행에서 설명하는 내용이 연결되는 모델의 이름입니다.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||이 노드에 해당하는 특성의 이름입니다.|  
|`NODE_NAME`|`DBTYPE_WSTR`||노드 이름입니다. 현재 이 열은 `NODE_UNIQUE_NAME`과 동일한 값을 포함하지만 이후 릴리스에서 변경될 수 있습니다.|  
|`NODE_UNIQUE_NAME`|`DBTYPE_WSTR`||노드의 고유한 이름입니다.|  
|`NODE_TYPE`|`DBTYPE_I4`||노드의 유형입니다. 다음 값 중 하나를 생성합니다. 타사 데이터 마이닝 알고리즘에서 이 목록을 확장할 수 있습니다.<br /><br /> -   `DM_NODE_TYPE_CLASSIFICATION_TREE_ROOT` (`2`)<br />-   `DM_NODE_TYPE_TREE_INTERIOR` (`3`)<br />-   `DM_NODE_TYPE_TREE_DISTRIBUTION` (`4`)<br />-   `DM_NODE_TYPE_CLUSTER` (`5`)<br />-   `DM_NODE_TYPE_UNKNOWN` (`6`)<br />-   `DM_NODE_TYPE_ITEMSET` (`7`)<br />-   `DM_NODE_TYPE_ASSOCIATION_RULE` (`8`)<br />-   `DM_NODE_TYPE_NB_PREDICTABLE_ATTRIBUTE` (`9`)<br />-   `DM_NODE_TYPE_NB_INPUT_ATTRIBUTE` (`10`)<br />-   `DM_NODE_TYPE_NB_INPUT_ATTRIBUTE_STATE` (`11`)<br />-   `DM_NODE_TYPE_SEQUENCE` (`13`)<br />-   `DM_NODE_TYPE_TRANSITION` (`14`)<br />-   `DM_NODE_TYPE_TIME_SERIES` (`15`)<br />-   `DM_NODE_TYPE_TS_TREE` (`16`)<br />-   `DM_NODE_TYPE_NN_SUBNETWORK` (`17`) 신경망, 하위 네트워크<br />-   `DM_NODE_TYPE_NN_INPUT_LAYER` (`18`) 신경망, 입력된 계층 (입력 노드의 부모)<br />-   **DM_NODE_TYPE_NN_HIDDEN_LAYER** (`19`) 신경망, 숨겨진된 계층 (숨겨진 노드의 부모)<br />-   `DM_NODE_TYPE_NN_OUTPUT_LAYER` (`20`) 신경망, 출력 계층 (출력 노드의 부모)<br />-   `DM_NODE_TYPE_NN_INPUT_NODE` (`21`) 신경망, 입력된 노드<br />-   `DM_NODE_TYPE_NN_HIDDEN_NODE` (`22`) 신경망, 숨겨진된 노드<br />-   `DM_NODE_TYPE_NN_OUTPUT_NODE` (`23`) 신경망, 출력 노드<br />-   `DM_NODE_TYPE_NN_MARGINAL_STAT_NODE` (`24`) 신경망, 한계 통계 노드<br />-   **DM_NODE_TYPE_REGRESSION_TREE_ROOT** (`25`)<br />-   `DM_NODE_TYPE_NB_MARGINAL_STAT_NODE` (`26`) 신경망, 한계 통계 노드|  
|`NODE_GUID`|`DBTYPE_GUID`||노드 GUID입니다. 이 열은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 지원하지 않으므로 항상 `NULL`입니다.|  
|`NODE_CAPTION`|`DBTYPE_WSTR`||노드와 연결된 레이블 또는 캡션입니다. 이 속성은 주로 표시용으로 사용됩니다.|  
|`CHILDREN_CARDINALITY`|`DBTYPE_UI4`||노드에 있는 예상 자식 수입니다.|  
|`PARENT_UNIQUE_NAME`|`DBTYPE_WSTR`||노드 부모의 고유한 이름입니다. 루트 수준의 모든 노드에 대해서 `NULL`이 반환됩니다.|  
|`NODE_DESCRIPTION`|`DBTYPE_WSTR`||노드에 대한 알기 쉬운 설명입니다.|  
|`NODE_RULE`|`DBTYPE_WSTR`||노드에 포함된 규칙에 대한 XML 설명입니다.|  
|`MARGINAL_RULE`|`DBTYPE_WSTR`||부모 노드에서 해당 노드로 이동하는 규칙에 대한 XML 설명입니다.|  
|`NODE_PROBABILITY`|`DBTYPE_R8`||이 노드와 관련된 확률입니다.|  
|`MARGINAL_PROBABILITY`|`DBTYPE_R8`||부모 노드에서 해당 노드에 도달할 확률입니다.|  
|`NODE_DISTRIBUTION`|`DBTYPE_HCHAPTER`||노드의 확률 히스토그램을 포함하는 테이블입니다.|  
|`NODE_SUPPORT`|`DBTYPE_R8`||이 노드를 지지하는 사례 수입니다.|  
|`MSOLAP_MODEL_COLUMN`|`DBTYPE_WSTR`||이 노드가 관련된 모델 정의 열의 이름입니다.|  
|`MSOLAP_NODE_SCORE`|`DBTYPE_R8`||이 노드에 대해 계산된 점수입니다.|  
|`MSOLAP_NODE_SHORT_CAPTION`|`DBTYPE_WSTR`||읽기 쉽도록 표시용으로 사용할 수 있는 노드의 간단한 캡션입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 `DMSCHEMA_MINING_MODEL_CONTENT` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|(선택 사항)|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|(선택 사항)|  
|`MODEL_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`NODE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`NODE_UNIQUE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`NODE_TYPE`|`DBTYPE_I4`|(선택 사항)|  
|`NODE_GUID`|`DBTYPE_WSTR`|(선택 사항)|  
|`NODE_CAPTION`|`DBTYPE_WSTR`|(선택 사항)|  
|`TREE_OPERATION`|`DBTYPE_UI4`|(선택 사항) 추가적인 주의 사항은 아래를 참조하십시오.|  
  
 `TREE_OPERATION` 제한은 `DMSCHEMA_MINING_MODEL_CONTENT` 행 집합의 특정 열에 없으며 Tree 연산자를 지정합니다. 사용자는 `NODE_UNIQUE_NAME` 제한과 Tree 연산자(`ANCESTORS`, `CHILDREN`, `SIBLINGS`, `PARENT`, `DESCENDANTS`, `SELF`)를 지정하여 요청된 멤버 집합을 가져올 수 있습니다. `SELF` 연산자에는 반환된 행 목록에 있는 노드 자체에 대한 행이 포함되어 있습니다. 다음 표는 `TREE_OPERATION` 제한에 대한 비트맵 정의를 구성하는 상수에 대한 설명입니다. 논리 `OR` 연산자를 사용하여 상수를 결합할 수 있습니다.  
  
|상수|값|  
|--------------|-----------|  
|**DMTREEOP_ANCESTORS**|`0x00000020`|  
|**DMTREEOP_CHILDREN**|`0x00000001`|  
|**DMTREEOP_SIBLINGS**|`0x00000002`|  
|**DMTREEOP_PARENT**|`0x00000004`|  
|**DMTREEOP_SELF**|`0x00000008`|  
|**DMTREEOP_DESCENDANTS**|`0x00000010`|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 스키마 행 집합](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
