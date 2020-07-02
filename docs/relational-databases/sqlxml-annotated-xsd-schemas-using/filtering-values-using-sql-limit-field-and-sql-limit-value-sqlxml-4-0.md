---
title: 'Sql: limit 필드 및 sql: limit 값 (SQLXML)으로 필터링'
description: 'SQLXML 4.0의 sql: limit 필드 및 sql: limit 값 주석을 사용 하 여 제한 값을 기준으로 쿼리에서 반환 되는 데이터를 필터링 하는 방법에 대해 알아봅니다.'
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, filtering values
- limiting values [SQLXML]
- limit-value annotation
- limit-field annotation
- sql:limit-field
- sql:limit-value
- filtering [SQLXML]
ms.assetid: c0f7ae92-eeec-430e-a66a-f22c3ae64a5e
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 50732a867c0329610b0a03eebcd97d3f3224d6e0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750775"
---
# <a name="filtering-values-using-sqllimit-field-and-sqllimit-value-sqlxml-40"></a>sql:limit-field와 sql:limit-value를 사용하여 값 필터링(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  데이터베이스 쿼리를 통해 반환되는 행을 어떤 제한 값을 기준으로 제한할 수 있습니다. **Sql: limit 필드** 및 **sql: limit 값** 주석은 제한 값이 포함 된 데이터베이스 열을 식별 하 고 반환 되는 데이터를 필터링 하는 데 사용할 특정 제한 값을 지정 하는 데 사용 됩니다.  
  
 **Sql: limit 필드** 주석은 제한 값이 포함 된 열을 식별 하는 데 사용 됩니다. 각 매핑된 요소나 특성에서 허용 됩니다.  
  
 **Sql: limit 값** 주석은 **sql: limit 필드** 주석에 지정 된 열에 제한 된 값을 지정 하는 데 사용 됩니다. **Sql: limit 값** 주석은 선택 사항입니다. **Sql: limit 값** 을 지정 하지 않으면 NULL 값이 가정 됩니다.  
  
> [!NOTE]  
>  매핑된 SQL 열이 **real**유형인 **sql: limit 필드** 를 사용할 때 SQLXML 4.0은 XML 스키마에 지정 된 대로 **sql: limit 값** 을 **nvarchar** 지정 된 값으로 변환 합니다. 이 경우 공학용 표기법을 사용하여 10진수 제한 값을 지정해야 합니다. 자세한 내용은 아래 2번 예를 참조하십시오.  
  
## <a name="examples"></a>예제  
 이러한 예를 사용하여 작업 예제를 만들려면 다음과 같은 제품이 설치되어 있어야 합니다.  
  
-   Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   MDAC 2.6 이상  
  
 아래의 예에서는 템플릿을 사용하여 매핑 XSD 스키마를 기준으로 XPath 쿼리를 지정합니다.  
  
### <a name="a-limiting-the-customer-addresses-returned-to-a-specific-address-type"></a>A. 고객 주소를 제한하여 특정 주소 형식만 반환  
 이 예에서 데이터베이스에는 다음과 같은 두 개의 테이블이 있습니다.  
  
-   Customer (CustomerID, CompanyName)  
  
