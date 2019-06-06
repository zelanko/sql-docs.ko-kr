---
title: NamedParameters 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ce517f4ba3f2fc4a80932024a8fe51ac285cdb7d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707301"
---
# <a name="namedparameters-property-ado"></a>NamedParameters 속성(ADO)
매개 변수 이름 공급자에 전달할지 여부를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 ADO 값을 전달이 속성이 true 이면를 **이름** 에서 각 매개 변수의 속성을 **매개 변수** 컬렉션에 대 한를 [명령 개체](../../../ado/reference/ado-api/command-object-ado.md)합니다. 공급자에서 매개 변수와 일치 하도록 매개 변수 이름을 사용 합니다 **CommandText** 하거나 **CommandStream** 속성입니다. 이 속성이 false 인 경우 (기본값), 매개 변수 이름을 무시 되 고 공급자에서 매개 변수 값과 일치 하도록 매개 변수의 순서를 사용 합니다 **CommandText** 또는 **CommandStream** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandStream 속성 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
