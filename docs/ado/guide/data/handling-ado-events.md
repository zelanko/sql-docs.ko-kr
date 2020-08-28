---
description: ADO 이벤트 처리
title: ADO 이벤트 처리 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
author: rothja
ms.author: jroth
ms.openlocfilehash: ff36542abb462ffc63e8704a5c6c3cdd6670d280
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980704"
---
# <a name="handling-ado-events"></a>ADO 이벤트 처리
ADO 이벤트 모델은 작업이 시작 되기 전이나 완료 된 후에 *이벤트*또는 알림을 발행 하는 특정 동기 및 비동기 ADO 작업을 지원 합니다. 이벤트는 실제로 응용 프로그램에서 정의 하는 이벤트 처리기 루틴에 대 한 호출입니다.  
  
 작업이 시작 되기 전에 발생 하는 이벤트 그룹에 대 한 처리기 함수 또는 프로시저를 제공 하는 경우 작업에 전달 된 매개 변수를 검사 하거나 수정할 수 있습니다. 아직 실행 되지 않았기 때문에 작업을 취소 하거나 작업을 완료할 수 있습니다.  
  
 작업을 완료 한 후에 발생 하는 이벤트는 ADO를 비동기식으로 사용 하는 경우 특히 중요 합니다. 예를 들어 비동기 [레코드 집합](../../reference/ado-api/open-method-ado-recordset.md) 을 시작 하는 응용 프로그램은 작업이 완료 될 때 실행 완료 이벤트에 의해 알려집니다.  
  
 ADO 이벤트 모델을 사용 하면 응용 프로그램에 약간의 오버 헤드가 추가 되지만 루프를 사용 하 여 개체의 [상태](../../reference/ado-api/state-property-ado.md) 속성 모니터링과 같은 비동기 작업을 처리 하는 다른 방법 보다 훨씬 더 많은 유연성이 제공 됩니다.  
  
> [!NOTE]
>  이벤트를 처리 하려면 ADO에 메시지 펌프가 있거나 STA (단일 스레드 아파트) 모델에 사용 해야 합니다. ADO 이벤트는 숨겨진 창을 만들어 내부적으로 처리 됩니다. ADO는 이벤트를 발생 시켜야 할 때이 창에 메시지를 게시 합니다. 이 작업은 연결 지점에서 **IConnectionPoint:: Advise** 를 호출한 스레드로 이벤트가 전송 되도록 하기 위한 것입니다. 이 아키텍처는 알림을 받아야 하는 스레드가 창 메시지를 펌프 하지 않는 경우 문제를 일으킬 수 있습니다. 잠재적 문제에는 스레드에 전달 되지 않는 ADO 이벤트와 전역 창 브로드캐스트가 시간 초과 되어 숨겨진 창에서 메시지를 처리 하지 않으므로 전체 시스템 속도가 느려질 수 있습니다. 일반적으로 STA 스레드에는 메시지 펌프가 실행 되므로이 문제는 STA 스레드에 포함 되지 않습니다. 그러나 MTA 스레드에는 일반적으로 메시지 펌프가 없으므로 일반적으로이 문제는 MTA 스레드에 포함 됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ADO 이벤트 처리기 요약](./ado-event-handler-summary.md)  
  
-   [이벤트 형식](./types-of-events.md)  
  
-   [이벤트 매개 변수](./event-parameters.md)  
  
-   [이벤트 처리기가 함께 작동하는 방법](./how-event-handlers-work-together.md)  
  
-   [언어별 ADO 이벤트 인스턴스](./ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>참고 항목  
 [ADO 이벤트 처리기 요약](./ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스화](./ado-event-instantiation-by-language.md)   
 [ADO 이벤트](../../reference/ado-api/ado-events.md)   
 [이벤트 매개 변수](./event-parameters.md)   
 [이벤트 형식](./types-of-events.md)