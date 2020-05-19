---
title: 'Sql: is 상수를 사용 하 여 상수 요소 만들기 (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 37270dbed7a457a9e0adf5816ce02c502c8601f8
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703638"
---
# <a name="creating-constant-elements-using-sqlis-constant-sqlxml-40"></a>sql:is-constant를 사용하여 상수 요소 만들기(SQLXML 4.0)
  상수 요소, 즉 데이터베이스 테이블 또는 열에 매핑되지 않는 XSD 스키마의 요소를 지정 하려면 주석을 사용할 수 있습니다 `sql:is-constant` . 이 주석은 부울 값(0=false, 1=true)을 사용합니다. 허용되는 값은 0, 1, true 및 false입니다. `sql:is-constant` 주석은 특성이 없는 요소에 지정할 수 있습니다. 값이 true(또는 1)인 요소에 이 주석을 지정하면 해당 요소는 데이터베이스에 매핑되지 않지만 XML 문서에 계속 표시됩니다.  
  
 `sql:is-constant` 주석은 다음과 같은 용도로 사용할 수 있습니다.  
  
-   XML 문서에 최상위 요소 추가. XML 문서에는 단일 최상위 요소(root 요소)가 필요합니다.  
  
-   모든 주문을 래핑하는 ** \< orders>** 요소와 같은 컨테이너 요소 만들기  
  
 `sql:is-constant`주석은 ** \< complexType>** 요소에 추가할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예를 실행 하기 위한 요구 사항](../sqlxml/requirements-for-running-sqlxml-examples.md)을 참조 하세요.  
  
### <a name="a-specifying-sqlis-constant-to-add-a-container-element"></a>A. 컨테이너 요소를 추가하는 sql:is-constant 지정  
 주석이 추가 된이 XSD 스키마에서 ** \< customerorders>** 은 `sql:is-constant` 값이 1 인 특성을 지정 하 여 상수 요소로 정의 됩니다. 따라서 ** \< customerorders>** 은 데이터베이스 테이블 또는 열에 매핑되지 않습니다. 이 상수 요소는 자식 요소 ** \<>순서 대로** 구성 됩니다.  
  
 ** \< Customerorders>** 는 어떠한 데이터베이스 테이블이 나 열에도 매핑되지 않지만 결과 XML에는 자식 요소 ** \<>순서** 를 포함 하는 컨테이너 요소로 표시 됩니다.  
  
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
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 쿼리 실행](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
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
  
  
