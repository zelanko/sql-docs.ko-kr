---
title: 구성 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 934acda419b734f577de4c8127184d3dd18ea650
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150143"
---
# <a name="configuration-element-dta"></a>Configuration 요소(DTA)
  작업 튜닝 시에 데이터베이스 엔진 튜닝 관리자가 분석할 기존 및 가상 물리적 디자인 구조로 구성된 사용자 지정 구성입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
    <Server>...</Server>  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions  
    <Configuration [SpecificationMode="Relative" | "Absolute"]>  
    ...code removed here...  
    </Configuration>  
</DTAInput>  
```  
  
## <a name="element-attributes"></a>요소 특성  
  
|Configuration 특성|Description|  
|-----------------------------|-----------------|  
|`SpecificationMode`|(선택 사항) 데이터베이스 엔진 튜닝 관리자가 지정된 구성을 현재의 기존 구성과 관련하여 분석해야 하는지 아니면 완전히 새로운 독립 실행형 구성으로 분석해야 하는지 여부를 지정합니다. **string** 데이터 형식을 사용하여 허용된 다음 값 중 하나로 이 특성을 지정할 수 있습니다.<br /><br /> `Relative`: <br />                  튜닝할 데이터베이스에 있는 물리적 디자인 구조(인덱스, 인덱싱된 뷰, 분할)의 현재 기존 구성과 관련하여 지정된 구성을 평가합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다. <br />`<Configuration SpecificationMode="Relative">`<br /><br /> `Absolute`: <br />                  지정된 구성을 독립 실행형 구성으로 평가합니다. Absolute를 지정한 경우 데이터베이스 엔진 튜닝 관리자는 기존 구성을 고려하지 않습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.<br />`<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각 `DTAInput` 요소에 한 번만 사용할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[DTAInput 요소&#40;DTA&#41;](dtainput-element-dta.md)|  
|**자식 요소**|[Configuration의 Server 요소&#40;DTA&#41;](server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
