---
title: "ADO 이벤트 처리 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a451023d3e3501ac60cd2724349337f30c46b689
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="handling-ado-events"></a>ADO 이벤트 처리
ADO 이벤트 모델 지원 발급 하는 특정 동기 및 비동기 ADO 작업 *이벤트*, 또는 알림을 작업이 시작 되기 전에 또는 완료 된 후 발생 합니다. 이벤트는 실제로 응용 프로그램에서 정의 하는 이벤트 처리기 루틴에 전화 합니다.  
  
 작업이 시작 되기 전에 발생 하는 이벤트 그룹에 대 한 처리기 함수 또는 프로시저를 제공 하는 경우를 검사 하거나 작업에 전달 된 매개 변수를 수정할 수 있습니다. 아직 실행 되지 것 않았습니다, 때문에 작업을 취소 하거나 완료 되도록 합니다.  
  
 작업이 완료 된 후 발생 하는 이벤트는 비동기적으로 ADO를 사용 하는 경우에 특히 중요 합니다. 예를 들어 하는 응용 프로그램 시작 비동기 [Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 작업은 작업이 면 실행 완료 이벤트에 의해 알림이 전송 됩니다.  
  
 응용 프로그램에 약간의 오버 헤드를 추가 하지만 모니터링 같은 비동기 작업을 처리 하는 다른 방법 보다 훨씬 더 많은 유연성을 제공 ADO 이벤트 모델을 사용 하는 [상태](../../../ado/reference/ado-api/state-property-ado.md) 루프가 있는 개체의 속성입니다.  
  
> [!NOTE]
>  이벤트를 처리 하려면 ADO는 메시지 펌프가 또는 단일 스레드 아파트 (STA) 모델에서 사용할 수 있어야 합니다. ADO 이벤트 숨겨진된 창을 만들어 내부적으로 처리 됩니다. ADO는 이벤트 발생 해야 하는 경우이 창에 메시지를 게시 합니다. 이렇게 호출 하는 스레드에 이벤트를 전송 **IConnectionPoint::Advise** 연결 지점에 대해 합니다. 이 아키텍처는 알림을 받아야 하는 스레드 창 메시지를 펌핑 하지 않는 경우 문제가 발생할 수 있습니다. 스레드 및 제한 시간 초과 수 있는 숨겨진된 창 메시지를 처리 하지 않는 때문에 전체 시스템 속도가 느려지지 글로벌 창 브로드캐스트에 제공 되지 않는 ADO 이벤트를 포함 하는 잠재적 문제. STA 스레드는 일반적으로이 문제는 하지 명확 하 게 STA 스레드에서 실행 하는 메시지 펌프를 가집니다. 하지만 MTA 스레드 일반적으로 없으므로 메시지 펌프 문제는 일반적으로 명확 하 게 MTA 스레드에서 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [이벤트 유형](../../../ado/guide/data/types-of-events.md)  
  
-   [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)  
  
-   [이벤트 처리기가 함께 작동하는 방법](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [언어별 ADO 이벤트 인스턴스](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스 생성](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO 이벤트](../../../ado/reference/ado-api/ado-events.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 유형](../../../ado/guide/data/types-of-events.md)

