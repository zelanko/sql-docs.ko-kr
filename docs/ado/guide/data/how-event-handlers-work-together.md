---
description: 이벤트 처리기가 함께 작동하는 방법
title: 이벤트 처리기가 함께 작동 하는 방식 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
author: rothja
ms.author: jroth
ms.openlocfilehash: 39e50c060dc602cb2bdd3541a454624e41b4d5b3
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805975"
---
# <a name="how-event-handlers-work-together"></a>이벤트 처리기가 함께 작동하는 방법
Visual Basic 프로그래밍 하지 않는 한 **연결** 및 **레코드 집합** 이벤트에 대 한 모든 이벤트 처리기는 실제로 모든 이벤트를 처리 하는지 여부에 관계 없이 구현 되어야 합니다. 구현 해야 하는 작업의 양은 프로그래밍 언어에 따라 달라 집니다. 자세한 내용은 [언어별 ADO 이벤트 인스턴스화](./ado-event-instantiation-by-language.md)를 참조 하세요.  
  
## <a name="paired-event-handlers"></a>쌍을 이루는 이벤트 처리기  
 각 이벤트 처리기에는 연결 된 **완전** 한 이벤트 처리기가 있습니다. 예를 들어 응용 프로그램에서 필드의 값을 변경 하면 **WillChangeField** 이벤트 처리기가 호출 됩니다. 변경이 허용 되는 경우 응용 프로그램은 **Adstatus** 매개 변수를 변경 되지 않은 상태로 두고 작업을 수행 합니다. 작업이 완료 되 면 **FieldChangeComplete** 이벤트에서 작업이 완료 되었음을 응용 프로그램에 알립니다. 성공적으로 완료 되 면 **Adstatus** 에 **adstatusok**가 포함 됩니다. 그렇지 않으면 **Adstatus** 에 **adStatusErrorsOccurred** 가 포함 되 고 오류 **개체를 확인 하 여 오류의** 원인을 확인 해야 합니다.  
  
 **WillChangeField** 가 호출 되 면 변경이 수행 되지 않도록 결정할 수 있습니다. 이 경우 **Adstatus** 를 **adstatuscancel로 설정 합니다.** 작업이 취소 되 고 **FieldChangeComplete** 이벤트가 **Adstatus** 값 **adStatusErrorsOccurred**를 수신 합니다. **Error** 개체에는 **adErrOperationCancelled** 포함 되어 있으므로 **FieldChangeComplete** 처리기에서 작업이 취소 되었음을 알 것입니다. 그러나 매개 변수가 프로시저에 대 한 **adStatusCantDeny** 로 설정 된 경우 **Adstatus** 를 **adstatuscancel** 로 설정 해도 아무런 효과가 없으므로 **adstatus** 매개 변수 값을 변경 하기 전에이 값을 확인 해야 합니다.  
  
 경우에 따라 작업에서 두 개 이상의 이벤트를 발생 시킬 수 있습니다. 예를 들어 **레코드 집합** 개체에는 **필드** 변경 및 **레코드** 변경에 대 한 쌍으로 된 이벤트가 있습니다. 응용 프로그램에서 **필드**의 값을 변경 하면 **WillChangeField** 이벤트 처리기가 호출 됩니다. 작업을 계속할 수 있는 것으로 확인 되 면 **WillChangeRecord** 이벤트 처리기도 발생 합니다. 이 처리기 에서도 이벤트를 계속 진행할 수 있는 경우 변경 내용이 적용 되 고 **FieldChangeComplete** 및 **RecordChangeComplete** 이벤트 처리기가 호출 됩니다. 특정 작업에 대 한 이벤트 처리기가 호출 되는 순서는 정의 되어 있지 않으므로 특정 시퀀스의 호출 처리기에 의존 하는 코드를 작성 하지 않아야 합니다.  
  
 여러 이벤트가 발생 하는 경우에는 이벤트 중 하나가 보류 중인 작업을 취소할 수 있습니다. 예를 들어 응용 프로그램에서 **필드**의 값을 변경 하면 **WillChangeField** 및 **WillChangeRecord** 이벤트 처리기가 일반적으로 호출 됩니다. 그러나 첫 번째 이벤트 처리기에서 작업이 취소 되 면 연결 된 **전체** 처리기가 **adstatusoperationcancelled**를 사용 하 여 즉시 호출 됩니다. 두 번째 처리기는 호출 되지 않습니다. 그러나 첫 번째 이벤트 처리기가 이벤트를 계속 진행할 수 있으면 다른 이벤트 처리기가 호출 됩니다. 그런 다음 작업을 취소 하면 **모든 완료** 이벤트가 이전 예제와 같이 호출 됩니다.  
  
