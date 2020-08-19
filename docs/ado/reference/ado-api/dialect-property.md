---
description: Dialect 속성
title: 언어 속성 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e106c76b859f9ccdf1e977cfe3a0ac784cb78740
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444075"
---
# <a name="dialect-property"></a>Dialect 속성
[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 또는 [commandstream](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성의 언어를 나타냅니다. 언어는 공급자가 문자열 또는 스트림을 구문 분석 하는 데 사용 하는 구문 및 일반 규칙을 정의 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **언어** 속성에는 명령 텍스트 또는 스트림의 언어를 나타내는 유효한 GUID가 포함 되어 있습니다. 이 속성의 기본값은 {C8B521FB-5CF3-11CE-ADE5-00AA0044773D}입니다 .이 값은 공급자가 명령 텍스트 또는 스트림을 해석 하는 방법을 선택 해야 함을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 사용자가이 속성 값을 읽을 때 ADO에서 공급자를 쿼리하지 않습니다. [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체에 현재 저장 된 값의 문자열 표현을 반환 합니다.  
  
 사용자가 **언어** 속성을 설정 하면 ADO에서 guid의 유효성을 검사 하 고 제공 된 값이 올바른 guid가 아닌 경우 오류를 발생 시킵니다. **언어** 속성에서 지 원하는 GUID 값을 확인 하려면 공급자에 대 한 설명서를 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Execute 메서드(ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)
