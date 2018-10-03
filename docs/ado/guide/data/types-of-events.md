---
title: 유형의 이벤트 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b324857816df774486716978425d1332a695952a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708471"
---
# <a name="types-of-events"></a>이벤트 형식
기본적인 두 가지 이벤트가 있습니다. "이벤트는" 작업이 시작 되기 전에 호출 됩니다, 이름에 "는"는 대개-예를 들어 **WillChangeRecordset** 또는 **WillConnect**합니다. 이름에 "완료"를 포함 하는 경우 일반적으로 완료 된 후 호출 되는 이벤트-예를 들어 **RecordChangeComplete** 하거나 **ConnectComplete**합니다. 예외 존재-와 같은 **InfoMessage** -연결된 된 작업이 완료 된 후 이러한 현상이 발생 하지만 합니다.  
  
## <a name="will-events"></a>이벤트는  
 이벤트 처리기는 호출 전에 작업 시작 검사 또는 작업 매개 변수를 수정 하 고 다음 작업을 취소 하거나 완료할 수 있도록 기회를 제공 합니다. 이러한 이벤트 처리기 루틴에는 일반적으로 형식의 이름을 가진 **는*이벤트 * * * 합니다.  
  
## <a name="complete-events"></a>완료 이벤트  
 작업이 완료 된 후 호출 이벤트 처리기가 작업을 완료 하는 응용 프로그램에 알릴 수 있습니다. 이러한 이벤트 처리기는 이벤트 처리기를 보류 중인 작업을 취소 하는 경우에 알립니다. 이러한 이벤트 처리기 루틴에는 일반적으로 형식의 이름을 가진 ***이벤트 * 완료**합니다.  
  
 쌍에서 및 완료 이벤트는 일반적으로 사용 됩니다.  
  
## <a name="other-events"></a>다른 이벤트  
 다른 이벤트 처리기-이름이 없는 폼의 이벤트, 즉 **는 * 이벤트*** 또는 ***이벤트 * 완료** -작업이 완료 된 후에 호출 됩니다. 이러한 이벤트는 **연결 끊기**하십시오 **EndOfRecordset**, 및 **InfoMessage**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 처리기가 함께 작동하는 방법](../../../ado/guide/data/how-event-handlers-work-together.md)
