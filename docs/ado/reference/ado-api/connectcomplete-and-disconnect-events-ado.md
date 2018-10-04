---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1466b8f718318d8224ec2c7dcf3e873139fffed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752771"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>ConnectComplete 및 Disconnect 이벤트(ADO)
합니다 **ConnectComplete** 이벤트 연결이 시작 된 후 호출 됩니다. 합니다 **연결 끊기** 이벤트 연결이 종료 된 후 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 경우에 발생 한 오류에 설명 합니다 값 *adStatus* 됩니다 **adStatusErrorsOccurred**; 설정 되지 않은 고, 그렇지 합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 반환 값 항상 **adStatusOK**합니다.  
  
 때 **ConnectComplete** 가 호출이 매개 변수 설정 **adStatusCancel** 경우는 **WillConnect** 이벤트에서 보류 중인 연결의 취소를 요청 합니다.  
  
 이 매개 변수를 설정 하거나 이벤트가 반환 되기 전에 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다. 그러나 닫았다가 합니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 하면 이러한 이벤트 다시 발생 합니다.  
  
 *pConnection*  
 합니다 **연결** 이 이벤트에 적용 되는 개체입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
