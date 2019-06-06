---
title: ADO 이벤트 처리 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 162cac52920b076e4388a74a251cd347137f49cd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702014"
---
# <a name="handling-ado-events"></a>ADO 이벤트 처리
ADO 이벤트 모델을 실행 하는 특정 동기 및 비동기 ADO 작업을 지원 *이벤트*, 또는 알림을 작업이 시작 되기 전에 또는 완료 된 후 발생 합니다. 이벤트는 실제로 응용 프로그램에서 정의 하는 이벤트 처리기 루틴을 호출 합니다.  
  
 그룹 작업을 시작 하기 전에 발생 하는 이벤트의 처리기 함수 또는 프로시저를 제공 하는 경우에 검사 수도 있고 작업에 전달 된 매개 변수를 수정할 수 있습니다. 아직 실행 되지 하에, 때문에 작업을 취소 하거나 완료 되도록 허용 합니다.  
  
 작업이 완료 된 후 발생 하는 이벤트는 비동기적으로 ADO를 사용 하는 경우에 특히 중요 합니다. 비동기 시작 하는 응용 프로그램 예를 들어 [Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 되 면 작업 실행 완료 이벤트에서 작업에 알립니다.  
  
 ADO 이벤트 모델을 사용 하 여 응용 프로그램에 약간의 오버 헤드를 추가 하지만 모니터링과 같은 비동기 작업을 처리 하는 다른 방법 보다 훨씬 더 많은 유연성을 제공 합니다 [상태](../../../ado/reference/ado-api/state-property-ado.md) 루프를 사용 하 여 개체의 속성입니다.  
  
> [!NOTE]
>  이벤트를 처리 하려면 ADO는 메시지 펌프가 또는 단일 스레드 아파트 (STA) 모델에서 사용할 수 있어야 합니다. ADO 이벤트 숨겨진된 창을 만들어 내부적으로 처리 됩니다. ADO는 이벤트를 발생 해야 하는 경우이 창에 메시지를 게시 합니다. 호출한 스레드는 이벤트는 전송 되도록 하려면 이렇게 **IConnectionPoint::Advise** 연결 지점에 있습니다. 이 아키텍처는 알림을 받아야 하는 스레드 창 메시지를 펌프 하지 않는 경우 문제가 발생할 수 있습니다. 잠재적인 문제에는 스레드 및 전역 창 브로드캐스트 제한 시간 초과 가능한 경우 숨겨진된 windows 메시지 처리 안 함 때문에 전체 시스템 속도 저하에 배달 되지 않는 ADO 이벤트가 포함 됩니다. STA 스레드는 일반적으로이 문제는 없습니다 표출 STA 스레드에서 실행 하는 메시지 펌프를 가집니다. 그러나 MTA 스레드 일반적으로 없으므로 메시지 펌프 문제는 일반적으로 표출 MTA 스레드에서 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [이벤트 유형](../../../ado/guide/data/types-of-events.md)  
  
-   [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)  
  
-   [이벤트 처리기가 함께 작동하는 방법](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [언어별 ADO 이벤트 인스턴스](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO 이벤트](../../../ado/reference/ado-api/ado-events.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 유형](../../../ado/guide/data/types-of-events.md)
