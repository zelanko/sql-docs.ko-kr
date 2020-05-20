---
title: DateModified 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
author: rothja
ms.author: jroth
ms.openlocfilehash: ccd916a8b9e9c500d3b718371b01831cc0ef292f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759209"
---
# <a name="datemodified-property-adox"></a>DateModified 속성(ADOX)
개체가 마지막으로 수정 된 날짜를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 수정 된 날짜를 지정 하는 **Variant** 값을 반환 합니다. 공급자가 **DateModified** 을 지원 하지 않으면 값이 null입니다.  
  
## <a name="remarks"></a>설명  
 새로 추가 된 개체의 **DateModified** 속성은 null입니다. 새 [뷰나](../../../ado/reference/adox-api/view-object-adox.md) [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md)를 추가한 후에는 **DateModified** 속성에 대 한 값을 얻기 위해 [뷰](../../../ado/reference/adox-api/views-collection-adox.md) 또는 [프로시저](../../../ado/reference/adox-api/procedures-collection-adox.md) 컬렉션의 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드를 호출 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Procedure 개체(ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table 개체(ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[View 개체(ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>참고 항목  
 [DateCreated 및 DateModified 속성 예제 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 속성(ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
