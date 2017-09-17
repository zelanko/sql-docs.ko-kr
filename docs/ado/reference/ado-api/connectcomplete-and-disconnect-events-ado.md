---
title: "ConnectComplete와 연결 끊기 이벤트 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Disconnect
- Connection::ConnectComplete
- ConnectComplete
- Connection::Disconnect
helpviewer_keywords:
- Disconnect event [ADO]
- ConnectComplete event [ADO]
ms.assetid: 568f5252-d069-4d99-a01b-2ada87ad1304
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ebd4363f166a67a6e48fee41c2585b68de93bc98
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete 연결 끊기 이벤트 (ADO) 및
**ConnectComplete** 이벤트 연결이 시작 된 후 호출 됩니다. **연결 끊기** 이벤트 연결이 종료 된 후 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류를 설명 하는 것의 값 *adStatus* 은 **adStatusErrorsOccurred**; 설정 되지 않은 그렇지 않은 경우.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 값은 반환은 항상 **adStatusOK**합니다.  
  
 때 **ConnectComplete** 은 호출,이 매개 변수 설정 **adStatusCancel** 경우는 **WillConnect** 이벤트에서 보류 중인 연결의 취소를 요청 합니다.  
  
 이 이벤트 중 하나를 반환 하기 전에이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다. 그러나 닫고 다시 열어는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 하면 이러한 이벤트를 다시 발생 합니다.  
  
 *pConnection*  
 **연결** 이 이벤트에 적용 되는 개체입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
