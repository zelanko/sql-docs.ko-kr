---
title: DefinedSize 속성 | Microsoft Docs
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
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b060258acc6e267ff9e518aa4591bdfd0eef69e
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277562"
---
# <a name="definedsize-property"></a>DefinedSize 속성
데이터 용량 나타냅니다는 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환은 **긴** 필드 개체의 데이터 형식에 따라 달라 집니다; 참조 하는 필드의 정의 된 크기를 반영 하는 값 [형식](../../../ado/reference/ado-api/type-property-ado.md) 자세한 정보에 대 한 합니다. 고정 길이 데이터 형식을 사용 하는 필드에 대 한 반환 값 (바이트)에서 데이터 형식의 크기입니다. 가변 길이 데이터 형식을 사용 하는 필드를 다음 중 하나입니다.  
  
1.  문자에서 필드의 최대 길이 (에 대 한 **집합이 있으므로 필요** 및 **adVarWChar**) 또는 바이트 (에 대 한 **adVarBinary**, 및 **adVarNumeric**) 필드에 정의 된 길이입니다. 예를 들어 **adVarChar(5)** 필드의 최대 길이는 5입니다.  
  
2.  문자에서 데이터 형식의 최대 길이 (에 대 한 **adChar** 및 **adWChar**) 또는 바이트 (에 대 한 **adBinary** 및 **adNumeric**) 하는 경우는 필드에는 정의 된 길이가 없습니다.  
  
3.  ~ 0 (비트, 값이 0, 모든 비트가 1로 설정 됩니다) 경우의 정의 된 최대 길이 필드 또는 데이터 형식이 아닙니다.  
  
4.  데이터 형식의 길이 갖지 않는 경우이 설정은 ~ 0 (비트, 값이 0, 모든 비트가 1로 설정 됩니다).  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **DefinedSize** 속성의 데이터 용량을 확인 하는 **필드** 개체입니다.  
  
 **DefinedSize** 및 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) 속성은 서로 다릅니다. 예를 들어 한 **필드** 개체의 선언 된 형식과 **집합이 있으므로 필요** 및 **DefinedSize** 50으로 단일 문자를 포함 하는 속성 값입니다. **ActualSize** 반환 하는 속성 값은 단일 문자 길이 (바이트)에서입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [ActualSize 및 DefinedSize 속성 예제 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 및 DefinedSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize 속성(ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
