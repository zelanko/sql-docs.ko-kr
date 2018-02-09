---
title: "Name 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eac3504e262f52700351c9d4313ed39d9723c844
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="name-property-ado"></a>Name 속성 (ADO)
개체의 이름을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 개체의 이름을 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **이름** 속성을 할당 하는 이름 또는의 이름을 검색 한 **명령**, **속성**, **필드**, 또는 **매개 변수**  개체입니다.  
  
 에 값은 읽기/쓰기는 **명령** 개체에서 읽기 전용 및는 **속성** 개체입니다.  
  
 에 대 한는 **필드** 개체 **이름** 일반적으로 읽기 전용입니다. 그러나에 대 한 새로운 **필드** 에 추가 된 개체는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md), **이름** 은 읽기/쓰기 후에 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성에 대 한는 **필드** 지정 된 데이터 공급자가 성공적으로 새 추가 하 고 **필드** 호출 하 여는 [ 업데이트](../../../ado/reference/ado-api/update-method.md) 의 메서드는 **필드** 컬렉션입니다.  
  
 에 대 한 **매개 변수** 개체에 아직 추가 되지는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션은 **이름** 속성은 읽기/쓰기가 가능 합니다. 추가 대 한 **매개 변수** 개체 및 다른 모든 개체는 **이름** 속성은 읽기 전용입니다. 이름은은 컬렉션 내에서 고유할 필요가 없습니다.  
  
 검색할 수 있습니다는 **이름** 을 참조할 수 있습니다를 개체 이름으로 직접 서 수 참조를 사용 하 여 개체의 속성입니다. 예를 들어 경우 `rstMain.Properties(20).Name` 생성 `Updatability`, 이후에로이 속성을 참조할 수 있습니다 `rstMain.Properties("Updatability")`합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Field 개체](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|[속성 개체(ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [특성 및 이름 속성 예 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [특성 및 이름 속성 예 (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
