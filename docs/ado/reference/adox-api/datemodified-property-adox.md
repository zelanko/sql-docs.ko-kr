---
title: DateModified 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 755697fa07c0b1dd57c3fba658613e9c6cfe30a4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35285622"
---
# <a name="datemodified-property-adox"></a>DateModified 속성 (ADOX)
개체를 마지막으로 수정한 날짜를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **Variant** 수정 된 날짜를 지정 하는 값입니다. 값이 null 경우 **DateModified** 공급자에서 지원 되지 않습니다.  
  
## <a name="remarks"></a>Remarks  
 **DateModified** 속성이 새로 추가 된 개체에 대 한 null입니다. 새 추가 후 [보기](../../../ado/reference/adox-api/view-object-adox.md) 또는 [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md)를 호출 해야 합니다는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 의 메서드는 [뷰](../../../ado/reference/adox-api/views-collection-adox.md) 또는 [프로시저 ](../../../ado/reference/adox-api/procedures-collection-adox.md) 컬렉션에 대 한 값을 가져오려면는 **DateModified** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Procedure 개체(ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[View 개체(ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>관련 항목  
 [DateCreated 및 DateModified 속성 예제 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 속성(ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
