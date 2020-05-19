---
title: Append 메서드 (ADOX 키) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
author: rothja
ms.author: jroth
ms.openlocfilehash: 5d4797344958391dca278e23be2efafa6d1b3f69
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764034"
---
# <a name="append-method-adox-keys"></a>Append 메서드(ADOX 키)
[키](../../../ado/reference/adox-api/keys-collection-adox.md) 컬렉션에 새 [키](../../../ado/reference/adox-api/key-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *키*  
 추가할 **키** 개체 또는 만들고 추가할 키의 이름입니다.  
  
 *KeyType*  
 (선택 사항) 키의 유형을 지정 하는 **Long** 값입니다. *키* 매개 변수는 **키** 개체의 [Type](../../../ado/reference/adox-api/type-property-key-adox.md) 속성에 해당 합니다.  
  
 *열*  
 (선택 사항) 인덱싱할 열의 이름을 지정 하는 **문자열** 값입니다. *Columns* 매개 변수는 [Column](../../../ado/reference/adox-api/column-object-adox.md) 개체의 [Name](../../../ado/reference/adox-api/name-property-adox.md) 속성 값에 해당 합니다.  
  
 *RelatedTable*  
 (선택 사항) 관련 테이블의 이름을 지정 하는 **문자열** 값입니다. *RelatedTable* 매개 변수는 [Table](../../../ado/reference/adox-api/table-object-adox.md) 개체의 **Name** 속성 값에 해당 합니다.  
  
 *RelatedColumn*  
 (선택 사항) 외래 키에 대 한 관련 열의 이름을 지정 하는 **문자열** 값입니다. *RelatedColumn* 매개 변수는 [Column](../../../ado/reference/adox-api/column-object-adox.md) 개체의 **Name** 속성 값에 해당 합니다.  
  
## <a name="remarks"></a>설명  
 *Columns* 매개 변수는 열 이름 또는 열 이름 배열을 사용할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Keys 컬렉션(ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append 메서드 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
