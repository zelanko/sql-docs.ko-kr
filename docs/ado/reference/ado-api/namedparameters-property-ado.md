---
title: "NamedParameters 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Command::NamedParameters
helpviewer_keywords: NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da97908abd0b7ba06231c4cd20567e80cfdfed20
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="namedparameters-property-ado"></a>NamedParameters 속성 (ADO)
매개 변수 이름 공급자에 전달 해야 하는지 여부를 나타냅니다.  
  
## <a name="remarks"></a>주의  
 이 속성이 true 이면 ADO의 값을 전달는 **이름** 속성의 각 매개 변수에 **매개 변수** 에 대 한 컬렉션은 [명령 개체](../../../ado/reference/ado-api/command-object-ado.md)합니다. 공급자는 매개 변수 이름에서 매개 변수를 사용 하 여는 **CommandText** 또는 **CommandStream** 속성입니다. 이 속성이 false 이면 (기본값) 이면 매개 변수 이름은 무시 되 고 매개 변수에 값과 일치 하도록 매개 변수 순서를 사용 하는 공급자는 **CommandText** 또는 **CommandStream** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandStream 속성 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
