---
title: "DMSCHEMA_MINING_MODEL_CONTENT 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DMSCHEMA_MINING_MODEL_CONTENT
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_MODEL_CONTENT rowset
ms.assetid: 1e85d9e7-3b74-42ac-b94e-f52f76d8a25d
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 23410bac137e67e81e6e7b302f81c5cfd5db8b71
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="dmschemaminingmodelcontent-rowset"></a>DMSCHEMA_MINING_MODEL_CONTENT 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]클라이언트 응용 프로그램을 데이터 마이닝 모델의 내용을 검색할 수 있습니다. 클라이언트 응용 프로그램에서는 이 항목의 마지막에 설명된 특수 트리 작업 제한을 사용하여 마이닝 모델의 내용을 탐색할 수 있습니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DMSCHEMA_MINING_MODEL_CONTENT** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||카탈로그 이름입니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 이 열을 모델이 멤버인 데이터베이스의 이름으로 채웁니다.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||정규화되지 않은 스키마 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **VT_NULL**합니다.|  
|**모델 이름**|**DBTYPE_WSTR**||이 행에서 설명하는 내용이 연결되는 모델의 이름입니다.|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||이 노드에 해당하는 특성의 이름입니다.|  
|**NODE_NAME**|**DBTYPE_WSTR**||노드 이름입니다. 이 열과 동일한 값을 포함 하는 현재 **NODE_UNIQUE_NAME**경우에이 수는 이후 릴리스에서 변경 합니다.|  
|**NODE_UNIQUE_NAME**|**DBTYPE_WSTR**||노드의 고유한 이름입니다.|  
|**NODE_TYPE**|**DBTYPE_I4**||노드의 유형입니다. 다음 값 중 하나를 생성합니다. 타사 데이터 마이닝 알고리즘에서 이 목록을 확장할 수 있습니다.<br /><br /> **DM_NODE_TYPE_CLASSIFICATION_TREE_ROOT** (**2**)<br /><br /> **DM_NODE_TYPE_TREE_INTERIOR** (**3**)<br /><br /> **DM_NODE_TYPE_TREE_DISTRIBUTION** (**4**)<br /><br /> **DM_NODE_TYPE_CLUSTER** (**5**)<br /><br /> **DM_NODE_TYPE_UNKNOWN** (**6**)<br /><br /> **DM_NODE_TYPE_ITEMSET** (**7**)<br /><br /> **DM_NODE_TYPE_ASSOCIATION_RULE** (**8**)<br /><br /> **DM_NODE_TYPE_NB_PREDICTABLE_ATTRIBUTE** (**9**)<br /><br /> **DM_NODE_TYPE_NB_INPUT_ATTRIBUTE** (**10**)<br /><br /> **DM_NODE_TYPE_NB_INPUT_ATTRIBUTE_STATE** (**11**)<br /><br /> **DM_NODE_TYPE_SEQUENCE** (**13**)<br /><br /> **DM_NODE_TYPE_TRANSITION** (**14**)<br /><br /> **DM_NODE_TYPE_TIME_SERIES** (**15**)<br /><br /> **DM_NODE_TYPE_TS_TREE** (**16**)<br /><br /> **DM_NODE_TYPE_NN_SUBNETWORK** (**17**) 신경망, 하위 네트워크<br /><br /> **DM_NODE_TYPE_NN_INPUT_LAYER** (**18**) 신경망, 입력된 계층 (입력 노드의 부모)<br /><br /> **DM_NODE_TYPE_NN_HIDDEN_LAYER** (**19**) 신경망, 숨겨진된 계층 (숨겨진 노드의 부모)<br /><br /> **DM_NODE_TYPE_NN_OUTPUT_LAYER** (**20**) 신경망, 출력 계층 (출력 노드의 부모)<br /><br /> **DM_NODE_TYPE_NN_INPUT_NODE** (**21**) 신경망, 입력된 노드<br /><br /> **DM_NODE_TYPE_NN_HIDDEN_NODE** (**22**) 신경망, 숨겨진된 노드<br /><br /> **DM_NODE_TYPE_NN_OUTPUT_NODE** (**23**) 신경망, 출력 노드<br /><br /> **DM_NODE_TYPE_NN_MARGINAL_STAT_NODE** (**24**) 신경망, 한계 통계 노드<br /><br /> **DM_NODE_TYPE_REGRESSION_TREE_ROOT** (**25**)<br /><br /> **DM_NODE_TYPE_NB_MARGINAL_STAT_NODE** (**26**) 신경망, 한계 통계 노드|  
|**NODE_GUID**|**DBTYPE_GUID**||노드 GUID입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**NODE_CAPTION**|**DBTYPE_WSTR**||노드와 연결된 레이블 또는 캡션입니다. 이 속성은 주로 표시용으로 사용됩니다.|  
|**CHILDREN_CARDINALITY**|**DBTYPE_UI4**||노드에 있는 예상 자식 수입니다.|  
|**PARENT_UNIQUE_NAME**|**DBTYPE_WSTR**||노드 부모의 고유한 이름입니다. **NULL** 에 루트 수준의 모든 노드에 대해 반환 됩니다.|  
|**NODE_DESCRIPTION**|**DBTYPE_WSTR**||노드에 대한 알기 쉬운 설명입니다.|  
|**NODE_RULE**|**DBTYPE_WSTR**||노드에 포함된 규칙에 대한 XML 설명입니다.|  
|**MARGINAL_RULE**|**DBTYPE_WSTR**||부모 노드에서 해당 노드로 이동하는 규칙에 대한 XML 설명입니다.|  
|**NODE_PROBABILITY와**|**DBTYPE_R8**||이 노드와 관련된 확률입니다.|  
|**MARGINAL_PROBABILITY**|**DBTYPE_R8**||부모 노드에서 해당 노드에 도달할 확률입니다.|  
|**NODE_DISTRIBUTION**|**DBTYPE_HCHAPTER**||노드의 확률 히스토그램을 포함하는 테이블입니다.|  
|**NODE_SUPPORT**|**DBTYPE_R8**||이 노드를 지지하는 사례 수입니다.|  
|**MSOLAP_MODEL_COLUMN**|**DBTYPE_WSTR**||이 노드가 관련된 모델 정의 열의 이름입니다.|  
|**MSOLAP_NODE_SCORE**|**DBTYPE_R8**||이 노드에 대해 계산된 점수입니다.|  
|**MSOLAP_NODE_SHORT_CAPTION**|**DBTYPE_WSTR**||읽기 쉽도록 표시용으로 사용할 수 있는 노드의 간단한 캡션입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 **DMSCHEMA_MINING_MODEL_CONTENT** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|(선택 사항)|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|(선택 사항)|  
|**모델 이름**|**DBTYPE_WSTR**|(선택 사항)|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**NODE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**NODE_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**NODE_TYPE**|**DBTYPE_I4**|(선택 사항)|  
|**NODE_GUID**|**DBTYPE_WSTR**|(선택 사항)|  
|**NODE_CAPTION**|**DBTYPE_WSTR**|(선택 사항)|  
|**TREE_OPERATION**|**DBTYPE_UI4**|(선택 사항) 추가적인 주의 사항은 아래를 참조하십시오.|  
  
 제한은 **TREE_OPERATION**의 특정 열에는 **DMSCHEMA_MINING_MODEL_CONTENT** 행 집합 아니라, tree 연산자를 지정 합니다. 소비자를 지정할 수는 **NODE_UNIQUE_NAME** 제한과 tree 연산자 (**상위**, **자식**, **형제**,  **부모**, **하위 항목**, **자체**) 요청 된 멤버 집합을 가져올 수 있습니다. **자체** 연산자 반환 된 행의 목록에서 노드 자체에 대 한 행이 포함 됩니다. 다음 표에서 설명에 대 한 비트맵 정의 구성 하는 상수는 **TREE_OPERATION** 제한 합니다. 논리를 사용 하 여 혼합 **또는** 연산자입니다.  
  
|상수|값|  
|--------------|-----------|  
|**DMTREEOP_ANCESTORS**|**0x00000020**|  
|**DMTREEOP_CHILDREN**|**0x00000001**|  
|**DMTREEOP_SIBLINGS**|**0x00000002**|  
|**DMTREEOP_PARENT**|**0x00000004**|  
|**DMTREEOP_SELF**|**0x00000008**|  
|**DMTREEOP_DESCENDANTS**|**0x00000010**|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 스키마 행 집합](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
