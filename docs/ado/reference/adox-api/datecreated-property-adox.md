---
title: DateCreated 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3b29411e3f1fff9213bdc9bbdfb61c06c78c3e0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="datecreated-property-adox"></a>DateCreated 속성 (ADOX)
개체가 만들어진 날짜를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **Variant** 만든 날짜를 지정 하는 값입니다. 값이 null 경우 **DateCreated** 공급자에서 지원 되지 않습니다.  
  
## <a name="remarks"></a>주의  
 **DateCreated** 속성이 새로 추가 된 개체에 대 한 null입니다. 새 추가 후 [보기](../../../ado/reference/adox-api/view-object-adox.md) 또는 [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md)를 호출 해야 합니다는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 의 메서드는 [뷰](../../../ado/reference/adox-api/views-collection-adox.md) 또는 [프로시저 ](../../../ado/reference/adox-api/procedures-collection-adox.md) 컬렉션에 대 한 값을 가져오려면는 **DateCreated** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Procedure 개체(ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[View 개체(ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [DateCreated 및 DateModified 속성 예제 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified 속성(ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
