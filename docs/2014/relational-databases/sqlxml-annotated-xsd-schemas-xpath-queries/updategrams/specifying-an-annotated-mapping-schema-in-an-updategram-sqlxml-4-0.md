---
title: Updategram에서 주석이 추가 된 매핑 스키마 지정 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, updategrams
- data types [SQLXML], mapping schema in updategrams
- updategrams [SQLXML], annotated mapping schemas
- annotated XDR schemas, updategrams
- inverse attribute
- parent-child relationships [SQLXML]
- mapping-schema attribute
- mapping schema [SQLXML], updategrams
- sql:inverse
ms.assetid: 2e266ed9-4cfb-434a-af55-d0839f64bb9a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 627ab54ed35cbc0a43c5a0eac26a1397199edbd8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014661"
---
# <a name="specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-40"></a>Updategram에 주석이 추가된 매핑 스키마 지정(SQLXML 4.0)
  이 항목에서는 Updategram에 지정된 매핑 스키마(XSD 또는 XDR)를 사용하여 업데이트를 처리하는 방법에 대해 설명합니다. Updategram에서 updategram의 요소와 특성을의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]테이블과 열에 매핑하는 데 사용할 주석이 추가 된 매핑 스키마의 이름을 제공할 수 있습니다. Updategram에 매핑 스키마가 지정되어 있으면 Updategram에 지정된 요소 및 특성 이름이 매핑 스키마의 요소와 특성에 매핑되어야 합니다.  
  
 매핑 스키마를 지정 하려면 `mapping-schema` ** \<sync>** 요소의 특성을 사용 합니다. 다음 예에서는 두 개의 Updategram을 보여 줍니다. 하나는 단순한 매핑 스키마를 사용하고 다른 하나는 더 복잡한 스키마를 사용합니다.  
  
