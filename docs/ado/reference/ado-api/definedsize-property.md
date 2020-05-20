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
author: rothja
ms.author: jroth
ms.openlocfilehash: 08a7842a2fbfb2bd34f02ad2e45871132111a68f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757399"
---
# <a name="definedsize-property"></a>DefinedSize 속성
[필드](../../../ado/reference/ado-api/field-object.md) 개체의 데이터 용량을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 필드 개체의 데이터 형식에 따라 결정 되는 필드의 정의 된 크기를 반영 하는 **Long** 값을 반환 합니다. 자세한 내용은 [형식](../../../ado/reference/ado-api/type-property-ado.md) 을 참조 하세요. 고정 길이 데이터 형식을 사용 하는 필드의 경우 반환 값은 데이터 형식의 크기 (바이트)입니다. 가변 길이 데이터 형식을 사용 하는 필드의 경우 다음 중 하나입니다.  
  
1.  필드의 최대 길이 ( **adVarChar** 및 **adVarWChar**의 경우) 또는 바이트 ( **adVarBinary**의 경우) 또는 (예: **) 필드**의 길이가 정의 된 경우입니다. 예를 들어 **adVarChar (5)** 필드의 최대 길이는 5입니다.  
  
2.  필드에 정의 된 길이가 없는 경우 문자 ( **Adchar** 및 **adchar**의 경우) 또는 바이트 ( **adchar** 및 **adchar**의 경우)에 있는 데이터 형식의 최대 길이입니다.  
  
3.  ~ 0 (비트, 값은 0이 아닙니다. 모든 비트가 1로 설정 됩니다. 필드와 데이터 형식이 모두 정의 된 최대 길이를 갖고 있지 않은 경우).  
  
4.  길이가 없는 데이터 형식의 경우이 값은 ~ 0 (비트)으로 설정 되 고 값이 0이 아닌 경우 모든 비트가 1로 설정 됩니다.  
  
## <a name="remarks"></a>설명  
 **DefinedSize** 속성을 사용 하 여 **필드** 개체의 데이터 용량을 확인 합니다.  
  
 **DefinedSize** 및 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) 속성이 다릅니다. 예를 들어 **adVarChar** 의 선언 된 형식이 있는 **Field** 개체와 단일 문자를 포함 하는 **DefinedSize** 속성 값 50이 있다고 가정 합니다. 반환 되는 **ActualSize** 속성 값은 단일 문자의 바이트 길이입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [ActualSize 및 DefinedSize 속성 예제 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 및 DefinedSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize 속성(ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