-   Addresses (CustomerID, AddressType, StreetAddress)  
  
 고객에 대해 배달 주소 및/또는 요금 청구서 주소가 존재할 수 있습니다. AddressType 열의 값은 Shipping과 Billing입니다.  
  
 **ShipTo** Schema 특성이 주소 관계의 StreetAddress 열에 매핑되는 매핑 스키마입니다. 이 특성에 대해 반환 되는 값은 **sql: limit 필드** 및 **sql: limit 값** 주석을 지정 하 여 배송 주소로만 제한 됩니다. 마찬가지로 **BillTo** 스키마 특성은 고객의 청구 주소만 반환 합니다.  
  
 스키마는 다음과 같습니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustAddr"  
        parent="Customer"  
        parent-key="CustomerID"  
        child="Addresses"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Customer" >  
   <xsd:complexType>  
        <xsd:sequence>  
        <xsd:element name="BillTo"   
                       type="xsd:string"   
                       sql:relation="Addresses"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="billing"  
                       sql:relationship="CustAddr" >  
        </xsd:element>  
        <xsd:element name="ShipTo"   
                       type="xsd:string"   
                       sql:relation="Addresses"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="shipping"  
                       sql:relationship="CustAddr" >  
        </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:int" />   
        <xsd:attribute name="CompanyName"  type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  **Tempdb** 데이터베이스에 두 개의 테이블을 만듭니다.  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (CustomerID int primary key,   
                           CompanyName varchar(30))  
    CREATE TABLE Addresses(CustomerID int,   
                           StreetAddress varchar(50),  
                           AddressType varchar(10))  
    ```  
  
2.  예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Customer values (1, 'Company A')  
    INSERT INTO Customer values (2, 'Company B')  
  
    INSERT INTO Addresses values  
               (1, 'Obere Str. 57 Berlin', 'billing')  
    INSERT INTO Addresses values  
               (1, 'Avda. de la Constituci?n 2222 M?xico D.F.', 'shipping')  
    INSERT INTO Addresses values  
               (2, '120 Hanover Sq., London', 'billing')  
    INSERT INTO Addresses values  
               (2, 'Forsterstr. 57, Mannheim', 'shipping')  
    ```  
  
3.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 LimitFieldValue.xml로 저장합니다.  
  
