---
title: FOR XML에서 EXPLICIT 모드 사용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- EXPLICIT FOR XML mode
- FOR XML clause, EXPLICIT mode
- FOR XML EXPLICIT mode
ms.assetid: 8b26e8ce-5465-4e7a-b237-98d0f4578ab1
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 58e0ac44e282d6d2de4b989cd0e0940aa3b6866c
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889699"
---
# <a name="use-explicit-mode-with-for-xml"></a>FOR XML에서 EXPLICIT 모드 사용
  [FOR XML을 사용하는 XML 생성](../xml/for-xml-sql-server.md)항목에 설명된 것과 같이 RAW 및 AUTO 모드에서는 쿼리 결과로 생성되는 XML의 모양을 상세하게 조정할 수 없습니다. 하지만 EXPLICIT 모드에서는 쿼리 결과로 생성되는 XML의 모양을 좀 더 상세하게 조정할 수 있습니다.  
  
 XML에 예상되는 중첩과 같은 필수 XML에 대한 추가 정보는 쿼리의 일부로 명시적으로 지정하는 방식으로 EXPLICIT 모드 쿼리를 작성해야 합니다. 요청한 XML에 따라 EXPLICIT 모드 쿼리를 작성하는 작업은 복잡할 수 있습니다. EXPLICIT 모드 쿼리를 작성하는 것보다는 [PATH 모드 사용](../xml/use-path-mode-with-for-xml.md) 의 설명에 따라 중첩을 사용하는 것이 더 간단합니다.  
  
 EXPLICIT 모드에서 쿼리의 일부로 원하는 XML을 기술하기 때문에 생성된 XML은 형식이 올바르고 유효해야 합니다.  
  
## <a name="rowset-processing-in-explicit-mode"></a>EXPLICIT 모드의 행 집합 처리  
 EXPLICIT 모드는 쿼리 실행으로부터 만들어지는 행 집합을 XML 문서로 변환합니다. EXPLICIT 모드의 경우 XML문서를 만들기 위해서는 행 집합이 특정 형식을 가져야 합니다. 이를 위해서는 처리 논리에서 원하는 XML을 생성할 수 있도록 특정 형식을 지닌 행 집합인 **범용 테이블**을 생성하는 SELECT 쿼리를 작성해야 합니다.  
  
 먼저 쿼리는 다음 두 메타데이터 열을 생성해야 합니다.  
  
-   첫 번째 열은 현재 요소에 대한 정수 형식의 태그 번호를 제공해야 하며 열 이름은 **Tag**여야 합니다. 쿼리에서는 행 집합으로부터 생성될 각 요소의 고유 태그 번호를 제공해야 합니다.  
  
-   두 번째 열은 부모 요소의 태그 번호를 제공해야 하며 이 열 이름은 **Parent**여야 합니다. 이러한 빙식으로 Tag 및 Parent 열은 계층 정보를 제공합니다.  
  
 이러한 메타데이터 열 값은 열 이름의 정보와 함께 원하는 XML을 생성하는 데 사용됩니다. 쿼리에서는 특정 방식으로 열 이름을 제공해야 합니다. 또한 **Parent** 열에 있는 0 또는 NULL은 해당 요소에 부모가 없음을 나타냅니다. 요소는 최상위 요소로 XML에 추가됩니다.  
  
 쿼리에 의해 생성된 범용 열이 XML 결과를 생성하도록 처리되는 방법을 이해하려면 이 범용 테이블을 생성하는 쿼리를 작성했다고 가정해 보십시오.  
  
 ![예제 범용 테이블](../../database-engine/media/xmlutable.gif "Sample universal table")  
  
 이 범용 테이블에 대해 다음 사항을 유의하십시오.  
  
-   처음 두 열은 **Tag** 및 **Parent** 이며 메타 열입니다. 이러한 값은 계층을 결정합니다.  
  
-   열 이름은 이 항목의 후반에 설명된 바와 같은 특정 방식으로 지정됩니다.  
  
-   이 범용 테이블로부터 XML을 생성할 때 이 테이블의 데이터는 열 그룹으로 수직 분할됩니다. 그룹화는 **Tag** 값 및 열 이름에 따라 결정됩니다. XML을 생성할 때 처리 논리는 각 행에 대해 하나의 열 그룹을 선택하고 요소를 생성합니다. 이 예에서는 다음 사항이 적용됩니다.  
  
    -   첫 번째 행에 있는 **Tag** 열 값 1에 대해 이름에 동일한 태그 번호 **Customer!1!cid** 및 **Customer!1!name**이 포함된 열은 하나의 그룹을 형성합니다. 이러한 열은 행을 처리하는 데 사용되며 생성된 요소의 모양은 <`Customer id=... name=...`>임을 알 수 있습니다. 열 이름 형식은 이 항목의 후반에 설명됩니다.  
  
    -   **Tag** 열 값이 2인 행에 대해 **Order!2!id** 및 **Order!2!date** 열은 이후에 <`Order id=... date=... /`> 요소를 생성하는 데 사용되는 그룹을 형성합니다.  
  
    -   **Tag** 열 값이 3인 행에 대해 **OrderDetail!3!id!id** 및 **OrderDetail!3!pid!idref** 열은 그룹을 형성합니다. 이러한 각 행은 이러한 열로부터 <`OrderDetail id=... pid=...`> 요소를 생성합니다.  
  
