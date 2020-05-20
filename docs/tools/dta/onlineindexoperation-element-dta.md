---
title: OnlineIndexOperation 요소(DTA)
description: dta 유틸리티에서 OnlineIndexOperation 요소는 데이터베이스 엔진 튜닝 관리자에서 추천되는 항목을 온라인으로 만들 수 있는지 여부를 지정합니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- OnlineIndexOperation element
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 2718b5b697fcbf8371d80203aa1d8e51386c1f9b
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151846"
---
# <a name="onlineindexoperation-element-dta"></a>OnlineIndexOperation 요소(DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

데이터베이스 엔진 튜닝 관리자가 권장하는 인덱스, 인덱싱된 뷰 또는 파티션을 온라인으로 만들 수 있는지 여부를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 최대 길이 없음|  
|**허용된 값**|**OFF**<br /> 권장되는 물리적 디자인 구조를 온라인으로 만들 수 없습니다.<br /><br /> **ON**<br /> 권장되는 모든 물리적 디자인 구조를 온라인으로 만들 수 있습니다.<br /><br /> **MIXED**<br /> 데이터베이스 엔진 튜닝 관리자는 가능한 경우 온라인으로 만들 수 있는 물리적 디자인 구조를 제안합니다.<br /><br /> 이 요소에 이러한 값 중 하나를 사용합니다. 인덱스를 온라인으로 만들 경우 **ONLINE = ON** 키워드가 개체 정의에 추가됩니다.|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 사용할 경우 **TuningOptions** 요소에 한 번만 사용할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소&#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예제를 보려면 [단순 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
