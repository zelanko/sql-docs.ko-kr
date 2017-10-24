---
title: "Item 속성 (ADO) | Microsoft Docs"
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
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 59779714027c0ff619293d01de851daec7bbe158
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="item-property-ado"></a>Item 속성 (ADO)
이름 또는 서 수는 컬렉션의 특정 멤버를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
Set object = collection.Item ( Index )  
```  
  
## <a name="return-value"></a>반환 값  
 개체 참조를 반환합니다.  
  
## <a name="parameters"></a>매개 변수  
 *인덱스*  
 A **Variant** 은 이름 또는 컬렉션에 있는 개체의 서 수를 계산 되는 식입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **항목** 속성을 컬렉션에서 특정 개체를 반환 합니다. 경우 **항목** 에 해당 하는 컬렉션에서 개체를 찾을 수 없습니다는 *인덱스* 인수, 오류가 발생 합니다. 또한 일부 컬렉션; 명명 된 개체를 지원 하지 않습니다. 이러한 컬렉션에 대 한 서 수 참조를 사용 해야 합니다.  
  
 **항목** 속성은 모든 컬렉션에 대 한 기본 속성; 따라서 다음 구문 형식은 서로 전환이 가능 합니다.  
  
```  
collection.Item (Index)  
collection (Index)  
```  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Axes 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Columns 컬렉션(ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Dimensions 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Errors 컬렉션(ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Groups 컬렉션(ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Indexes 컬렉션(ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys 컬렉션(ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Levels 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Members 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Positions 컬렉션(ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Procedures 컬렉션(ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Tables 컬렉션(ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Users 컬렉션(ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Views 컬렉션(ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>관련 항목:  
 [항목 속성 예제 (VB)](../../../ado/reference/ado-api/item-property-example-vb.md)   
 [Item 속성 예제(VC++)](../../../ado/reference/ado-api/item-property-example-vc.md)   

