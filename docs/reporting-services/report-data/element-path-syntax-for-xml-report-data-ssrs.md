---
title: XML 보고서 데이터를 위한 요소 경로 구문 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- ElementPath syntax
- XML [Reporting Services], data retrieval
ms.assetid: 07bd7a4e-fd7a-4a72-9344-3258f7c286d1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 967ffe24035094296d467e4a60225f31b1558cc5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77077664"
---
# <a name="element-path-syntax-for-xml-report-data-ssrs"></a>XML 보고서 데이터를 위한 요소 경로 구문(SSRS)
  보고서 디자이너에서 대/소문자 구분 요소 경로를 정의하여 XML 데이터 원본에서 보고서에 사용할 데이터를 지정할 수 있습니다. 요소 경로는 XML 데이터 원본의 XML 계층 노드와 해당 특성으로 이동하는 방법을 나타냅니다. 기본 요소 경로를 사용하려면 데이터 세트 쿼리나 XML **ElementPath**의 XML **Query**를 비워 둡니다. XML 데이터 원본에서 데이터가 검색될 때 텍스트 값이 있는 요소 노드와 요소 노드 특성은 결과 집합의 열이 됩니다. 쿼리를 실행하면 노드 및 특성 값은 행 데이터가 됩니다. 열은 보고서 데이터 창에 데이터 세트 필드 컬렉션으로 표시됩니다. 이 항목에서는 요소 경로 구문을 설명합니다.  
  
