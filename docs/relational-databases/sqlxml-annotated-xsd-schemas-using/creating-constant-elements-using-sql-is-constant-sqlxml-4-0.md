---
title: 'Sql: is 상수 (SQLXML)를 사용 하 여 상수 요소 만들기'
description: 'SQLXML 4.0에서 sql: is 상수 주석을 사용 하 여 데이터베이스 테이블 또는 열에 매핑되지 않는 XSD 스키마에 상수 요소를 만드는 방법에 대해 알아봅니다.'
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- sql:is-constant
- XSD schemas [SQLXML], constant elements
- element mapping [SQLXML], constant elements
- is-constant annotation
- constant elements [SQLXML]
- annotated XSD schemas, constant elements
ms.assetid: 940eea1b-54f5-445f-b844-c894d9f3941b
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 50e2a6efad0cf14739fe2ef28135ea797ce6140e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750819"
---
# <a name="creating-constant-elements-using-sqlis-constant-sqlxml-40"></a>sql:is-constant를 사용하여 상수 요소 만들기(SQLXML 4.0)

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  상수 요소, 즉 데이터베이스 테이블 또는 열에 매핑되지 않는 XSD 스키마의 요소를 지정 하려면 **sql: is 상수** 주석을 사용할 수 있습니다. 이 주석은 부울 값(0=false, 1=true)을 사용합니다. 허용되는 값은 0, 1, true 및 false입니다. **Sql: is 상수** 주석은 특성이 없는 요소에 지정할 수 있습니다. 값이 true(또는 1)인 요소에 이 주석을 지정하면 해당 요소는 데이터베이스에 매핑되지 않지만 XML 문서에 계속 표시됩니다.  
  
 **Sql: is 상수** 주석을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   XML 문서에 최상위 요소 추가. XML 문서에는 단일 최상위 요소(root 요소)가 필요합니다.  
  
-   **\<Orders>** 모든 주문을 래핑하는 요소와 같은 컨테이너 요소 만들기  
  
 **Sql: is 상수** 주석은 요소에 추가할 수 있습니다 **\<complexType>** .  
  
## <a name="examples"></a>예제  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예를 실행 하기 위한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)을 참조 하세요.  
  
### <a name="a-specifying-sqlis-constant-to-add-a-container-element"></a>A. 컨테이너 요소를 추가하는 sql:is-constant 지정  
 주석이 추가 된이 XSD 스키마에서 **\<CustomerOrders>** 은 값이 1 인 **sql: is 상수** 특성을 지정 하 여 상수 요소로 정의 됩니다. 따라서 **\<CustomerOrders>** 는 데이터베이스 테이블 또는 열에 매핑되지 않습니다. 이 상수 요소는 **\<Order>** 자식 요소로 구성 됩니다.  
  
 **\<CustomerOrders>** 는 어떠한 데이터베이스 테이블이 나 열에도 매핑되지 않지만 결과 XML에는 자식 요소를 포함 하는 컨테이너 요소로 표시 됩니다 **\<Order>** .  
  
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
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="CustomerOrders" sql:is-constant="1" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"  
                           sql:relationship="CustOrders"   
                           maxOccurs="unbounded" >  
                <xsd:complexType>  
                   <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                   <xsd:attribute name="OrderDate" type="xsd:date" />  
                   <xsd:attribute name="CustomerID" type="xsd:string" />  
                </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>  
         </xsd:sequence>  
          <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 isConstant.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 isConstant.xml을 저장한 디렉터리와 같은 디렉터리에 isConstantT.xml로 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="isConstant.xml">  
            Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(isConstant.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\isConstant.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  

     자세한 내용은 [ADO를 사용 하 여 SQLXML 쿼리 실행](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
<Customer CustomerID="1">   
  <CustomerOrders>   
    <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1" />   
    <Order SalesOrderID="44501" OrderDate="2001-11-01" CustomerID="1" />   
    <Order SalesOrderID="45283" OrderDate="2002-02-01" CustomerID="1" />   
    <Order SalesOrderID="46042" OrderDate="2002-05-01" CustomerID="1" />   
    ...  
  </CustomerOrders>   
</Customer>   
</ROOT>  
```  
  
  
