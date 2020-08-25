---
description: 열 개체(ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f620dd4c8c8c5b3e00c8875b18686259d71429d7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771122"
---
# <a name="column-object-adox"></a>열 개체(ADOX)
테이블, 인덱스 또는 키에서 열을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 다음 코드는 새 **열**을 만듭니다.  
  
 `Dim obj As New Column`  
  
 **열** 개체의 속성 및 컬렉션을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name 속성 (ADOX)](./name-property-adox.md) 속성을 사용 하 여 열을 식별 합니다.  
  
-   [유형 속성 (키) (ADOX)](./type-property-key-adox.md) 속성을 사용 하 여 열의 데이터 형식을 지정 합니다.  
  
-   열이 고정 길이 인지 확인 하거나 [Attributes 속성 (ADOX)](./attributes-property-adox.md) 속성을 사용 하 여 null 값을 포함할 수 있는지 확인 합니다.  
  
-   [DefinedSize 속성 (ADOX)](./definedsize-property-adox.md) 속성을 사용 하 여 열의 최대 크기를 지정 합니다.  
  
-   숫자 데이터 값에 대해 [NumericScale 속성 (ADOX)](./numericscale-property-adox.md) 속성을 사용 하 여 소수 자릿수를 지정 합니다.  
  
-   숫자 데이터 값에는 [Precision 속성 (ADOX)](./precision-property-adox.md) 속성을 사용 하 여 최대 전체 자릿수를 지정 합니다.  
  
-   [ParentCatalog 속성 (adox)](./parentcatalog-property-adox.md) 속성을 사용 하 여 열을 소유 하는 [카탈로그 개체 (adox)](./catalog-object-adox.md) 를 지정 합니다.  
  
-   키 열의 경우 [RelatedColumn property (ADOX)](./relatedcolumn-property-adox.md) 속성을 사용 하 여 관련 테이블의 관련 열 이름을 지정 합니다.  
  
-   인덱스 열의 경우 정렬 순서가 [SortOrder 속성 (ADOX)](./sortorder-property-adox.md) 속성을 사용 하 여 오름차순 인지 또는 내림차순 인지를 지정 합니다.  
  
-   [속성 컬렉션 (ADO)](../ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 공급자별 속성에 액세스 합니다.  
  
> [!NOTE]
>  데이터 공급자가 **열** 개체의 모든 속성을 지원할 수 있는 것은 아닙니다. 공급자가 지원 하지 않는 속성에 대 한 값을 설정 하면 오류가 발생 합니다. 새 **열** 개체의 경우 개체가 컬렉션에 추가 되 면 오류가 발생 합니다. 기존 개체의 경우 속성을 설정할 때 오류가 발생 합니다.  
>   
>  **열** 개체를 만들 때 선택적 속성에 대해 적절 한 기본값이 있으면 공급자가 속성을 지원 하지 않을 수 있습니다. 공급자가 지 원하는 속성에 대 한 자세한 내용은 공급자 설명서를 참조 하십시오.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [열 개체 속성, 메서드 및 이벤트](./column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Columns 및 Tables Append 메서드, Name 속성 예제 (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 메서드, Table Type 속성 예제 (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX 코드 예제: NumericScale 및 Precision 속성 예제 (VB)](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [ParentCatalog 속성 예제 (VB)](./parentcatalog-property-example-vb.md)   
 [SortOrder 속성 예제 (VB)](./sortorder-property-example-vb.md)   
 [Columns 컬렉션 (ADOX)](./columns-collection-adox.md)   
 [Properties 컬렉션(ADO)](../ado-api/properties-collection-ado.md)