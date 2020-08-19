---
description: 속성 (#import를 사용 하는 Visual C++ 구문 인덱스)
title: 속성 (#import를 사용 하는 Visual C++ 구문 인덱스) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'Property collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 80988ca7-f514-438d-bf6f-9390dfe93fc3
author: rothja
ms.author: jroth
ms.openlocfilehash: 4774f6224a156f11ac4c08c1576321f7dc42986b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442635"
---
# <a name="property-visual-c-syntax-index-with-import"></a>속성 (#import를 사용 하는 Visual C++ 구문 인덱스)
## <a name="properties"></a>속성  
  
```  
long GetAttributes( );  
void PutAttributes( long plAttributes );  
__declspec(property(get=GetAttributes,put=PutAttributes)) long  
    Attributes;  
  
_bstr_t GetName( );  
__declspec(property(get=GetName)) _bstr_t Name;  
  
enum DataTypeEnum GetType( );  
__declspec(property(get=GetType)) enum DataTypeEnum Type;  
  
_variant_t GetValue( );  
void PutValue( const _variant_t & pval );  
__declspec(property(get=GetValue,put=PutValue)) _variant_t Value;  
```  
  
## <a name="see-also"></a>참고 항목  
 [속성 개체(ADO)](../../../ado/reference/ado-api/property-object-ado.md)
