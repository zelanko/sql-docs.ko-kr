---
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
ms.openlocfilehash: 9722bdc585920fb5dcc70ac95afcf2e854a0fa50
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764984"
---
# <a name="state-property-ado-md"></a>State 속성(ADO MD)
셀 집합의 현재 상태를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체의 현재 조건을 나타내는 정수 ( **Long** )를 반환 하며 읽기 전용입니다. 유효한 값은 **adStateClosed** (0) 및 **adstateopen** (1)입니다.  
  
## <a name="remarks"></a>설명  
 [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) 상수 이름을 사용 하려면 프로젝트에서 ADO 형식 라이브러리를 참조 해야 합니다. 자세한 내용은 [ADO MD ADO 사용](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) 을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [Close 메서드 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open 메서드(ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
