---
description: WillConnect 이벤트(ADO)
title: WillConnect 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillConnect
- Connection::WillConnect
helpviewer_keywords:
- WillConnect event [ADO]
ms.assetid: da561d58-eb58-446c-a4fd-1838c76073c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 259ef55060d7968d9ec557c831412ad58609a6df
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987784"
---
# <a name="willconnect-event-ado"></a>WillConnect 이벤트(ADO)
**WillConnect** 이벤트는 연결을 시작 하기 전에 호출 됩니다.  
  
 **적용 대상:** [CONNECTION 개체 (ADO)](./connection-object-ado.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 보류 중인 연결에 대 한 연결 정보를 포함 하는 **문자열** 입니다.  
  
 *UserID*  
 보류 중인 연결에 대 한 사용자 이름을 포함 하는 **문자열** 입니다.  
  
 *암호*  
 보류 중인 연결에 대 한 암호를 포함 하는 **문자열** 입니다.  
  
 *Options*  
 공급자가 *ConnectionString*을 평가 하는 방법을 나타내는 **Long** 값입니다. 유일한 옵션은 **adAsyncOpen**입니다.  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md) 상태 값입니다.  
  
 이 이벤트가 호출 되 면이 매개 변수는 기본적으로 **Adstatusok** 로 설정 됩니다. 이벤트에서 보류 중인 작업의 취소를 요청할 수 없는 경우 **adStatusCantDeny** 로 설정 됩니다.  
  
 이 이벤트가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다. 이 알림을 취소 한 연결 작업을 요청 하려면이 매개 변수를 **Adstatuscancel** 로 설정 합니다.  
  
 *pConnection*  
 이 이벤트 알림이 적용 되는 [연결](./connection-object-ado.md) 개체입니다. **WillConnect** 이벤트 처리기에서 **연결** 의 매개 변수를 변경 해도 **연결**에는 영향을 주지 않습니다.  
  
## <a name="remarks"></a>설명  
 **WillConnect** 가 호출 되 면 *ConnectionString*, *UserID*, *Password*및 *Options* 매개 변수가이 이벤트를 발생 시킨 작업 (보류 중인 연결)에서 설정한 값으로 설정 되 고 이벤트에서 반환 되기 전에 변경 될 수 있습니다. **WillConnect** 는 보류 중인 연결을 취소 하는 요청을 반환할 수 있습니다.  
  
 이 이벤트가 취소 되 면 **adStatusErrorsOccurred**로 설정 된 *adstatus* 매개 변수를 사용 하 여 **connectcomplete** 가 호출 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../guide/data/ado-event-handler-summary.md)