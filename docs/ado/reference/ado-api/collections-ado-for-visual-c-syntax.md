---
description: 컬렉션(Visual C++ 구문에 대한 ADO)
title: 컬렉션 (Visual C++ 구문에 대 한 ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
author: rothja
ms.author: jroth
ms.openlocfilehash: b4bc59facd753bf6d36c3a79d06a4efe29e7c235
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975384"
---
# <a name="collections-ado-for-visual-c-syntax"></a>컬렉션(Visual C++ 구문에 대한 ADO)
## <a name="parameters"></a>매개 변수  
  
### <a name="methods"></a>메서드  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Append 메서드(ADO)](./append-method-ado.md)  
  
-   [Delete 메서드(ADO 매개 변수 컬렉션)](./delete-method-ado-parameters-collection.md)  
  
-   [Refresh 메서드(ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>속성  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Count 속성(ADO)](./count-property-ado.md)  
  
-   [Item 속성(ADO)](./item-property-ado.md)  
  
## <a name="fields"></a>필드  
  
### <a name="methods"></a>메서드  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Append 메서드(ADO)](./append-method-ado.md)  
  
-   [Delete 메서드(ADO 매개 변수 컬렉션)](./delete-method-ado-parameters-collection.md)  
  
-   [Refresh 메서드(ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>속성  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Count 속성(ADO)](./count-property-ado.md)  
  
-   [Item 속성(ADO)](./item-property-ado.md)  
  
## <a name="errors"></a>오류  
  
### <a name="methods"></a>메서드  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Clear 메서드(ADO)](./clear-method-ado.md)  
  
-   [Refresh 메서드(ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>속성  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Count 속성(ADO)](./count-property-ado.md)  
  
-   [Item 속성(ADO)](./item-property-ado.md)  
  
## <a name="properties"></a>속성  
  
### <a name="methods"></a>메서드  
  
```  
Refresh(void);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Refresh 메서드(ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>속성  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [Count 속성(ADO)](./count-property-ado.md)  
  
-   [Item 속성(ADO)](./item-property-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Errors 컬렉션 (ADO)](./errors-collection-ado.md)   
 [Fields 컬렉션 (ADO)](./fields-collection-ado.md)   
 [Parameters 컬렉션 (ADO)](./parameters-collection-ado.md)   
 [Properties 컬렉션(ADO)](./properties-collection-ado.md)