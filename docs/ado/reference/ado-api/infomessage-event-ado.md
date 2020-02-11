---
title: InfoMessage 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25eef06b7e25538cb874d99af98aee95495b95ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932339"
---
# <a name="infomessage-event-ado"></a>InfoMessage 이벤트(ADO)
**InfoMessage** 이벤트는 **connectionevent** 작업 중에 경고가 발생할 때마다 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 이 매개 변수는 반환 되는 모든 오류를 포함 합니다. 여러 오류가 반환 되는 경우 **오류** 컬렉션을 열거 하 여 찾습니다.  
  
 *adStatus*  
 [Eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 경고가 발생 하는 경우 *Adstatus* 는 **adstatusok** 로 설정 되 고 *pError* 에는 경고가 포함 됩니다.  
  
 이 이벤트가 반환 되기 전에이 매개 변수를 **adStatusUnwantedEvent** 로 설정 하 여 후속 알림이 발생 하지 않도록 합니다.  
  
 *pConnection*  
 [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 경고가 발생 한 연결입니다. 예를 들어 **연결 개체를** 열거나 **연결**에서 [명령을](../../../ado/reference/ado-api/command-object-ado.md) 실행할 때 경고가 발생할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