> [!NOTE]  
>  요소 경로 구문은 네임스페이스로부터 독립적입니다. 요소 경로에 네임스페이스를 사용하려면 [XML 보고서 데이터를 위한 XML 쿼리 구문&#40;SSRS&#41;](../../reporting-services/report-data/xml-query-syntax-for-xml-report-data-ssrs.md)에 설명된 대로 XML **ElementPath** 요소를 포함하는 XML 쿼리 구문을 사용합니다.  
  
 다음 표에서는 요소 경로를 정의하는 데 사용되는 규칙을 설명합니다.  
  
|규칙|사용 대상|  
|----------------|--------------|  
|**굵게**|표시된 대로 입력해야 하는 텍스트입니다.|  
|&#124; (세로줄)|각 구문 항목을 구분합니다. 항목 중 하나만 선택할 수 있습니다.|  
|`[ ]`(대괄호)|선택적 구문 항목입니다. 대괄호는 입력하지 않습니다.|  
|**{ }** (중괄호)|구문 항목의 매개 변수 범위를 지정합니다.|  
|[**,**...*n*]|앞의 항목이 *n* 번 반복될 수 있음을 나타냅니다. 각 항목은 쉼표로 구분됩니다.|  
  
## <a name="syntax"></a>구문  
  
```  
  
Element path ::=  
    ElementNode[/Element path]  
ElementNode ::=  
    XMLName[(Encoding)][{[FieldList]}]  
XMLName ::=  
    [NamespacePrefix:]XMLLocalName  
Encoding ::=  
        HTMLEncoded | Base64Encoded  
FieldList ::=  
    Field[,FieldList]  
Field ::=  
    Attribute | Value | Element | ElementNode  
Attribute ::=  
        @XMLName[(Type)]  
Value ::=  
        @[(Type)]  
Element ::=  
    XMLName[(Type)]  
Type ::=  
        String | Integer | Boolean | Float | Decimal | Date | XML   
NamespacePrefix ::=  
    Identifier that specifies the namespace.  
XMLLocalName :: =  
    Identifier in the XML tag.   
```  
  
## <a name="remarks"></a>설명  
 다음 표에는 요소 경로에서 사용되는 용어가 요약되어 있습니다. 이 표의 예에서는 XML 문서 예인 Customers.xml을 참조하며 이 문서는 이 항목의 예 섹션에 포함되어 있습니다.  
  
> [!NOTE]  
>  XML 태그는 대/소문자를 구분합니다. 요소 경로에 ElementNode를 지정할 경우 데이터 원본의 XML 태그와 일치해야 합니다.  
  
|용어|정의|  
|----------|----------------|  
|요소 경로|XML 데이터 원본을 사용하여 데이터 세트의 필드 데이터를 검색하기 위해 XML 문서 내에서 이동할 노드 시퀀스를 정의합니다.|  
|**ElementNode**|XML 문서의 XML 노드입니다. 노드는 태그로 지정되며 다른 노드와 계층 관계에 있습니다. 예를 들어, \<Customers>는 루트 요소 노드이고 \<Customer>는 \<Customers>의 하위 요소입니다.|  
|**XMLName**|노드의 이름입니다. 예를 들어 Customers 노드의 이름은 Customers입니다. **XMLName** 에 네임스페이스 식별자를 접두사로 사용하면 모든 노드에 고유 이름을 지정할 수 있습니다.|  
|**인코딩**|이 요소에 대한 **Value** 가 인코딩된 XML이므로 이 값을 디코딩하여 이 요소의 하위 요소로 포함해야 함을 나타냅니다.|  
|**FieldList**|데이터를 검색하는 데 사용할 요소 및 특성 집합을 정의합니다.<br /><br /> 지정하지 않으면 모든 특성 및 하위 요소가 필드로 사용됩니다. 빈 필드 목록을 지정하는 경우(**{}**) 이 노드의 필드는 사용되지 않습니다.<br /><br /> **FieldList** 에 **Value** 와 **Element** 또는 **ElementNode**가 모두 포함될 수는 없습니다.|  
|**필드**|데이터 세트 필드로 검색되는 데이터를 지정합니다.|  
|**Attribute**|**ElementNode**내의 이름 값 쌍입니다. 예를 들어 요소 노드 \<Customer ID="1">에서 **ID**는 특성이며 **\@ID(Integer)** 는 해당 데이터 필드 **ID**에 정수 형식으로 "1"을 반환합니다.|  
|**값**|요소의 값입니다. **Value** 는 요소 경로의 마지막 **ElementNode** 에만 사용할 수 있습니다. 예를 들어 \<Return>은 리프 노드이므로 요소 경로의 끝에 이 노드를 포함하면 **Return {@}** 값은 **Chair**가 됩니다.|  
|**Element**|명명된 하위 요소의 값입니다. 예를 들어 Customers {}/Customer {}/LastName은 LastName 요소에 대한 값만 검색합니다.|  
|**형식**|이 요소에서 만든 필드에 사용할 선택적 데이터 형식입니다.|  
|**NamespacePrefix**|**NamespacePrefix** 는 XML 쿼리 요소에 정의되어 있습니다. XML 쿼리 요소가 없으면 XML **ElementPath** 의 네임스페이스가 무시됩니다. XML 쿼리 요소가 있으면 XML **ElementPath** 에 선택적 특성 **IgnoreNamespaces**가 포함됩니다. IgnoreNamespaces가 **true**이면 XML **ElementPath** 및 XML 문서의 네임스페이스가 무시됩니다. 자세한 내용은 [XML 보고서 데이터를 위한 XML 쿼리 구문&#40;SSRS&#41;](../../reporting-services/report-data/xml-query-syntax-for-xml-report-data-ssrs.md)를 참조하세요.|  
  
## <a name="example---no-namespaces"></a>예 - 네임스페이스가 없는 경우  
 다음 예에서는 XML 문서 Customers.xml을 사용합니다. 이 표에서는 요소 경로 구문의 예를 보여 주고 XML 문서를 기본 데이터 원본으로 하여 데이터 세트를 정의하는 쿼리에 해당 요소 경로를 사용한 결과를 보여 줍니다.  
  
> [!NOTE]  
>  요소 경로가 비어 있으면 쿼리는 기본 요소 경로인 첫 번째 리프 노드 컬렉션 경로를 사용합니다. 첫 번째 예에서 요소 경로를 비워 둔 것은 /Customers/Customer/Orders/Order 요소 경로를 지정한 것과 같습니다. 경로와 함께 모든 노드 값과 특성이 결과 세트에 반환되고 노드 이름과 특성 이름은 데이터 세트 필드로 나타납니다.  
  
 **예 1**: *비어 있음*  
  
|주문|수량|ID|FirstName|LastName|Customer.ID|xmlns|  
|-----------|---------|--------|---------------|--------------|-----------------|-----------|  
|Chair|6|1|Bobby|Moore|11|https\://www.adventure-works.com|  
|테이블|1|2|Bobby|Moore|11|https\://www.adventure-works.com|  
|Sofa|2|8|Crystal|Hu|20|https\://www.adventure-works.com|  
|EndTables|2|15|Wyatt|Diaz|33|https\://www.adventure-works.com|  
  
 **예제 #2**: `Customers {}/Customer`  
  
|FirstName|LastName|ID|  
|---------------|--------------|--------|  
|Bobby|Moore|11|  
|Crystal|Hu|20|  
|Wyatt|Diaz|33|  
  
 **예제 #3**: `Customers {}/Customer {}/LastName`  
  
|LastName|  
|--------------|  
|Moore|  
|Hu|  
|Diaz|  
  
 **예제 #4**: `Customers {}/Customer {}/Orders/Order {@,@Qty}`  
  
|주문|수량|  
|-----------|---------|  
|Chair|6|  
|테이블|1|  
|Sofa|2|  
|EndTables|2|  
  
 **예제 #5**: `Customers {}/Customer/Orders/Order{ @ID(Integer)}`  
  
|Order.ID|FirstName|LastName|ID|  
|--------------|---------------|--------------|--------|  
|1|Bobby|Moore|11|  
|2|Bobby|Moore|11|  
|8|Crystal|Hu|20|  
|15|Wyatt|Diaz|33|  
  
#### <a name="xml-document-customersxml"></a>XML 문서: Customers.xml  
 이전 섹션의 요소 경로 예를 사용하려면 이 XML을 복사하여 보고서 디자이너에서 액세스할 수 있는 URL에 저장한 다음 해당 XML 문서를 XML 데이터 원본으로 사용합니다(예: `https://localhost/Customers.xml`).  
  
```  
<?xml version="1.0"?>  
<Customers xmlns="https://www.adventure-works.com">  
   <Customer ID="11">  
      <FirstName>Bobby</FirstName>  
      <LastName>Moore</LastName>  
      <Orders>  
         <Order ID="1" Qty="6">Chair</Order>  
         <Order ID="2" Qty="1">Table</Order>  
      </Orders>  
      <Returns>  
         <Return ID="1" Qty="2">Chair</Return>  
      </Returns>  
   </Customer>  
   <Customer ID="20">  
      <FirstName>Crystal</FirstName>  
      <LastName>Hu</LastName>  
      <Orders>  
         <Order ID="8" Qty="2">Sofa</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
   <Customer ID="33">  
      <FirstName>Wyatt</FirstName>  
      <LastName>Diaz</LastName>  
      <Orders>  
         <Order ID="15" Qty="2">EndTables</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
</Customers>  
```  
  
 또는 다음과 같은 절차에 따라 연결 문자열이 없는 XML 데이터 원본을 만들고 쿼리에 Customers.XML을 포함할 수 있습니다.  
  
###### <a name="to-embed-customersxml-in-a-query"></a>쿼리에 Customers.XML을 포함하려면  
  
1.  빈 연결 문자열을 사용하여 XML 데이터 원본을 만듭니다.  
  
2.  XML 데이터 원본에 대한 새 데이터 세트를 만듭니다.  
  
3.  **데이터 세트 속성** 대화 상자에서 **쿼리 디자이너**를 클릭합니다. 텍스트 기반의 쿼리 디자이너 대화 상자가 열립니다.  
  
4.  쿼리 창에서 다음 두 줄을 입력합니다.  
  
     `<Query>`  
  
     `<XmlData>`  
  
5.  Customers.XML을 복사하여 쿼리 창에서 `<XmlData>`다음에 텍스트를 붙여 넣습니다.  
  
6.  쿼리 창에서 Customers.XML로부터 복사한 첫 번째 줄을 삭제합니다. `<?xml version="1.0"?>`  
  
7.  쿼리 끝에 다음 두 줄을 추가합니다.  
  
     `<XmlData>`  
  
     `<Query>`  
  
8.  **쿼리 실행** (!)을 클릭합니다.  
  
     다음 열과 함께 4줄의 데이터로 결과 집합이 표시됩니다. `xmlns`, `Customer.ID`, `FirstName`, `LastName`, `ID`, `Qty`, `Order`  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [XML 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Reporting Services 자습서 &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)   
 [보고서 데이터 창에서 필드 추가, 편집, 새로 고침&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
  
