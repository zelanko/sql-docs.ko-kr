---
title: id 함수 (XQuery) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 80bb427800f57ddaa07e5e53f21b03df9e8317d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62933687"
---
# <a name="functions-on-sequences---id"></a>시퀀스 함수 - id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  하나 이상의 제공 된 값을 xs: idref 값과 일치 하는 xs: id 값을 사용 하 여 요소 노드의 시퀀스를 반환 *$arg*합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 하나 이상의 xs:IDREF 값입니다.  
  
## <a name="remarks"></a>Remarks  
 함수 결과는 후보 xs:IDREF 목록에 있는 하나 이상의 xs:IDREF에 일치하는 xs:ID 값이 있는 문서 순서대로 된 XML 인스턴스의 요소 시퀀스입니다.  
  
 요소와 일치하는 xs:IDREF 값이 없으면 이 함수는 빈 시퀀스를 반환합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예를 제공 **xml** 유형 열에는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>1\. IDREF 특성 값을 기반으로 요소 검색  
 다음 예에서는 fn: id를 사용 하 여 검색 하는 <`employee`> 요소에 IDREF 관리자 특성을 기반으로 합니다. 이 예에서 관리자 특성은 IDREF 유형 특성이고 eid 특성은 ID 유형 특성입니다.  
  
 특정 관리자 특성 값을 **id ()** 찾습니다 함수는 <`employee`> ID 유형 특성 값이 입력된 IDREF 값 일치 하는 요소. 즉, 특정 직원에 대 한 합니다 **합한 것** 함수는 직원 관리자를 반환 합니다.  
  
 다음은 이 예에서 수행된 작업입니다.  
  
-   XML 스키마 컬렉션이 생성됩니다.  
  
-   형식화 된 **xml** 변수는 XML 스키마 컬렉션을 사용 하 여 만들어집니다.  
  
-   참조 하는 ID 특성 값이 있는 요소를 검색 하는 쿼리를 **manager** IDREF 특성을 <`employee`> 요소입니다.  
  
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
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>2\. OrderList IDREFS 특성 값을 기반으로 요소 검색  
 다음 예제에서는 OrderList 특성에에서는 <`Customer`> 요소는 IDREFS 형식 특성입니다. 특정 고객에 대한 주문 ID를 나열합니다. 각 주문 id가는 <`Order`> 자식 요소는 <`Customer`> 순서 값을 제공 하 합니다.  
  
 쿼리 식 `data(CustOrders:Customers/Customer[1]/@OrderList)[1]`은 첫 번째 고객에 대한 IDRES 목록에서 첫 번째 값을 검색합니다. 이 값은 다음에 전달 된 **합한 것** 함수입니다. 함수를 찾습니다는 <`Order`> 요소의 OrderID 특성 값에 대 한 입력이 일치 하는 **합한 것** 함수입니다.  
  
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
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인수가 두 개인 버전을 지원 하지 않습니다 **합한 것**입니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인수 유형이 필요 **합한 것** xs:IDREF*의 하위 형식으로 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시퀀스 함수](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
