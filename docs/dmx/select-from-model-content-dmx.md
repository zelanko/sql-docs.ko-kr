---
title: "SELECT FROM &lt;모델&gt;합니다. 콘텐츠 (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- FROM
- Content
dev_langs:
- DMX
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- SELECT FROM <model>.CONTENT statement
ms.assetid: a270b33f-77be-41fa-9340-2f6cb0dd75e5
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d4a5f64e297e59d612be82f99e14f89df081be12
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgtcontent-dmx"></a>SELECT FROM &lt;모델&gt;합니다. 콘텐츠 (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 데이터 마이닝 모델의 마이닝 모델 스키마 행 집합을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>인수  
 *n*  
 (선택 사항) 반환할 행의 수를 지정하는 정수입니다.  
  
 *식 목록*  
 Content 스키마 행 집합에서 파생된 열의 쉼표로 구분된 목록입니다.  
  
 *모델*  
 모델 식별자입니다.  
  
 *조건 식*  
 (선택 사항) 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 (선택 사항) 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>주의  
 The **SELECT FROM** *\<model>***. 콘텐츠** 문은 각 알고리즘에 관련 된 내용을 반환 합니다. 예를 들어 사용자 지정 응용 프로그램에서 연결 규칙 모델의 모든 규칙 설명을 사용하려는 경우 사용할 수는 **SELECT FROM \<모델 >. 콘텐츠** 문을 모델의 NODE_RULE 열에 있는 값을 반환 합니다.  
  
 다음 표에서는 마이닝 모델 콘텐츠에 포함된 열을 나열합니다.  
  