4.  다음 템플릿(LimitFieldValueT.xml)을 만들고 이전 단계에서 스키마(LimitFieldValue.xml)를 저장한 것과 같은 디렉터리에 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="LimitFieldValue.xml">  
            /Customer  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(LimitFieldValue.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\MyDir\LimitFieldValue.xml"  
    ```  
  
5.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  

     자세한 내용은 [ADO를 사용 하 여 SQLXML 쿼리 실행](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 결과입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer CustomerID="1" CompanyName="Company A">   
     <BillTo>Obere Str. 57 Berlin</BillTo>   
     <ShipTo>Avda. de la Constituci?n 2222 M?xico D.F.</ShipTo>   
  </Customer>   
  <Customer CustomerID="2" CompanyName="Company B">   
     <BillTo>120 Hanover Sq., London</BillTo>   
     <ShipTo>Forsterstr. 57, Mannheim</ShipTo>   
   </Customer>   
</ROOT>  
```  
  
### <a name="b-limiting-results-based-on-a-discount-value-of-type-real-data"></a>B. Real 데이터 형식의 할인 값을 기준으로 결과 제한  
 이 예에서 데이터베이스에는 다음과 같은 두 개의 테이블이 있습니다.  
  
-   Orders (OrderID)  
  
-   OrderDetails (OrderID, ProductID, UnitPrice, Quantity, Price, Discount)  
  
 이는 주문 정보의 **orderid** 특성이 주문 관계의 orderid 열에 매핑되는 매핑 스키마입니다. 이 특성에 대해 반환 되는 값은 **sql:** 2.0000000 및 **sql: limit 값** 주석을 사용 하 여 할인율 (0.2) 값을 사용 하는 **할인율** 으로만 제한 됩니다.  
  
 스키마는 다음과 같습니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
   <xsd:appinfo>  
    <sql:relationship name="OrderOrderDetails"  
        parent="Orders"  
        parent-key="OrderID"  
        child="OrderDetails"  
        child-key="OrderID" />  
   </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="root" sql:is-constant="1">  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="Order" sql:relation="Orders" >  
          <xsd:complexType>  
             <xsd:sequence>  
                <xsd:element name="orderDetail"   
                       sql:relation="OrderDetails"   
                       sql:limit-field="Discount"                       sql:limit-value="2.0000000e-001"  
                       sql:relationship="OrderOrderDetails">  
                   <xsd:complexType>  
                     <xsd:attribute name="OrderID"   />   
                     <xsd:attribute name="ProductID" />   
                     <xsd:attribute name="Discount"  />   
                     <xsd:attribute name="Quantity"  />   
                     <xsd:attribute name="UnitPrice" />   
                   </xsd:complexType>  
                </xsd:element>  
            </xsd:sequence>  
           <xsd:attribute name="OrderID"/>   
          </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
   </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  **Tempdb** 데이터베이스에 두 개의 테이블을 만듭니다.  
  
    ```  
    USE tempdb  
    CREATE TABLE Orders ([OrderID] int NOT NULL ) ON [PRIMARY]  
    ALTER TABLE Orders WITH NOCHECK ADD   
    CONSTRAINT [PK_Orders] PRIMARY KEY  CLUSTERED (  
       [OrderID]  
     )  ON [PRIMARY]   
    CREATE TABLE [OrderDetails] (  
       [OrderID] int NOT NULL ,  
       [ProductID] int NOT NULL ,  
       [UnitPrice] money NULL ,  
       [Quantity] smallint NOT NULL ,  
       [Discount] real NOT NULL   
    ) ON [PRIMARY]  
    ```  
  
2.  예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Orders ([OrderID]) values (10248)  
    INSERT INTO Orders ([OrderID]) values (10250)  
    INSERT INTO Orders ([OrderID]) values (10251)  
    INSERT INTO Orders ([OrderID]) values (10257)  
    INSERT INTO Orders ([OrderID]) values (10258)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10248,11,14,12,0)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10250,51,42.4,35,0.15)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10251,22,16.8,6,0.05)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10257,77,10.4,15,0)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10258,2,15.2,50,0.2)  
    ```  
  
3.  디렉터리에 스키마(LimitFieldValue.xml)를 저장합니다.  
  
4.  다음 테스트 스크립트(TestQuery.vbs)를 만들어 MyServer를 현재 사용 중인 SQL Server 컴퓨터의 이름으로 수정한 다음 이전 단계에서 스키마를 저장한 것과 같은 디렉터리에 저장합니다.  
  
    ```  
    Set conn = CreateObject("ADODB.Connection")  
    conn.Open "Provider=SQLOLEDB;Data Source=MyServer;Database=tempdb;Integrated Security=SSPI"  
    conn.Properties("SQLXML Version") = "sqlxml.4.0"   
    Set cmd = CreateObject("ADODB.Command")  
    Set stm = CreateObject("ADODB.Stream")  
    Set cmd.ActiveConnection = conn  
    stm.open  
    result ="none"  
    strXPathQuery="/root"  
    DBGUID_XPATH = "{EC2A4293-E898-11D2-B1B7-00C04F680C56}"  
    cmd.Dialect = DBGUID_XPATH  
    cmd.CommandText = strXPathQuery  
    cmd.Properties("Mapping schema") = "LimitFieldReal.xml"  
    cmd.Properties("Output Stream").Value = stm  
    cmd.Properties("Output Encoding") = "utf-8"  
    WScript.Echo "executing for xml query"  
    On Error Resume Next  
    cmd.Execute , ,1024  
    if err then  
    Wscript.Echo err.description  
    Wscript.Echo err.Number  
    Wscript.Echo err.source  
    On Error GoTo 0  
    else  
    stm.Position = 0  
    result  = stm.ReadText  
    end if  
    WScript.Echo result  
    Wscript.Echo "done"  
    ```  
  
5.  Windows 탐색기에서 TestQuery.vbs 파일을 클릭하여 실행합니다.  
  
     다음은 결과입니다.  
  
    ```  
    <root>  
      <Order OrderID="10248"/>  
      <Order OrderID="10250"/>  
      <Order OrderID="10251"/>  
      <Order OrderID="10257"/>  
      <Order OrderID="10258">  
        <orderDetail OrderID="10258"   
                     ProductID="2"   
                     Discount="0.2"   
                     Quantity="50"/>  
      </Order>  
    </root>  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [float 및 real &#40;Transact-sql&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)   
 [nchar 및 nvarchar &#40;Transact-sql&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [SQL Server Native Client 설치](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)   
 [쿼리에 주석이 추가 된 XSD 스키마 사용 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml/annotated-xsd-schemas/using-annotated-xsd-schemas-in-queries-sqlxml-4-0.md)  
  
  
