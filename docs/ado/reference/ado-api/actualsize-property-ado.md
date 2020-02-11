---
title: ActualSize 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d405113044d10244d8c4fc3483c6220bf630dc5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921429"
---
# <a name="actualsize-property-ado"></a>ActualSize 속성(ADO)
필드 값의 실제 길이 (바이트)를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **Long** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **ActualSize** 속성을 사용 하 여 [필드](../../../ado/reference/ado-api/field-object.md) 개체 값의 실제 길이를 반환 합니다. 모든 필드에 대해 **ActualSize** 속성은 읽기 전용입니다. ADO에서 **필드** 개체 값의 길이를 확인할 수 없는 경우 **ActualSize** 속성은 **adunknown**을 반환 합니다.  
  
 **ActualSize** 및 [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) 속성은 다음 예제와 같이 다릅니다. **AdVarChar** 의 선언 된 형식 및 최대 길이가 50 자인 **Field** 개체는 50의 **DefinedSize** 속성 값을 반환 하지만 반환 하는 **ActualSize** 속성 값은 현재 레코드의 필드에 저장 된 데이터의 길이입니다. **DefinedSize** 가 255 바이트 보다 큰 **필드** 는 가변 길이 열로 처리 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [ActualSize 및 DefinedSize 속성 예제 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 및 DefinedSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 속성](../../../ado/reference/ado-api/definedsize-property.md)
