---
description: DateCreated 속성(ADOX)
title: DateCreated 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ae2c0fcfdc164906f0216abb45f98f705de9cd4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770742"
---
# <a name="datecreated-property-adox"></a>DateCreated 속성(ADOX)
개체를 만든 날짜를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 만든 날짜를 지정 하는 **Variant** 값을 반환 합니다. 공급자가 **DateCreated** 을 지원 하지 않으면 값이 null입니다.  
  
## <a name="remarks"></a>설명  
 새로 추가 된 개체의 **DateCreated** 속성은 null입니다. 새 [뷰나](./view-object-adox.md) [프로시저](./procedure-object-adox.md)를 추가한 후에는 **DateCreated** 속성에 대 한 값을 얻기 위해 [뷰](./views-collection-adox.md) 또는 [프로시저](./procedures-collection-adox.md) 컬렉션의 [Refresh](../ado-api/refresh-method-ado.md) 메서드를 호출 해야 합니다.  
  
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
 [DateModified 속성(ADOX)](./datemodified-property-adox.md)