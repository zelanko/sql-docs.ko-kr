---
description: Count 속성(ADO)
title: Count 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f821642915bdb01e67f673fab871df0541c63ad
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775692"
---
# <a name="count-property-ado"></a>Count 속성(ADO)
컬렉션의 개체 수를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 **Long** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Count** 속성을 사용 하 여 지정 된 컬렉션에 있는 개체 수를 확인 합니다.  
  
 컬렉션 멤버의 번호는 0으로 시작 하므로 항상 0 멤버부터 시작 하 여 **Count** 속성 값에서 1을 뺀 값으로 끝나는 루프를 코딩 해야 합니다. Microsoft Visual Basic를 사용 하 고 **Count** 속성을 확인 하지 않고 컬렉션의 멤버를 반복 하려는 경우 **for Each ...를 사용 하 여 다음** 명령입니다.  
  
 **Count** 속성이 0 이면 컬렉션에 개체가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Axes 컬렉션(ADO MD)](../ado-md-api/axes-collection-ado-md.md)  
        [Columns 컬렉션(ADOX)](../adox-api/columns-collection-adox.md)  
        [CubeDefs 컬렉션(ADO MD)](../ado-md-api/cubedefs-collection-ado-md.md)  
        [Dimensions 컬렉션(ADO MD)](../ado-md-api/dimensions-collection-ado-md.md)  
        [Errors 컬렉션(ADO)](./errors-collection-ado.md)  
        [Fields 컬렉션(ADO)](./fields-collection-ado.md)  
        [Groups 컬렉션(ADOX)](../adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Hierarchies 컬렉션(ADO MD)](../ado-md-api/hierarchies-collection-ado-md.md)  
        [Indexes 컬렉션(ADOX)](../adox-api/indexes-collection-adox.md)  
        [Keys 컬렉션(ADOX)](../adox-api/keys-collection-adox.md)  
        [Levels 컬렉션(ADO MD)](../ado-md-api/levels-collection-ado-md.md)  
        [Members 컬렉션(ADO MD)](../ado-md-api/members-collection-ado-md.md)  
        [Parameters 컬렉션(ADO)](./parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Positions 컬렉션(ADO MD)](../ado-md-api/positions-collection-ado-md.md)  
        [Procedures 컬렉션(ADOX)](../adox-api/procedures-collection-adox.md)  
        [Properties 컬렉션(ADO)](./properties-collection-ado.md)  
        [Tables 컬렉션(ADOX)](../adox-api/tables-collection-adox.md)  
        [Users 컬렉션(ADOX)](../adox-api/users-collection-adox.md)  
        [Views 컬렉션(ADOX)](../adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [Count 속성 예제 (VB)](./count-property-example-vb.md)   
 [Count 속성 예제 (VC + +)](./count-property-example-vc.md)   
 [Refresh 메서드(ADO)](./refresh-method-ado.md)