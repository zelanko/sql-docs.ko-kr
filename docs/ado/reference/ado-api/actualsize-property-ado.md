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
manager: craigg
ms.openlocfilehash: 4676f1d0a9d96779303898631164101bbdc4201d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065411"
---
# <a name="actualsize-property-ado"></a>ActualSize 속성(ADO)
필드의 값 (바이트)의 실제 길이 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 반환 된 **긴** 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 합니다 **ActualSize** 의 실제 길이 반환 하도록 속성을 [필드](../../../ado/reference/ado-api/field-object.md) 개체의 값입니다. 모든 필드에는 **ActualSize** 속성은 읽기 전용입니다. ADO의 길이 확인할 수 없는 경우는 **필드** 개체의 값을 **ActualSize** 속성에서 반환 **adUnknown**합니다.  
  
 합니다 **ActualSize** 및 [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) 속성은 다음 예와에서 같이 다릅니다. **필드** 개체의 선언 형식과 **집합이 있으므로 필요** 최대 길이인 50 자 반환 하 고는 **DefinedSize** 속성 값이 50 하지만  **ActualSize** 반환 하는 속성 값은 현재 레코드의 필드에 저장 된 데이터의 길이입니다. **필드** 사용 하 여는 **DefinedSize** 보다 255 바이트 가변 길이 열으로 처리 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [ActualSize 및 DefinedSize 속성 예제 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 및 DefinedSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 속성](../../../ado/reference/ado-api/definedsize-property.md)
