---
description: DateModified 속성(ADOX)
title: DateModified 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 613dbf829009e4e471844b0d49285817d75316b6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984744"
---
# <a name="datemodified-property-adox"></a>DateModified 속성(ADOX)
개체가 마지막으로 수정 된 날짜를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 수정 된 날짜를 지정 하는 **Variant** 값을 반환 합니다. 공급자가 **DateModified** 을 지원 하지 않으면 값이 null입니다.  
  
## <a name="remarks"></a>설명  
 새로 추가 된 개체의 **DateModified** 속성은 null입니다. 새 [뷰나](./view-object-adox.md) [프로시저](./procedure-object-adox.md)를 추가한 후에는 **DateModified** 속성에 대 한 값을 얻기 위해 [뷰](./views-collection-adox.md) 또는 [프로시저](./procedures-collection-adox.md) 컬렉션의 [Refresh](../ado-api/refresh-method-ado.md) 메서드를 호출 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [프로시저 개체(ADOX)](./procedure-object-adox.md)  
    :::column-end:::
    :::column:::
        [테이블 개체(ADOX)](./table-object-adox.md)  
    :::column-end:::
    :::column:::
        [보기 개체(ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [DateCreated 및 DateModified 속성 예제 (VB)](./datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 속성(ADOX)](./datecreated-property-adox.md)