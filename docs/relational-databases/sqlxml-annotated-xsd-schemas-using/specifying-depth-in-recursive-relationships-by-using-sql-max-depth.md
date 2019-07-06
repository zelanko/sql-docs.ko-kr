---
title: Sql:max를 사용 하 여 재귀 관계의 깊이 지정-깊이 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- max-depth annotation
- XPath queries [SQLXML], recursive relationships
- depth in recursive relationships [SQLXML]
- annotated XSD schemas, recursive relationships
- relationships [SQLXML], recursive relationships
- self joins
- recursive relationships [SQLXML]
- recursion [SQLXML]
- sql:max-depth
- recursive joins [SQLXML]
ms.assetid: 0ffdd57d-dc30-44d9-a8a0-f21cadedb327
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2cb9e99581ad5af36ddacd33599c05ead61b4e13
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581941"
---
# <a name="specifying-depth-in-recursive-relationships-by-using-sqlmax-depth"></a>sql:max-depth를 사용하여 재귀 관계의 깊이 지정
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  관계형 데이터베이스에서 테이블이 자신과 관계를 맺고 있는 경우 재귀 관계라고 합니다. 예를 들어 supervisor-supervisee 관계에서 직원 레코드를 저장하는 테이블은 자신과 관계가 있습니다. 이 경우 employees 테이블은 관계의 한쪽에서는 supervisor 역할을 하고 다른 쪽에서는 supervisee 역할을 합니다.  
  
 요소와 해당 상위 항목이 동일한 유형인 경우 매핑 스키마에 재귀 관계가 포함될 수 있습니다.  
  
## <a name="example-a"></a>예 1  
 다음 테이블을 살펴보십시오.  
  
```  
Emp (EmployeeID, FirstName, LastName, ReportsTo)  
```  
  
 이 테이블에서 ReportsTo 열은 관리자의 직원 ID를 저장합니다.  
  
 다음 XML 조각에서처럼 관리자가 계층 구조의 맨 위에 있고 해당 관리자에게 보고하는 직원이 해당하는 계층에 표시되는 직원에 대한 XML 계층 구조를 생성하려고 한다고 가정합니다. 새로운이 조각에 표시 되는 *재귀 트리* 직원 1에 대 한 합니다.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
     <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
     <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
        <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
          <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
