---
title: '관계를 사용 하 여 sql (SQLXML 4.0): relationship 지정 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- parent attribute [SQLXML]
- element relationships [SQLXML]
- multiple element relationships
- attribute relationships [SQLXML]
- sql:relationship
- relationship chains [SQLXML]
- IDREF relationships [SQLXML]
- parent-child relationships [SQLXML]
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- relationships [SQLXML], specifying
- unnamed relationships
- ID relationships [SQLXML]
- hierarchical relationships [SQLXML]
- named relationships [SQLXML]
ms.assetid: 98820afa-74e1-4e62-b336-6111a3dede4c
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: beb6101d78206d30fa52be3e90ed62f4e2b8b2de
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290369"
---
# <a name="specifying-relationships-using-sqlrelationship-sqlxml-40"></a>sql:relationship을 사용하여 관계 지정(SQLXML 4.0)
  XML 문서의 요소는 서로 관련될 수 있습니다. 이러한 요소는 계층적으로 중첩될 수 있으며 요소 간에 ID, IDREF 또는 IDREFS 관계가 지정될 수 있습니다.  
  
 예를 들어, XSD 스키마에서에서는  **\<고객 >** 요소에 포함 되어  **\<순서 >** 자식 요소입니다. 스키마는 AdventureWorks 데이터베이스에 매핑된 경우 합니다  **\<고객 >** 요소는 Sales.Customer 테이블에 매핑합니다 및  **\<순서 >** 요소가 매핑되는 Sales.SalesOrderHeader 테이블입니다. 이러한 기본 테이블인 Sales.Customer와 Sales.SalesOrderHeader는 고객 주문과 관련하여 서로 관련되어 있습니다. Sales.SalesOrderHeader 테이블의 CustomerID는 Sales.Customer 테이블의 CustomerID 기본 키를 참조하는 외래 키입니다. `sql:relationship` 주석을 사용하면 매핑 스키마 요소 간에 이러한 관계를 설정할 수 있습니다.  
  
 주석이 추가된 XSD 스키마에서 `sql:relationship` 주석은 요소가 매핑되는 기본 테이블 간의 기본 키 및 외래 키 관계를 기반으로 스키마 요소를 계층적으로 중첩하는 데 사용됩니다. `sql:relationship` 주석을 지정할 때는 다음을 확인해야 합니다.  
  
-   부모 테이블(Sales.Customer)과 자식 테이블(Sales.SalesOrderHeader).  
  
