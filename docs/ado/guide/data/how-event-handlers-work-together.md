---
title: 이벤트 처리기를 함께 작동 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cb02a96e6ee3d28c67e21996677c02b58fc97c07
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718385"
---
# <a name="how-event-handlers-work-together"></a>이벤트 처리기가 함께 작동하는 방법
Visual Basic의 경우에 대 한 모든 이벤트 처리기에서 프로그래밍 하는 경우가 아니면 **연결** 하 고 **Recordset** 여부 실제로 처리의 모든 이벤트에 관계 없이 이벤트에 구현, 되어야 합니다. 구현 작업을 수행 해야 하는 프로그래밍 언어에 따라 다릅니다. 자세한 내용은 [언어별 ADO 이벤트 인스턴스](../../../ado/guide/data/ado-event-instantiation-by-language.md)합니다.  
  
## <a name="paired-event-handlers"></a>쌍으로 연결 된 이벤트 처리기  
 각는 이벤트 처리기에 연결 된 **완료** 이벤트 처리기입니다. 응용 프로그램 필드의 값을 변경 하는 경우 예를 들어 합니다 **WillChangeField** 이벤트 처리기가 호출 됩니다. 변경 허용 되는 경우 응용 프로그램 유지 합니다 **adStatus** 변경 되지 않은 매개 변수 및 작업이 수행 됩니다. 작업이 완료 되는 **FieldChangeComplete** 이벤트는 작업이 완료 되는 응용 프로그램에 알립니다. 성공적으로 완료 되 면 **adStatus** 포함 **adStatusOK**이 고, 그렇지 않으면 **adStatus** 포함 **adStatusErrorsOccurred** 및 확인 해야 합니다 **오류** 오류의 원인을 확인 하는 개체입니다.  
  
 때 **WillChangeField** 는 호출을 알 수 있습니다는 변경 내용을 만들지 않아야 합니다. 이 경우에 설정할 **adStatus** 에 **adStatusCancel 합니다.** 작업이 취소 되 고 **FieldChangeComplete** 이벤트를 수신는 **adStatus** 값 **adStatusErrorsOccurred**합니다. **오류** 개체에 포함 되어 **adErrOperationCancelled** 되도록 하 **FieldChangeComplete** 처리기 인식 작업이 취소 되었습니다. 하지만 값을 확인 해야 합니다 **adStatus** 설정 이기 때문에 변경 하기 전에 매개 변수 **adStatus** 하 **adStatusCancel** 매개 변수는 설정 된 경우 효과가 없습니다 하 **adStatusCantDeny** 절차 항목입니다.  
  
 경우에 따라 작업 둘 이상의 이벤트를 발생 시킬 수 있습니다. 예를 들어를 **레코드 집합** 개체에 대 한 이벤트 쌍을 이루는 **필드** 변경 하 고 **레코드** 변경 합니다. 응용 프로그램의 값을 변경 하는 경우는 **필드**서 **WillChangeField** 이벤트 처리기가 호출 됩니다. 작업을 계속할 수를 결정 하는 경우는 **WillChangeRecord** 이벤트 처리기에도 발생 합니다. 이 처리기에는 이벤트를 계속 허용 하면, 변경 하며 **FieldChangeComplete** 하 고 **RecordChangeComplete** 이벤트 처리기가 호출 됩니다. 특정 한 순서로 처리기 호출에 의존 하는 코드를 작성 하지 말아야 하므로 특정 작업에 대 한 이벤트 처리기가 호출 되는 순서 정의 되지 않았습니다.  
  
 인스턴스에서 여러는 이벤트가 발생 하는 보류 중인 작업이 취소 될 수 있습니다 이벤트 중 하나입니다. 응용 프로그램의 값을 변경 하는 경우 예를 들어를 **필드**모두 **WillChangeField** 하 고 **WillChangeRecord** 이벤트 처리기는 일반적으로 호출 됩니다. 그러나 연결 된 첫 번째 이벤트 처리기에서 작업이 취소 되는 경우 **Complete** 처리기가 즉시 호출 **adStatusOperationCancelled**합니다. 두 번째 처리기가 호출 되지 않습니다. 그러나 첫 번째 이벤트 처리기는 이벤트가 진행을 허용 하는 경우 다른 이벤트 처리기 호출 됩니다. 그런 다음 작업을 취소 하는 경우 둘 다 **완료** 이벤트 앞의 예제와 같이 호출 됩니다.  
  
## <a name="unpaired-event-handlers"></a>쌍을 이루지 않는 이벤트 처리기  
 이벤트가 아닌 상태를 전달 하기만 **adStatusCantDeny**를 반환 하 여 모든 이벤트에 대 한 이벤트 알림을 해제할 수 있습니다 **adStatusUnwantedEvent** 에 *상태*매개 변수입니다. 예를 들어, 프로그램 **Complete** 이벤트 처리기가 처음 호출을 반환할 수 있습니다 **adStatusUnwantedEvent**합니다. 이후에 받게만 **는** 이벤트입니다. 그러나 여러 가지 원인에 대 한 몇 가지 이벤트를 트리거할 수 있습니다. 이 경우 이벤트를 받을 가능성이 *이유* 매개 변수입니다. 돌아오면 **adStatusUnwantedEvent**, 해당 특정 이유로 발생 하는 경우에 해당 이벤트에 대 한 알림 수신을 중지 해야 합니다. 즉, 이벤트가 트리거될 수 각 원인에 대 한 알림을 잠재적으로 받게 됩니다.  
  
 단일 **는** 이벤트 처리기는 작업에 사용할 매개 변수를 검토 하려는 경우 유용할 수 있습니다. 해당 작업 매개 변수를 수정 하거나 작업을 취소할 수 있습니다.  
  
 또는 두고 **완료** 이벤트 알림을 사용 하도록 설정 합니다. 첫 번째는 이벤트 처리기가 호출 되 면 반환 **adStatusUnwantedEvent**합니다. 이후에 받게만 **완료** 이벤트입니다.  
  
 단일 **완료** 이벤트 처리기는 비동기 작업을 관리 하는 데 유용할 수 있습니다. 각 비동기 작업에 적절 한 **완료** 이벤트입니다.  
  
 예를 들어 큰를 채우는 데 시간이 오래 걸릴 수 있습니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 적절 하 게 작성 된 응용 프로그램을 시작할 수 있습니다는 `Recordset.Open(...,adAsyncExecute)` 작업 하 고 다른 처리를 사용 하 여 계속 합니다. 결국 됩니다 알림을 합니다 **레코드 집합** 채워집니다는 **ExecuteComplete** 이벤트.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>단일 이벤트 처리기 및 여러 개체  
 Microsoft Visual C++® 같은 프로그래밍 언어의 유연성을 사용 하면 이벤트 처리기 여러 개체에서 이벤트를 처리 하나일 수 있습니다. 예를 들어 하나 있을 수 있습니다 **연결 끊기** 이벤트 처리기에서 여러 이벤트 처리 **연결** 개체입니다. 연결 중 하나를 종료 하는 경우는 **연결 끊기** 이벤트 처리기가 호출 되어야 합니다. 해당 이벤트 처리기 개체 매개 변수 설정 되므로 이벤트를 발생 시킨 연결을 확인할 수 있습니다 **연결** 개체입니다.  
  
> [!NOTE]
>  Visual Basic의 해당 언어에는 이벤트 처리기에 하나의 개체만 상호 연결할 수 있으므로이 기법을 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 유형](../../../ado/guide/data/types-of-events.md)
