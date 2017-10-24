---
title: "Column 개체 (ADOX) | Microsoft Docs"
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
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5a8a5047f4cd4655ebe1dd041e44949ca361c54
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="column-object-adox"></a>Column 개체 (ADOX)
테이블, 인덱스 또는 키에서 열을 나타냅니다.  
  
## <a name="remarks"></a>주의  
 다음 코드에서는 새 **열**:  
  
 `Dim obj As New Column`  
  
 속성과 컬렉션을 사용 하 여 한 **열** 개체를 할 수 있습니다.  
  
-   식별 된 열은 [Name 속성 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   사용 하 여 열의 데이터 형식을 지정 된 [Type 속성 (Key) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md) 속성입니다.  
  
-   열이 고정 길이 또는 null 값을 포함할 수 있는 경우 확인 된 [특성 속성 (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md) 속성입니다.  
  
-   사용 하 여 열의 최대 크기 지정은 [DefinedSize 속성 (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md) 속성입니다.  
  
-   숫자 데이터 값을 사용 하 여 배율 지정는 [NumericScale 속성 (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md) 속성입니다.  
  
-   숫자 데이터 값에 대 한 지정 된 최대 전체 자릿수는 [정밀도 속성 (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md) 속성입니다.  
  
-   지정 된 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md) 인 열을 소유 하는 [ParentCatalog 속성 (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) 속성입니다.  
  
-   키 열에 대 한 관련 열의 이름을 포함 하는 관련된 테이블에서 지정 된 [RelatedColumn 속성 (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md) 속성입니다.  
  
-   인덱스 열의 정렬 순서가 오름차순 인지 아니면 내림차순으로 지정 된 [SortOrder 속성 (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md) 속성입니다.  
  
-   사용 하 여 공급자별 속성에 액세스는 [속성 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
> [!NOTE]
>  모든 속성이 **열** 개체는 데이터 공급자에서 지원 될 수 있습니다. 공급자를 지원 하지 않는 속성에 대 한 값을 사용 하도록 설정한 경우 오류가 발생 합니다. 새 **열** 개체는 개체 컬렉션에 추가할 때 오류가 발생 합니다. 기존 개체에 대 한 속성을 설정할 때 오류가 발생 합니다.  
>   
>  만들 때 **열** 개체의 경우에 선택적 속성에 대 한 적절 한 기본값이 있는지 공급자 속성을 지원 하도록 보장 하지 않습니다. 공급자에서 지원 되는 속성에 대 한 자세한 내용은 공급자 설명서를 참조 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Column 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 및 열 이름 속성 예제 (VB) 메서드 추가](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [테이블 형식 속성 예제 (VB) 연결 Close 메서드](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [키 추가 방법, 키 형식, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX 코드 예: NumericScale 및 전체 자릿수 속성 예제 (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 속성 예제 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