-   부모 테이블과 자식 테이블 간의 관계를 구성하는 열(예: 부모 테이블과 자식 테이블에 모두 표시되는 CustomerID 열)  
  
 이 정보는 적절한 계층을 생성하는 데 사용됩니다.  
  
 테이블 이름과 필요한 조인 정보를 제공하려면 다음 특성을 `sql:relationship` 주석에 지정합니다. 이러한 특성은만 유효 합니다  **\<sql: relationship >** 요소:  
  
 **이름**  
 관계의 고유한 이름을 지정합니다.  
  
 **Parent**  
 부모 관계(테이블)를 지정합니다. 이 특성은 옵션입니다. 특성이 지정되지 않으면 문서의 자식 계층에 있는 정보에서 부모 테이블 이름을 가져옵니다. 스키마를 사용한 것과 동일한 두 명의 부모-자식 계층 구조를 지정 하는 경우  **\<sql: relationship >** 다른 부모 요소를 지정 하지 않으면 부모 특성에 있지만  **\<sql: 관계 >** 합니다. 이 정보는 스키마의 계층에서 가져옵니다.  
  
 **parent-key**  
 부모의 부모 키를 지정합니다. 부모 키가 여러 열로 구성된 경우 값은 사이에 공백을 두고 지정합니다. 여러 열로 구성된 키에 대해 지정된 값과 해당 자식 키에 지정된 값 간에는 위치 매핑이 있습니다.  
  
 **자식**  
 자식 관계(테이블)를 지정합니다.  
  
 **child-key**  
 부모의 부모 키를 참조하는 자식의 자식 키를 지정합니다. 자식 키가 여러 특성(열)으로 구성된 경우 자식 키 값은 사이에 공백을 두고 지정합니다. 여러 열로 구성된 키에 대해 지정된 값과 해당 부모 키에 지정된 값 간에는 위치 매핑이 있습니다.  
  
 **역**  
 이 특성에 지정 된  **\<sql: relationship >** updategram에서 사용 됩니다. 자세한 내용은 [sql: relationship에 sql: inverse 특성 지정](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)합니다.  
  
 합니다 `sql:key-fields` 주석이 있는 자식 요소를 포함 하는 요소에 지정 해야 합니다는  **\<sql: relationship >** 요소와 자식 간에 정의 및의 기본 키를 제공 하지 않습니다는 부모 요소에 지정 된 테이블입니다. 스키마를 지정 하지 않는 경우에  **\<sql: relationship >** 를 지정 해야 합니다 `sql:key-fields` 적절 한 계층을 생성 합니다. 자세한 내용은 [sql:를 사용 하 여 Identifying Key Columns-필드](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)합니다.  
  
 올바른 중첩 결과를 얻으려면 모든 스키마에 `sql:key-fields`를 지정하는 것이 좋습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예 실행에 대 한 요구 사항](../sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-the-sqlrelationship-annotation-on-an-element"></a>1. 요소에 sql:relationship 주석 지정  
 다음과 같은 주석이 추가 된 XSD 스키마에 포함 되어 있습니다  **\<고객 >** 하 고  **\<순서 >** 요소입니다. **\<순서 >** 요소는 자식 요소를  **\<고객 >** 요소입니다.  
  
 스키마에는 `sql:relationship` 주석은에 지정 됩니다는  **\<순서 >** 자식 요소입니다. 에 정의 된 관계 자체를  **\<xsd: appinfo >** 요소입니다.  
  
 합니다  **\<관계 >** 요소는 Sales.Customer 테이블의 CustomerID 기본 키를 가리키는 외래 키로 Sales.SalesOrderHeader 테이블의 CustomerID를 식별 합니다. 고객에 게 속한 주문은의 자식 요소로 표시 되는 따라서  **\<고객 >** 요소입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                    sql:relationship="CustOrders" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 앞의 스키마는 명명된 관계를 사용합니다. 명명되지 않은 관계도 지정할 수 있습니다. 결과는 같습니다.  
  
 다음은 명명되지 않은 관계가 지정되는 수정된 스키마입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer"  type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader">  
           <xsd:annotation>  
            <xsd:appinfo>  
              <sql:relationship   
                parent="Sales.Customer"  
                parent-key="CustomerID"  
                child="Sales.SalesOrderHeader"  
                child-key="CustomerID" />  
            </xsd:appinfo>  
           </xsd:annotation>  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 sql-relationship.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. sql-relationship.xml을 저장한 디렉터리에 파일을 sql-relationshipT.xml로 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-relationship.xml">  
            /Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(sql-relationship.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 대한 상대 경로입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\sql-relationship.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [실행 SQLXML 쿼리에 ADO를 사용 하 여](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)입니다.  
  
 결과 집합은 다음과 같습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer CustomerID="1">   
    <Order OrderID="43860" CustomerID="1" />   
    <Order OrderID="44501" CustomerID="1" />   
    <Order OrderID="45283" CustomerID="1" />   
    <Order OrderID="46042" CustomerID="1" />   
  </Customer>   
</ROOT>  
```  
  
### <a name="b-specifying-a-relationship-chain"></a>2. 관계 체인 지정  
 이 예에서는 AdventureWorks 데이터베이스에서 가져온 데이터를 사용하는 다음과 같은 XML 문서가 필요하다고 가정해 보겠습니다.  
  
```  
<Order SalesOrderID="43659">  
  <Product Name="Mountain Bike Socks, M"/>   
  <Product Name="Sport-100 Helmet, Blue"/>  
  ...  
</Order>  
...  
```  
  
 하나는 XML 문서에는 Sales.SalesOrderHeader 테이블의 각 주문에 대 한  **\<순서 >** 요소입니다. 및 각  **\<순서 >** 요소에는 목록이  **\<제품 >** 자식 요소를 순서 대로 요청 된 각 제품에 대 한 합니다.  
  
 이 계층 구조를 생성 하는 XSD 스키마를 지정 하려면 두 개의 관계를 지정 해야 합니다: OrderOD와 ODProduct 합니다. OrderOD 관계는 Sales.SalesOrderHeader와 Sales.SalesOrderDetail 테이블 간의 부모-자식 관계를 지정합니다. ODProduct 관계는 Sales.SalesOrderDetail와 Production.Product 테이블 간의 관계를 지정합니다.  
  
 다음 스키마에는 `msdata:relationship` 주석이 합니다  **\<제품 >** 두 값을 지정 하는 요소: OrderOD와 ODProduct. 이 두 값이 지정되는 순서가 중요합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <msdata:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  
    <msdata:relationship name="ODProduct"  
          parent="Sales.SalesOrderDetail"  
          parent-key="ProductID"  
          child="Production.Product"  
          child-key="ProductID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID"  
                     msdata:relationship="OrderOD ODProduct">  
          <xsd:complexType>  
             <xsd:attribute name="Name" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
    </xsd:complexType>  
</xsd:schema>  
```  
  
 명명된 관계를 지정하는 대신 익명 관계를 지정할 수 있습니다. 이 경우 전체 내용의  **\<주석 >**...  **\</annotation >**, 두 개의 관계를 설명 하는의 자식 요소로 나타낼  **\<제품 >** 합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID" >  
         <xsd:annotation>  
          <xsd:appinfo>  
           <msdata:relationship   
               parent="Sales.SalesOrderHeader"  
               parent-key="SalesOrderID"  
               child="Sales.SalesOrderDetail"  
               child-key="SalesOrderID" />  
  
           <msdata:relationship   
               parent="Sales.SalesOrderDetail"  
               parent-key="ProductID"  
               child="Production.Product"  
               child-key="ProductID" />  
         </xsd:appinfo>  
       </xsd:annotation>  
       <xsd:complexType>  
          <xsd:attribute name="Name" type="xsd:string" />  
       </xsd:complexType>  
     </xsd:element>  
   </xsd:sequence>  
   <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
  </xsd:complexType>  
 </xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 relationshipChain.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. relationshipChain.xml을 저장한 디렉터리에 파일을 relationshipChainT.xml로 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationshipChain.xml">  
            /Order  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(relationshipChain.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 대한 상대 경로입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\relationshipChain.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [실행 SQLXML 쿼리에 ADO를 사용 하 여](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)입니다.  
  
 결과 집합은 다음과 같습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Order SalesOrderID="43659">  
    <Product Name="Mountain Bike Socks, M" />   
    <Product Name="Sport-100 Helmet, Blue" />   
    <Product Name="AWC Logo Cap" />   
    <Product Name="Long-Sleeve Logo Jersey, M" />   
    <Product Name="Long-Sleeve Logo Jersey, XL" />   
    ...  
  </Order>  
  ...  
</ROOT>  
```  
  
### <a name="c-specifying-the-relationship-annotation-on-an-attribute"></a>3. 특성에 관계 주석 지정  
 이 예의 스키마에 포함 되어는 \<고객 > 요소를 \<CustomerID > 자식 요소 및 IDREFS 형식의 OrderIDList 특성입니다. \<고객 > 요소는 AdventureWorks 데이터베이스의 Sales.Customer 테이블에 매핑됩니다. 기본적으로이 매핑의 범위는 모든 자식 요소에 적용 하거나 하지 않는 한 특성 `sql:relation` 된 자식 요소 또는 특성의 경우에 를사용하여적절한기본키/외래키관계를정의해야합니다\<관계 > 요소입니다. `relation` 주석을 사용하여 다른 테이블을 지정하는 자식 요소 또는 특성은 `relationship` 주석도 지정해야 합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="CustomerID"   type="xsd:string" />   
     </xsd:sequence>  
     <xsd:attribute name="OrderIDList"   
                     type="xsd:IDREFS"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:field="SalesOrderID"  
                     sql:relationship="CustOrders" >  
        </xsd:attribute>  
    </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 relationship-on-attribute.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 파일에 붙여넣습니다. relationship-on-attribute.xml을 저장한 디렉터리에 파일을 relationship-on-attributeT.xml로 저장합니다. 템플릿의 쿼리에서는 CustomerID가 1인 고객을 선택합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-on-attribute.xml">  
        /Customer[CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(relationship-on-attribute.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 대한 상대 경로입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\relationship-on-attribute.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [실행 SQLXML 쿼리에 ADO를 사용 하 여](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)입니다.  
  
 결과 집합은 다음과 같습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer OrderIDList="43860 44501 45283 46042">  
    <CustomerID>1</CustomerID>   
  </Customer>  
</ROOT>  
```  
  
### <a name="d-specifying-sqlrelationship-on-multiple-elements"></a>4. 여러 요소에 대해 sql:relationship 지정  
 이 예제에서 주석이 추가 된 XSD 스키마를 포함 합니다  **\<고객 >** 합니다  **\<순서 >**, 및  **\<OrderDetail >** 요소입니다.  
  
 **\<순서 >** 요소는 자식 요소를  **\<고객 >** 요소입니다. **\<sql: relationship >** 에 지정 된  **\<순서 >** 자식 요소 고객에 게 속한 주문은의 자식 요소로 표시 되는 따라서  **\<고객 >**.  
  
 합니다  **\<순서 >** 요소를 포함 합니다  **\<OrderDetail >** 자식 요소입니다. **\<sql: relationship >** 에 지정 됩니다  **\<OrderDetail >** 자식 요소를 주문에 속하는 주문 정보는 자식 요소로 표시 되도록 **\<순서 >** 요소입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
        parent="Sales.Customer"  
        parent-key="CustomerID"  
        child="Sales.SalesOrderHeader"  
        child-key="CustomerID" />  
  
    <sql:relationship name="OrderOrderDetail"  
        parent="Sales.SalesOrderHeader"  
        parent-key="SalesOrderID"  
        child="Sales.SalesOrderDetail"  
        child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
              sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                             sql:relationship="OrderOrderDetail"   
                             maxOccurs="unbounded" >  
                  <xsd:complexType>  
                    <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                    <xsd:attribute name="ProductID" type="xsd:string" />  
                    <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 relationship-multiple-elements.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. relationship-multiple-elements.xml을 저장한 디렉터리에 파일을 relationship-multiple-elementsT.xml로 저장합니다. 템플릿의 쿼리에서는 CustomerID가 1이고 SalesOrderID가 43860인 고객의 주문 정보를 반환합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-multiple-elements.xml">  
        /Customer[@CustomerID=1]/Order[@SalesOrderID=43860]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(relationship-multiple-elements.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 대한 상대 경로입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\relationship-multiple-elements.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [실행 SQLXML 쿼리에 ADO를 사용 하 여](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)입니다.  
  
 결과 집합은 다음과 같습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1">  
     <OrderDetail SalesOrderID="43860" ProductID="761" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="770" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="758" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="765" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="762" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="768" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="763" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="756" OrderQty="1" />   
  </Order>  
</ROOT>  
```  
  
### <a name="e-specifying-the-sqlrelationship-without-the-parent-attribute"></a>5. 지정 된 \<sql: relationship > parent 특성 없이  
 이 예제를 지정 하는  **\<sql: relationship >** 없이 **부모** 특성입니다. 예를 들어 다음과 같은 직원 테이블을 가정해 보십시오.  
  
```  
Emp1(SalesPersonID, FirstName, LastName, ReportsTo)  
Emp2(SalesPersonID, FirstName, LastName, ReportsTo)  
```  
  
 다음 XML 뷰에 합니다  **\<Emp1 >** 하 고  **\<Emp2 >** Sales.Emp1 및 Sales.Emp2 테이블 매핑 요소:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="EmpOrders"  
          parent-key="SalesPersonID"  
          child="Sales.SalesOrderHeader"  
          child-key="SalesPersonID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Emp1" sql:relation="Sales.Emp1" type="EmpType" />  
  <xsd:element name="Emp2" sql:relation="Sales.Emp2" type="EmpType" />  
   <xsd:complexType name="EmpType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:relationship="EmpOrders" >  
          <xsd:complexType>  
             <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesPersonID"   type="xsd:integer" />   
        <xsd:attribute name="LastName"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 스키마에서 모두를  **\<Emp1 >** 요소와  **\<Emp2 >** 형식의 요소는 `EmpType`합니다. 형식 `EmpType` 에 대해 설명 합니다는  **\<순서 >** 자식 요소와 해당  **\<sql: relationship >** 합니다. 이 경우에 식별할 수 있는 단일 부모가 없는  **\<sql: relationship >** 사용 하 여 합니다 **부모** 특성입니다. 이 상황에서 지정 하지 않으면 합니다 **부모** 특성  **\<sql: relationship >**; **부모** 에서 특성 정보를 가져옵니다는 스키마의 계층입니다.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  AdventureWorks 데이터베이스에 다음 테이블을 만듭니다.  
  
    ```  
    USE AdventureWorks  
    CREATE TABLE Sales.Emp1 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    CREATE TABLE Sales.Emp2 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    ```  
  
2.  테이블에 다음 예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Sales.Emp1 values (279, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Sales.Emp1 values (282, 'Andrew', 'Fuller',1)  
    INSERT INTO Sales.Emp1 values (276, 'Janet', 'Leverling',1)  
    INSERT INTO Sales.Emp2 values (277, 'Margaret', 'Peacock',3)  
    INSERT INTO Sales.Emp2 values (283, 'Steven', 'Devolio',4)  
    INSERT INTO Sales.Emp2 values (275, 'Nancy', 'Buchanan',5)  
    INSERT INTO Sales.Emp2 values (281, 'Michael', 'Suyama',6)  
    ```  
  
3.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 relationship-noparent.xml로 저장합니다.  
  
4.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. relationship-noparent.xml을 저장한 디렉터리에 파일을 relationship-noparentT.xml로 저장합니다. 템플릿의 쿼리에서 모든 선택 된 \<Emp1 > 요소 (따라서 부모는 Emp1).  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationship-noparent.xml">  
            /Emp1  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(relationship-noparent.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 대한 상대 경로입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\relationship-noparent.xml"  
    ```  
  
5.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [실행 SQLXML 쿼리에 ADO를 사용 하 여](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)입니다.  
  
 다음은 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<Emp1 SalesPersonID="276" LastName="Leverling">  
  <Order SalesOrderID="43663" CustomerID="510" />   
  <Order SalesOrderID="43666" CustomerID="511" />   
  <Order SalesOrderID="43859" CustomerID="259" />  
  ...  
</Emp1>  
```  
  
  
