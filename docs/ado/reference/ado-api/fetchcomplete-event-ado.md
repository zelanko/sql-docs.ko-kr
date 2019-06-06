---
title: FetchComplete 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7b5fb32f567dcfffb6112e843b53cb99a3b106bc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697894"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete 이벤트(ADO)
**FetchComplete** 긴 비동기 작업의 모든 레코드에 검색 된 후 이벤트 라고 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>구문  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류에 설명 합니다 값 **adStatus** 됩니다 **adStatusErrorsOccurred**; 설정 되지 않은 고, 그렇지 합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 이 매개 변수를로이 이벤트를 호출 하면 **adStatusOK** 이벤트를 발생 시킨 작업에 성공, 또는 **adStatusErrorsOccurred** 작업이 실패 합니다.  
  
 이 이벤트는 반환 하기 전에이 매개 변수를 설정 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다.  
  
 *pRecordset*  
 A **레코드 집합** 개체입니다. 검색 된 레코드는 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하도록 **FetchComplete** with Microsoft Visual Basic, Visual Basic 6.0 이상가 필요 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
