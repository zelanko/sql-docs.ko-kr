---
title: Count 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edda8415ad83ee3aa874ec1e3e6dd6f8e20b41b7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="count-property-ado"></a>Count 속성 (ADO)
컬렉션의 개체 수를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **긴** 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **Count** 속성을 지정된 된 컬렉션에 있는 개체의 수를 확인 합니다.  
  
 컬렉션의 멤버에 대 한 번호는 0부터 시작, 때문에 항상 코드를 작성 해야 루프는 0부터 시작 및 끝 값으로는 **Count** 속성 값-1입니다. Microsoft Visual Basic을 사용 하는 경우 확인 하지 않고 컬렉션의 멤버를 반복 하는 **Count** 속성을 사용 하 여는 **각각에 대해... 다음** 명령입니다.  
  
 경우는 **Count** 속성이 0 이면 컬렉션에는 개체가 있습니다.  
  
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
 [Count 속성 예제 (VB)](../../../ado/reference/ado-api/count-property-example-vb.md)   
 [Count 속성 예제 (VC + +)](../../../ado/reference/ado-api/count-property-example-vc.md)   
 [Refresh 메서드(ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
