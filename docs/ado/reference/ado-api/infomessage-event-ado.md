---
title: InfoMessage 이벤트 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6cce906c08e524c3a709c573394a72df89eac8e
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35279192"
---
# <a name="infomessage-event-ado"></a>InfoMessage 이벤트 (ADO)
**InfoMessage** 이벤트 중에 경고가 발생할 때마다 호출 됩니다는 **ConnectionEvent** 작업 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pError*  
 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다. 이 매개 변수에 반환 되는 모든 오류를 포함 합니다. 여러 개의 오류가 반환 되는 경우이 열거는 **오류** 를 기다리며 컬렉션입니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다. 경고가 발생 하면 *adStatus* 로 설정 된 **adStatusOK** 및 *pError* 는 경고를 포함 합니다.  
  
 이 이벤트를 반환 하기 전에이 매개 변수를 설정 **adStatusUnwantedEvent** 알림 메시지가 방지 하기 위해 합니다.  
  
 *pConnection*  
 A [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 경고가 발생 한 연결입니다. 경고를 열 때 발생할 수 있습니다는 예를 들어는 **연결** 개체 또는 실행 한 [명령](../../../ado/reference/ado-api/command-object-ado.md) 에 **연결**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
