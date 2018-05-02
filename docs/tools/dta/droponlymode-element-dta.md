---
title: DropOnlyMode 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- DropOnlyMode element
ms.assetid: 80960676-7581-4074-889b-80ee665963dd
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 251034d3df259b718056d6bde779bb1b4aad3d59
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="droponlymode-element-dta"></a>DropOnlyMode 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  데이터베이스 엔진 튜닝 관리자가 튜닝 세션 동안에 기존 인덱스, 인덱싱된 뷰 또는 파티션을 삭제하는 것만 고려해야 하도록 지정합니다. 이 튜닝 옵션을 지정하면 새 물리적인 디자인 구조는 고려되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <DropOnlyMode>...</DropOnlyMode>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
 **데이터 형식 및 길이**  
  
 **기본값**  
  
 **발생 빈도**: 선택 사항입니다. 각 **TuningOptions** 요소에 한 번만 사용할 수 있습니다. **TuningOptions** 요소에 다음 요소를 지정한 경우 사용할 수 없습니다.  
  
-   [FeatureSet 요소&#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning 요소&#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [KeepExisting 요소&#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md)는 **ALL**로 설정됨  
  
## <a name="element-relationships"></a>요소 관계  
 **부모 요소**: [TuningOptions 요소&#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
 **자식 요소**  
  
## <a name="example"></a>예제  
 다음 예에서는 **TuningOptions** 가 지정된 데이터베이스 엔진 튜닝 관리자 XML 입력 파일의 **DropOnlyMode** 섹션을 보여 줍니다. 이 예에서 튜닝 시간은 24시간(1440분)으로 제한되며 기존의 모든 클러스터형 인덱스 및 비클러스터형 인덱스는 삭제 처리됩니다.  
  
```xml  
<TuningOptions  
  <TuningTimeInMin>1440</Name>  
  <KeepExisting>ALIGNED</KeepExisting>  
  <DropOnlyMode />  
</TuningOptions>  
```  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
