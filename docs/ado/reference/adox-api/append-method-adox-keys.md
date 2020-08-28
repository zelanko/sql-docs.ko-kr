---
description: Append 메서드(ADOX 키)
title: Append 메서드 (ADOX 키) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 2531031808c16db4892fb0b759a8a8d819a2222d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985484"
---
# <a name="append-method-adox-keys"></a>Append 메서드(ADOX 키)
[키](./keys-collection-adox.md) 컬렉션에 새 [키](./key-object-adox.md) 개체를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Key*  
 추가할 **키** 개체 또는 만들고 추가할 키의 이름입니다.  
  
 *KeyType*  
 선택 사항입니다. 키의 유형을 지정 하는 **Long** 값입니다. *키* 매개 변수는 **키** 개체의 [Type](./type-property-key-adox.md) 속성에 해당 합니다.  
  
 *열*  
 선택 사항입니다. 인덱싱할 열의 이름을 지정 하는 **문자열** 값입니다. *Columns* 매개 변수는 [Column](./column-object-adox.md) 개체의 [Name](./name-property-adox.md) 속성 값에 해당 합니다.  
  
 *RelatedTable*  
 선택 사항입니다. 관련 테이블의 이름을 지정 하는 **문자열** 값입니다. *RelatedTable* 매개 변수는 [Table](./table-object-adox.md) 개체의 **Name** 속성 값에 해당 합니다.  
  
 *RelatedColumn*  
 선택 사항입니다. 외래 키에 대 한 관련 열의 이름을 지정 하는 **문자열** 값입니다. *RelatedColumn* 매개 변수는 [Column](./column-object-adox.md) 개체의 **Name** 속성 값에 해당 합니다.  
  
## <a name="remarks"></a>설명  
 *Columns* 매개 변수는 열 이름 또는 열 이름 배열을 사용할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Keys 컬렉션(ADOX)](./keys-collection-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append 메서드 (ADOX Columns)](./append-method-adox-columns.md)   
 [Append 메서드 (ADOX Groups)](./append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](./append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 프로시저)](./append-method-adox-procedures.md)   
 [Append 메서드 (ADOX Tables)](./append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](./append-method-adox-users.md)   
 [Append 메서드(ADOX 보기)](./append-method-adox-views.md)