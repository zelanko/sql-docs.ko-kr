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
ms.openlocfilehash: d63c413ebed585782ca5ce0568119dd7e05bf8ac
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932068"
---
# <a name="namedparameters-property-ado"></a>NamedParameters 속성(ADO)
매개 변수 이름을 공급자에 게 전달할지 여부를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 이 속성이 true 이면 ADO는 [명령 개체](../../../ado/reference/ado-api/command-object-ado.md)의 **매개 변수** 컬렉션에 있는 각 매개 변수의 **Name** 속성 값을 전달 합니다. 공급자는 매개 변수 이름을 사용 하 여 **CommandText** 또는 **commandstream** 속성의 매개 변수를 일치 시킵니다. 이 속성이 false (기본값) 이면 매개 변수 이름이 무시 되 고 공급자가 매개 변수 순서를 사용 하 여 값을 **CommandText** 또는 **commandstream** 속성의 매개 변수와 일치 시킵니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandStream 속성 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