...  
...  
</root>  
```  
  
 이 조각에서 직원 5는 직원 4에게, 직원 4는 직원 3에게, 직원 3 및 2는 직원 1에게 보고합니다.  
  
 이러한 결과를 얻으려면 다음 XSD 스키마를 사용하고 해당 스키마에 대해 XPath 쿼리를 지정할 수 있습니다. 스키마에 설명 합니다는  **\<Emp >** 구성 된 유형의 요소는  **\<Emp >** EmployeeType 동일한 형식의 자식 요소입니다. 이는 요소와 해당 상위 항목이 동일한 유형인 재귀 관계입니다. 또한 스키마에서는  **\<sql: relationship >** supervisor와 supervisee 간의 부모-자식 관계를 설명 합니다. 이 사실은  **\<sql: relationship >** 에서 Emp는 부모 및 자식 테이블입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="6" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 관계가 재귀적이므로 스키마에서 재귀 깊이를 지정할 방법이 필요합니다. 그렇지 않으면 무한 재귀(직원이 직원에게 보고하고 이 직원은 또 다른 직원에게 보고하는 등)가 생성됩니다. 합니다 **sql:max-깊이** 주석을 사용 하면 재귀가 계속 깊이에서 지정할 수 있습니다. 에 대 한 값을 지정 하려면이 특정 예제의 **sql:max-깊이**를 얼마나 깊이 관리 계층은 회사에서 알고 있어야 합니다.  
  
> [!NOTE]  
>  스키마를 지정 합니다 **sql:-필드** 주석을 하지만 지정 하지 않습니다는 **sql:-값** 주석입니다. 따라서 결과 계층 구조에서 최상위 노드는 누구에게도 보고하지 않는 직원 (ReportsTo은 NULL입니다.) 지정 **sql:-필드** 지정 하지 않으면 **sql:-값** (기본값은 NULL) 주석이 작업을 수행 합니다. 가능한 모든 보고를 포함 하는 결과 XML 트리 (테이블의 모든 직원에 대 한 보고 트리)를 제거 합니다 **sql:-필드** 스키마에서 주석입니다.  
  
> [!NOTE]  
>  다음 절차에서는 tempdb 데이터베이스를 사용합니다.  
  
#### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  tempdb 데이터베이스에서 가상 루트가 가리키는 Emp라는 예제 테이블을 만듭니다.  
  
    ```  
    USE tempdb  
    CREATE TABLE Emp (  
           EmployeeID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    ```  
  
2.  다음 예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Emp values (1, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Emp values (2, 'Andrew', 'Fuller',1)  
    INSERT INTO Emp values (3, 'Janet', 'Leverling',1)  
    INSERT INTO Emp values (4, 'Margaret', 'Peacock',3)  
    INSERT INTO Emp values (5, 'Steven', 'Devolio',4)  
    INSERT INTO Emp values (6, 'Nancy', 'Buchanan',5)  
    INSERT INTO Emp values (7, 'Michael', 'Suyama',6)  
    ```  
  
3.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 maxDepth.xml로 저장합니다.  
  
4.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 maxDepth.xml을 저장한 디렉터리와 같은 디렉터리에 maxDepthT.xml로 저장합니다. 템플릿의 쿼리는 Emp 테이블의 모든 직원을 반환합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="maxDepth.xml">  
        /Emp  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(maxDepth.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\maxDepth.xml"  
    ```  
  
5.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다. 자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 다음은 결과입니다.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
    <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
      <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
        <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
          <Emp FirstName="Nancy" EmployeeID="6" LastName="Buchanan">  
            <Emp FirstName="Michael" EmployeeID="7" LastName="Suyama" />   
          </Emp>  
        </Emp>  
      </Emp>  
    </Emp>  
  </Emp>  
</root>  
```  
  
> [!NOTE]  
>  다른 깊이의 계층 구조에서 결과 얻으려면의 값을 변경 합니다 **sql:max-깊이** 스키마에서 주석을 템플릿을 각 변경 후에 다시 실행 하 고 합니다.  
  
 이전 스키마에 모든 합니다  **\<Emp >** 요소에 특성의 동일한 집합에 정확 하 게 했습니다 (**EmployeeID**를 **FirstName**, 및  **LastName**). 다음 스키마 추가 반환 하도록 약간 수정 되었습니다 **ReportsTo** 모두에 대 한 특성을  **\<Emp >** 을 관리자에 게 보고 하는 요소.  
  
 예를 들어 다음 XML 조각에서는 직원 1의 부하 직원을 보여 줍니다.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
<Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2"   
       ReportsTo="1" LastName="Fuller" />   
  <Emp FirstName="Janet" EmployeeID="3"   
       ReportsTo="1" LastName="Leverling">  
...  
...  
```  
  
 다음은 수정된 스키마입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:documentation>  
      Customer-Order-Order Details Schema  
      Copyright 2000 Microsoft. All rights reserved.  
    </xsd:documentation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"  
                  parent-key="EmployeeID"  
                  child="Emp"  
                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
                   type="EmpType"   
                   sql:relation="Emp"   
                   sql:key-fields="EmployeeID"   
                   sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmpType">  
    <xsd:sequence>  
       <xsd:element name="Emp"   
                    type="EmpType"   
                    sql:relation="Emp"   
                    sql:key-fields="EmployeeID"  
                    sql:relationship="SupervisorSupervisee"  
                    sql:max-depth="6"/>  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:int" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
    <xsd:attribute name="ReportsTo" type="xsd:int" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
## <a name="sqlmax-depth-annotation"></a>sql:max-depth 주석  
 재귀 관계로 이루어진 스키마에서는 재귀 깊이를 명시적으로 지정해야 합니다. 요청된 결과를 반환하는 해당 FOR XML EXPLICIT 쿼리를 성공적으로 생성하려면 이 작업을 수행해야 합니다.  
  
 사용 된 **sql:max-깊이** 스키마에 설명 된 재귀 관계의 재귀 깊이 지정 하려면 스키마에서 주석입니다. 값을 **sql:max-깊이** 주석은 재귀 횟수를 나타내는 양의 정수 (1 ~ 50):  값이 1는 요소에서 재귀가 중단 되는 **sql:max-깊이** 주석이 지정 되지 않으면 값이 2는 요소에서 다음 수준에서 재귀가 중단 됩니다 **sql:max-깊이** 지정 ; 등에입니다.  
  
> [!NOTE]  
>  기본 구현에서는 매핑 스키마에 대해 지정된 XPath 쿼리가 SELECT ... FOR XML EXPLICIT 쿼리로 합니다. 이 쿼리에서는 한정된 재귀 깊이를 지정해야 합니다. 에 대해 지정한 값이 높을수록 **sql:max-깊이**클수록 FOR XML EXPLICIT 쿼리는 생성 됩니다. 그러면 검색 시간이 느려질 수 있습니다.  
  
> [!NOTE]  
>  Updategrams 및 XML 대량 로드에서는 max-depth 주석을 무시합니다. 따라서 max-depth에 지정하는 값에 상관없이 재귀 업데이트 또는 삽입이 수행됩니다.  
  
## <a name="specifying-sqlmax-depth-on-complex-elements"></a>복잡한 요소에 대해 sql:max-depth 지정  
 합니다 **sql:max-깊이** 주석은 모든 복합 콘텐츠 요소에 지정할 수 있습니다.  
  
### <a name="recursive-elements"></a>재귀적 요소  
 경우 **sql:max-깊이** 부모 요소와 재귀 관계의 자식 요소에서 지정 합니다 **sql:max-깊이** 부모에 지정 된 주석이 우선 합니다. 예를 들어 다음 스키마에에서는 **sql:max-깊이** 주석은 부모 및 자식 직원 요소 모두에 지정 됩니다. 이 예에서 **sql:max-깊이 = 4**에 지정 된 된  **\<Emp >** 부모 요소 (supervisor 역할을 재생)가 우선 적용 됩니다. 합니다 **sql:max-깊이** 자식 요소에서 지정 된  **\<Emp >** (supervisee 역할을 재생) 요소는 무시 됩니다.  
  
#### <a name="example-b"></a>예 2  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo"   
                          sql:max-depth="3" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="2" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 이 스키마를 테스트하려면 이 항목의 앞부분에 있는 예 1에 제공된 단계를 따릅니다.  
  
### <a name="nonrecursive-elements"></a>비재귀 요소  
 경우는 **sql:max-깊이** 재귀가 발생 하지 않는 스키마의 요소에 주석이 지정 된 경우 무시 됩니다. 다음 스키마에는  **\<Emp >** 구성 요소를  **\<상수 >** 포함 하는 자식 요소를를  **\<Emp >** 자식 요소입니다.  
  
 이 스키마에는 **sql:max-깊이** 에 지정 된 주석 합니다  **\<상수 >** 사이 재귀 관계가 없으므로 요소는 무시 됩니다는  **\<Emp >** 부모 하며  **\<상수 >** 자식 요소입니다. 간에 재귀가 발생 하지만 합니다  **\<Emp >** 상위 하며  **\<Emp >** 자식입니다. 스키마를 지정 합니다 **sql:max-깊이** 둘 다에서 주석입니다. 따라서 합니다 **sql:max-깊이** 상위 항목에서 지정 된 주석 ( **\<Emp >** supervisor 역할에서)가 우선 적용 됩니다.  
  
#### <a name="example-c"></a>예 3  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"   
                  child="Emp"   
                  parent-key="EmployeeID"   
                  child-key="ReportsTo"/>  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
               sql:relation="Emp"   
               type="EmpType"  
               sql:limit-field="ReportsTo"  
               sql:max-depth="1" />  
    <xsd:complexType name="EmpType" >  
      <xsd:sequence>  
       <xsd:element name="Constant"   
                    sql:is-constant="1"   
                    sql:max-depth="20" >  
         <xsd:complexType >  
           <xsd:sequence>  
            <xsd:element name="Emp"   
                         sql:relation="Emp" type="EmpType"  
                         sql:relationship="SupervisorSupervisee"   
                         sql:max-depth="3" />  
         </xsd:sequence>  
         </xsd:complexType>  
         </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="EmployeeID" type="xsd:int" />  
    </xsd:complexType>  
</xsd:schema>  
```  
  
 이 스키마를 테스트하려면 이 항목의 앞부분에 있는 예 1에 제공된 단계를 따릅니다.  
  
## <a name="complex-types-derived-by-restriction"></a>제한에 의해 파생되는 복합 유형  
 복합 유형이 파생 있다면  **\<제한 >** , 해당 기본 복합 유형의 요소를 지정할 수 없습니다는 **sql:max-깊이** 주석입니다. 이러한 경우에는 **sql:max-깊이** 주석 파생 된 형식의 요소에 추가할 수 있습니다.  
  
 반면에 의해 복합 유형이 파생 있다면  **\<확장 >** , 해당 기본 복합 유형의 요소를 지정할 수는 **sql:max-깊이** 주석입니다.  
  
 예를 들어 다음 XSD 스키마 때문에 오류가 발생 합니다 **sql:max-깊이** 주석은 기본 형식에 지정 됩니다. 파생 된 형식에는이 주석이 지원 되지 않습니다  **\<제한 >** 다른 형식에서입니다. 이 문제를 해결 하려면 스키마를 변경 하 고 지정 해야 합니다 **sql:max-깊이** 파생 된 유형의 요소에서 주석입니다.  
  
#### <a name="example-d"></a>예 4  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:complexType name="CustomerBaseType">   
    <xsd:sequence>  
       <xsd:element name="CID" msdata:field="CustomerID" />  
       <xsd:element name="CompanyName"/>  
       <xsd:element name="Customers" msdata:max-depth="3">  
         <xsd:annotation>  
           <xsd:appinfo>  
             <msdata:relationship  
                     parent="Customers"  
                     parent-key="CustomerID"  
                     child-key="CustomerID"  
                     child="Customers" />  
           </xsd:appinfo>  
         </xsd:annotation>  
       </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
  <xsd:element name="Customers" type="CustomerType"/>  
  <xsd:complexType name="CustomerType">  
    <xsd:complexContent>  
       <xsd:restriction base="CustomerBaseType">  
          <xsd:sequence>  
            <xsd:element name="CID"   
                         type="xsd:string"/>  
            <xsd:element name="CompanyName"   
                         type="xsd:string"  
                         msdata:field="CName" />  
            <xsd:element name="Customers"   
                         type="CustomerType" />  
          </xsd:sequence>  
       </xsd:restriction>  
    </xsd:complexContent>  
  </xsd:complexType>  
</xsd:schema>   
```  
  
 스키마의 **sql:max-깊이** 에 지정 되어를 **CustomerBaseType** 복합 형식입니다. 스키마도 지정는  **\<고객 >** 형식의 요소가 **CustomerType**에서 파생 된 **CustomerBaseType**합니다. 이러한 스키마에 지정 된 XPath 쿼리 때문에 오류가 생성 됩니다 **sql:max-깊이** 제한 기본 형식의 정의 된 요소에서 지원 되지 않습니다.  
  
## <a name="schemas-with-a-deep-hierarchy"></a>중첩이 많은 계층 구조가 있는 스키마  
 요소에 자식 요소가 있고 자식 요소에는 또 다른 자식 요소가 있는 형식의 중첩이 많은 계층 구조를 포함하는 스키마가 있을 수 있습니다. 경우는 **sql:max-깊이** (요소로 최상위 수준 1, 2, 수준 자식 및 등) 500 개가 넘는 수준의 계층이 포함 된 XML 문서를 생성 하는 이러한 스키마에 지정 된 주석을, 오류가 반환 됩니다.  
  
  
