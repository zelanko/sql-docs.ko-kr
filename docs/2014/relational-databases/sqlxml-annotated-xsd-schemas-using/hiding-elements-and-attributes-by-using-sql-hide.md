---
title: Sql:hide를 사용 하 여 요소 및 특성을 숨기기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- hiding elements
- element mapping [SQLXML], hiding attributes and elements
- hide annotation
- sql:hide
- table/view mapping [SQLXML], hiding attributes and elements
- table mapping [SQLXML], hiding attributes and elements
- hiding attributes
- annotated XSD schemas, hiding attributes and elements
- attribute mapping [SQLXML], hiding attributes and elements
- column mapping [SQLXML]
- element hiding [SQLXML]
- XSD schemas [SQLXML], hiding attributes and elements
- attribute hiding [SQLXML]
ms.assetid: 0978301b-f068-46b6-82b9-dc555161f52e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 541f5ccff727552730e4648552ad5126fdfd4858
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52793615"
---
# <a name="hiding-elements-and-attributes-by-using-sqlhide"></a>sql:hide를 사용하여 요소 및 특성 숨기기
  XSD 스키마에 대해 XPath 쿼리를 실행하면 결과 XML 문서에는 스키마에 지정된 요소와 특성이 포함됩니다. `sql:hide` 주석을 사용하여 일부 요소와 특성이 스키마에서 숨겨지도록 지정할 수 있습니다. 이는 쿼리의 선택 조건에 스키마의 특정 요소나 특성이 필요하지만 생성되는 XML 문서에는 해당 요소나 특성이 포함되지 않게 하려는 경우에 유용합니다.  
  
 `sql:hide` 주석은 부울 값(0=false, 1=true)을 사용합니다. 허용되는 값은 0, 1, true 및 false입니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예 실행에 대 한 요구 사항](../sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-sqlhide-on-an-attribute"></a>1. 특성에 sql:hide 지정  
 이루어져 있으며이 예에서 XSD 스키마는  **\<Person.Contact >** 요소를 사용 하 여 **ContactID**, **이름**, 및 **성** 속성입니다.  
  
  **\<Person.Contact >** 요소는 복합 형식이 고, 따라서 (기본 매핑) 같은 이름의 테이블에 매핑됩니다. 모든 특성의  **\<Person.Contact >** 요소는 단순 형식 및 AdventureWorks 데이터베이스에서 Person.Contacttable에 동일한 이름의 열에 매핑됩니다. 스키마에는 `sql:hide` 주석은에 지정 됩니다 합니다 **ContactID** 특성. 이 스키마에 대해 XPath 쿼리를 지정 하면 **ContactID** XML 문서에 반환 되지 않습니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID"  sql:hide="true" />   
       <xsd:attribute name="FirstName"   type="xsd:string" />   
       <xsd:attribute name="LastName"    type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 Hide.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 Hide.xml을 저장한 디렉터리와 같은 디렉터리에 HideT.xml로 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="Hide.xml">  
            /Person.Contact[@ContactID="1"]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(Hide.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\Hide.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 결과 집합은 다음과 같습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <Person.Contact FirstName="Gustavo" LastName="Achong" />   
</ROOT>  
```  
  
 요소에 대해 `sql:hide`를 지정하면 생성되는 XML 문서에 요소와 해당 특성 또는 자식 요소가 표시되지 않습니다. 다른 XSD 스키마는 다음과 같습니다 `sql:hide` 에 지정 된  **\<OD >** 요소:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:annotation>  
    <xsd:documentation>  
      Sales.Customer-Sales.SalesOrderHeader-Sales.SalesOrderDetail Schema  
      Copyright 2004 Microsoft. All rights reserved.  
    </xsd:documentation>  
    <xsd:appinfo>  
      <sql:relationship name="CustomerOrder"  
         parent="Sales.Customer"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Sales.SalesOrderHeader" />  
       <sql:relationship name="OrderOrderDetails"  
                  parent="Sales.SalesOrderHeader"  
                  parent-key="SalesOrderID"  
                  child-key="SalesOrderID"  
                  child="Sales.SalesOrderDetail"/>  
    </xsd:appinfo>  
  </xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Sales.Customer">  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
                     maxOccurs="unbounded"   
                     sql:relationship="CustomerOrder">  
          <xsd:complexType>  
            <xsd:sequence>  
               <xsd:element name="OD" sql:relation="Sales.SalesOrderDetail"                                       maxOccurs="unbounded"                                       sql:relationship="OrderOrderDetails"                                       sql:hide="1">  
                  <xsd:complexType>  
                    <xsd:attribute name="SalesOrderID" type="xsd:string"/>  
                    <xsd:attribute name="ProductID" type="xsd:string"/>  
                  </xsd:complexType>  
               </xsd:element>  
            </xsd:sequence>  
          <xsd:attribute name="CustomerID" type="xsd:string"/>  
          <xsd:attribute name="OID" sql:field="SalesOrderID"   
                                    type="xsd:string"/>  
          <xsd:attribute name="OrderDate" type="xsd:date"/>   
        </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
    <xsd:attribute name="CID" sql:field="CustomerID"   
                                type="xsd:string"/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 때 XPath 쿼리 (예를 들어 `/Customers[@CID="1"]`) 지정이 스키마에 대해 생성 되는 XML 문서에 포함 되어 있지 않습니다는  **\<OD >** 요소와 그 자식,이 부분 결과에 표시 된 대로:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customers CID="1">  
    <Order CustomerID="1" OID="43860" OrderDate="2001-08-01" />   
    <Order CustomerID="1" OID="44501" OrderDate="2001-11-01" />   
    <Order CustomerID="1" OID="45283" OrderDate="2002-02-01" />   
    <Order CustomerID="1" OID="46042" OrderDate="2002-05-01" />   
  </Customers>  
</ROOT>  
```  
  
  