> [!NOTE]  
>  이 설명서에서는 사용자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 템플릿 및 매핑 스키마 지원에 대해 잘 알고 있다고 가정합니다. 자세한 내용은 주석이 추가 된 [XSD 스키마 소개 &#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)를 참조 하세요. XDR을 사용 하는 레거시 응용 프로그램의 경우 [SQLXML 4.0&#41;에서 사용 되지 &#40;주석이 추가 된 Xdr 스키마 ](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)를 참조 하세요.  
  
## <a name="dealing-with-data-types"></a>데이터 형식 처리  
 `image`스키마가을 사용 `binary` `varbinary` [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `sql:datatype`하 여, 또는 데이터 형식을 지정 하 고 xml 데이터 형식을 지정 하지 않는 경우 updategram는 xml 데이터 형식이 인 `binary base 64`것으로 가정 합니다. 데이터가 `bin.base` 유형인 경우 명시적으로 유형(`dt:type=bin.base` 또는 `type="xsd:hexBinary"`)을 지정해야 합니다.  
  
 스키마에서 `dateTime`, `date` 또는 `time` XSD 데이터 형식을 지정하는 경우 `sql:datatype="dateTime"`을 사용하여 해당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식도 지정해야 합니다.  
  
 형식의 매개 변수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 처리할 때 매핑 스키마의 적절 `sql:datatype="money"` 한 노드에 명시적으로를 지정 해야 합니다. `money`  
  
## <a name="examples"></a>예  
 다음 예제를 사용 하 여 작업 예제를 만들려면 [SQLXML 예를 실행 하기 위한 요구 사항](../../sqlxml/requirements-for-running-sqlxml-examples.md)에 지정 된 요구 사항을 충족 해야 합니다.  
  
### <a name="a-creating-an-updategram-with-a-simple-mapping-schema"></a>A. 단순한 매핑 스키마를 사용하여 Updategram 만들기  
 다음 XSD 스키마 (sampleschema.xml)는 ** \<customer>** 요소를 Sales. customer 테이블에 매핑하는 매핑 스키마입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustID"    
                       sql:field="CustomerID"   
                       type="xsd:string" />  
        <xsd:attribute name="RegionID"    
                       sql:field="TerritoryID"    
                       type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 다음 Updategram은 Sales.Customer 테이블에 레코드를 삽입하고 이전 매핑 스키마를 사용하여 이 데이터를 테이블에 올바르게 매핑합니다. Updategram는 스키마에 정의 된 것과 같은 요소 이름인 ** \<Customer>** 를 사용 합니다. Updategram에서 특정 스키마를 지정하기 때문에 이 작업은 필수입니다.  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 SampleUpdateSchema.xml로 저장합니다.  
  
2.  아래 Updategram 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 SampleUpdateSchema.xml을 저장한 디렉터리와 같은 디렉터리에 SampleUpdategram.xml로 저장합니다.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleUpdateSchema.xml">  
        <updg:before>  
          <Customer CustID="1" RegionID="1"  />  
        </updg:before>  
        <updg:after>  
          <Customer CustID="1" RegionID="2" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
     매핑 스키마(SampleUpdateSchema.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
   <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
         xmlns:dt="urn:schemas-microsoft-com:datatypes"   
         xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
     <ElementType name="Customer" sql:relation="Sales.Customer" >  
       <AttributeType name="CustID" />  
       <AttributeType name="RegionID" />  
  
       <attribute type="CustID" sql:field="CustomerID" />  
       <attribute type="RegionID" sql:field="TerritoryID" />  
     </ElementType>  
   </Schema>   
```  
  
### <a name="b-inserting-a-record-by-using-the-parent-child-relationship-specified-in-the-mapping-schema"></a>B. 매핑 스키마에 지정된 부모-자식 관계를 사용하여 레코드 삽입  
 스키마 요소를 연결할 수 있습니다. Sql: relationship>요소는 스키마 요소 간의 부모-자식 관계를 지정 합니다. ** \<** 이 정보는 기본 키/외래 키 관계가 있는 해당 테이블을 업데이트하는 데 사용됩니다.  
  
 다음 매핑 스키마 (sampleschema.xml)는 ** \<Order>** 및 ** \<OD>** 라는 두 개의 요소로 구성 됩니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="OD"   
                     sql:relation="Sales.SalesOrderDetail"  
                     sql:relationship="OrderOD" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID"   type="xsd:integer" />  
              <xsd:attribute name="ProductID" type="xsd:integer" />  
             <xsd:attribute name="UnitPrice"  type="xsd:decimal" />  
             <xsd:attribute name="OrderQty"   type="xsd:integer" />  
             <xsd:attribute name="UnitPriceDiscount"   type="xsd:decimal" />  
  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesOrderID"  type="xsd:integer" />  
        <xsd:attribute name="OrderDate"  type="xsd:date" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 다음 updategram에서는이 XSD 스키마를 사용 하 여 주문 43860에 대해 새 주문 정보 레코드 ( ** \<after>** 블록의 ** \<OD>** 요소)를 추가 합니다. `mapping-schema` 특성은 Updategram의 매핑 스키마를 지정하는 데 사용됩니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43860" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43860" >  
           <OD ProductID="753" UnitPrice="$10.00"  
               Quantity="5" Discount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 SampleUpdateSchema.xml로 저장합니다.  
  
2.  위 Updategram 템플릿을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 SampleUpdateSchema.xml을 저장한 디렉터리와 같은 디렉터리에 SampleUpdategram.xml로 저장합니다.  
  
     매핑 스키마(SampleUpdateSchema.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="OD" sql:relation="Sales.SalesOrderDetail" >  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="ProductID" />  
    <AttributeType name="UnitPrice"  dt:type="fixed.14.4" />  
    <AttributeType name="OrderQty" />  
    <AttributeType name="UnitPriceDiscount" />  
  
    <attribute type="SalesOrderID" />  
    <attribute type="ProductID" />  
    <attribute type="UnitPrice" />  
    <attribute type="OrderQty" />  
    <attribute type="UnitPriceDiscount" />  
</ElementType>  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="OrderDate" />  
  
    <attribute type="CustomerID" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <element type="OD" >  
             <sql:relationship   
                   key-relation="Sales.SalesOrderHeader"  
                   key="SalesOrderID"  
                   foreign-key="SalesOrderID"  
                   foreign-relation="Sales.SalesOrderDetail" />  
    </element>  
</ElementType>  
</Schema>  
```  
  
### <a name="c-inserting-a-record-by-using-the-parent-child-relationship-and-inverse-annotation-specified-in-the-xsd-schema"></a>C. XSD 스키마에 지정된 부모-자식 관계 및 inverse 주석을 사용하여 레코드 삽입  
 이 예에서는 Updategram 논리가 XSD에 지정된 부모-자식 관계를 사용하여 업데이트를 처리하는 방법 및 `inverse` 주석이 사용되는 방법을 보여 줍니다. `inverse` 주석에 대 한 자세한 내용은 sql: [relationship에 Sql: 역함수 지정 &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)를 참조 하세요.  
  
 이 예에서는 다음 테이블이 **tempdb** 데이터베이스에 있다고 가정 합니다.  
  
-   `Cust (CustomerID, CompanyName)`. 여기서 `CustomerID`는 기본 키입니다.  
  
-   `Ord (OrderID, CustomerID)`. 여기서 `CustomerID`는 `CustomerID` 테이블의 `Cust` 기본 키를 참조하는 외래 키입니다.  
  
 Updategram은 다음 XSD 스키마를 사용하여 Cust 및 Ord 테이블에 레코드를 삽입합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
       <sql:relationship name="OrdCust" inverse="true"  
                  parent="Ord"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Cust"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
<xsd:element name="Order" sql:relation="Ord">  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customer" sql:relationship="OrdCust"/>  
    </xsd:sequence>  
    <xsd:attribute name="OrderID"   type="xsd:int"/>  
    <xsd:attribute name="CustomerID" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
<xsd:element name="Customer" sql:relation="Cust">  
  <xsd:complexType>  
     <xsd:attribute name="CustomerID"  type="xsd:string"/>  
    <xsd:attribute name="CompanyName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
</xsd:schema>  
```  
  
 이 예의 XSD 스키마에는 ** \<Customer>** 와 ** \<Order>** 요소가 있으며 두 요소 간의 부모-자식 관계를 지정 합니다. 부모 요소와 ** \<Customer>** 를 자식 요소로 ** \<>순서** 를 식별 합니다.  
  
 Updategram 처리 논리에서는 부모-자식 관계에 대한 정보를 사용하여 레코드가 테이블에 삽입되는 순서를 확인합니다. 이 예에서 updategram 논리는 먼저 Ord 테이블에 레코드를 삽입 한 다음 ( ** \<Order>** 는 부모), ** \<Customer>** 가 자식 이기 때문에 Cust 테이블에 레코드를 삽입 하려고 시도 합니다. 하지만 데이터베이스 테이블 스키마에 포함된 기본 키/외래 키 정보 때문에 이 삽입 작업을 수행하면 데이터베이스에서 외래 키 위반이 발생하고 삽입이 실패합니다.  
  
 업데이트 작업 중에 부모-자식 관계를 updategram 논리에 지시 하려면 ** \<relationship>** 요소에 `inverse` 주석을 지정 합니다. 그 결과, 레코드가 먼저 Cust 테이블에 추가된 다음 Ord 테이블에 추가되어 작업이 성공합니다.  
  
 다음 Updategram은 지정한 XSD 스키마를 사용하여 Ord 테이블에 주문(OrderID=2)을 삽입하고 Cust 테이블에 고객(CustomerID='AAAAA')을 삽입합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before/>  
    <updg:after>  
      <Order OrderID="2" CustomerID="AAAAA" >  
        <Customer CustomerID="AAAAA" CompanyName="AAAAA Company" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  **Tempdb** 데이터베이스에 다음 테이블을 만듭니다.  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust(CustomerID varchar(5) primary key,   
                      CompanyName varchar(20))  
    GO  
    CREATE TABLE Ord (OrderID int primary key,   
                      CustomerID varchar(5) references Cust(CustomerID))  
    GO  
    ```  
  
2.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 SampleUpdateSchema.xml로 저장합니다.  
  
3.  위 Updategram 템플릿을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 SampleUpdateSchema.xml을 저장한 디렉터리와 같은 디렉터리에 SampleUpdategram.xml로 저장합니다.  
  
     매핑 스키마(SampleUpdateSchema.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
4.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Updategram 보안 고려 사항은 SQLXML 4.0&#41;&#40;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
