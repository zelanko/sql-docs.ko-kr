---
title: SELECT FROM &lt;모델&gt;합니다. (DMX)의 경우 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f65aa4dc64e795235286eccd9f3283216ba6f4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62658774"
---
# <a name="select-from-ltmodelgtcases-dmx"></a>SELECT FROM &lt;모델&gt;합니다. 사례 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  드릴스루를 지원하며 모델 학습에 사용된 사례를 반환합니다. 또한 마이닝 구조와 마이닝 모델 모두에 드릴스루가 사용되도록 설정되어 있고 적절한 권한이 있으면 마이닝 모델에 포함되지 않은 구조 열도 반환할 수 있습니다.  
  
 마이닝 모델에 드릴스루가 사용되도록 설정되지 않은 경우에는 문이 실패합니다.  
  
> [!NOTE]  
>  DMX(Data Mining Extensions)에서는 모델을 만들 때만 드릴스루를 사용할 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 사용하여 기존 모델에 드릴스루를 추가할 수 있지만 사례를 보거나 쿼리하려면 먼저 모델을 다시 처리해야 합니다.  
  
 드릴스루를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [CREATE MINING MODEL &#40;DMX&#41;](../dmx/create-mining-model-dmx.md)하십시오 [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md), 및 [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>인수  
 *n*  
 (선택 사항) 반환할 행의 수를 지정하는 정수입니다.  
  
 *expression list*  
 쉼표로 구분된 식 목록입니다. 식은 열 식별자, UDF(사용자 정의 함수), VBA 함수 등을 포함할 수 있습니다.  
  
 마이닝 모델에 포함되지 않은 구조 열을 포함하려면 `StructureColumn('<structure column name>')` 함수를 사용합니다.  
  
 *model*  
 모델 식별자입니다.  
  
 *조건 식*  
 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 (선택 사항) 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>Remarks  
 마이닝 모델과 마이닝 구조 모두에 드릴스루가 사용되도록 설정되어 있으면 모델과 구조에 대해 드릴스루 권한을 가지는 역할의 멤버인 사용자는 마이닝 모델에 포함되지 않은 마이닝 구조 열에 액세스할 수 있습니다. 따라서 중요 한 데이터 나 개인 정보를 보호 하려면 구성 않아야 개인 정보를 마스킹 권한을 부여 하 여 데이터 원본 뷰 **AllowDrillthrough** 반드시 필요한 경우에 마이닝 구조에 대 한 권한이 있습니다.  
  
 합니다 [지연 &#40;DMX&#41; ](../dmx/lag-dmx.md) 함수를 반환 하거나 각 사례와 초기 시간 사이의 지연 시간에 필터링 할 시계열 모델과 함께 사용할 수 있습니다.  
  
 사용 하는 [IsInNode &#40;DMX&#41; ](../dmx/isinnode-dmx.md) 함수를 **여기서** 절에 스키마 행 집합의 NODE_UNIQUE_NAME 열에 지정 된 노드와 관련 된 사례만 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 마이닝 구조에 기반한 기반으로 하는 타겟 메일링을 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]데이터베이스와 연결된 된 마이닝 모델. 자세한 내용은 [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)합니다.  
  
### <a name="example-1-drillthrough-to-model-cases-and-structure-columns"></a>예 1: 모델 사례 및 구조 열으로 드릴스루  
 다음 예에서는 대상 메일 모델을 테스트하는 데 사용된 모든 사례에 대해 열을 반환합니다. 모델이 작성되는 마이닝 구조에 홀드아웃 테스트 데이터 집합이 없으면 이 쿼리는 0개의 사례를 반환합니다. 식 목록을 사용하여 필요한 열만 반환할 수 있습니다.  
  
```  
SELECT * FROM [TM Decision Tree].Cases  
WHERE IsTestCase();  
```  
  
### <a name="example-2-drillthrough-to-training-cases-in-a-specific-node"></a>예 2: 특정 노드의 학습 사례로 드릴스루  
 다음 예에서는 Cluster 2를 학습하는 데 사용된 사례만 반환합니다. Cluster 2에 대한 노드의 NODE_UNIQUE_NAME 열 값은 '002'입니다. 이 예에서는 또한 마이닝 모델에 포함되지 않은 [Customer Key]라는 구조 열 하나를 반환하고 이 열에 `CustomerID`라는 별칭을 제공합니다. 구조 열의 이름은 문자열 값으로 전달되므로 대괄호가 아니라 따옴표로 묶어야 합니다.  
  
```  
SELECT StructureColumn('Customer Key') AS CustomerID, *   
FROM [TM_Clustering].Cases  
WHERE IsTrainingCase()  
AND IsInNode('002')  
```  
  
 구조 열을 반환하려면 마이닝 모델과 마이닝 구조 모두에 드릴스루 권한이 설정되어 있어야 합니다.  
  
> [!NOTE]  
>  모든 마이닝 모델 유형이 드릴스루를 지원하지는 않습니다. 드릴스루를 지 원하는 모델에 대 한 자세한 내용은 [드릴스루 쿼리 &#40;데이터 마이닝&#41;](../analysis-services/data-mining/drillthrough-queries-data-mining.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [선택 &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