-   XML 계층을 생성할 때 행은 순서대로 처리됩니다. XML 계층은 다음과 같이 결정됩니다.  
  
    -   첫 번째 행은 **Tag** 값 1과 **Parent** 값 NULL을 지정합니다. 따라서 해당 요소인 <`Customer`> 요소는 XML에서 최상위 요소로 추가됩니다.  
  
        ```  
        <Customer cid="C1" name="Janine">  
        ```  
  
    -   두 번째 행은 **Tag** 값 2와 **Parent** 값 1을 식별합니다. 따라서 <`Order`> 요소는 <`Customer`> 요소의 자식으로 추가됩니다.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
        ```  
  
    -   다음 두 행은 **Tag** 값 3과 **Parent** 값 2를 식별합니다. 따라서 두 <`OrderDetail`> 요소는 <`Order`> 요소의 자식으로 추가됩니다.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
        ```  
  
    -   마지막 행은 **Tag** 번호로 2를 식별하고 **Parent** 태그 번호로 1을 식별합니다. 따라서 다른 <`Order`> 요소 자식이 <`Customer`> 부모 요소에 추가됩니다.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
           </Order>  
           <Order id="O2" date="3/29/1997">  
        </Customer>  
        ```  
  
 요약하면 EXPLICIT 모드에서는 **Tag** 및 **Parent** 메타 열의 값과 열 이름에 제공된 정보 및 행의 올바른 순서로 원하는 XML이 생성됩니다.  
  
### <a name="universal-table-row-ordering"></a>범용 테이블 행 순서 지정  
 XML을 생성할 때 범용 테이블의 행은 순서대로 처리됩니다. 따라서 해당 부모와 연결된 올바른 자식 요소를 검색하려면 각 부모 노드 바로 다음에 해당 자식 노드가 오도록 행 집합의 행 순서를 지정해야 합니다.  
  
## <a name="specifying-column-names-in-a-universal-table"></a>범용 테이블에 열 이름 지정  
 EXPLICIT 모드 쿼리를 작성할 때 결과 행 집합에 있는 열 이름은 다음 형식에 따라 지정되어야 합니다. 이러한 형식은 지시어를 사용하여 지정된 요소 및 특성 이름과 기타 추가 정보를 포함하는 변환 정보를 제공합니다.  
  
 일반 형식은 다음과 같습니다.  
  
```  
  
