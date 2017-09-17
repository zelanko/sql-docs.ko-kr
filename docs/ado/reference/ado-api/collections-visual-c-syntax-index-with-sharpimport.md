---
title: "컬렉션 (Visual c + + 구문 있는 인덱스 #import) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 093e3933796d490f2dc40d8af493dc639fdb19a3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="collections-visual-c-syntax-index-with-import"></a>컬렉션 (Visual c + + 구문 인덱스 #import 사용)
컬렉션 특정 공용 메서드와 속성을 상속 한다는 알아야는 것이 유용 합니다.  
  
 모든 컬렉션 상속는 **Count** 속성 및 **새로 고침** 메서드 및 모든 컬렉션에 추가 **항목** 속성입니다. **오류** 추가 하는 컬렉션의 **지우기** 메서드. **매개 변수** 컬렉션 상속는 **Append** 및 **삭제** 메서드 동안는 **필드** 컬렉션 추가 **Append**, **삭제**, 및 **업데이트** 메서드.  
  
## <a name="properties-collection"></a>속성 컬렉션  
  
### <a name="methods"></a>메서드  
  
```  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>속성  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="errors-collection"></a>오류 컬렉션  
  
### <a name="methods"></a>메서드  
  
```  
HRESULT Clear( );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>속성  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="parameters-collection"></a>Parameters 컬렉션  
  
### <a name="methods"></a>메서드  
  
```  
HRESULT Append( IDispatch * Object );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>속성  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="fields-collection"></a>Fields 컬렉션  
  
### <a name="methods"></a>메서드  
  
```  
HRESULT Append( _bstr_t Name, enum DataTypeEnum Type, long DefinedSize, enum FieldAttributeEnum Attrib, const _variant_t & FieldValue = vtMissing );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
HRESULT Update( );  
```  
  
### <a name="properties"></a>속성  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Errors 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
