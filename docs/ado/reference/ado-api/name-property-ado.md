---
title: Name 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3717aa3ec95c92500d66c968446f7711a6cd4e74
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828651"
---
# <a name="name-property-ado"></a>Name 속성(ADO)
개체의 이름을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **문자열** 개체의 이름을 나타내는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **이름을** 속성에 이름을 할당의 이름을 검색 하는 **명령**, **속성**, **필드**, 또는 **매개 변수**  개체입니다.  
  
 값은 읽기/쓰기를 **명령** 개체에서 읽기 전용으로 설정 하 고는 **속성** 개체입니다.  
  
 에 대 한는 **필드** 개체를 **이름** 일반적으로 읽기 전용입니다. 그러나에 대 한 새 **필드** 에 추가 된 개체를 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md)를 **이름** 는 읽기/쓰기 후에 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성을 **필드** 지정 된 데이터 공급자에 성공적으로 추가 하 고 **필드** 호출 하 여를 [ 업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 **필드** 컬렉션입니다.  
  
 에 대 한 **매개 변수** 개체에 아직 추가 되지 합니다 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션을 **이름** 속성은 읽기/쓰기입니다. 추가 대 한 **매개 변수** 개체 및 다른 모든 개체를 **이름** 속성은 읽기 전용입니다. 이름은은 컬렉션 내에서 고유할 필요가 없습니다.  
  
 검색할 수 있습니다 합니다 **이름을** 지나면 참조할 수 있습니다 개체 이름으로 직접 서 수 참조를 사용 하 여 개체의 속성입니다. 예를 들어 경우 `rstMain.Properties(20).Name` 생성 `Updatability`, 이후에이 속성을 참조할 수 있습니다 `rstMain.Properties("Updatability")`합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Field 개체](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|[속성 개체(ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Attributes 및 Name 속성 예제 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Attributes 및 Name 속성 예제 (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
