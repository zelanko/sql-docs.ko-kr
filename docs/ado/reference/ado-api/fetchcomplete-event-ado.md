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
author: rothja
ms.author: jroth
ms.openlocfilehash: 850709dd8b4370360f5c06105266fb2c2510916c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757129"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete 이벤트(ADO)
**Fetchcomplete** 이벤트는 긴 비동기 작업의 모든 레코드를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)으로 검색 한 후에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. **Adstatus** 값이 **adStatusErrorsOccurred**인 경우 발생 하는 오류를 설명 합니다. 그렇지 않으면 설정 되지 않습니다.  
  
 *adStatus*  
 [Eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 이 이벤트가 호출 되 면이 매개 변수는 이벤트를 발생 시킨 작업이 성공한 경우 **Adstatusok** 로 설정 되 고, 작업이 실패 한 경우에는 **adStatusErrorsOccurred** 로 설정 됩니다.  
  
 이 이벤트가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 *pRecordset*  
 **레코드 집합** 개체입니다. 레코드를 검색할 개체입니다.  
  
## <a name="remarks"></a>설명  
 Microsoft Visual Basic에서 **Fetchcomplete** 를 사용 하려면 Visual Basic 6.0 이상이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
