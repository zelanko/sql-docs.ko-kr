---
title: 'sql: 오버플로 필드 (SQLXML)'
description: 'Sql: 오버플로 필드 주석을 사용 하 여 XML 문서에서 사용 되지 않은 모든 데이터를 수신 하는 오버플로 열로 열을 식별 하는 방법에 대해 알아봅니다.'
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: f005182b-6151-432d-ab22-3bc025742cd3
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d0fa21bcd570a5f5196dfbc1bdf8e1bb6186cb8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462944"
---
# <a name="annotation-interpretation---sqloverflow-field"></a>주석 해석 - sql:overflow-field
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  스키마에서 열을 오버플로 열로 식별하여 XML 문서에서 사용되지 않은 데이터를 모두 받을 수 있습니다. 이 열은 **sql: 오버플로 필드** 주석을 사용 하 여 스키마에 지정 됩니다. 오버플로 열을 여러 개 지정할 수도 있습니다.  
  
 **Sql: 오버플로 필드가** 정의 된 XML 노드 (요소 또는 특성)가 범위에 들어올 때마다 오버플로 열이 활성화 되 고 소비 되지 않은 데이터를 수신 합니다. 노드가 범위를 벗어나면 오버플로 열이 더 이상 활성화되지 않고 XML 대량 로드를 통해 이전 오버플로 필드(있는 경우)가 활성화됩니다.  
  
 오버플로 열에 데이터를 저장 하는 경우 XML 대량 로드는 **sql: 오버플로 필드가** 정의 된 부모 요소의 여는 태그와 닫는 태그를 저장 합니다.  
  
 예를 들어, 다음 스키마는 및 요소에 대해 설명 합니다 **\<Customers>** **\<CustOrder>** . 이러한 각 요소는 오버플로 열을 식별합니다.  
  
```  
<?xml version="1.0" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
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
 <xsd:element name="ROOT" sql:is-constant="1">  
  <xsd:complexType>  
    <xsd:sequence>   
      <xsd:element name="Customers"   
                   sql:relation="Cust"  
                   sql:overflow-field="OverflowColumn">  
        <xsd:complexType>  
             <xsd:sequence>   
             <xsd:element name="CustomerID" type="xsd:integer"/>  
             <xsd:element name="CompanyName"  type="xsd:string"/>  
             <xsd:element name="City" type="xsd:string"/>  
             <xsd:element name="Order"  
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder"  
                          sql:overflow-field="OverflowColumn">  
               <xsd:complexType>  
                 <xsd:attribute name="OrderID"/>  
                 <xsd:attribute name="CustomerID"/>  
               </xsd:complexType>  
             </xsd:element>  
          </xsd:sequence>   
        </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 스키마에서 **\<Customer>** 요소는 Cust 테이블에 매핑되고 **\<Order>** 요소는 CustOrder 테이블에 매핑됩니다.  
  
 **\<Customer>** 및 요소는 모두 **\<Order>** 오버플로 열을 식별 합니다. 따라서 XML 대량 로드는 요소에 있는 모든 자식 요소와 특성을 **\<Customer>** Cust 테이블의 오버플로 열에 저장 하 고 **\<Order>** CustOrder 테이블의 오버플로 열에서 요소의 소비 되지 않은 모든 자식 요소와 특성을 저장 합니다.  
  
### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  이 예에서 제공하는 스키마를 SampleSchema.xml로 저장합니다.  
  
2.  다음 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE Cust (  
              CustomerID     int         PRIMARY KEY,  
              CompanyName    varchar(20) NOT NULL,  
              City           varchar(20) DEFAULT 'Seattle',  
              OverflowColumn nvarchar(200))  
    GO  
    CREATE TABLE CustOrder (  
              OrderID        int         PRIMARY KEY,  
              CustomerID     int         FOREIGN KEY REFERENCES  
                                              Cust(CustomerID),  
              OverflowColumn nvarchar(200))  
    GO  
    ```  
  
3.  다음 예제 XML 데이터를 SampleXMLData.xml로 저장합니다.  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
          <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
     </Customers>  
     <Customers>  
       <CustomerID>1112</CustomerID>  
       <CompanyName>Toms Spezialitten</CompanyName>  
       <City><![CDATA[LA]]> </City>  
       <xyz><address>111 Maple, Seattle</address></xyz>     
       <Order OrderID="3" />  
     </Customers>  
       <Customers>  
       <CustomerID>1113</CustomerID>  
       <CompanyName>Victuailles en stock</CompanyName>  
       <Order OrderID="4" />  
      </Customers>  
    </ROOT>  
    ```  
  
4.  XML 대량 로드를 실행하려면 이 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] VBScript(Visual Basic Scripting Edition) 예를 Sample.vbs로 저장한 다음 이 스크립트를 실행합니다.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
