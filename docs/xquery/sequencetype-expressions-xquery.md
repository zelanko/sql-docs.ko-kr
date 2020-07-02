---
title: SequenceType 식 (XQuery) | Microsoft Docs
description: 의 XQuery SequenceType 식 인스턴스와로 캐스팅 하는 방법에 대해 알아봅니다.
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
ms.openlocfilehash: 909d3cb49879a94c466e58f83997e32c468d9df8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85643353"
---
# <a name="sequencetype-expressions-xquery"></a>SequenceType 식(XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery에서는 값이 항상 시퀀스입니다. 값 유형을 시퀀스 유형이라고 합니다. 이 시퀀스 유형은 XQuery 식 **의 인스턴스에서** 사용할 수 있습니다. XQuery 식에서 유형을 참조해야 할 경우 XQuery 사양에 설명된 SequenceType 구문이 사용됩니다.  
  
 원자성 형식 이름은 XQuery 식 **으로 캐스트** 에도 사용할 수 있습니다. 에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SequenceTypes에 대 한 XQuery **cast as** 식 및 **인스턴스** 는 부분적으로 지원 됩니다.  
  
## <a name="instance-of-operator"></a>instance of 연산자  
 연산자 **의 인스턴스** 를 사용 하 여 지정 된 식의 동적 또는 런타임 형식 값을 확인할 수 있습니다. 예를 들면 다음과 같습니다.  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 `instance of`연산자는 `Occurrence indicator` 결과 시퀀스의 카디널리티, 항목 수를 지정 합니다. 카디널리티가 지정되지 않은 경우 1로 간주됩니다. 에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 물음표 (**?)** 발생 표시만 지원 됩니다. **?** 발생 표시기는가 `Expression` 0 개 또는 1 개 항목을 반환할 수 있음을 나타냅니다. 그렇다면 **?** 발생 표시기가 지정 된 `instance of` 경우에는가 `Expression` `SequenceType` `Expression` singleton을 반환 하는지 또는 빈 시퀀스를 반환 하는지 여부에 관계 없이 형식이 지정 된와 일치 하는 경우 True를 반환 합니다.  
  
 그렇다면 **?** 발생 표시기가 지정 되지 않은 경우 `sequence of` 형식이 지정 된와 `Expression` 일치 하 `Type` 고 단일 항목을 반환 하는 경우에만 True를 반환 합니다 `Expression` .  
  
 **참고** 더하기 기호 ( **+** )와 별표 (**&#42;**) 발생 지표는에서 지원 되지 않습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 다음 예에서는 XQuery 연산자**의 인스턴스** 를 사용 하는 방법을 보여 줍니다.  
  
### <a name="example-a"></a>예 1  
 다음 예에서는 **xml** 형식 변수를 만들고이에 대 한 쿼리를 지정 합니다. 쿼리 식은 `instance of` 연산자를 지정하여 첫 번째 피연산자가 반환한 동적 값 유형이 두 번째 피연산자에 지정된 유형과 일치하는지 여부를 확인합니다.  
  
 다음 쿼리는 125 값이 지정 된 **xs: integer**형식의 인스턴스인 경우 True를 반환 합니다.  
  
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
  
 식에서 **data ()** 는 열과 연결 된 스키마에 따라 형식이 xs: String 인 제품 modelid 특성의 형식화 된 값을 반환 합니다. 따라서 `instance of`에서는 True를 반환합니다.  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 자세한 내용은 [형식화 된 Xml과 형식화 되지 않은 Xml 비교](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조 하세요.  
  
 다음 쿼리는 부울 `instance of` 식을 Usetheboolean 특성이 xs: integer 형식 인지 여부를 확인 합니다.  
  
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
 Union 형식을 사용할 때 `instance of` 의 식에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 제한이 있습니다. 특히 요소 또는 특성의 형식이 공용 구조체 형식이 면에서 `instance of` 정확한 형식을 결정 하지 못할 수 있습니다. 따라서 SequenceType에 사용된 원자성 유형이 simpleType 계층에서 실제 식 유형의 최상위 부모가 아닐 경우 쿼리에서 False를 반환합니다. 즉, SequenceType에 지정된 원자성 유형은 anySimpleType의 직계 자식이어야 합니다. 형식 계층 구조에 대 한 자세한 내용은 [XQuery의 형식 캐스팅 규칙](../xquery/type-casting-rules-in-xquery.md)을 참조 하세요.  
  
 다음 쿼리 예에서는 아래의 작업을 수행합니다.  
  
-   정수, 문자열 유형 등의 공용 구조체 유형이 정의된 XML 스키마 컬렉션을 만듭니다.  
  
-   XML 스키마 컬렉션을 사용 하 여 형식화 된 **xml** 변수를 선언 합니다.  
  
-   변수에 예제 XML 인스턴스를 할당합니다.  
  
-   변수를 쿼리하여 공용 구조체 유형을 처리할 때의 `instance of` 동작을 보여 줍니다.  
  
 다음은 쿼리입니다.  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 `instance of` 식에 지정한 SequenceType이 지정된 실제 식 유형의 최상위 부모가 아니므로 다음 쿼리는 False를 반환합니다. 즉, <>의 값은 `TestElement` 정수 형식입니다. 최상위 부모는 xs:decimal입니다. 그러나 xs:decimal는 `instance of` 연산자의 두 번째 피연산자로 지정되지 않습니다.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="http://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 xs:integer의 최상위 부모는 xs:decimal이므로 쿼리를 수정하고 쿼리에서 xs:decimal을 SequenceType으로 지정할 경우 쿼리는 True를 반환합니다.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="http://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>예 4  
 이 예에서는 먼저 XML 스키마 컬렉션을 만들고이 컬렉션을 사용 하 여 **xml** 변수를 입력 합니다. 그런 다음 형식화 된 **xml** 변수를 쿼리하여 기능을 보여 줍니다 `instance of` .  
  
 다음 XML 스키마 컬렉션은 단순 형식 myType 및 myType 형식의 요소 <>을 정의 합니다 `root` .  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
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
  
 이제 형식화 된 **xml** 변수를 만들고 쿼리 합니다.  
  
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
  
-   <`Customer`> 요소가 **orderlist** IDREFS 유형 특성을 포함 하 고 <`Order`> 요소의 **ORDERID** ID 유형 특성이 있는 XML 스키마 컬렉션을 만듭니다.  
  
-   형식화 된 **xml** 변수를 만들고 여기에 샘플 xml 인스턴스를 할당 합니다.  
  
-   변수에 대한 쿼리를 지정합니다. 쿼리 식은 첫 번째 <>의 OrderList IDRERS 형식 특성에서 첫 번째 주문 ID 값을 검색 합니다 `Customer` . 검색된 값은 IDREF 유형입니다. 따라서 `instance of`에서는 True를 반환합니다.  
  
```  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
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
  
-   **스키마 요소 ()** 및 **스키마 특성 ()** 시퀀스 형식은 연산자와 비교할 때 지원 되지 않습니다 `instance of` .  
  
-   `(1,2) instance of xs:integer*`와 같은 전체 시퀀스는 지원되지 않습니다.  
  
-   와 같이 형식 이름을 지정 하는 **요소 ()** 시퀀스 형식의 폼을 사용 하는 경우에는 `element(ElementName, TypeName)` 물음표 (?)로 형식을 정규화 해야 합니다. 예를 들어 `element(Title, xs:string?)`는 요소가 null일 수 있음을 나타냅니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는를 사용 하 여 **xsi: nil** 속성의 런타임 검색을 지원 하지 않습니다 `instance of` .  
  
-   공용 구조체로 형식화된 요소나 특성에서 `Expression`의 값을 가져올 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 파생되지 않은 기본 유형만 식별할 수 있습니다. 이 기본 유형에서 값 유형이 파생됩니다. 예를 들어 <`e1`> 정적 형식이 (xs: integer | xs: string)로 정의 된 경우 다음은 False를 반환 합니다.  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     그러나 `data(<e1>123</e1>) instance of xs:decimal`에서는 True를 반환합니다.  
  
-   **처리 명령 ()** 및 **문서 노드 ()** 시퀀스 형식의 경우 인수가 없는 폼만 허용 됩니다. 예를 들어 `processing-instruction()`은 사용할 수 있지만 `processing-instruction('abc')`은 사용할 수 없습니다.  
  
## <a name="cast-as-operator"></a>cast as 연산자  
 **Cast as** expression을 사용 하 여 값을 특정 데이터 형식으로 변환할 수 있습니다. 예를 들면 다음과 같습니다.  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 `AtomicType` 뒤에 물음표(?)가 필요합니다. 예를 들어 다음 쿼리와 같이 `"2" cast as xs:integer?` 문자열 값을 정수로 변환 합니다.  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 다음 쿼리에서 **data ()는 데이터** 형식의 제품 modelid 특성의 형식화 된 값을 반환 합니다. `cast as`연산자는 값을 xs: integer로 변환 합니다.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 이 쿼리에서는 명시적으로 **data ()** 를 사용 하지 않아도 됩니다. `cast as` 식은 입력 식에 암시적 원자화를 수행합니다.  
  
### <a name="constructor-functions"></a>생성자 함수  
 원자성 유형 생성자 함수를 사용할 수 있습니다. 예를 들어, 연산자를 사용 하는 대신 `cast as` `"2" cast as xs:integer?` 다음 예제와 같이 **xs: integer ()** 생성자 함수를 사용할 수 있습니다.  
  
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
  
 사용자 정의 원자성 유형에도 생성자를 사용할 수 있습니다. 예를 들어 XML 데이터 형식과 연결 된 XML 스키마 컬렉션에서 단순 형식을 정의 하는 경우 **myType ()** 생성자를 사용 하 여 해당 형식의 값을 반환할 수 있습니다.  
  
#### <a name="implementation-limitations"></a>구현 시 제한 사항  
  
-   XQuery 식 **typeswitch**, **castable**및 **treat** 는 지원 되지 않습니다.  
  
-   **로 캐스트** 하려면 물음표 (?)가 필요 합니다. 원자 형식 후  
  
-   **xs: QName** 은 캐스팅 형식으로 지원 되지 않습니다. 대신 **확장 된 QName을** 사용 하십시오.  
  
-   **xs: date**, **xs: time**및 **Xs: datetime** 에는 Z로 표시 되는 표준 시간대가 필요 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [XQuery 식](../xquery/xquery-expressions.md)   
 [Type System &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
