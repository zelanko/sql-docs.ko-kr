---
title: Column 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db2c2dbe6af2a50fc2507a9ade92d83e0502f2ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966915"
---
# <a name="column-object-adox"></a>열 개체(ADOX)
테이블, 인덱스 또는 키에서 열을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 다음 코드를 만듭니다 **열**:  
  
 `Dim obj As New Column`  
  
 속성 및 컬렉션을 **열** 개체를 할 수 있습니다.  
  
-   사용 하 여 열을 식별 합니다 [이름 속성 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   사용 하 여 열의 데이터 형식을 지정 합니다 [Type 속성 (키) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md) 속성입니다.  
  
-   열이 고정 길이 또는 null 값을 포함할 수 있는 경우를 확인 합니다 [특성 속성 (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md) 속성입니다.  
  
-   사용 하 여 열의 최대 크기를 지정 합니다 [DefinedSize 속성 (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md) 속성입니다.  
  
-   숫자 데이터 값에 대 한 사용 하 여 눈금을 지정 합니다 [NumericScale 속성 (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md) 속성입니다.  
  
-   숫자 데이터 값을 사용 하 여 최대 전체 자릿수를 지정 합니다 [전체 자릿수 속성 (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md) 속성입니다.  
  
-   지정 된 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md) 인 열을 소유 하는 합니다 [ParentCatalog 속성 (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) 속성.  
  
-   키 열에 대 한 관련 열의 이름을 사용 하 여 관련된 테이블에 지정 된 [RelatedColumn 속성 (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md) 속성입니다.  
  
-   인덱스 열의 정렬 순서가 오름차순 이나 내림차순으로 하는지 여부를 지정 합니다 [SortOrder 속성 (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md) 속성입니다.  
  
-   공급자별 속성에 액세스 합니다 [속성 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
> [!NOTE]
>  속성 중 일부만 **열** 데이터 공급자에서 지원 되는 개체입니다. 공급자를 지원 하지 않는 속성의 값을 사용 하도록 설정한 경우 오류가 발생 합니다. 새로운 **열** 개체는 개체 컬렉션에 추가할 때 오류가 발생 합니다. 기존 개체에 대 한 속성을 설정할 때 오류가 발생 합니다.  
>   
>  만들면 **열** 개체 선택적 속성에 대 한 적절 한 기본값이 있는지 공급자 속성을 지원 하도록 보장 하지 않습니다. 공급자에서 지원 되는 속성에 대 한 자세한 내용은 공급자 설명서를 참조 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Column 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 메서드, 키 유형, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX 코드 예제: NumericScale 및 Precision 속성 예제 (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 속성 예제 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Properties 컬렉션(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
