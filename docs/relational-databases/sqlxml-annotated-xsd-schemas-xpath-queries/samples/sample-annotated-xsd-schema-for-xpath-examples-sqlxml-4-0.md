---
title: XPath에 대해 주석이 추가 된 샘플 XSD 스키마 (SQLXML)
description: SQLXML 4.0의 XPath 쿼리를 보여 주기 위해이 섹션의 예제에서 사용 하는 주석이 추가 된 XSD 스키마를 확인 합니다.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], annotated XSD schemas in queries
- annotated XSD schemas, samples
- annotated XSD schemas, queries
ms.assetid: fefa2cc8-2d3c-4336-aeae-ce063a3a8df2
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a3919201b1e65277d9fc248c48ece00d98c69940
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725863"
---
# <a name="sample-annotated-xsd-schema-for-xpath-examples-sqlxml-40"></a>XPath 예에 대한 주석이 추가된 예제 XSD 스키마(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  이 섹션의 예제 XPath 쿼리는 매핑 스키마를 참조합니다. 해당 매핑 스키마는 주석이 추가된 XSD(XML 스키마) 파일입니다. 매핑 스키마에 대 한 자세한 내용은 [주석이 추가 된 XSD 스키마 소개 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)을 참조 하세요.  
  
 주석이 추가된 XSD 스키마에 대해 XPath 쿼리를 실행하려면 다음 작업을 수행해야 합니다.  
  
-   XPath 쿼리가 포함된 템플릿을 만듭니다. 이 템플릿에서 XPath 쿼리를 실행할 대상 매핑 스키마를 지정합니다. 이 경우 매핑 스키마를 디렉터리 (또는 해당 하위 디렉터리 중 하나)에 저장 해야 합니다 .이 경우 템플릿 파일에 연결 된 상대 경로는 템플릿의 **매핑 스키마** 특성 값으로 지정 됩니다.  
  
-   쿼리를 실행하는 데 ADO에 대한 SQLXML 확장을 사용하는 테스트 애플리케이션을 만듭니다. 자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 이 섹션의 모든 예에서는 이해를 돕기 위해 템플릿에 XPath 쿼리를 지정하고 ADO를 사용하여 템플릿을 실행합니다. 따라서 SampleSchema1.xml이라는 다음 매핑 스키마 파일을 사용해야 합니다. 이 파일을 템플릿이 저장된 디렉터리에 저장합니다.  
  
## <a name="sample-annotated-xsd-schema-sampleschema1xml"></a>주석이 추가된 예제 XSD 스키마(SampleSchema1.xml)  
  
```  
<?xml version="1.0"?>  
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
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustOrders" />  
     </xsd:sequence>  
     <xsd:attribute name="CustomerID" type="xsd:ID"/>  
     <xsd:attribute name="TerritoryID"/>  
     <xsd:attribute name="AccountNumber"/>  
     <xsd:attribute name="CustomerType"/>  
     <xsd:attribute name="Orders" type="xsd:IDREFS" sql:prefix="Ord-"/>  
  </xsd:complexType>  
  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" type="OrderType"/>  
  
  <xsd:complexType name="OrderType">  
     <xsd:sequence>  
        <xsd:element name="OrderDetail"   
                     sql:relation="Sales.SalesOrderDetail"  
                     sql:relationship="OrderOrderDetail" />  
     </xsd:sequence>  
     <xsd:attribute name="SalesOrderID" type="xsd:ID" sql:prefix="Ord-"/>  
     <xsd:attribute name="SalesPersonID"/>  
     <xsd:attribute name="OrderDate"/>  
     <xsd:attribute name="DueDate"/>  
     <xsd:attribute name="ShipDate"/>  
  </xsd:complexType>  
  
  <xsd:element name="OrderDetail" sql:relation="Sales.SalesOrderDetail" type="OrderDetailType"/>  
  
  <xsd:complexType name="OrderDetailType">  
    <xsd:attribute name="ProductID" type="xsd:IDREF"/>  
    <xsd:attribute name="UnitPrice"/>  
    <xsd:attribute name="OrderQty"/>  
    <xsd:attribute name="UnitPriceDiscount"/>  
  </xsd:complexType>  
  
  <xsd:element name="UnitPriceDiscount" sql:relation="Sales.SalesOrderDetail" type="DiscountType"/>  
  
  <xsd:complexType name="DiscountType">  
    <xsd:simpleContent>  
       <xsd:extension base="xsd:string">  
          <xsd:anyAttribute namespace="##other" processContents="lax"/>  
       </xsd:extension>  
    </xsd:simpleContent>  
  </xsd:complexType>  
  
  <xsd:element name="Contact" sql:relation="Person.Contact" type="ContactType"/>  
  
  <xsd:complexType name="ContactType">  
    <xsd:attribute name="ContactID"/>  
    <xsd:attribute name="LastName"/>  
    <xsd:attribute name="FirstName"/>  
    <xsd:attribute name="Title"/>  
  </xsd:complexType>  
  
</xsd:schema>  
```  
  
  
