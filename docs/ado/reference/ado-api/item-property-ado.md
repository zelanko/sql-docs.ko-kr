---
description: Item 속성(ADO)
title: Item 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameters::GetItem
- Indexes::GetItem
- Parameters::Item
- Tables::Item
- Procedures::Item
- Users::GetItem
- Tables::GetItem
- Procedures::GetItem
- Users::get_Item
- Users::Item
- Views::GetItem
- Groups::Item
- Groups::get_Item
- Columns::Item
- Indexes::Item
- Fields15::GetItem
- Columns::GetItem
- Fields::Item
- Indexes::get_Item
- Columns::get_Item
- Fields15::Item
- Views::get_Item
- Groups::GetItem
- Errors::get_Item
- Fields15::get_Item
- Tables::get_Item
- Views::Item
- Errors::GetItem
- Parameters::get_Item
- Errors::Item
- Procedures::get_Item
helpviewer_keywords:
- Item property [ADO]
ms.assetid: e11484bb-c5c7-42d8-9bb8-21572125d727
author: rothja
ms.author: jroth
ms.openlocfilehash: d2581d0834325d56daa8ea1043ac3915942961eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443405"
---
# <a name="item-property-ado"></a>Item 속성(ADO)
이름 또는 서 수를 기준으로 컬렉션의 특정 멤버를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
Set object = collection.Item ( Index )  
```  
  
## <a name="return-value"></a>Return Value  
 개체 참조를 반환 합니다.  
  
## <a name="parameters"></a>매개 변수  
 *Index*  
 컬렉션에 있는 개체의 이름 또는 서 수로 계산 되는 **변형** 식입니다.  
  
## <a name="remarks"></a>설명  
 **Item** 속성을 사용 하 여 컬렉션에서 특정 개체를 반환 합니다. **항목** 에서 *인덱스* 인수에 해당 하는 컬렉션의 개체를 찾을 수 없는 경우 오류가 발생 합니다. 또한 일부 컬렉션은 명명 된 개체를 지원 하지 않습니다. 이러한 컬렉션의 경우 서 수 참조를 사용 해야 합니다.  
  
 **Item** 속성은 모든 컬렉션에 대 한 기본 속성입니다. 따라서 다음 구문 형식은 서로 바꿔 사용할 수 있습니다.  
  
```  
collection.Item (Index)  
collection (Index)  
```  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Axes 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)  
        [Columns 컬렉션(ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
        [CubeDefs 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)  
        [Dimensions 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)  
        [Errors 컬렉션(ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
        [Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
        [Groups 컬렉션(ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Hierarchies 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)  
        [Indexes 컬렉션(ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
        [Keys 컬렉션(ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
        [Levels 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)  
        [Members 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)  
        [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Positions 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)  
        [Procedures 컬렉션(ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
        [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)  
        [Tables 컬렉션(ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
        [Users 컬렉션(ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
        [Views 컬렉션(ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [Item 속성 예제 (VB)](../../../ado/reference/ado-api/item-property-example-vb.md)   
 [Item 속성 예제(VC++)](../../../ado/reference/ado-api/item-property-example-vc.md)   
