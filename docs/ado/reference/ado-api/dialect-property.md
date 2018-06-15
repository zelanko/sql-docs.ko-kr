---
title: Dialect 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::Dialect
helpviewer_keywords:
- Dialect property
ms.assetid: 329c3a71-ba88-4009-b04f-2f52195a5957
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 638d02511078028fa6c5b1337fdb1b095d8e5c85
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277922"
---
# <a name="dialect-property"></a>언어 속성
언어 나타냅니다는 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 또는 [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성입니다. 언어 구문 및 공급자가 문자열 또는 스트림에 구문 분석을 사용 하는 일반 규칙을 정의 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **언어** 속성 스트림 또는 명령 텍스트의 언어를 나타내는 유효한 GUID를 포함 합니다. 이 속성에 대 한 기본값은 {C8B521FB-5CF3-11CE-ADE5-00AA0044773D} 공급자 명령 텍스트 또는 스트림에 해석 하는 방법을 선택 해야는 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 사용자;이 속성의 값을 읽을 때 서비스에서 ADO 공급자를 쿼리하지 않습니다. 에 현재 저장 된 값의 문자열 표현을 반환는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.  
  
 사용자 설정 하는 경우는 **언어** 속성을 ADO GUID의 유효성을 검사 하 고 제공 된 값이 올바른 GUID 없으면 오류를 발생 시킵니다. 지 원하는 GUID 값을 확인 하 여 공급자에 대 한 설명서를 참조는 **언어** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Execute 메서드(ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)
