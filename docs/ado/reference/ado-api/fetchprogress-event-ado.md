---
description: FetchProgress 및(ADO)
title: FetchProgress 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
author: rothja
ms.author: jroth
ms.openlocfilehash: b84b963f42c83191c613dbb4849288fc862df474
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973334"
---
# <a name="fetchprogress-event-ado"></a>FetchProgress 및(ADO)
**Fetchprogress**이벤트는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)으로 현재 검색 된 행의 수를 보고 하는 긴 비동기 작업 중에 주기적으로 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *진행률*  
 인출 작업에서 현재 검색 된 레코드 수를 나타내는 **Long** 값입니다.  
  
 *MaxProgress*  
 검색할 것으로 예상 되는 최대 레코드 수를 나타내는 **Long** 값입니다.  
  
 *adStatus*  
 [Eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 *pRecordset*  
 레코드를 검색 중인 개체인 **레코드 집합** 개체입니다.  
  
## <a name="remarks"></a>설명  
 행 **레코드 집합과**함께 **fetchprogress** 를 사용 하는 경우 *진행률* 및 *Maxprogress* 매개 변수 값은 기본 [커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 행 집합에서 파생 됩니다. 반환 된 값은 현재 챕터의 레코드 수 뿐만 아니라 기본 행 집합의 총 레코드 수를 나타냅니다.  
  
> [!NOTE]
>  Microsoft Visual Basic에서 **Fetchprogress** 를 사용 하려면 Visual Basic 6.0 이상이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
