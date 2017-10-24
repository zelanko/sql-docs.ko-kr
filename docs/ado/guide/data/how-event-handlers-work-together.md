---
title: "이벤트 처리기 함께 작동 하는 방법 | Microsoft Docs"
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
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a2e603819e2d4c44bf612d62f86f448c560e0828
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="how-event-handlers-work-together"></a>이벤트 처리기 함께 작동 하는 방법
Visual Basic의 경우에 대 한 모든 이벤트 처리기에서 프로그래밍 하는 경우가 아니면 **연결** 및 **레코드 집합** 여부 실제로 처리의 모든 이벤트에 관계 없이 이벤트에 구현, 되어야 합니다. 구현 작업을 수행 해야 하는 프로그래밍 언어에 따라 다릅니다. 자세한 내용은 참조 [언어별 ADO 이벤트 인스턴스 생성](../../../ado/guide/data/ado-event-instantiation-by-language.md)합니다.  
  
## <a name="paired-event-handlers"></a>쌍으로 연결 된 이벤트 처리기  
 각 Will 이벤트 처리기에 연결 된 **완료** 이벤트 처리기입니다. 응용 프로그램 필드의 값을 변경 하는 경우 예를 들어는 **WillChangeField** 이벤트 처리기가 호출 됩니다. 변경이 허용 되 면 응용 프로그램 둡니다는 **adStatus** 매개 변수 변경 되지 않은 하 고 작업을 수행 합니다. 작업이 완료 되는 **FieldChangeComplete** 이벤트는 작업이 완료 되는 응용 프로그램에 알립니다. 성공적으로 완료 된 경우 **adStatus** 포함 **adStatusOK**, 그렇지 않으면 **adStatus** 포함 **adStatusErrorsOccurred** 및 확인 해야 합니다는 **오류** 오류의 원인을 파악 하는 개체입니다.  
  
 때 **WillChangeField** 는 호출을 하는지 확인할 수 있습니다는 변경 되지 않습니다 수 있도록 합니다. 이 경우에 설정 **adStatus** 를 **adStatusCancel 합니다.** 작업이 취소 되 고 **FieldChangeComplete** 이벤트 수신는 **adStatus** 값 **adStatusErrorsOccurred**합니다. **오류** 개체에 포함 되어 **adErrOperationCancelled** 하 여 **FieldChangeComplete** 처리기 알고 작업이 취소 되었습니다. 하지만 값을 확인 해야는 **adStatus** 설정 때문에 변경 하기 전에 매개 변수 **adStatus** 를 **adStatusCancel** 는 매개 변수를 설정한 경우 효과가 없습니다 **adStatusCantDeny** 절차 항목입니다.  
  
 경우에 따라 작업 하나 이상의 이벤트를 발생 시킬 수 있습니다. 예를 들어는 **레코드 집합** 개체에 대 한 이벤트는 쌍이 **필드** 변경 내용 및 **레코드** 변경 합니다. 응용 프로그램의 값을 변경 하는 경우는 **필드**, **WillChangeField** 이벤트 처리기가 호출 됩니다. 경우에 작업을 계속할 수는 **WillChangeRecord** 이벤트 처리기에도 발생 합니다. 이 처리기에는 이벤트를 계속 허용 하면, 변경 및 **FieldChangeComplete** 및 **RecordChangeComplete** 이벤트 처리기가 호출 됩니다. 특정 작업에 대 한 이벤트 처리기가 호출 되는 순서를 정의 하지 않은 특정 시퀀스에서 처리기를 호출 하는 방법에 의존 하는 코드를 작성 하지 않아야 합니다.  
  
 인스턴스에서 여러는 이벤트가 발생 보류 중인 작업이 취소 될 수 있습니다 이벤트 중 하나입니다. 응용 프로그램의 값을 변경 하는 경우 예를 들어 한 **필드**모두 **WillChangeField** 및 **WillChangeRecord** 일반적으로 이벤트 처리기를 호출 합니다. 그러나 연결 된 첫 번째 이벤트 처리기에서 작업이 취소 되는 경우 **완료** 처리기가 즉시 호출 **adStatusOperationCancelled**합니다. 두 번째 처리기가 호출 되지 않습니다. 그러나 첫 번째 이벤트 처리기 이벤트를 계속 허용 하는 경우 다른 이벤트 처리기 호출 됩니다. 다음 작업을 취소 하는 경우 둘 다 **완료** 이벤트는 이전 예제와 같이 호출 됩니다.  
  
## <a name="unpaired-event-handlers"></a>짝이 없는 이벤트 처리기  
 에 전달 된 상태도 않은 이벤트 **adStatusCantDeny**를 반환 하 여 모든 이벤트에 대 한 이벤트 알림을 해제할 수 있습니다 **adStatusUnwantedEvent** 에 *상태*매개 변수입니다. 예를 들어 프로그램 **완료** 이벤트 처리기가 처음으로 호출을 반환할 수 있습니다 **adStatusUnwantedEvent**합니다. 이후에 받습니다만 **됩니다** 이벤트입니다. 그러나 여러 가지 원인에 대 한 일부 이벤트를 트리거할 수 있습니다. 이 경우 이벤트를 받을 가능성이 *이유* 매개 변수입니다. 돌아가서 **adStatusUnwantedEvent**, 특정 이유로 발생 하는 경우에 해당 이벤트에 대 한 알림 수신을 중지 됩니다. 즉, 잠재적으로 알림 이벤트가 트리거될 수 가능한 각 이유에 표시 됩니다.  
  
 단일 **됩니다** 이벤트 처리기는 작업에 사용할 수 있는 매개 변수를 검사 하려는 경우 유용할 수 있습니다. 이러한 작업 매개 변수를 수정 하거나 작업을 취소할 수 있습니다.  
  
 또는 두고 **완료** 이벤트 알림을 사용 하도록 설정 합니다. 첫 번째 이벤트 처리기가 호출 될 때 반환할 **adStatusUnwantedEvent**합니다. 이후에 받습니다만 **완료** 이벤트입니다.  
  
 단일 **완료** 이벤트 처리기는 비동기 작업을 관리 하는 데 유용할 수 있습니다. 각 비동기 작업에 적합 한 **완료** 이벤트입니다.  
  
 예를 들어 큰 채우는 데 시간이 오래 걸리므로 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 적절 하 게 작성 된 응용 프로그램을 시작할 수 있습니다는 `Recordset.Open(...,adAsyncExecute)` 작업 다른 처리를 계속 합니다. 결국 수 있을 때 알림을 **레코드 집합** 의해 채워집니다는 **ExecuteComplete** 이벤트입니다.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>단일 이벤트 처리기 및 여러 개체  
 Microsoft Visual C++® 같은 프로그래밍 언어의 유연성을 사용 하면 여러 개체에서 이벤트 처리기 프로세스 이벤트 하나일 수 있습니다. 예를 들어 하나 있을 수 있습니다 **연결 끊기** 여러 이벤트 처리기 프로세스 이벤트 **연결** 개체입니다. 연결 중 하나가 종료 된 경우는 **연결 끊기** 이벤트 처리기 호출 됩니다. 이벤트 처리기 개체 매개 변수가 해당 요소에 설정 되므로 이벤트를 발생 시킨 연결을 확인할 수 있습니다 **연결** 개체입니다.  
  
> [!NOTE]
>  이 기술은 해당 언어에는 이벤트 처리기에 하나의 개체만 간에 상관 관계 수 때문에 Visual Basic에서 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스 생성](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 유형](../../../ado/guide/data/types-of-events.md)

