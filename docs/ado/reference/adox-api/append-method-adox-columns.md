---
title: Append 메서드 (ADOX 열) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6493157c00e5a71c7c2f085191231bb33bb5279a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967329"
---
# <a name="append-method-adox-columns"></a>Append 메서드(ADOX 열)
새로 추가 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체를 [열](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *열*  
 합니다 **열** 추가할 개체나 새로 만들어 추가할 열의 이름입니다.  
  
 *형식*  
 (선택 사항) A **긴** 열의 데이터 형식을 지정 하는 값입니다. *형식* 에 해당 하는 매개 변수를 [형식](../../../ado/reference/adox-api/type-property-column-adox.md) 속성을 **열** 개체입니다.  
  
 *DefinedSize*  
 (선택 사항) A **긴** 열의 크기를 지정 하는 값입니다. 합니다 *DefinedSize* 에 해당 하는 매개 변수를 [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) 속성을 **열** 개체입니다.  
  
> [!NOTE]
>  추가할 때 오류가 발생 합니다는 **열** 에 **열** 의 컬렉션은 [인덱스](../../../ado/reference/adox-api/index-object-adox.md) 경우를 **열** 를 에존재하지않는[표](../../../ado/reference/adox-api/table-object-adox.md) 에 이미 추가 된는 [테이블](../../../ado/reference/adox-api/tables-collection-adox.md) 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Columns 컬렉션(ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys Append 메서드, 키 유형, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append 메서드 (ADOX 그룹)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
