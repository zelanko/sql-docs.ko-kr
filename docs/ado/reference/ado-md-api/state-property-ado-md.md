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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 812863395c2980f341ed2419eee1d9d661f19dd0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822168"
---
# <a name="state-property-ado-md"></a>State 속성(ADO MD)
셀 집합의 현재 상태를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 반환을 **긴** 의 현재 상태를 나타내는 정수를 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체 및 읽기 전용입니다. 다음 값이 잘못 되었습니다: **adStateClosed** (0) 및 **adStateOpen** (1).  
  
## <a name="remarks"></a>Remarks  
 사용 하 여 [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) 상수 이름을 프로젝트에서 참조 ADO 형식 라이브러리에 있어야 합니다. 참조 [ADO MD를 사용 하 여 ADO를 사용 하 여](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) 자세한 내용은 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목  
 [Close 메서드 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open 메서드(ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