ElementName!TagNumber!AttributeName!Directive  
```  
  
 다음은 형식의 각 부분에 대한 설명입니다.  
  
 *ElementName*  
 요소의 일반적인 결과 식별자입니다. 예를 들어 **Customers**가 *ElementName*으로 지정된 경우 \<Customers> 요소가 생성됩니다.  
  
 *TagNumber*  
 요소에 할당된 고유 태그 값입니다. 이 값은 두 메타데이터 열인 **Tag** 및 **Parent**를 통해 결과 XML에서의 요소 중첩을 결정합니다.  
  
 *AttributeName*  
 지정된 *ElementName*을 생성하기 위해 특성 이름을 제공합니다. 이 동작은 *Directive* 가 지정되지 않은 경우의 동작입니다.  
  
 *Directive* 가 지정되어 있고 **xml**, **cdata**또는 **element**인 경우 이 값은 *ElementName*의 요소 자식을 생성하는 데 사용되고 열 값이 여기에 추가됩니다.  
  
 *Directive*를 지정하면 *AttributeName* 을 비워 둘 수 있습니다. 예를 들면 ElementName!TagNumber!!Directive와 같습니다. 이 경우 열 값은 *ElementName*에 직접 포함됩니다.  
  
 *Directive*  
 *Directive* 는 선택 항목으로서 XML 생성을 위한 추가 정보를 제공하는 데 사용할 수 있습니다. *Directive* 에는 두 가지 용도가 있습니다.  
  
 하나는 값을 ID, IDREF 및 IDREFS로 인코딩하는 것입니다. **ID**, **IDREF**및 **IDREFS** 키워드를 *Directive*로 지정할 수 있습니다. 이러한 지시어는 특성 유형을 덮어씁니다. 이렇게 하면 문서 간 연결을 만들 수 있습니다.  
  
 또한 *Directive* 를 사용하여 문자열 데이터를 XML로 매핑하는 방법을 나타낼 수 있습니다. **hide**, **element, elementxsinil**, **xml**, **xmltext**및 **cdata** 키워드는 *Directive*로 사용될 수 있습니다. **hide** 지시어는 노드를 숨깁니다. 이 키워드는 정렬 목적으로만 값을 검색하고 결과 XML에는 표시되지 않도록 하려는 경우에 유용합니다.  
  
 **element** 지시어는 특성 대신 포함된 요소를 생성합니다. 포함된 데이터는 엔터티로 인코딩됩니다. 예를 들어 **<** 문자는 &lt;가 됩니다. NULL 열 값에 대해 경우 요소가 생성되지 않습니다. Null 열 값에 대해 요소를 생성하려면 **elementxsinil** 지시어를 지정합니다. 이렇게 하면 특성이 xsi:nil=TRUE인 요소가 생성됩니다.  
  
 **xml** 지시어는 **element** 지시어와 비슷하지만 엔터티 인코딩이 발생하지 않는다는 점이 다릅니다. **element** 지시어는 **ID**, **IDREF**또는 **IDREFS**와 조합될 수 있지만 **xml** 지시어는 **hide**를 제외한 다른 지시어와는 조합될 수 없습니다.  
  
 **cdata** 지시어는 CDATA 섹션으로 데이터를 묶어서 포함시킵니다. 내용은 인코딩된 엔터티가 아닙니다. 원래 데이터 형식은 **varchar**, **nvarchar**, **text**또는 **ntext**와 같은 텍스트 유형이어야 합니다. 이 지시어와 함께 사용할 수 있는 것은 **hide**뿐입니다. 이 지시어를 사용할 때는 *AttributeName* 을 지정하지 말아야 합니다.  
  
 이러한 두 그룹 간 지시어 조합은 대부분의 경우 허용되지만 자체 그룹에서 지시어를 조합하는 것은 허용되지 않습니다.  
  
 *Customer!1* 과 같은 *Directive* 및 **AttributeName**이 지정되지 않은 경우 **Customer!1!!element** 와 같은 **element**지시어가 내포되고 열 데이터가 *ElementName*에 포함됩니다.  
  
 **xmltext** 지시어가 지정된 경우 열 내용은 문서의 나머지 부분에 통합된 단일 태그로 묶입니다. 이 지시어는 OPENXML에 의해 열에 저장된 사용되지 않은 오버플로 XML 데이터를 인출하는 데 유용합니다. 자세한 내용은 [OPENXML&#40;SQL Server&#41;](../xml/openxml-sql-server.md)을 참조하세요.  
  
 *AttributeName* 이 지정된 경우 태그 이름이 지정된 이름으로 바뀝니다. 그렇지 않으면 엔터티 인코딩 없이 포함 내용의 시작 위치에 내용을 배치하여 묶는 요소의 현재 특성 목록에 특성이 포함됩니다. 이 지시어가 있는 열은 **varchar**, **nvarchar**, **char**, **nchar**, **text**또는 **ntext**와 같은 텍스트 유형이어야 합니다. 이 지시어와 함께 사용할 수 있는 것은 **hide**뿐입니다. 이 지시어는 열에 저장된 오버플로 데이터를 인출하는 데 유용합니다. 내용이 잘 작성된 XML이 아니면 동작이 정의되지 않습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 예에서는 EXPLICIT 모드를 사용하는 방법을 보여 줍니다.  
  
-   [예제: 직원 정보 검색](../xml/example-retrieving-employee-information.md)  
  
-   [예제: ELEMENT 지시어 지정](../xml/example-specifying-the-element-directive.md)  
  
-   [예제: ELEMENTXSINIL 지시어 지정](../xml/example-specifying-the-elementxsinil-directive.md)  
  
-   [예: EXPLICIT 모드를 사용하여 형제 생성](../xml/example-constructing-siblings-with-explicit-mode.md)  
  
-   [예제: ID 및 IDREF 지시어 지정](../xml/example-specifying-the-id-and-idref-directives.md)  
  
-   [예제: ID 및 IDREFS 지시어 지정](../xml/example-specifying-the-id-and-idrefs-directives.md)  
  
-   [예제: HIDE 지시어 지정](../xml/example-specifying-the-hide-directive.md)  
  
-   [예제: ELEMENT 지시어 및 엔터티 인코딩 지정](../xml/example-specifying-the-element-directive-and-entity-encoding.md)  
  
-   [예제: CDATA 지시어 지정](../xml/example-specifying-the-cdata-directive.md)  
  
-   [예: XMLTEXT 지시어 지정](../xml/example-specifying-the-xmltext-directive.md)  
  
## <a name="see-also"></a>관련 항목  
 [FOR XML에서 RAW 모드 사용](../xml/use-raw-mode-with-for-xml.md)   
 [FOR XML에서 AUTO 모드 사용](../xml/use-auto-mode-with-for-xml.md)   
 [FOR XML에서 PATH 모드 사용](../xml/use-path-mode-with-for-xml.md)   
 [SELECT&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML&#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
