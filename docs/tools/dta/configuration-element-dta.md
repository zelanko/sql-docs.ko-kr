---
title: Configuration 요소(DTA)
description: dta 유틸리티에서 Configuration 요소는 기존 및 가상 물리적 디자인 구조로 구성된 사용자 지정 구성입니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 7f2a4dc5efe06c0490eeeef2d88128808fe34ef0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732157"
---
# <a name="configuration-element-dta"></a>Configuration 요소(DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
|**SpecificationMode**|(선택 사항) 데이터베이스 엔진 튜닝 관리자가 지정된 구성을 현재의 기존 구성과 관련하여 분석해야 하는지 아니면 완전히 새로운 독립 실행형 구성으로 분석해야 하는지 여부를 지정합니다. **string** 데이터 형식을 사용하여 허용된 다음 값 중 하나로 이 특성을 지정할 수 있습니다.<br /><br /> **Relative**:<br />                  튜닝할 데이터베이스에 있는 물리적 디자인 구조(인덱스, 인덱싱된 뷰, 분할)의 현재 기존 구성과 관련하여 지정된 구성을 평가합니다. 다음은 그 예입니다.<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**:<br />                  지정된 구성을 독립 실행형 구성으로 평가합니다. Absolute를 지정한 경우 데이터베이스 엔진 튜닝 관리자는 기존 구성을 고려하지 않습니다. 다음은 그 예입니다.<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각 **DTAInput** 요소에 한 번만 사용할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[DTAInput 요소&#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**자식 요소**|[Configuration의 Server 요소&#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
