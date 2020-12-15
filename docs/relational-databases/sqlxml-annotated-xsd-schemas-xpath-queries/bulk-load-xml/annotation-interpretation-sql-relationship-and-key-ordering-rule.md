---
title: 'sql: relationship 및 키 순서 지정 규칙 (SQLXML)'
description: 'SQLXML에서 sql: relationship 요소 및 키 순서 지정 규칙을 사용 하는 방법에 대해 알아봅니다.'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- key ordering rules [SQLXML]
- relationship annotation
ms.assetid: 914cb152-09f5-4b08-b35d-71940e4e9986
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1846a3db3194a81ce1d1522ac175e3988d3d3d23
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462934"
---
# <a name="annotation-interpretation---sqlrelationship-and-key-ordering-rule"></a>주석 해석 - sql:relationship 및 키 순서 지정 규칙
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  XML 대량 로드는 해당 노드의 범위가 시작될 때 레코드를 생성하고 해당 노드의 범위가 끝날 때 이러한 노드를 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 보내기 때문에 레코드의 데이터는 노드 범위 내에 있어야 합니다.  
  
 **\<Customer>** **\<Order>** 요소를 사용 하 여 및 요소 (한 명의 고객에 게 여러 개의 주문을 놓을 수 있음) 간의 일 대 다 관계를 지정 하는 다음 XSD 스키마를 고려해 보십시오 **\<sql:relationship>** .  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"<>   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 **\<Customer>** 요소 노드가 범위에 들어가면 XML 대량 로드에서 고객 레코드를 생성 합니다. 이 레코드는 XML 대량 로드 읽기가 끝날 때까지 유지 **\</Customer>** 됩니다. 요소 노드를 처리할 때 **\<Order>** XML 대량 로드는를 사용 하 여 **\<sql:relationship>** 부모 요소에서 CustOrder 테이블의 customerid 외래 키 열 값을 가져옵니다 **\<Customer>** **\<Order>** .이 요소는 **customerid** 특성을 지정 하지 않기 때문입니다. 즉 **\<Customer>** , 요소를 정의할 때를 지정 하기 전에 스키마에 **CustomerID** 특성을 지정 해야 합니다 **\<sql:relationship>** . 그렇지 않고 **\<Order>** 요소가 범위에 들어가면 Xml 대량 로드는 CustOrder 테이블에 대 한 레코드를 생성 하 고, Xml 대량 로드가 끝 태그에 도달 하면 **\</Order>** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CustomerID 외래 키 열 값을 사용 하지 않고에 레코드를 보냅니다.  
  
 이 예에서 제공하는 스키마를 SampleSchema.xml로 저장합니다.  
  
### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  다음 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
               CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
               CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
2.  다음 예제 데이터를 SampleXMLData.xml로 저장합니다.  
  
    ```  
    <ROOT>    
      <Customers>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
        <CustomerID>1111</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>    
        <Order OrderID="3" />  
        <CustomerID>1112</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
        <CustomerID>1113</CustomerID>  
      </Customers>  
    </ROOT>  
    ```  
  
3.  XML 대량 로드를 실행하려면 다음 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] VBScript(Visual Basic Scripting Edition) 예제를 MySample.vbs로 저장한 다음 실행합니다.  

    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
     그러면 XML 대량 로드가 CustOrder 테이블의 CustomerID 외래 키 열에 NULL 값을 삽입합니다. 자식 요소가 자식 요소 앞에 나타나도록 XML 샘플 데이터를 수정 하는 경우 **\<CustomerID>** **\<Order>** 예상 결과를 얻을 수 있습니다. Xml 대량 로드는 지정 된 외래 키 값을 열에 삽입 합니다.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID"  />  
   <ElementType name="CompanyName" />  
   <ElementType name="City"        />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
                 <sql:relationship  
                        key-relation    ="Cust"  
                        key             ="CustomerID"  
                        foreign-key     ="CustomerID"  
                        foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
  
