---
title: 컬렉션 (Visual c + + 구문에 대 한 ADO) | Microsoft Docs
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
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da75220f32fcd90d0785d802b5281cb5016da063
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="collections-ado-for-visual-c-syntax"></a>컬렉션 (Visual c + + 구문에 대 한 ADO)
## <a name="parameters"></a>매개 변수  
  
### <a name="methods"></a>메서드  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Append 메서드(ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete 메서드(ADO 매개 변수 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh 메서드(ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>속성  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Count 속성(ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 속성(ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="fields"></a>필드  
  
### <a name="methods"></a>메서드  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Append 메서드(ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete 메서드(ADO 매개 변수 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh 메서드(ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>속성  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Count 속성(ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 속성(ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="errors"></a>오류  
  
### <a name="methods"></a>메서드  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Clear 메서드(ADO)](../../../ado/reference/ado-api/clear-method-ado.md)  
  
-   [Refresh 메서드(ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>속성  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Count 속성(ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 속성(ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="properties"></a>속성  
  
### <a name="methods"></a>메서드  
  
```  
Refresh(void);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Refresh 메서드(ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>속성  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Count 속성(ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 속성(ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Errors 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
