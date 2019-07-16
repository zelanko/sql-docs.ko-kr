---
title: Value 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e35dd93e6d90a81934d8f272ea79c5eb7c8a97c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913919"
---
# <a name="value-property-ado"></a>Value 속성(ADO)

에 할당 된 값을 나타내는 [필드](../../../ado/reference/ado-api/field-object.md)를 [매개 변수](../../../ado/reference/ado-api/parameter-object.md), 또는 [속성](../../../ado/reference/ado-api/property-object-ado.md) 개체입니다.
  
## <a name="settings-and-return-values"></a>설정 및 반환 값

설정 하거나 반환을 **Variant** 개체의 값을 나타내는 값입니다. 기본값에 따라 달라 집니다 합니다 [형식](../../../ado/reference/ado-api/type-property-ado.md) 속성입니다.
  
## <a name="remarks"></a>설명

사용 합니다 **값** 속성을 설정 하거나 데이터를 반환 **필드** 개체를 설정 하거나 매개 변수 값을 반환 **매개 변수** 개체를 설정 하거나 사용 하 여 속성 설정을 반환 하려면 또는 **속성** 개체입니다. 여부는 **값** 속성이 읽기/쓰기 또는 읽기 전용으로 다양 한 요인에 따라 다릅니다. 자세한 내용은 해당 개체 항목을 참조 하세요.

ADO 허용 설정 및 사용 하 여 긴 이진 데이터를 반환 합니다 **값** 속성입니다.
  
> [!NOTE]
> 에 대 한 **매개 변수** 개체, ADO 읽기 합니다 **값** 속성 공급자에서 한 번만 합니다. 명령에 포함 된 경우는 **매개 변수** 인 **값** 속성은 비어 있으며 만든를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 명령에서 먼저 닫아야 하는 확인을  **레코드 집합** 를 검색 하기 전에 **값** 속성입니다. 일부 공급자에 대 한이 고, 그렇지 합니다 **값** 속성이 비어 있을 수 및 올바른 값이 포함 되지 않습니다.
> 
> 새로운 **필드** 에 추가 된 개체를 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체를 **값** 속성을 설정 해야 합니다 다른 하기 전에 **필드** 속성을 지정할 수 있습니다. 첫 번째, 특정 값에 대 한는 **값** 속성 할당 받아야 및 [업데이트](../../../ado/reference/ado-api/update-method.md) 에 **필드** 라는 컬렉션입니다. 와 같은 다른 속성에 차례로 [형식](../../../ado/reference/ado-api/type-property-ado.md) 또는 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 액세스할 수 있습니다.
  
## <a name="applies-to"></a>적용 대상
  
||||  
|-|-|-|  
|[Field 개체](../../../ado/reference/ado-api/field-object.md)|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|[속성 개체(ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>관련 항목

[속성 예제 (VB)를 값](../../../ado/reference/ado-api/value-property-example-vb.md)
[값 속성 예제 (VC + +)](../../../ado/reference/ado-api/value-property-example-vc.md) 
