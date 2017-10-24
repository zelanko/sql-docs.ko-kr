---
title: "ActualSize 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d66019d7a71dd480f1a88a28fe94d72a176497c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="actualsize-property-ado"></a>ActualSize 속성 (ADO)
필드의 실제 길이 나타내는??? s 바이트 값입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 반환 된 **긴** 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **ActualSize** 의 실제 길이 반환 하는 [필드](../../../ado/reference/ado-api/field-object.md) 개체의 값입니다. 모든 필드에는 **ActualSize** 속성은 읽기 전용입니다. ADO의 길이 확인할 수 없는 경우는 **필드** 개체의 값은 **ActualSize** 속성에서 반환 **adUnknown**합니다.  
  
 **ActualSize** 및 [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) 속성이 다르면 다음 예제와 같이 합니다. A **필드** 개체의 선언 된 형식과 **집합이 있으므로 필요** 반환 하는 최대 길이는 50 자는 **DefinedSize** 속성 값이 50, 되지만 ** ActualSize** 반환 되는 속성 값은 현재 레코드의 필드에 저장 된 데이터의 길이입니다. **필드** 와 **DefinedSize** 이상 255 바이트 가변 길이 열으로 처리 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ActualSize 및 DefinedSize 속성 예제 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 및 DefinedSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 속성](../../../ado/reference/ado-api/definedsize-property.md)

