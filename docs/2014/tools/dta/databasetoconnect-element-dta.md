---
title: DatabaseToConnect 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a29e28782207d5da0e3166669c6c38a7119f597
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161594"
---
# <a name="databasetoconnect-element-dta"></a>DatabaseToConnect 요소(DTA)
  작업 튜닝 시 데이터베이스 엔진 튜닝 관리자가 연결되는 첫 번째 데이터베이스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|`string`길이 제한 없음된.|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각각에 대 한 번만 사용할 수 있습니다 `TuningOptions` 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소 &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**자식 요소**|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 사용 하 여 `DatabaseToConnect` 데이터베이스 엔진 튜닝 관리자가 튜닝 세션을 시작할 때 연결 하려는 첫 번째 데이터베이스의 이름을 지정 합니다. 이 요소에서는 데이터베이스를 하나만 지정할 수 있습니다. 여러 데이터베이스 이름을 지정할 경우 데이터베이스 엔진 튜닝 관리자는 오류를 반환합니다.  
  
## <a name="example"></a>예제  
 사용 예제를 보려면 [인라인 워크로드가 포함된 XML 입력 파일 예제&#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
