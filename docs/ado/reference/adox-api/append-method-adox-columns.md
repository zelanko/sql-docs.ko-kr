---
title: "Append 메서드 (ADOX 열) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords: Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c9efd9a8f7333bf2cfeb649bf1a1db32de37c3c3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="append-method-adox-columns"></a>Append 메서드 (ADOX 열)
새로 추가 [열](../../../ado/reference/adox-api/column-object-adox.md) 개체는 [열](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>매개 변수  
 *열*  
 **열** 추가할 개체 또는 새로 만들어 추가할 열의 이름입니다.  
  
 *형식*  
 (선택 사항) A **긴** 열의 데이터 형식을 지정 하는 값입니다. *형식* 에 해당 하는 매개 변수는 [형식](../../../ado/reference/adox-api/type-property-column-adox.md) 속성은 **열** 개체입니다.  
  
 *DefinedSize*  
 (선택 사항) A **긴** 열 크기를 지정 하는 값입니다. *DefinedSize* 에 해당 하는 매개 변수는 [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) 속성은 **열** 개체입니다.  
  
> [!NOTE]
>  추가할 때 오류가 발생 합니다는 **열** 에 **열** 컬렉션은 [인덱스](../../../ado/reference/adox-api/index-object-adox.md) 경우는 **열** 는 에존재하지않는[테이블](../../../ado/reference/adox-api/table-object-adox.md) 이미에 추가 된는 [테이블](../../../ado/reference/adox-api/tables-collection-adox.md) 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Columns 컬렉션(ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 열 이름 속성 예제 (VB) 메서드 추가](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [키 추가 방법, 키 형식, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append 메서드 (ADOX 그룹)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 메서드 (ADOX 인덱스)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 메서드 (ADOX 키)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 메서드 (ADOX 프로시저)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 메서드 (ADOX 테이블)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 메서드 (ADOX 사용자)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 메서드(ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
