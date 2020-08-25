---
description: CommandType 속성(ADO)
title: CommandType 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandType
helpviewer_keywords:
- CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
author: rothja
ms.author: jroth
ms.openlocfilehash: 0216a04051ee45cf92d5451396c8012dbd47fe7b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776092"
---
# <a name="commandtype-property-ado"></a>CommandType 속성(ADO)
[명령](./command-object-ado.md) 개체의 유형을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 하나 이상의 [CommandTypeEnum](./commandtypeenum.md) 값을 설정 하거나 반환 합니다.  
  
> [!NOTE]
>  **Adcmdfile** 또는 **adCmdTableDirect** 에 **CommandTypeEnum** 값을 사용 하지 **마세요.** 이러한 값은 [레코드 집합](./recordset-object-ado.md)의 [Open](./open-method-ado-recordset.md) 및 [Requery](./requery-method.md) 메서드에서 옵션 으로만 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **CommandType** 속성을 사용 하 여 [CommandText](./commandtext-property-ado.md) 속성의 평가를 최적화 합니다.  
  
 **CommandType** 속성 값을 기본값인 **adcmdunknown**으로 설정 하면 ADO에서 **CommandText** 속성이 SQL 문, 저장 프로시저 또는 테이블 이름 인지 확인 하기 위해 공급자를 호출 해야 하기 때문에 성능이 저하 될 수 있습니다. 사용 중인 명령의 유형을 알고 있는 경우 **CommandType** 속성을 설정 하면 ADO가 관련 코드로 직접 이동 하도록 지시 합니다. **CommandType** 속성이 **CommandText** 속성의 명령 유형과 일치 하지 않으면 [Execute](./execute-method-ado-command.md) 메서드를 호출할 때 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)