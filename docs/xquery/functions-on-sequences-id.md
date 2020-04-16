---
title: ID 함수 (X쿼리) | 마이크로 소프트 문서
description: XQuery id 함수를 사용하여 제공된 xs:IDREF 값과 함께 문서 순서대로 XML 인스턴스의 요소 시퀀스를 반환하는 방법을 알아봅니다.
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
- fn:id function
- id function
ms.assetid: de99fc60-d0ad-4117-a17d-02bdde6512b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 45b7f9f7ee9fa301b10c29fafb663c3a307509d7
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388510"
---
# <a name="functions-on-sequences---id"></a>시퀀스 함수 - id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  *$arg*제공된 하나 이상의 xs:IDREF 값과 일치하는 xs:ID 값을 사용하여 요소 노드 시퀀스를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 하나 이상의 xs:IDREF 값입니다.  
  
## <a name="remarks"></a>설명  
 함수 결과는 후보 xs:IDREF 목록에 있는 하나 이상의 xs:IDREF에 일치하는 xs:ID 값이 있는 문서 순서대로 된 XML 인스턴스의 요소 시퀀스입니다.  
  
 요소와 일치하는 xs:IDREF 값이 없으면 이 함수는 빈 시퀀스를 반환합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스의 다양한 xml 형식 열에 저장된 **XML** 인스턴스에 대한 XQuery 예제를 제공합니다.  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. IDREF 특성 값을 기반으로 요소 검색  
 다음 예제에서는 fn:id를 사용하여 `employee` IDREF 관리자 특성을 기반으로 <> 요소를 검색합니다. 이 예에서 관리자 특성은 IDREF 유형 특성이고 eid 특성은 ID 유형 특성입니다.  
  
 특정 관리자 특성 값의 경우 **id()** `employee` 함수는 id type 값값이 입력 IDREF 값과 일치하는 <> 요소를 찾습니다. 즉, 특정 직원의 **경우 id()** 함수는 직원 관리자를 반환합니다.  
  
 다음은 이 예에서 수행된 작업입니다.  
  
-   XML 스키마 컬렉션이 생성됩니다.  
  
-   XML 스키마 컬렉션을 사용하여 형식이 입력된 **xml** 변수가 만들어집니다.  
  
-   쿼리는 <`employee`> 요소의 **관리자** IDREF 특성에서 참조하는 ID 특성 값이 있는 요소를 검색합니다.  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
            <element name="employees" type="e:EmployeesType"/>  
            <complexType name="EmployeesType">  
                 <sequence>  
                      <element name="employee" type="e:EmployeeType" minOccurs="0" maxOccurs="unbounded" />  
                 </sequence>  
            </complexType>    
  
            <complexType name="EmployeeType">  
                        <attribute name="eid" type="ID" />  
                        <attribute name="name" type="string" />  
                        <attribute name="manager" type="IDREF" />  
            </complexType>         
</schema>'  
go  
```  
  
```  
declare @x xml(SC)  
set @x='<e:employees xmlns:e="emp">  
<employee eid="e1" name="Joe" manager="e10" />  
<employee eid="e2" name="Bob" manager="e10" />  
<employee eid="e10" name="Dave" manager="e10" />  
</e:employees>'  
  
select @x.value(' declare namespace e="emp";   
 (fn:id(e:employees/employee[@name="Joe"]/@manager)/@name)[1]', 'varchar(50)')   
Go  
```  
  
 쿼리는 "Dave"를 값으로 반환합니다. 즉 Dave가 Joe의 관리자라는 의미입니다.  
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>B. OrderList IDREFS 특성 값을 기반으로 요소 검색  
 다음 예제에서 <`Customer`> 요소의 OrderList 특성은 IDREFS 형식 특성입니다. 특정 고객에 대한 주문 ID를 나열합니다. 각 주문 id에 대해 `Order` 주문 값을 제공하는 `Customer` <> 아래에 <> 요소 자식이 있습니다.  
  
 쿼리 식 `data(CustOrders:Customers/Customer[1]/@OrderList)[1]`은 첫 번째 고객에 대한 IDRES 목록에서 첫 번째 값을 검색합니다. 그런 다음 이 값은 **id()** 함수에 전달됩니다. 그런 다음 함수는 `Order` orderID 특성 값이 **id()** 함수에 입력과 일치하는 <> 요소를 찾습니다.  
  
```  
drop xml schema collection SC  
go  
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
select @x.query('declare namespace CustOrders="Customers";  
  id(data(CustOrders:Customers/Customer[1]/@OrderList)[1])')  
  
-- result  
<Order OrderID="OrderA">  
  <OrderValue>11</OrderValue>  
</Order>  
```  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]**id()** 의 2인수 버전을 지원하지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]**id()** 인수 형식이 xs:IDREF*의 하위 유형이어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [시퀀스 함수](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
