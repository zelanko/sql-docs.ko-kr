---
title: "SELECT FROM &lt;모델&gt;합니다. SAMPLE_CASES (DMX) | Microsoft Docs"
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
- SAMPLE_CASES
- SELECT
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- SELECT FROM <model>.SAMPLE_CASES statement
- mining models [Analysis Services], sample cases
- sample cases [DMX]
- training mining models
ms.assetid: e7a34b9b-3562-4503-bfa7-dd9b12db480a
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3c1e90c2d4fd6b7dab565550bc4b08a4a33192ee
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgtsamplecases-dmx"></a>SELECT FROM &lt;모델&gt;합니다. SAMPLE_CASES (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터 마이닝 모델의 학습에 사용되는 사례를 보여 주는 샘플 사례를 반환합니다.  
  
 이 문을 사용하려면 마이닝 모델을 만들 때 드릴스루를 활성화해야 합니다. 드릴스루를 사용 하는 방법에 대 한 자세한 내용은 참조 [CREATE MINING MODEL &#40; DMX &#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md), 및 [ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.SAMPLE_CASES  
[WHERE <condition list>] ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>인수  
 *n*  
 (선택 사항) 반환할 행의 수를 지정하는 정수입니다.  
  
 *식 목록*  
 쉼표로 구분된 관련 열 식별자 목록입니다.  
  
 *모델*  
 모델 식별자입니다.  
  
 *조건 목록*  
 (선택 사항) 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 (선택 사항) 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>주의  
 샘플 사례가 생성되지만 실제로 학습 데이터에는 없을 수 있습니다. 반환된 사례는 지정된 내용 노드와 관련됩니다.  
  
 하지만 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘은 유일한 [!INCLUDE[msCoName](../includes/msconame-md.md)] SELECT FROM 사용을 지 원하는 알고리즘 \<모델 >. SAMPLE_CASES, 타사 알고리즘 수 지원할 수도 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Target Mail 마이닝 모델의 학습에 사용되는 샘플 사례를 반환합니다. 사용 하는 [IsInNode &#40; DMX &#41;](../dmx/isinnode-dmx.md) 함수는 **여기서** 절 '000000003' 노드와 관련 된 사례만 반환 합니다. 노드 문자열은 스키마 행 집합의 NODE_UNIQUE_NAME 열에서 찾을 수 있습니다.  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SELECT&#40; DMX &#41;](../dmx/select-dmx.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

