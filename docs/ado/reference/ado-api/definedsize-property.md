---
title: DefinedSize 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4267776593637a01aef38a218f7272261fd1d448
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140169"
---
# <a name="definedsize-property"></a>DefinedSize 속성
데이터 용량을 나타냅니다는 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **긴** 필드 개체의 데이터 형식에 따라 달라 집니다;을 참조 하는 필드가 정의 된 크기를 반영 하는 값 [형식](../../../ado/reference/ado-api/type-property-ado.md) 자세한. 고정 길이 데이터 형식을 사용 하는 필드의 반환 값은 크기 (바이트)에서 데이터 형식입니다. 가변 길이 데이터 형식을 사용 하는 필드의 경우이 다음 중 하나:  
  
1.  문자에서 필드의 최대 길이 (에 대 한 **집합이 있으므로 필요** 하 고 **adVarWChar**) 또는 바이트 (에 대 한 **adVarBinary**, 및 **adVarNumeric**) 필드에 정의 된 길이입니다. 예를 들어 **adVarChar(5)** 필드의 최대 길이 5입니다.  
  
2.  문자에서 데이터 형식의 최대 길이 (에 대 한 **adChar** 하 고 **adWChar**) 또는 바이트 (에 대 한 **adBinary** 하 고 **adNumeric**) 경우는 필드에 정의 된 길이가 없습니다.  
  
3.  ~ 0 (비트, 값이 0, 모든 비트가 1로 설정 된) 데이터 형식이 나 필드의 최대 길이 정의 된 경우.  
  
4.  데이터 형식의 길이가 없는 경우이 설정은 ~ 0 (비트, 값이 0, 모든 비트가 1로 설정 됩니다).  
  
## <a name="remarks"></a>Remarks  
 사용 된 **DefinedSize** 속성의 데이터 용량을 확인 하는 **필드** 개체.  
  
 합니다 **DefinedSize** 하 고 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) 속성이 다릅니다. 예를 들어를 **필드** 개체의 선언 형식과 **집합이 있으므로 필요** 와 **DefinedSize** 50으로 단일 문자가 포함 된 속성 값입니다. 합니다 **ActualSize** 반환 하는 속성 값이 단일 문자의 길이 (바이트)에서입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [ActualSize 및 DefinedSize 속성 예제 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 및 DefinedSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize 속성(ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
