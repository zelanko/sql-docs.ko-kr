---
title: "유형의 이벤트 | Microsoft Docs"
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
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 502c77b55eb0e3a60497fa10bf9fe8c8a412dc4d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-events"></a>이벤트 유형
이벤트의 두 기본 유형이 있습니다. "이벤트에 는" 작업이 시작 되기 전에 호출 되는, 일반적으로 이름에 "는"를 포함-예를 들어 **WillChangeRecordset** 또는 **WillConnect**합니다. 이벤트가 완료 된 후 일반적으로 호출 된 이벤트에 이름에 "Complete"는 포함-예를 들어 **RecordChangeComplete** 또는 **ConnectComplete**합니다. 예외가-와 같은 **InfoMessage** -하지만 연결된 작업이 완료 된 후 발생 합니다.  
  
## <a name="will-events"></a>이벤트는  
 이벤트 처리기에서 작업을 시작 하 여 제공 기회를 검사 하거나 작업 매개 변수를 수정 작업을 취소 하거나 완료 하기 전에 호출 됩니다. 이러한 이벤트 처리기 루틴에는 일반적으로 폼의 이름을 가진 * *됩니다*이벤트** *입니다.  
  
## <a name="complete-events"></a>이벤트를 완료 합니다.  
 작업이 완료 된 후 호출 된 이벤트 처리기가 작업을 완료 하는 응용 프로그램에 알릴 수 있습니다. 이러한 이벤트 처리기는 이벤트 처리기를 보류 중인 작업을 취소 하는 경우에 알립니다. 이러한 이벤트 처리기 루틴에는 일반적으로 폼의 이름을 가진 ** *이벤트*완료**합니다.  
  
 가 않으며 전체 이벤트 쌍에 일반적으로 사용 됩니다.  
  
## <a name="other-events"></a>다른 이벤트  
 다른 이벤트 처리기-즉, 이벤트를 폼의 이름이 없는 * *됩니다*이벤트** * 또는 ** *이벤트*완료** -만 호출 됩니다 작업을 완료 합니다. 이러한 이벤트는 **연결 끊기**, **EndOfRecordset**, 및 **InfoMessage**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스 생성](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 처리기가 함께 작동하는 방법](../../../ado/guide/data/how-event-handlers-work-together.md)
