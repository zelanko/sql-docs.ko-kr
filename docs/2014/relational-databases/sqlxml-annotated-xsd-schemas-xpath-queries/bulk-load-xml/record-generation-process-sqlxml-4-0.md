---
title: 기록 생성 과정 (SQLXML 4.0) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], record generation process
- node scopes [SQLXML]
- record subsets [SQLXML]
- scope [SQLXML]
- key ordering rules [SQLXML]
- record generation process for bulk loads [SQLXML]
- entering node scope [SQLXML]
- bulk load [SQLXML], record generation process
- leaving node scope [SQLXML]
- schema mapping [SQLXML]
ms.assetid: d8885bbe-6f15-4fb9-9684-ca7883cfe9ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b43765b03ba42cede8c6879e749f1701f306d1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013343"
---
# <a name="record-generation-process-sqlxml-40"></a>레코드 생성 프로세스(SQLXML 4.0)
  XML 대량 로드는 XML 입력 데이터를 처리하고 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 적절한 테이블로 사용할 수 있도록 레코드를 준비합니다. XML 대량 로드의 로직은 새 레코드를 생성할 시기, 레코드 필드로 복사할 자식 요소나 특성 값, 레코드가 완성되어 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 삽입할 수 있도록 보낼 준비가 끝나는 시기를 결정합니다.  
  
 XML 대량 로드는 전체 XML 입력 데이터를 메모리로 로드하지 않으며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 보내기 전에 전체 레코드 집합을 생성하지 않습니다. 이것은 XML 입력 데이터가 큰 문서일 수 있으며 전체 문서를 메모리로 로드하면 많은 비용이 들 수 있기 때문입니다. 대신 XML 대량 로드는 다음을 수행합니다.  
  
1.  매핑 스키마를 분석하고 필요한 실행 계획을 준비합니다.  
  
2.  실행 계획을 입력 스트림의 데이터에 적용합니다.  
  
 이 순차적 처리에서는 XML 입력 데이터를 특정 방식으로 제공해야 하므로 XML 대량 로드가 매핑 스키마를 분석하는 방법과 레코드 생성 프로세스가 발생하는 방식을 이해하고 있어야 합니다. 이러한 이해를 바탕으로 XML 대량 로드에 원하는 결과를 생성하는 매핑 스키마를 제공할 수 있습니다.  
  
 XML 대량 로드는 주석을 사용하여 명시적으로 지정되거나 기본 매핑을 통해 암시적으로 지정된 열 및 테이블 매핑을 비롯한 일반적인 매핑 스키마 주석과 조인 관계를 처리합니다.  
  
