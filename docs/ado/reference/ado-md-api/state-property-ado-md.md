---
description: State 속성(ADO MD)
title: State 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
author: rothja
ms.author: jroth
ms.openlocfilehash: efc3b140b2864aec7151e1235010c4a14b0b3a64
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777862"
---
# <a name="state-property-ado-md"></a>State 속성(ADO MD)
셀 집합의 현재 상태를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 [셀 집합](./cellset-object-ado-md.md) 개체의 현재 조건을 나타내는 정수 ( **Long** )를 반환 하며 읽기 전용입니다. 유효한 값은 **adStateClosed** (0) 및 **adstateopen** (1)입니다.  
  
## <a name="remarks"></a>설명  
 [ObjectStateEnum](../ado-api/objectstateenum.md) 상수 이름을 사용 하려면 프로젝트에서 ADO 형식 라이브러리를 참조 해야 합니다. 자세한 내용은 [ADO MD ADO 사용](../../guide/multidimensional/using-ado-with-ado-md.md) 을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [Close 메서드 (ADO MD)](./close-method-ado-md.md)   
 [Open 메서드(ADO MD)](./open-method-ado-md.md)