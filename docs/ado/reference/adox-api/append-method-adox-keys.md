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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ea4e06fa790e8a360cfb1254b3064b3b540e7842
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708351"
---
# <a name="append-method-adox-keys"></a>Append 메서드(ADOX 키)
새로 추가 [키](../../../ado/reference/adox-api/key-object-adox.md) 개체를 [키](../../../ado/reference/adox-api/keys-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Key*  
 합니다 **키** 만들고 추가 하는 키의 이름 또는 추가할 개체입니다.  
  
 *KeyType*  
 (선택 사항) A **긴** 키의 형식을 지정 하는 값입니다. *키* 에 해당 하는 매개 변수를 [형식](../../../ado/reference/adox-api/type-property-key-adox.md) 속성을 **키** 개체입니다.  
  
 *열*  
 (선택 사항) A **문자열** 인덱싱할 열 이름을 지정 하는 값입니다. *열* 매개 변수 값에 해당 합니다 [이름](../../../ado/reference/adox-api/name-property-adox.md) 의 속성을 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체입니다.  
  
 *RelatedTable*  
 (선택 사항) A **문자열** 관련된 테이블의 이름을 지정 하는 값입니다. *RelatedTable* 매개 변수 값에 해당 합니다 **이름** 의 속성을 [테이블](../../../ado/reference/adox-api/table-object-adox.md) 개체입니다.  
  
 *RelatedColumn*  
 (선택 사항) A **문자열** 외래 키에 대 한 관련 열의 이름을 지정 하는 값입니다. *RelatedColumn* 매개 변수 값에 해당 합니다 **이름** 의 속성을 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 *열* 열의 이름 또는 열 이름의 배열 매개 변수를 사용할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Keys 컬렉션(ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목  
 [Keys Append 메서드, 키 유형, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append 메서드 (ADOX 열)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 메서드 (ADOX 그룹)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