> [!NOTE]  
>  여기에서는 주석이 추가된 XSD 또는 XDR 매핑 스키마를 잘 알고 있다고 가정합니다. 스키마에 대 한 자세한 내용은 [주석 XSD 스키마 소개 &#40;SQLXML 4.0&#41; ](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md) 또는 [주석 XDR 스키마 &#40;SQLXML 4.0에서 사용 되지 않습니다&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
 레코드 생성을 이해하려면 다음 개념을 이해해야 합니다.  
  
-   노드 범위  
  
-   레코드 생성 규칙  
  
-   레코드 하위 집합 및 키 순서 지정 규칙  
  
-   레코드 생성 규칙의 예외  
  
## <a name="scope-of-a-node"></a>노드 범위  
 XML 문서의 노드 (요소 또는 특성)가 *범위* XML 대량 로드에서 XML 입력된 데이터 스트림을 것으로 발견 되는 경우. 요소 노드의 경우 요소의 시작 태그로 요소의 범위가 시작됩니다. 특성 노드의 경우 특성 이름으로 특성의 범위가 시작됩니다.  
  
 범위에 사용할 데이터가 더 이상 없을 때 노드에서 범위가 끝납니다. 즉, 끝 태그(요소 노드의 경우)나 특성 값 끝(특성 노드의 경우)에서 범위가 끝납니다.  
  
## <a name="record-generation-rule"></a>레코드 생성 규칙  
 노드(요소 또는 특성)에서 범위가 시작되면 해당 노드에서 레코드가 생성될 수 있습니다. 이러한 레코드는 연결된 노드가 범위에 속하는 동안 유지됩니다. 노드가 범위를 벗어나면 XML 대량 로드는 생성된 레코드가 완성된 것으로 간주하여 해당 레코드를(데이터와 함께) 삽입할 수 있도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 보냅니다.  
  
 예를 들어, 다음 XSD 스키마 조각을 고려해 보십시오.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Customers" >  
   <xsd:complexType>  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
     <xsd:attribute name="CompanyName" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 스키마에 지정 된  **\<고객 >** 요소를 **CustomerID** 및 **CompanyName** 특성. `sql:relation` 주석 맵 합니다  **\<고객 >** Customers 테이블에는 요소입니다.  
  
 다음 XML 문서 조각을 고려하십시오.  
  
```  
<Customer CustomerID="1" CompanyName="xyz" />  
<Customer CustomerID="2" CompanyName="abc" />  
...  
```  
  
 XML 대량 로드에 이전 단락에서 설명한 스키마와 XML 데이터가 입력으로 제공되면 XML 대량 로드는 원본 데이터에서 다음과 같은 방식으로 노드(요소와 특성)를 처리합니다.  
  
-   첫 번째 시작 태그  **\<고객 >** 요소 범위에서 요소를 가져옵니다. 이 노드는 Customers 테이블에 매핑되므로 XML 대량 로드는 Customers 테이블에 대한 레코드를 생성합니다.  
  
-   스키마의 모든 특성에는  **\<고객 >** Customers 테이블의 열에 있는 요소 지도. 이러한 특성의 범위가 시작되면 XML 대량 로드는 해당 값을 부모 범위에 의해 미리 생성된 고객 레코드에 복사합니다.  
  
-   XML 대량 로드의 끝 태그에 도달 하는 경우는  **\<고객 >** 요소는 요소 범위를 벗어날. 그러면 XML 대량 로드는 레코드가 완료된 것으로 간주하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 해당 레코드를 보냅니다.  
  
 XML 대량 로드 각각에 대해이 과정을 따르는 후속  **\<고객 >** 요소.  
  
> [!IMPORTANT]  
>  이 모델에서는 끝 태그에 도달할 때(또는 노드가 범위를 벗어날 때) 레코드가 삽입되므로 레코드와 관련된 모든 데이터를 노드 범위 내에 정의해야 합니다.  
  
## <a name="record-subset-and-the-key-ordering-rule"></a>레코드 하위 집합 및 키 순서 지정 규칙  
 `<sql:relationship>`을 사용하는 매핑 스키마를 지정할 때 하위 집합이라는 용어는 관계의 외래 쪽에서 생성되는 레코드 집합을 나타냅니다. 다음 예에서는 CustOrder 레코드가 `<sql:relationship>`의 외래 쪽에 있습니다.  
  
 예를 들어 데이터베이스에 다음과 같은 테이블이 포함된다고 가정합니다.  
  
-   Cust (CustomerID, CompanyName, City)  
  
-   CustOrder (CustomerID, OrderID)  
  
 CustOrder 테이블의 CustomerID는 Cust 테이블의 CustomerID 기본 키를 참조하는 외래 키입니다.  
  
 이제 다음과 같은 주석이 추가된 XSD 스키마에 지정된 XML 뷰를 고려해 보십시오. 이 스키마에서는 `<sql:relationship>`을 사용하여 Cust 및 CustOrder 테이블 간의 관계를 지정합니다.  
  
```  
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
  
 예제 XML 데이터와 작업 예제를 만드는 단계는 아래에 지정되어 있습니다.  
  
-   경우는  **\<고객 >** XML 데이터 파일의 요소 노드가 범위에 입력, XML 대량 로드는 Cust 테이블에 대 한 레코드를 생성 합니다. 그런 다음 XML 대량 로드에서 필요한 열 값 (CustomerID, CompanyName, City)에 복사는  **\<CustomerID >** ,  **\<CompanyName >** , 및  **\<도시 >** 이러한 요소와 자식 요소 범위를 시작 합니다.  
  
-   경우는  **\<주문 >** 요소 노드가 범위를 입력, XML 대량 로드는 CustOrder 테이블에 레코드를 생성 합니다. XML 대량 로드의 값이 복사는 **OrderID** 이 레코드에 대 한 특성입니다. 가져온 CustomerID 열에 필요한 값은  **\<CustomerID >** 의 자식 요소는  **\<고객 >** 요소. 에 지정 된 정보를 사용 하는 XML 대량 로드 `<sql:relationship>` 경우가 아니면이 레코드에 대 한 CustomerID 외래 키 값을 가져오려고 합니다 **CustomerID** 특성에 지정 된를  **\<순서 >** 요소입니다. 일반 규칙은 자식 요소가 외래 키 특성 값을 명시적으로 지정하는 경우 XML 대량 로드가 해당 값을 사용하고 지정된 `<sql:relationship>`을 사용하여 부모 요소에서 값을 가져오지 않는 것입니다. 이  **\<주문 >** 요소 노드가 범위를 벗어나면 XML 대량 로드는 레코드를 전송, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다음 모든 후속 처리 및  **\<주문 >** element 노드 같은 방법으로 합니다.  
  
-   마지막으로  **\<고객 >** 요소 노드가 범위를 벗어날. 이 시점에서 XML 대량 로드가 고객 레코드를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 보냅니다. XML 대량 로드는 XML 데이터 스트림의 모든 후속 고객에 대해 이 프로세스를 따릅니다.  
  
 여기서 매핑 스키마에 대한 두 가지 사항을 확인할 수 있습니다.  
  
-   스키마 "포함" 규칙을 만족 하는 경우 (고객 순서와 관련 된 모든 데이터가 연결된 된 범위 내에서 정의 됩니다 예를 들어,  **\<고객 >** 및  **\<주문 >** element 노드), 대량 로드에 성공 하면.  
  
-   설명 하는  **\<고객 >** 요소를 해당 자식 요소는 적절 한 순서로 지정 됩니다. 이 경우는  **\<CustomerID >** 전에 자식 요소가 지정 되어 있는  **\<순서 >** 자식 요소. 즉, 입력된 XML 데이터 파일에는  **\<CustomerID >** 요소 값을 외래 키로 사용할 수 최대값은  **\<주문 >** 요소의 범위에 들어갈. 키 특성이 먼저 지정되므로 이것은 "키 순서 지정 규칙"입니다.  
  
     지정 하는 경우는  **\<CustomerID >** 후 자식 요소는  **\<주문 >** 값은 자식 요소를 사용할 수 없는 경우는  **\< 주문 >** 요소 범위를 입력 합니다. 경우는  **\</순서 >** 끝 태그를 읽은 다음, CustOrder 테이블에 레코드 형식이 있으면 완전 고 원하는 결과 얻을 수 없는 CustomerID 열에 NULL 값을 갖는 CustOrder 테이블에 삽입 됩니다.  
  
#### <a name="to-create-a-working-sample"></a>작업 예제를 만들려면  
  
1.  이 예에서 제공하는 스키마를 SampleSchema.xml로 저장합니다.  
  
2.  다음 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                 OrderID        int         PRIMARY KEY,  
                 CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
3.  다음 예제 XML 입력 데이터를 SampleXMLData.xml로 저장합니다.  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>   
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
        <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  XML 대량 로드를 실행하려면 다음 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] VBScript(Visual Basic Scripting Edition) 예제(BulkLoad.vbs)를 저장한 다음 실행합니다.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
## <a name="exceptions-to-the-record-generation-rule"></a>레코드 생성 규칙의 예외  
 노드가 IDREF 또는 IDREFS 형식인 경우 XML 대량 로드는 범위가 시작될 때 노드에 대한 레코드를 생성하지 않습니다. 따라서 스키마의 특정 위치에 레코드의 완전한 설명이 존재해야 합니다. IDREFS 형식이 무시되는 것처럼 `dt:type="nmtokens"` 주석이 무시됩니다.  
  
 예를 들어 다음 XSD 스키마를 설명 하는  **\<고객 >** 및  **\<주문 >** 요소. **\<고객 >** 요소에 포함 된 **OrderList** IDREFS 유형의 특성. `<sql:relationship>` 태그는 고객과 주문 목록 간의 일 대 다 관계를 지정합니다.  
  
 스키마는 다음과 같습니다.  
  
```  
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
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="CompanyName" type="xsd:string" />  
    <xsd:attribute name="City" type="xsd:string" />  
    <xsd:attribute name="OrderList"   
                       type="xsd:IDREFS"   
                       sql:relation="CustOrder"   
                       sql:field="OrderID"  
                       sql:relationship="CustCustOrder" >  
    </xsd:attribute>  
  </xsd:complexType>  
 </xsd:element>  
  
  <xsd:element name="Order" sql:relation="CustOrder" >  
   <xsd:complexType>  
    <xsd:attribute name="OrderID" type="xsd:string" />  
    <xsd:attribute name="CustomerID" type="xsd:integer" />  
    <xsd:attribute name="OrderDate" type="xsd:date" />  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 대량 로드에서 IDREFS 유형의 노드를 무시 하면 레코드를 생성 하지 않습니다 때의 **OrderList** 특성 노드가 범위를 입력 합니다. 따라서 Orders 테이블에 주문 레코드를 추가하려면 스키마의 특정 위치에서 해당 주문을 설명해야 합니다. 이 스키마에 지정 하는  **\<주문 >** 요소를 사용 하면 XML 대량 로드는 Orders 테이블에 주문 레코드를 추가 합니다. **\<주문 >** 요소는 CustOrder 테이블에 레코드를 작성 하는 데 필요한 모든 특성을 설명 합니다.  
  
 되도록 해야는 **CustomerID** 및 **OrderID** 값에  **\<고객 >** 의 값과 일치 하는 요소는  **\<주문 >** 요소. 참조 무결성을 유지하는 책임은 사용자에게 있습니다.  
  
#### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  다음 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
                  CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
                  CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID),  
                  OrderDate      datetime DEFAULT '2000-01-01')  
    GO  
    ```  
  
2.  이 예에서 제공하는 매핑 스키마를 SampleSchema.xml로 저장합니다.  
  
3.  다음 예제 XML 데이터를 SampleXMLData.xml로 저장합니다.  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1111" CompanyName="Sean Chai" City="NY"  
                 OrderList="Ord1 Ord2" />  
      <Customers CustomerID="1112" CompanyName="Dont Know" City="LA"  
                 OrderList="Ord3 Ord4" />  
      <Order OrderID="Ord1" CustomerID="1111" OrderDate="1999-01-01" />  
      <Order OrderID="Ord2" CustomerID="1111" OrderDate="1999-02-01" />  
      <Order OrderID="Ord3" CustomerID="1112" OrderDate="1999-03-01" />  
      <Order OrderID="Ord4" CustomerID="1112" OrderDate="1999-04-01" />  
    </ROOT>  
    ```  
  
4.  XML 대량 로드를 실행하려면 이 VBScript 예(SampleVB.vbs)를 저장한 다음 실행합니다.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