> [!NOTE]  
>  알고리즘은 콘텐츠를 올바르게 표시하기 위해 열을 다르게 해석할 수 있습니다. 각 알고리즘 및 해석 하 고 각 모델 유형에 대해 콘텐츠 마이닝 모델을 쿼리 하는 방법에 대 한 팁에 대 한 콘텐츠는 마이닝 모델에 대 한 참조 [마이닝 모델 콘텐츠 &#40; Analysis Services-데이터 마이닝 &#41; ](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
|CONTENT 행 집합 열|Description|  
|---------------------------|-----------------|  
|MODEL_CATALOG|카탈로그 이름입니다. 공급자가 카탈로그를 지원하지 않을 경우 NULL입니다.|  
|MODEL_SCHEMA|정규화되지 않은 스키마 이름입니다. 공급자가 스키마를 지원하지 않을 경우 NULL입니다.|  
|MODEL_NAME|모델 이름입니다. 이 열에는 NULL이 포함될 수 없습니다.|  
|ATTRIBUTE_NAME|노드에 해당하는 특성 이름입니다.|  
|NODE_NAME|노드 이름입니다.|  
|NODE_UNIQUE_NAME|모델 내에서 노드의 고유한 이름입니다.|  
|NODE_TYPE|노드 유형을 나타내는 정수입니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.|  
|NODE_GUID|노드 GUID입니다. GUID가 없는 경우 NULL입니다.|  
|NODE_CAPTION|노드에 연결된 레이블 또는 캡션이며 주로 표시 목적으로 사용됩니다. 캡션이 없는 경우 NODE_NAME이 반환됩니다.|  
|CHILDREN_CARDINALITY|노드에 있는 자식 수입니다.|  
|PARENT_UNIQUE_NAME|노드 부모의 고유한 이름입니다.|  
|NODE_DESCRIPTION|노드에 대한 설명입니다.|  
|NODE_RULE|노드에 포함된 규칙을 나타내는 XML 조각입니다. XML 문자열 형식은 PMML 표준을 기반으로 합니다.|  
|MARGINAL_RULE|부모에서 해당 노드로 이동하는 경로를 설명하는 XML 조각입니다.|  
|NODE_PROBABILITY|해당 노드에서 끝나는 경로의 확률입니다.|  
|MARGINAL_PROBABILITY|부모 노드에서 해당 노드에 도달할 확률입니다.|  
|NODE_DISTRIBUTION|노드의 값 분포를 설명하는 통계가 들어 있는 테이블입니다.|  
|NODE_SUPPORT|이 노드를 지원하는 사례 수입니다.|  
  
## <a name="examples"></a>예  
 다음 코드는 타겟 메일링 마이닝 구조에 추가된 의사 결정 트리 모델에 대한 부모 노드의 ID를 반환합니다.  
  
```  
SELECT MODEL_NAME, NODE_NAME FROM [TM Decision Tree].CONTENT  
WHERE NODE_TYPE = 1  
```  
  
 예상 결과:  
  
|MODEL_NAME|NODE_NAME|  
|-----------------|----------------|  
|TM_DecisionTree|0|  
  
 다음 쿼리에서 **IsDescendant** 함수를 이전 쿼리에서 반환 된 노드의 인접 한 자식을 반환 합니다.  
  
> [!NOTE]  
>  에 대 한 인수로 NODE_ID를 반환 하는 하위 select 문을 사용할 수 없습니다 NODE_NAME의 값은 문자열을는 **IsDescendant** 함수입니다.  
  
```  
SELECT NODE_NAME, NODETYPE, NODE_CAPTION   
FROM [TM Decision Tree].CONTENT  
WHERE ISDESCENDANT('0')  
```  
  
 예상 결과:  
  
 모델이 의사 결정 트리 모델이므로 모델 부모 노드의 하위 항목에는 예측 가능한 특성을 나타내는 한계 통계 노드 하나와 입력 특성 및 값이 들어 있는 여러 노드가 포함되어 있습니다. 자세한 내용은 [의사 결정 트리 모델에 대한 마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="using-the-flattened-keyword"></a>FLATTENED 키워드 사용  
 마이닝 모델 콘텐츠의 중첩 테이블 열에는 모델에 대한 유용한 정보가 들어 있는 경우가 많습니다. FLATTENED 키워드를 사용하면 계층적 행 집합을 지원하는 공급자를 사용하지 않아도 중첩 테이블 열에서 데이터를 검색할 수 있습니다.  
  
 다음 쿼리에서는 Naïve Bayes 모델에서 한계 통계 노드(NODE_TYPE = 26) 하나를 반환합니다. 그러나 이 노드의 NODE_DISTRIBUTION 열에는 중첩 테이블이 들어 있습니다. 따라서 중첩 테이블 열이 평면화되고 중첩 테이블의 모든 행마다 행이 하나씩 반환됩니다. 스칼라 열인 MODEL_NAME의 값은 중첩 테이블의 각 행에서 반복됩니다.  
  
 또한 중첩 테이블 열의 이름만 지정하면 중첩 테이블의 각 열에 대해 새 열이 반환됩니다. 기본적으로 각 중첩 테이블 열의 이름 앞에 중첩 테이블의 이름이 추가됩니다.  
  
```  
SELECT FLATTENED MODEL_NAME, NODE_DISTRIBUTION  
FROM [TM_NaiveBayes].CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 예제 결과:  
  
|MODEL_NAME|NODE_DISTRIBUTION.ATTRIBUTE_NAME|NODE_DISTRIBUTION.ATTRIBUTE_VALUE|NODE_DISTRIBUTION.SUPPORT|NODE_DISTRIBUTION.PROBABILITY|NODE_DISTRIBUTION.VARIANCE|NODE_DISTRIBUTION.VALUETYPE|  
|-----------------|----------------------------------------|-----------------------------------------|--------------------------------|------------------------------------|---------------------------------|----------------------------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|0|1.|  
|TM_NaiveBayes|Bike Buyer|0|6556|0.506685215240745|0||  
|TM_NaiveBayes|Bike Buyer|1.|6383|0.493314784759255|0||  
  
 다음 예에서는 하위 SELECT 문을 사용하여 중첩 테이블에서 일부 열만 반환하는 방법을 보여 줍니다. 이와 같이 중첩 테이블의 이름에 별칭을 지정하면 간단하게 표시할 수 있습니다.  
  
```  
SELECT MODEL_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT] AS t  
FROM NODE_DISTRIBUTION)   
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 예제 결과:  
  
|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|  
|-----------------|-----------------------|------------------------|---------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|  
|TM_NaiveBayes|Bike Buyer|0|6556|  
|TM_NaiveBayes|Bike Buyer|1.|6383|  
  
## <a name="see-also"></a>관련 항목:  
 [SELECT&#40; DMX &#41;](../dmx/select-dmx.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

