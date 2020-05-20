---
title: Collections (#import를 사용 하는 Visual C++ 구문 인덱스) | Microsoft Docs
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
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
author: rothja
ms.author: jroth
ms.openlocfilehash: 9142282c2ee2cda5a2b545a3ef164581403ccba3
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758819"
---
# <a name="collections-visual-c-syntax-index-with-import"></a>Collections (#import를 사용 하는 Visual C++ 구문 인덱스)
컬렉션이 특정 공용 메서드 및 속성을 상속 한다는 것을 알고 있으면 유용 합니다.  
  
 모든 컬렉션은 **Count** 속성과 **Refresh** 메서드를 상속 하 고 모든 컬렉션은 **Item** 속성을 추가 합니다. **Errors** 컬렉션은 **Clear** 메서드를 추가 합니다. **Parameters** 컬렉션은 **append** 및 **delete** 메서드를 상속 하는 반면, **Fields** 컬렉션은 추가, **삭제**및 **업데이트** 메서드를 추가 합니다. **Append**  
  
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
  
## <a name="errors-collection"></a>Errors 컬렉션  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Errors 컬렉션 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
