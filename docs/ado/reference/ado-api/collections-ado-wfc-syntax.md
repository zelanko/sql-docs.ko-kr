---
title: 컬렉션 (ADO-WFC 구문) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- syntax indexes [ADO], ADO/WFC
- collections [ADO], ADO/WFC syntax
- ADO/WFC syntax index [ADO]
ms.assetid: 073f9a0e-c755-42dd-9f71-4647d68e331a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 943fdce253fe7197d5ac8793502bfe707cbb10ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699019"
---
# <a name="collections-ado---wfc-syntax"></a>컬렉션(ADO - WFC 구문)
**package com.ms.wfc.data**  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="methods"></a>메서드  
  
```  
public void append(com.ms.wfc.data.Parameter param)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public Parameter getItem(int n)  
public Parameter getItem(String s)  
```  
  
### <a name="properties"></a>속성  
  
```  
public int getCount()  
```  
  
## <a name="fields"></a>필드  
  
### <a name="methods"></a>메서드  
  
```  
public void append(String name, int type)  
public void append(String name, int type, int definedSize)  
public void append(String name, int type, int definedSize, int attrib)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public com.ms.wfc.data.Field getItem(int n)  
public com.ms.wfc.data.Field getItem(String s)  
```  
  
### <a name="properties"></a>속성  
  
```  
public int getCount()  
```  
  
## <a name="errors"></a>오류  
  
### <a name="methods"></a>메서드  
  
```  
public void clear()  
public void refresh()  
public com.ms.wfc.data.Error getItem(int n)  
public com.ms.wfc.data.Error getItem(String s)  
```  
  
### <a name="properties"></a>속성  
  
```  
public int getCount()  
```  
  
## <a name="see-also"></a>관련 항목  
 [Errors 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [필드 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
