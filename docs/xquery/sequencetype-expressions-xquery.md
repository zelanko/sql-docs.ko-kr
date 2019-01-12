---
title: SequenceType 식 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- SequenceType expressions
- instance of operator [XQuery]
- expressions [XQuery], SequenceType
- cast as operator
ms.assetid: ad3573da-d820-4d1c-81c4-a83c4640ce22
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 542cf5a0960e967d2bebb3889af0f03656004472
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124563"
---
# <a name="sequencetype-expressions-xquery"></a>SequenceType 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery에서는 값이 항상 시퀀스입니다. 값 유형을 시퀀스 유형이라고 합니다. 시퀀스 유형을에서 사용할 수는 **인스턴스의** XQuery 식입니다. XQuery 식에서 유형을 참조해야 할 경우 XQuery 사양에 설명된 SequenceType 구문이 사용됩니다.  
  
 에 원자성 유형 이름도 사용할 수도 있습니다는 **로 캐스팅** XQuery 식입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 **인스턴스의** 하 고 **로 캐스팅** 에서는 Sequencetype의 XQuery 식이 부분적으로 지원 됩니다.  
  
## <a name="instance-of-operator"></a>instance of 연산자  
 합니다 **인스턴스의** 지정한 식의 값의 동적 또는 런타임 형식을 확인 하려면 연산자를 사용할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 합니다 `instance of` 연산자는 `Occurrence indicator`, 카디널리티, 결과 시퀀스의 항목 수를 지정 합니다. 카디널리티가 지정되지 않은 경우 1로 간주됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 물음표만 (**?)**  발생 표시 지원 됩니다. **?** 발생 표시 함을 `Expression` 0 개 이상의 항목을 반환할 수 있습니다. 경우는 **?** 발생 표시를 지정 하면 `instance of` 경우 True를 반환 합니다 `Expression` 형식이 지정 된 일치 `SequenceType`여부에 관계 없이 `Expression` 단일 또는 빈 시퀀스를 반환 합니다.  
  
 경우는 **?** 발생 표시를 지정 하지 않으면 `sequence of` 경우에만 True를 반환 합니다는 `Expression` 일치 항목을 입력 합니다 `Type` 지정 및 `Expression` 단일 반환 합니다.  
  
 **참고** 더하기 기호 (**+**)와 별표 (**&#42;**) 발생 표시가 지원 되지 않습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 다음 예제에서는 사용을 보여 합니다**인스턴스의** XQuery 연산자입니다.  
  
### <a name="example-a"></a>예 1  
 다음 예제는 **xml** 변수를 입력 하 고이 대 한 쿼리를 지정 합니다. 쿼리 식은 `instance of` 연산자를 지정하여 첫 번째 피연산자가 반환한 동적 값 유형이 두 번째 피연산자에 지정된 유형과 일치하는지 여부를 확인합니다.  
  
 125 값은 지정 된 형식의 인스턴스가 다음 쿼리는 True를 반환 합니다 **xs: integer**:  
  
```  
declare @x xml  
set @x=''  
select @x.query('125 instance of xs:integer')  
go  
```  
  
 첫 번째 피연산자의 /a[1] 식에서 반환한 값이 요소이므로 다음 쿼리는 True를 반환합니다.  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('/a[1] instance of element()')  
go  
```  
  
 마찬가지로 첫 번째 식에서 식의 값 유형이 특성이므로 다음 쿼리에서 `instance of`는 True를 반환합니다.  
  
```  
declare @x xml  
set @x='<a attr1="x">1</a>'  
select @x.query('/a[1]/@attr1 instance of attribute()')  
go  
```  
  
 다음 예에서는 `data(/a[1]` 식이 xdt:untypedAtomic으로 형식화된 원자성 값을 반환합니다. 따라서 `instance of`에서는 True를 반환합니다.  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('data(/a[1]) instance of xdt:untypedAtomic')  
go  
```  
  
 다음 쿼리에서 `data(/a[1]/@attrA` 식은 형식화되지 않은 원자성 값을 반환합니다. 따라서 `instance of`에서는 True를 반환합니다.  
  
```  
declare @x xml  
set @x='<a attrA="X">1</a>'  
select @x.query('data(/a[1]/@attrA) instance of xdt:untypedAtomic')  
go  
```  
  
### <a name="example-b"></a>예 2  
 이 예에서는 AdventureWorks 예제 데이터베이스에 있는 형식화된 XML 열을 쿼리합니다. 쿼리 중인 열과 관련된 XML 스키마 컬렉션이 형식화 정보를 제공합니다.  
  
 식에서 **data ()** 형식인 열에 연결 된 스키마에 따라 xs: string ProductModelID 특성의 형식화 된 값을 반환 합니다. 따라서 `instance of`에서는 True를 반환합니다.  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조하세요.  
  
 다음 쿼리에서 usetheBoolean `instance of` LocationID 특성 유형이 xs: integer 인지 여부를 결정 하는 식:  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   /AWMI:root[1]/AWMI:Location[1]/@LocationID instance of attribute(LocationID,xs:integer)  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 CatalogDescription 유형의 XML 열에 대해서는 다음 쿼리가 지정됩니다. 이 열과 관련된 XML 스키마 컬렉션이 형식화 정보를 제공합니다.  
  
 쿼리에서는 `element(ElementName, ElementType?)` 식에 `instance of` 테스트를 사용하여 `/PD:ProductDescription[1]`이 특정 이름과 유형의 요소 노드를 반환하는지 확인합니다.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /PD:ProductDescription[1] instance of element(PD:ProductDescription, PD:ProductDescription?)  
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 쿼리에서 True를 반환합니다.  
  
### <a name="example-c"></a>예 3  
 공용 구조체 유형을 사용할 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 `instance of` 식에 제한 사항이 있습니다. 특히 요소나 특성의 유형이 공용 구조체 유형이면 `instance of`가 정확한 유형을 확인하지 못할 수도 있습니다. 따라서 SequenceType에 사용된 원자성 유형이 simpleType 계층에서 실제 식 유형의 최상위 부모가 아닐 경우 쿼리에서 False를 반환합니다. 즉, SequenceType에 지정된 원자성 유형은 anySimpleType의 직계 자식이어야 합니다. 형식 계층 구조에 대 한 자세한 내용은 참조 하세요. [XQuery의 형식 캐스트 규칙](../xquery/type-casting-rules-in-xquery.md)합니다.  
  
 다음 쿼리 예에서는 아래의 작업을 수행합니다.  
  
-   정수, 문자열 유형 등의 공용 구조체 유형이 정의된 XML 스키마 컬렉션을 만듭니다.  
  
-   형식화 된 선언 **xml** XML 스키마 컬렉션을 사용 하 여 변수입니다.  
  
-   변수에 예제 XML 인스턴스를 할당합니다.  
  
-   변수를 쿼리하여 공용 구조체 유형을 처리할 때의 `instance of` 동작을 보여 줍니다.  
  
 다음은 쿼리입니다.  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="https://www.w3.org/2001/XMLSchema" targetNamespace="https://ns" xmlns:ns="https://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 `instance of` 식에 지정한 SequenceType이 지정된 실제 식 유형의 최상위 부모가 아니므로 다음 쿼리는 False를 반환합니다. 즉, <`TestElement`>의 값은 정수 유형입니다. 최상위 부모는 xs:decimal입니다. 그러나 xs:decimal는 `instance of` 연산자의 두 번째 피연산자로 지정되지 않습니다.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="https://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="https://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 xs:integer의 최상위 부모는 xs:decimal이므로 쿼리를 수정하고 쿼리에서 xs:decimal을 SequenceType으로 지정할 경우 쿼리는 True를 반환합니다.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="https://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="https://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>예 4  
 이 예제에서는 먼저 XML 스키마 컬렉션을 만들고 사용 하 여 입력 하는 **xml** 변수입니다. 형식화 된 **xml** 변수 보여 주기 위해 다음 쿼리는 `instance of` 기능입니다.  
  
 다음 XML 스키마 컬렉션은 단순 유형 myType과 myType 유형의 <`root`> 요소를 정의합니다.  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="https://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
      <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
           <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
Go  
```  
  
 이제 만들어서 형식화 된 **xml** 변수 및 쿼리:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
   data(/ns:root[1]) instance of ns:myType')  
go  
```  
  
 myType 유형은 sqltypes 스키마에 정의된 varchar 유형의 제한으로 인해 파생되므로 `instance of`도 True를 반환합니다.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
go  
```  
  
### <a name="example-e"></a>예 5  
 다음 예에서는 식이 IDREFS 특성의 값 중 하나를 검색하고 `instance of`를 사용하여 값이 IDREF 유형인지 여부를 확인합니다. 이 예에서는 다음을 수행합니다.  
  
-   XML 스키마 컬렉션을 만듭니다는 <`Customer`> 요소에는 **OrderList** IDREFS 유형 특성 및 <`Order`> 요소에는 **OrderID** ID 유형 특성입니다.  
  
-   형식화 된 만듭니다 **xml** 변수와 예제 XML 인스턴스를 할당 합니다.  
  
-   변수에 대한 쿼리를 지정합니다. 쿼리 식이 첫 번째 <`Customer`>의 OrderList IDRERS 유형 특성에서 첫 번째 순서 ID 값을 검색합니다. 검색된 값은 IDREF 유형입니다. 따라서 `instance of`에서는 True를 반환합니다.  
  
```  
create xml schema collection SC as  
'<schema xmlns="https://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
  
select @x.query(' declare namespace CustOrders="Customers";   
 data(CustOrders:Customers/Customer[1]/@OrderList)[1] instance of xs:IDREF ? ') as XML_result  
```  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   합니다 **schema-element ()** 하 고 **schema-attribute()** 비교 하기 위해 시퀀스 유형은 지원 되지 않습니다는 `instance of` 연산자입니다.  
  
-   `(1,2) instance of xs:integer*`와 같은 전체 시퀀스는 지원되지 않습니다.  
  
-   한 형태를 사용 하는 경우는 **element()** 시퀀스와 같은 형식 이름을 지정 하는 유형의 `element(ElementName, TypeName)`, 물음표 (?)로 유형을 한 정해야 합니다. 예를 들어 `element(Title, xs:string?)`는 요소가 null일 수 있음을 나타냅니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 런타임 검색을 지원 하지 않습니다 합니다 **xsi: nil** 사용 하 여 속성 `instance of`합니다.  
  
-   공용 구조체로 형식화된 요소나 특성에서 `Expression`의 값을 가져올 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 파생되지 않은 기본 유형만 식별할 수 있습니다. 이 기본 유형에서 값 유형이 파생됩니다. 예를 들어 <`e1`>이 (xs:integer | xs:string) 정적 유형을 갖도록 정의되면 다음 예에서 False를 반환합니다.  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     그러나 `data(<e1>123</e1>) instance of xs:decimal`에서는 True를 반환합니다.  
  
-   에 대 한는 **processing-instruction()** 하 고 **document-node()** 시퀀스 형식이 인수가 없는 형태만 허용 됩니다. 예를 들어 `processing-instruction()`은 사용할 수 있지만 `processing-instruction('abc')`은 사용할 수 없습니다.  
  
## <a name="cast-as-operator"></a>cast as 연산자  
 합니다 **로 캐스팅** 식 값을 특정 데이터 형식으로 변환할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 `AtomicType` 뒤에 물음표(?)가 필요합니다. 예를 들어, 다음 쿼리에 표시 된 것 처럼 `"2" cast as xs:integer?` 문자열 값을 정수로 변환 합니다.  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 다음 쿼리에서 **data ()** 문자열 형식 ProductModelID 특성의 형식화 된 값을 반환 합니다. `cast as`연산자 값을 xs: integer로 변환 합니다.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 명시적으로 사용 **data ()** 이 쿼리에서 필요 하지 않습니다. `cast as` 식은 입력 식에 암시적 원자화를 수행합니다.  
  
### <a name="constructor-functions"></a>생성자 함수  
 원자성 유형 생성자 함수를 사용할 수 있습니다. 예를 들어, 사용 하는 대신를 `cast as` 연산자 `"2" cast as xs:integer?`를 사용할 수는 **xs:integer()** 다음 예제와 같이 생성자 함수:  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:integer("2")')  
```  
  
 다음 예에서는 2000-01-01Z에 해당하는 xs:date 값을 반환합니다.  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:date("2000-01-01Z")')  
```  
  
 사용자 정의 원자성 유형에도 생성자를 사용할 수 있습니다. 예를 들어, XML 스키마 컬렉션에 연결 된 XML 데이터 형식, 단순 형식을 정의 **myType()** 생성자를 사용 하 여 해당 형식의 값을 반환할 수 있습니다.  
  
#### <a name="implementation-limitations"></a>구현 시 제한 사항  
  
-   XQuery 식 **typeswitch**하십시오 **캐스팅할 수 있는**, 및 **처리** 지원 되지 않습니다.  
  
-   **로 캐스팅** 물음표 (?) 필요 합니다. atomic 형식입니다.  
  
-   **xs: qname** 캐스팅에 대 한 형식으로 지원 되지 않습니다. 사용 하 여 **Expanded-qname** 대신 합니다.  
  
-   **xs: date**, **xs: time**, 및 **xs: datetime** a에서 Z로 표시 되는 시간대가 필요 합니다.  
  
     표준 시간대를 지정하지 않았으므로 다음 쿼리는 실패합니다.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25")}</a>')  
    go  
    ```  
  
     값에 Z 표준 시간대 표시를 추가하면 쿼리가 작동합니다.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25Z")}</a>')  
    go  
    ```  
  
     다음은 결과입니다.  
  
    ```  
    <a>2002-05-25Z</a>  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [XQuery 식](../xquery/xquery-expressions.md)   
 [형식 시스템 &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
