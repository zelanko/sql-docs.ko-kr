---
title: "sql:-필드 및 sql:-(SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- limiting values [SQLXML]
- limit-value annotation
- limit-field annotation
- sql:limit-field
- sql:limit-value
- filtering [SQLXML]
ms.assetid: 402c21cf-9566-463f-a928-f94270c11db3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3cdaba9ced51e09a01947af986ce77a1d66cb6b6
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="annotation-interpretation---sqllimit-field-and-sqllimit-value"></a>주석 해석-sql:-필드 및 sql:-값
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
XML 대량 로드는 해당 정의별로 **sql:limit-field** 및 **sql:limit-value** 주석을 처리합니다. 자세한 내용은 참조 [필터링 사용 하 여 값-필드 및 sql:-값 &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md).  
  
 예를 들어 데이터베이스에 다음과 같은 테이블이 포함된다고 가정합니다.  
  
-   Customer (CustomerID, CompanyName)  
  
-   Addresses (CustomerID, StreetAddress, AddressType)  
  
 고객은 많은 주소를 가질 수 있으며, 각 주소에 주소 유형(예: 배달 주소 또는 요금 청구서 주소)이 연결되어 있습니다.  
  
 이제 다음과 같은 주석이 추가된 XSD 스키마에 지정된 이러한 테이블의 XML 뷰를 고려해 보십시오.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustAddr"  
        parent="Customer"  
        parent-key="CustomerID"  
        child="Address"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustomerID"   type="xsd:int" />   
        <xsd:attribute name="CompanyName"  type="xsd:string" />  
        <xsd:attribute name="BillTo"   
                       type="xsd:string"   
                       sql:relation="Address"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="billing"  
                       sql:relationship="CustAddr" >  
        </xsd:attribute>  
        <xsd:attribute name="ShipTo"   
                       type="xsd:string"   
                       sql:relation="Address"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="shipping"  
                       sql:relationship="CustAddr" >  
        </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 이 스키마와 XML 데이터를 받으면 XML 대량 로드는 BillTo 특성에 지정된 값을 CustAddress 테이블의 StreetAddress 열에 삽입하고 "billing" 값을 AddressType 열에 삽입합니다.  
  
 마찬가지로, XML 대량 로드는 ShipTo 특성에 지정된 값을 StreetAddress 열에 삽입하고 "shipping" 값을 AddressType 열에 삽입합니다.  
  
### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  이 예에서 제공하는 스키마를 SampleSchema.xml로 저장합니다.  
  
2.  다음 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE Customer(  
                     CustomerID     int         PRIMARY KEY,  
                     CompanyName    varchar(20) NOT NULL)  
    GO  
    CREATE TABLE Address(  
                      CustomerID     int        FOREIGN KEY REFERENCES   
                                                 Customer(CustomerID),   
                      StreetAddress  varchar(50),  
                      AddressType    varchar(10))  
    GO  
    ```  
  
3.  다음 예제 데이터를 SampleXMLData.xml로 저장합니다.  
  
    ```  
    <Customer CustomerID="1111" CompanyName="Sean Chai" City="NY"   
                 BillTo="111 Maple (Billing) "   
                 ShipTo="111 Maple (Shipping)" />  
    <Customer CustomerID="1112" CompanyName="Dont Know" City="LA"   
                 BillTo="222 Spruce (Billing)"   
                 ShipTo="222 Spruce (Shipping)" />  
    ```  
  
4.  XML 대량 로드를 실행하려면 이 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] VBScript(Visual Basic Scripting Edition) 예를 Sample.vbs로 저장한 다음 이 스크립트를 실행합니다.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.XMLFragment = True  
    objBL.CheckConstraints=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="CompanyName" />  
    <AttributeType name="BillTo" />  
    <AttributeType name="ShipTo" />  
  
    <attribute type="CustomerID" />  
    <attribute type="CompanyName" />  
    <attribute type="BillTo"   
                sql:limit-field="AddressType"  
                sql:limit-value="billing"  
                sql:field="StreetAddress"  
                sql:relation="Address" >  
                <sql:relationship   
                        key="CustomerID"  
                        key-relation="Customer"  
                        foreign-relation="Address"  
                        foreign-key="CustomerID" />  
    </attribute>  
    <attribute type="ShipTo"   
                sql:limit-field="AddressType"  
                sql:limit-value="shipping"  
                sql:field="StreetAddress"  
                sql:relation="Address" >  
                <sql:relationship   
                     key="CustomerID"  
                     key-relation="Customer"  
                     foreign-relation="Address"  
                     foreign-key="CustomerID" />  
    </attribute>  
</ElementType>  
</Schema>  
```  
  
  
