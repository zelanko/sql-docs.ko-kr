---
title: Dialect 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::Dialect
helpviewer_keywords:
- Dialect property
ms.assetid: 329c3a71-ba88-4009-b04f-2f52195a5957
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5c7e6aab3e3b33d02adcb067fff46b49973191b0
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698239"
---
# <a name="dialect-property"></a>Dialect 속성
언어를 나타냅니다 합니다 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 하거나 [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성입니다. 언어 구문 및 공급자 문자열 또는 스트림에 구문 분석 하는 데 사용 하는 일반 규칙을 정의 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 합니다 **언어** 속성 stream 명령 텍스트의 언어를 나타내는 유효한 GUID를 포함 합니다. 이 속성의 기본값은 {C8B521FB-5CF3-11CE-ADE5-00AA0044773D} 공급자 stream을 명령 텍스트를 해석 하는 방법을 선택 해야 하는 것이 나타내는입니다.  
  
## <a name="remarks"></a>Remarks  
 사용자는이 속성의 값을 읽을 때 ADO에서는 공급자를 쿼리하지 않습니다. 에 현재 저장 된 값의 문자열 표현을 반환 합니다 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
 사용자 설정 하는 경우는 **언어** 속성, ADO GUID의 유효성을 검사 하 고 제공 된 값이 올바른 GUID가 없으면 오류를 발생 시킵니다. 공급자에서 지원 되는 GUID 값을 확인 하려면 설명서를 참조 합니다 **언어** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Execute 메서드(ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)
