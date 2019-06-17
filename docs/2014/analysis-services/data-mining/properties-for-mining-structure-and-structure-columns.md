---
title: 마이닝 구조 및 구조 열에 대 한 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], column properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- properties [data mining]
ms.assetid: ce90f684-bb8c-4eca-b9e6-000794dbee16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: daa647673653280bfc4cf52398751aedfd65b9c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083056"
---
# <a name="properties-for-mining-structure-and-structure-columns"></a>마이닝 구조 및 구조 열의 속성
  데이터 마이닝 디자이너의 **마이닝 구조** 탭을 사용하여 마이닝 구조 및 마이닝 구조의 관련 열과 중첩 테이블의 속성을 설정하거나 변경할 수 있습니다. 이 탭에서 설정하는 속성은 해당 구조와 연결된 각 마이닝 모델로 전파됩니다.  
  
> [!NOTE]  
>  마이닝 구조에서 속성의 값을 변경하는 경우 이름이나 설명과 같은 메타데이터, 마이닝 구조 및 해당 모델도 다시 처리해야 모델을 보거나 쿼리할 수 있습니다.  
  
## <a name="properties-of-mining-structures-and-mining-structure-columns"></a>마이닝 구조 및 마이닝 구조 열의 속성  
 다음 표에서는 데이터 마이닝과 관련되어 있으며 **마이닝 구조** 탭에서 보거나 구성할 수 있는 마이닝 구조 및 마이닝 구조 열의 속성을 설명합니다. 이러한 속성을 보거나 구성하려면 트리 뷰에서 요소를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
-   구조의 속성을 보려면 마이닝 구조 제목을 클릭합니다.  
  
-   열 또는 중첩 테이블의 속성을 보려면 열 이름을 클릭합니다.  
  
### <a name="properties-of-the-mining-structure"></a>마이닝 구조 속성  
  
|속성|Description|  
|--------------|-----------------|  
|**CacheMode**|학습이 완료된 다음 학습에 사용된 사례를 캐시할지, 아니면 삭제할지를 지정합니다.<br /><br /> 참고: 이 속성으로 설정 되어 있어야 `KeepTrainingCases` 드릴스루 및 홀드 아웃을 사용 하도록 설정 합니다.|  
|**데이터 정렬**|열의 기본 데이터 정렬을 지정합니다. 데이터 정렬을 지정하지 않으면 서버의 데이터 정렬이 사용됩니다.|  
|**설명**|마이닝 구조를 설명합니다. 설명에는 구조에 있는 데이터의 용도와 컴퍼지션을 명시하는 것이 가장 좋습니다.|  
|**ErrorConfiguration(기본값)**|오류(있는 경우)의 특수 처리 옵션을 지정합니다.|  
|**HoldoutMaxCases**|테스트 데이터 집합으로 예약할 수 있는 최대 구조 사례 수를 지정합니다.  **HoldoutMaxCases** 와 **HoldoutPercent**모두에 대한 값을 지정하면 조건이 결합됩니다.<br /><br /> 참고: 이 속성을 설정 하려면 <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> 으로 설정 되어 있어야 `KeepTrainingCases`합니다.|  
|**HoldoutPercent**|테스트 데이터 집합으로 예약할 구조 사례의 비율을 지정합니다. **HoldoutMaxCases** 와 **HoldoutPercent**모두에 대한 값을 지정하면 조건이 결합됩니다.<br /><br /> 참고: 이 속성을 설정 하려면 <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> 으로 설정 되어 있어야 `KeepTrainingCases`합니다.|  
|**HoldoutSeed**|테스트 데이터 집합을 다시 만들 수 있도록 홀드아웃 테스트 집합의 분할을 초기화하는 초기값을 지정합니다.<br /><br /> 참고: 이 속성을 설정 하려면 <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> 으로 설정 되어 있어야 `KeepTrainingCases`합니다.|  
|**ID**|마이닝 구조의 고유 식별자를 표시합니다.<br /><br /> 구조를 만들 때 마이닝 구조에 할당한 이름이 ID로 사용됩니다. `Name` 속성에 대해 새 값을 입력하여 나중에 이름을 변경하면 새 이름이 별칭으로만 사용되며 ID는 변경되지 않습니다.|  
|**언어**|마이닝 구조의 캡션에 대한 언어를 지정합니다.|  
|`Name`|마이닝 구조의 이름이나 별칭을 지정합니다.<br /><br /> Name 속성의 값을 변경하면 새 이름이 캡션이나 별칭으로만 사용되며 마이닝 구조의 식별자는 변경되지 않습니다.|  
|**원본**|데이터 원본의 이름과 유형을 표시합니다.|  
  
### <a name="properties-of-the-mining-structure-columns"></a>마이닝 구조 열 속성  
  
|속성|Description|  
|--------------|-----------------|  
|**ClassifiedColumns**|분류된 열이 설명하는 열을 식별합니다.|  
|**콘텐츠**|열의 내용 유형입니다.|  
|**설명**|열에 대해 설명합니다. 열 설명은 열의 데이터가 데이터 마이닝에 대해 파생되거나 변경된 방식에 대한 정보를 제공하는 것이 가장 좋습니다.|  
|**DiscretizationBucketCount**|불연속화된 열의 버킷 수를 표시합니다.<br /><br /> 내용 유형이 `Discretized`로 설정된 경우에만 사용할 수 있습니다.<br /><br /> 이 속성은 읽기 전용입니다.|  
|**DiscretizationMethod**|열을 불연속화하는 데 사용된 방법을 표시합니다.<br /><br /> 내용 유형이 `Discretized`로 설정된 경우에만 사용할 수 있습니다.<br /><br /> 이 속성은 읽기 전용입니다.|  
|**배포**|열의 내용 분포를 지정합니다.|  
|**ID**|열의 식별자를 표시합니다.<br /><br /> 열의 Name 속성 값을 변경해도 ID 속성 값에는 아무런 영향이 없습니다.|  
|**IsKey**|열이 키 열인지 여부를 나타냅니다.|  
|**KeyColumns**|특정 특성에 대한 키 또는 키의 일부인 열의 정의를 포함합니다.|  
|**ModelingFlags**|알고리즘에서 사용 가능한 추가 매개 변수를 설정합니다.|  
|`Name`|열 이름입니다.|  
|**NameColumn**|부모 요소의 이름을 제공하는 열을 식별합니다.|  
|**원본**|열의 원본을 표시합니다.<br /><br /> 관계형 데이터 원본의 경우 값은 항상 **(없음)** 입니다.<br /><br /> OLAP 큐브를 기반으로 하는 구조의 경우 값은 중첩 테이블의 원본으로 사용되는 조각을 정의하는 MDX 문입니다.|  
|**SourceMeasureGroup**|측정값 그룹의 원본을 표시합니다.<br /><br /> 관계형 데이터 원본의 경우 값은 항상 **(없음)** 입니다.<br /><br /> OLAP 큐브를 기반으로 하는 구조의 경우 값은 중첩 테이블의 원본으로 사용되는 조각을 정의하는 MDX 문입니다.|  
|**형식**|열에 있는 내용의 데이터 형식입니다.|  
  
 속성을 설정하거나 변경하는 방법은 [마이닝 구조 태스크 및 방법](mining-structure-tasks-and-how-tos.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [관계형 마이닝 구조 만들기](create-a-relational-mining-structure.md)   
 [마이닝 구조 열](mining-structure-columns.md)  
  
  
