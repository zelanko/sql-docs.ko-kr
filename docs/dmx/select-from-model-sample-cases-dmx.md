---
title: 모델에서 &lt; 선택 &gt; 합니다. SAMPLE_CASES (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9e88ec6673a00e3776032f33390451207c2f399f
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670116"
---
# <a name="select-from-ltmodelgtsample_cases-dmx"></a>모델에서 &lt; 선택 &gt; 합니다. SAMPLE_CASES (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  데이터 마이닝 모델의 학습에 사용되는 사례를 보여 주는 샘플 사례를 반환합니다.  
  
 이 문을 사용하려면 마이닝 모델을 만들 때 드릴스루를 활성화해야 합니다. 드릴스루를 사용 하는 방법에 대 한 자세한 내용은 DMX를 사용 하 여 [마이닝 모델 &#40;만들기&#41;](../dmx/create-mining-model-dmx.md), [&#40;Dmx&#41;](../dmx/select-into-dmx.md)및 [ALTER 마이닝 구조 &#40;dmx&#41;](../dmx/alter-mining-structure-dmx.md)을 참조 하세요.  
  
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
  
 *model*  
 모델 식별자입니다.  
  
 *조건 목록*  
 (선택 사항) 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 (선택 사항) 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>설명  
 샘플 사례가 생성되지만 실제로 학습 데이터에는 없을 수 있습니다. 반환된 사례는 지정된 내용 노드와 관련됩니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]시퀀스 클러스터링 알고리즘은 [!INCLUDE[msCoName](../includes/msconame-md.md)] SELECT FROM model>의 사용을 지 원하는 유일한 알고리즘입니다 \< . SAMPLE_CASES 타사 알고리즘 에서도이를 지원할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Target Mail 마이닝 모델의 학습에 사용되는 샘플 사례를 반환합니다. **Where** 절에서 [IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md) 함수를 사용 하면 ' 000000003 ' 노드와 연결 된 사례만 반환 됩니다. 노드 문자열은 스키마 행 집합의 NODE_UNIQUE_NAME 열에서 찾을 수 있습니다.  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>참고 항목  
 [DMX &#40;선택&#41;](../dmx/select-dmx.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
