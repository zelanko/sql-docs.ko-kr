---
description: ConnectComplete 및 Disconnect 이벤트(ADO)
title: ConnectComplete 및 Disconnect 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: rothja
ms.author: jroth
ms.openlocfilehash: db04bbeed12f9097768763024270ece7275d5c3e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444545"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete 및 Disconnect 이벤트(ADO)
**Connectcomplete** 이벤트는 연결이 시작 된 후에 호출 됩니다. 연결 **끊기** 이벤트는 연결이 종료 된 후에 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. *Adstatus* 값이 **adStatusErrorsOccurred**인 경우 발생 하는 오류를 설명 합니다. 그렇지 않으면 설정 되지 않습니다.  
  
 *adStatus*  
 항상 **Adstatusok**를 반환 하는 [eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md) 값입니다.  
  
 **Connectcomplete** 가 호출 되 면이 매개 변수는 **WillConnect** 이벤트에서 보류 중인 연결 취소가 요청 된 경우 **adstatuscancel** 로 설정 됩니다.  
  
 두 이벤트를 반환 하기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다. 그러나 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 을 닫았다가 다시 열면 이러한 이벤트가 다시 발생 합니다.  
  
 *pConnection*  
 이 이벤트가 적용 되는 **연결** 개체입니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
