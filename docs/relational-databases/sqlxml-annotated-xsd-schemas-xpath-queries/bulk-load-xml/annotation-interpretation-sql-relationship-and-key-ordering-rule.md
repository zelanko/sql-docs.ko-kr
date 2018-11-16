---
title: 'sql: relationship 및 키 순서 지정 규칙 (SQLXML 4.0) | Microsoft 문서'
ms.custom: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ab60a5cae291c307b0717b2d90409e26b835327f
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675302"
---
# <a name="annotation-interpretation---sqlrelationship-and-key-ordering-rule"></a>주석 해석 - sql:relationship 및 키 순서 지정 규칙
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 대량 로드는 해당 노드의 범위가 시작될 때 레코드를 생성하고 해당 노드의 범위가 끝날 때 이러한 노드를 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 보내기 때문에 레코드의 데이터는 노드 범위 내에 있어야 합니다.  
  
 다음 XSD 스키마를 고려해 보십시오 사이 일 대 다 관계  **\<고객 >** 하 고  **\<순서 >** 요소 (한 명의 고객이 여러 개의 주문을 배치할 수) 사용 하 여 지정 된  **\<sql: relationship >** 요소:  
  
```  
<xsd:schema xmlns:xsd="https://www.w3.org/2001/XMLSchema"<>   
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
  
 로  **\<고객 >** 요소 노드의 범위가 시작 될, XML 대량 로드가 고객 레코드를 생성 합니다. 이 레코드 읽는 XML 대량 로드 될 때까지 유지  **\</Customer >** 합니다. 처리에서를  **\<순서 >** 요소 노드를 사용 하 여 XML 대량 로드  **\<sql: relationship >** CustOrder 테이블의 CustomerID 외래 키 열 값을 가져오려면  **\<고객 >** 때문에 부모 요소를를  **\<순서 >** 요소를 지정 하지 않습니다는 **CustomerID** 특성입니다. 에 정의 하는 것이  **\<고객 >** 지정 해야 요소를 **CustomerID** 지정 하기 전에 스키마의 특성  **\<sql: 관계 >** 합니다. 경우에이 고, 그렇지는  **\<순서 >** 요소의 범위가 시작, XML 대량 로드는 CustOrder 테이블에 대 한 레코드를 생성 및 XML 대량 로드에 도달 합니다  **\</>** 끝 태그에 해당 레코드를 보냅니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CustomerID 외래 키 열 값이 없는 합니다.  
  
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
  
     그러면 XML 대량 로드가 CustOrder 테이블의 CustomerID 외래 키 열에 NULL 값을 삽입합니다. XML 샘플 데이터를 수정 하는 경우 있도록를  **\<CustomerID >** 자식 요소 앞에 표시 된  **\<순서 >** 예상된 결과 가져오려면 자식 요소: XML 대량 로드 지정된 된 외래 키 값 열에 삽입합니다.  
  
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
  
  
