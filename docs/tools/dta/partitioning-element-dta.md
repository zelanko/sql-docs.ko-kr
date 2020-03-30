---
title: Partitioning 요소(DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Partitioning element
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 092a652783f5ccaa16e52fe915820a009e4fc274
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75306122"
---
# <a name="partitioning-element-dta"></a>Partitioning 요소(DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

분석 도중에 데이터베이스 엔진 튜닝 관리자에서 사용하도록 파티션 구성표를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <Partitioning>...</Partitioning>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 최대 길이 없음|  
|**허용된 값**|**NONE**<br /> 분할 안 함<br /><br /> **FULL**<br /> 전체 분할 (성능 향상 중심)<br /><br /> **ALIGNED**<br /> 정렬된 분할만 (관리 효율성 중심)<br /><br /> 이 요소에 이러한 값 중 하나만 사용합니다.<br /><br /> **ALIGNED** 는 데이터베이스 엔진 튜닝 관리자가 생성한 권장 구성에서 모든 제안된 인덱스는 인덱스가 정의된 기본 테이블과 동일한 방식으로 분할된다는 것을 의미합니다. 인덱싱된 뷰의 비클러스터형 인덱스는 인덱싱된 뷰에 정렬됩니다.|  
|**기본값**|**NONE**|  
|**발생 빈도**|**TuningOptions** 요소를 사용하지 않을 경우 **DropOnlyMode** 요소에 한 번만 지정해야 합니다. **DropOnlyMode** 를 사용하는 경우 **Partitioning**는 사용할 수 없습니다. 이러한 요소는 함께 사용할 수 없습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소&#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예제를 보려면 [단순 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
