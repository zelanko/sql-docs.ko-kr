---
title: 이벤트 유형 | Microsoft Docs
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
ms.openlocfilehash: c02d8d115a4336470c0e0d32aebabea63c05ab0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923812"
---
# <a name="types-of-events"></a>이벤트 형식
이벤트에는 두 가지 기본 유형이 있습니다. 작업이 시작 되기 전에 호출 되는 "이벤트"는 일반적으로 이름에 "WillChangeRecordset" (예: **** 또는 **WillConnect**)를 포함 합니다. 이벤트가 완료 된 후 호출 되는 이벤트는 일반적으로 이름에 "Complete"를 포함 합니다 (예: **RecordChangeComplete** 또는 **connectcomplete**). **InfoMessage** 와 같은 예외가 존재 하지만 연결 된 작업이 완료 된 후에 이러한 예외가 발생 합니다.  
  
## <a name="will-events"></a>이벤트를  
 작업을 시작 하기 전에 호출 되는 이벤트 처리기를 사용 하 여 작업 매개 변수를 검사 하거나 수정한 다음 작업을 취소 하거나 작업을 완료할 수 있습니다. 이러한 이벤트 처리기 루틴 <strong>은**</strong>일반적으로 형식의 이름이 있습니다.  
  
## <a name="complete-events"></a>전체 이벤트  
 작업이 완료 된 후 호출 되는 이벤트 처리기는 작업이 완료 되었음을 응용 프로그램에 알릴 수 있습니다. 이러한 이벤트 처리기는에서 이벤트 처리기가 보류 중인 작업을 취소 하는 경우에도 알립니다. 이러한 이벤트 처리기 루틴의 이름은 일반적으로 <strong> *이벤트*완료</strong>형식입니다.  
  
 는 일반적으로 쌍으로 사용 됩니다.  
  
## <a name="other-events"></a>기타 이벤트  
 다른 이벤트 처리기 즉, 이름이 형식이 아닌 이벤트 또는 이벤트 완료 인 이벤트는 작업이 완료 된 후 <strong> **</strong> 에만 호출 됩니다. <strong>** </strong> 이러한 이벤트는 **Disconnect**, **EndOfRecordset**및 **InfoMessage**입니다.  
  
## <a name="see-also"></a>참고 항목  
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)   
 [언어별 ADO 이벤트 인스턴스화](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [이벤트 매개 변수](../../../ado/guide/data/event-parameters.md)   
 [이벤트 처리기가 함께 작동하는 방법](../../../ado/guide/data/how-event-handlers-work-together.md)
