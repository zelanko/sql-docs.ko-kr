---
title: WillConnect 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49afc55924b0c1a00c153932f4992a0b603cd1b4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="willconnect-event-ado"></a>WillConnect 이벤트 (ADO)
**WillConnect** 이벤트 연결을 시작 하기 전에 호출 됩니다.  
  
 **적용 대상:** [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 A **문자열** 보류 중인 연결에 대 한 연결 정보가 들어 있는입니다.  
  
 *UserID*  
 A **문자열** 보류 중인 연결에 대 한 사용자 이름이 들어 있는입니다.  
  
 *암호*  
 A **문자열** 보류 중인 연결에 대 한 암호를 포함 하 합니다.  
  
 *옵션*  
 A **긴** 공급자를 평가 하는 방식을 나타내는 값의 *ConnectionString*합니다. 유일한 방법은 **adAsyncOpen**합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 이 이벤트를 호출할 때이로 설정 된 **adStatusOK** 기본적으로 합니다. 로 설정 된 **adStatusCantDeny** 경우이 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 이 이벤트를 반환 하기 전에이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다. 이 매개 변수를 설정 **adStatusCancel** 이 알림의 취소를 발생 시킨 연결 작업을 요청할 수 있습니다.  
  
 *pConnection*  
 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 이 이벤트 알림이 적용 되는 개체입니다. 매개 변수를 변경는 **연결** 여는 **WillConnect** 이벤트 처리기 영향을 미치지 것입니다는 **연결**합니다.  
  
## <a name="remarks"></a>주의  
 때 **WillConnect** 호출 되는 *ConnectionString*, *UserID*, *암호*, 및 *옵션* 매개 변수 (보류 중 연결)이이 이벤트를 발생 한 이벤트를 반환 하기 전에 변경할 수는 작업에 의해 설정 된 값으로 설정 됩니다. **WillConnect** 보류 중인 연결을 취소할 수는 요청을 반환 합니다.  
  
 이 이벤트가 취소 되 면 **ConnectComplete** 호출 됩니다는 *adStatus* 매개 변수 설정 **adStatusErrorsOccurred**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