## <a name="unpaired-event-handlers"></a>짝이 없는 이벤트 처리기  
 이벤트에 전달 된 상태가 **adStatusCantDeny**가 아니면 *Status* 매개 변수에 **adStatusUnwantedEvent** 을 반환 하 여 이벤트에 대 한 이벤트 알림을 해제할 수 있습니다. 예를 들어 **전체** 이벤트 처리기를 처음 호출 하는 경우 **adStatusUnwantedEvent**를 반환할 수 있습니다. 그런 다음 **에는 해당** 이벤트만 받게 됩니다. 그러나 일부 이벤트는 여러 가지 이유로 트리거될 수 있습니다. 이 경우 이벤트에 *Reason* 매개 변수가 포함 됩니다. **AdStatusUnwantedEvent**를 반환 하는 경우 해당 이벤트에 대 한 알림이 특정 원인에 대해 발생 하는 경우에만 수신을 중지 합니다. 즉, 이벤트를 트리거할 수 있는 가능한 각 원인에 대해 알림을 받을 수 있습니다.  
  
 단일 **이벤트 처리기는 작업** 에 사용 되는 매개 변수를 검사 하려는 경우에 유용할 수 있습니다. 이러한 작업 매개 변수를 수정 하거나 작업을 취소할 수 있습니다.  
  
 또는 **전체** 이벤트 알림을 사용 하도록 설정 된 상태로 둡니다. 첫 번째 이벤트 처리기가 호출 되 면 **adStatusUnwantedEvent**를 반환 합니다. 그런 다음에는 **완전** 한 이벤트만 받게 됩니다.  
  
 단일 **Complete** 이벤트 처리기는 비동기 작업을 관리 하는 데 유용할 수 있습니다. 각 비동기 작업에는 적절 한 **완료** 이벤트가 있습니다.  
  
 예를 들어, 대량 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체를 채우는 데 시간이 오래 걸릴 수 있습니다. 응용 프로그램이 적절 하 게 작성 되 면 작업을 시작 `Recordset.Open(...,adAsyncExecute)` 하 고 다른 처리를 계속할 수 있습니다. **ExecuteComplete** 이벤트로 **레코드 집합** 을 채울 때 알림이 표시 됩니다.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>단일 이벤트 처리기 및 여러 개체  
 Microsoft Visual C++®와 같은 프로그래밍 언어의 유연성을 사용 하면 하나의 이벤트 처리기에서 여러 개체의 이벤트를 처리할 수 있습니다. 예를 들어 여러 **연결** 개체에서 이벤트 처리기를 처리 하 **는 이벤트 처리기가 하나 있을** 수 있습니다. 연결 중 하나가 종료 되 면 **연결 끊기** 이벤트 처리기가 호출 됩니다. 이벤트 처리기 개체 매개 변수가 해당 **연결** 개체로 설정 되기 때문에 이벤트를 발생 시킨 연결을 확인할 수 있습니다.  
  
> [!NOTE]
>  이 기술은 하나의 개체만 이벤트 처리기와 상관 관계를 지정할 수 있으므로 Visual Basic에서 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO 이벤트 처리기 요약](./ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스화](./ado-event-instantiation-by-language.md)   
 [이벤트 매개 변수](./event-parameters.md)   
 [이벤트 형식](./types-of-events.md)