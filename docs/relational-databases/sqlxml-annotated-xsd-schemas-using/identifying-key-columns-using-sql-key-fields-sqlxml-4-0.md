---
title: 'Sql: 키 필드 (SQLXML)를 사용 하 여 키 열 식별'
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nesting XML results
- proper nesting in results [SQLXML]
- sql:key-fields
- XSD schemas [SQLXML], key columns
- identifying key columns [SQLXML]
- annotated XSD schemas, key columns
- key columns [SQLXML]
- relationships [SQLXML], key columns
- hierarchical relationships [SQLXML]
- key-fields annotation
ms.assetid: 1a5ad868-8602-45c4-913d-6fbb837eebb0
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 71d42f9f3f819dc12964ea0f13de92dfc8db5663
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257387"
---
# <a name="identifying-key-columns-using-sqlkey-fields-sqlxml-40"></a>sql:key-fields(SQLXML 4.0)를 사용하여 키 열 식별
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSD 스키마에 대해 XPath 쿼리가 지정된 경우 결과에서 올바른 중첩을 얻으려면 대부분 키 정보가 필요합니다. **Sql: 키-필드** 주석을 지정 하면 적절 한 계층이 생성 됩니다.  
  
> [!NOTE]  
>  적절 한 중첩을 위해 테이블에 매핑되는 요소에 대해 **sql: key 필드** 를 지정 하는 것이 좋습니다. 기본 결과 집합의 순서가 생성되는 XML에 중요합니다. **Sql: 키-필드** 를 지정 하지 않으면 생성 된 XML이 제대로 구성 되지 않을 수 있습니다.  
  
 **Sql: 키 필드** 의 값은 관계의 행을 고유 하 게 식별 하는 열을 식별 합니다. 행을 고유하게 식별하는 데 둘 이상의 열이 필요한 경우 열 값이 공백으로 구분됩니다.  
  
 요소에 요소와 자식 요소 사이에 정의 된 ** \<sql: relationship>** 포함 되어 있지만 부모 요소에 지정 된 테이블의 기본 키를 제공 하지 않는 경우 **sql: 키-필드** 주석을 사용 해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예를 실행 하기 위한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)을 참조 하세요.  
  
### <a name="a-producing-the-appropriate-nesting-when-sqlrelationship-does-not-provide-sufficient-information"></a>A. Sql: relationship>에서 \<충분 한 정보를 제공 하지 않을 때 적절 한 중첩을 생성 합니다.  
 이 예에서는 **sql: key 필드** 를 지정 해야 하는 경우를 보여 줍니다.  
  
 다음과 같은 스키마를 살펴 보십시오. **이 \<** 스키마는 order>요소가 부모이 고 ** \<customer>** 요소가 자식인 ** \<order>** 와 ** \<customer>** 요소 간의 계층을 지정 합니다.  
  
 Sql: relationship>태그는 부모-자식 관계를 지정 하는 데 사용 됩니다. ** \<** Sales.SalesOrderHeader 테이블의 CustomerID를 Sales.Customer 테이블의 CustomerID 자식 키를 참조하는 부모 키로 식별합니다. ** \<Sql: relationship>** 에 제공 된 정보는 부모 테이블 (SalesOrderHeader)에서 행을 고유 하 게 식별 하는 데 충분 하지 않습니다. 따라서 **sql: 키-필드** 주석이 없으면 생성 되는 계층 구조가 정확 하지 않습니다.  
  
 ** \<Order>** 에 지정 된 **sql: 키 필드** 를 사용 하 여 주석은 부모 (SalesOrderHeader 테이블)의 행을 고유 하 게 식별 하 고 해당 자식 요소가 부모 아래에 나타납니다.  
  
 스키마는 다음과 같습니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrdCust"  
        parent="Sales.SalesOrderHeader"  
        parent-key="CustomerID"  
        child="Sales.Customer"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
               sql:key-fields="SalesOrderID">  
   <xsd:complexType>  
     <xsd:sequence>  
     <xsd:element name="Customer" sql:relation="Sales.Customer"   
                       sql:relationship="OrdCust"  >  
       <xsd:complexType>  
         <xsd:attribute name="CustID" sql:field="CustomerID" />  
         <xsd:attribute name="SoldBy" sql:field="SalesPersonID" />  
       </xsd:complexType>  
     </xsd:element>  
     </xsd:sequence>  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name= "CustomerID" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>이 스키마의 작업 예제를 만들려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 KeyFields1.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. KeyFields1.xml을 저장한 디렉터리와 같은 디렉터리에 KeyFields1T.xml로 파일을 저장합니다. 템플릿의 XPath 쿼리는 CustomerID가 3 보다 작은 모든 ** \<주문>** 요소를 반환 합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="KeyFields1.xml">  
            /Order[@CustomerID < 3]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(KeyFields1.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields1.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  

     자세한 내용은 [ADO를 사용 하 여 SQLXML 쿼리 실행](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
    <Order SalesOrderID="43860" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="44501" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="45283" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    .....  
</ROOT>  
```  
  
### <a name="b-specifying-sqlkey-fields-to-produce-proper-nesting-in-the-result"></a>B. sql:key-fields를 지정하여 결과에서 올바른 중첩 생성  
 다음 스키마에는 ** \<sql: relationship>** 를 사용 하 여 지정 된 계층이 없습니다. 스키마에서는 HumanResources 테이블의 직원을 고유 하 게 식별 하기 위해 **sql: 키-필드** 주석을 지정 해야 합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="HumanResources.Employee" sql:key-fields="EmployeeID" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Title">  
          <xsd:complexType>  
            <xsd:simpleContent>  
              <xsd:extension base="xsd:string">  
                 <xsd:attribute name="EmployeeID" type="xsd:integer" />  
              </xsd:extension>  
            </xsd:simpleContent>  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
   </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>이 스키마의 작업 예제를 만들려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 KeyFields2.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. KeyFields2.xml을 저장한 디렉터리와 같은 디렉터리에 KeyFields2T.xml로 파일을 저장합니다. 템플릿의 XPath 쿼리에서는 ** \<HumanResources>** 요소를 모두 반환 합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="KeyFields2.xml">  
        /HumanResources.Employee  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(KeyFields2.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields2.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 쿼리 실행](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 결과입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <HumanResources.Employee>  
    <Title EmployeeID="1">Production Technician - WC60</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="2">Marketing Assistant</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="3">Engineering Manager</Title>   
  </HumanResources.Employee>  
  ...  
</ROOT>  
```  
  
  
