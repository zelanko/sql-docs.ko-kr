---
title: WillConnect 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22d30e389c61a66d417ad5baec99a8834a754047
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644791"
---
# <a name="willconnect-event-ado"></a>WillConnect 이벤트(ADO)
합니다 **WillConnect** 이벤트는 연결을 시작 하기 전에 호출 됩니다.  
  
 **적용 대상:** [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
WillConnect ConnectionString, UserID, Password, Options, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 A **문자열** 보류 중인 연결에 대 한 연결 정보를 포함 하는 합니다.  
  
 *UserID*  
 A **문자열** 보류 중인 연결에 대 한 사용자 이름을 포함 하는 합니다.  
  
 *암호*  
 A **문자열** 보류 중인 연결에 대 한 암호를 포함 하는 합니다.  
  
 *옵션*  
 A **긴** 공급자를 평가 해야 하는 방법을 나타내는 값을 *ConnectionString*합니다. 유일한 방법은 **adAsyncOpen**합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 이 매개 변수를로이 이벤트를 호출 하면 **adStatusOK** 기본적으로 합니다. 로 설정 되어 **adStatusCantDeny** 경우 이벤트는 보류 중인 작업의 취소를 요청할 수 없습니다.  
  
 이 이벤트는 반환 하기 전에이 매개 변수를 설정 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다. 이 매개 변수를 설정 **adStatusCancel** 이 알림의 취소를 발생 시킨 연결 작업을 요청 합니다.  
  
 *pConnection*  
 합니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 이 이벤트 알림이 적용 되는 개체입니다. 매개 변수를 변경 합니다 **연결** 여는 **WillConnect** 이벤트 처리기 영향을 주지 것입니다를 **연결**.  
  
## <a name="remarks"></a>Remarks  
 때 **WillConnect** 호출 되는 *ConnectionString*를 *UserID*를 *암호*, 및 *옵션* 매개 변수 (보류 중 연결)이이 이벤트를 발생 시킨 이벤트를 반환 하기 전에 변경할 수 있습니다 하는 작업에 의해 설정 된 값으로 설정 됩니다. **WillConnect** 보류 중인 연결을 취소 함을 요청을 반환 합니다.  
  
 이 이벤트를 취소 **ConnectComplete** 호출 하는 데 해당 *adStatus* 매개 변수 설정 **adStatusErrorsOccurred**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
