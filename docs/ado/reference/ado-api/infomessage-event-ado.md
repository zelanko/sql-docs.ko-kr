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
manager: jroth
ms.openlocfilehash: edc451ae2075a22c106f4e2395836e7d508a7808
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66694790"
---
# <a name="infomessage-event-ado"></a>InfoMessage 이벤트(ADO)
**InfoMessage** 중에 경고가 발생할 때마다 이벤트 라고는 **ConnectionEvent** 작업 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 이 매개 변수는 반환 되는 모든 오류를 포함 합니다. 여러 오류가 반환 되는 경우를 열거 합니다 **오류** 찾아 컬렉션입니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 경고가 발생 하면 *adStatus* 로 설정 된 **adStatusOK** 하며 *pError* 경고를 포함 합니다.  
  
 이 이벤트는 반환 하기 전에이 매개 변수를 설정 **adStatusUnwantedEvent** 후속 알림을 방지 하 합니다.  
  
 *pConnection*  
 A [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 경고가 발생 한 연결입니다. 열면 경고가 발생할 수 있습니다 예를 들어를 **연결** 개체 또는 실행을 [명령](../../../ado/reference/ado-api/command-object-ado.md) 에 **연결**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
