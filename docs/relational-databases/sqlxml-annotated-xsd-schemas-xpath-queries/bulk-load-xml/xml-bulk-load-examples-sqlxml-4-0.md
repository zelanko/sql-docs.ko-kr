---
title: XML 대량 로드 예 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- ConnectionCommand property
- XMLFragment property
- relationship chains [SQLXML]
- multiple table bulk loading
- examples [SQLXML], XML Bulk Load
- overflow data [SQLXML]
- sql:datatype
- transaction mode [SQLXML]
- CheckConstraints property
- sql:overflow-field
- XML Bulk Load [SQLXML], examples
- TempFilePath property
- datatype annotation
- Transaction property
- KeepIdentity property
- Execute method
- streaming XML data
- xml data type [SQL Server], SQLXML
- bulk load [SQLXML], examples
ms.assetid: 970e4553-b41d-4a12-ad50-0ee65d1f305d
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f70e66a02637b65e96cccc6001c9702d5253d5cd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257373"
---
# <a name="xml-bulk-load-examples-sqlxml-40"></a>XML 대량 로드 예(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  다음 예에서는 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 XML 대량 로드 기능을 보여 줍니다. 각 예는 XSD 스키마와 이에 해당하는 XDR 스키마를 제공합니다.  
  
## <a name="bulk-loader-script-validateandbulkloadvbs"></a>대량 로더 스크립트(ValidateAndBulkload.vbs)  
 VBScript ( [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition)로 작성 된 다음 스크립트는 xml 문서를 xml DOM에 로드 합니다. 스키마에 대해 유효성을 검사 합니다. 문서가 올바르면 XML 대량 로드를 실행 하 여 XML을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블로 로드 합니다. 이 스크립트는 이 항목의 뒷부분에서 이 스크립트를 참조하는 각 개별 예와 함께 사용할 수 있습니다.  
  
> [!NOTE]  
>  데이터 파일에서 업로드되는 내용이 없을 경우 XML 대량 로드는 경고 또는 오류를 표시하지 않습니다. 따라서 대량 로드 작업을 실행하기 전에 XML 데이터 파일의 유효성을 검사하는 것이 좋습니다.  
  
```vbs  
Dim FileValid  
  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
'Validate the data file prior to bulkload  
Dim sOutput   
sOutput = ValidateFile("SampleXMLData.xml", "", "SampleSchema.xml")  
WScript.Echo sOutput  
  
If FileValid Then  
   ' Check constraints and initiate transaction (if needed)  
   ' objBL.CheckConstraints = True  
   ' objBL.Transaction=True  
  'Execute XML bulkload using file.  
  objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
  set objBL=Nothing  
End If  
  
Function ValidateFile(strXmlFile,strUrn,strXsdFile)  
  
   ' Create a schema cache and add SampleSchema.xml to it.  
   Dim xs, fso, sAppPath  
   Set fso = CreateObject("Scripting.FileSystemObject")   
   Set xs = CreateObject("MSXML2.XMLSchemaCache.6.0")  
   sAppPath = fso.GetFolder(".")   
   xs.Add strUrn, sAppPath & "\" & strXsdFile  
  
   ' Create an XML DOMDocument object.  
   Dim xd   
   Set xd = CreateObject("MSXML2.DOMDocument.6.0")  
  
   ' Assign the schema cache to the DOM document.  
   ' schemas collection.  
   Set xd.schemas = xs  
  
   ' Load XML document as DOM document.  
   xd.async = False  
   xd.Load sAppPath & "\" & strXmlFile  
  
   ' Return validation results in message to the user.  
   If xd.parseError.errorCode <> 0 Then  
        ValidateFile = "Validation failed on " & _  
             strXmlFile & vbCrLf & _  
             "=======" & vbCrLf & _  
             "Reason: " & xd.parseError.reason & _  
             vbCrLf & "Source: " & _  
             xd.parseError.srcText & _  
             vbCrLf & "Line: " & _  
             xd.parseError.Line & vbCrLf  
             FileValid = False  
    Else  
        ValidateFile = "Validation succeeded for " & _  
             strXmlFile & vbCrLf & _  
             "========" & _  
             vbCrLf & "Contents to be bulkloaded" & vbCrLf  
             FileValid = True  
    End If  
End Function  
```  
  
## <a name="a-bulk-loading-xml-in-a-table"></a>A. 테이블에 XML 대량 로드  
 이 예에서는 ConnectionString 속성 (MyServer)에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 지정 된 인스턴스에 대 한 연결을 설정 합니다. 또한이 예제에서는 ErrorLogFile 속성을 지정 합니다. 따라서 오류 출력은 지정된 파일("C:\error.log")에 저장되며 위치는 다른 곳으로 변경할 수 있습니다. 또한 Execute 메서드는 매핑 스키마 파일 (Sampleschema.xml)과 XML 데이터 파일 (Samplexmldata.xml로)의 매개 변수를 포함 합니다. 대량 로드를 실행 하면 **tempdb** 데이터베이스에서 만든 Cust 테이블에 XML 데이터 파일의 내용에 따라 새 레코드가 포함 됩니다.  
  
#### <a name="to-test-a-sample-bulk-load"></a>예제 대량 로드를 테스트하려면  
  
1.  다음 테이블을 만듭니다.  
  
    ```sql  
    CREATE TABLE Cust(CustomerID  int PRIMARY KEY,  
                      CompanyName varchar(20),  
                      City        varchar(20));  
    GO  
    ```  
  
2.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleSchema.xml로 저장합니다. 이 파일에 다음 XSD 스키마를 추가합니다.  
  
    ```xml  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
       <xsd:element name="ROOT" sql:is-constant="1" >  
         <xsd:complexType>  
           <xsd:sequence>  
             <xsd:element name="Customers" sql:relation="Cust" maxOccurs="unbounded">  
               <xsd:complexType>  
                 <xsd:sequence>  
                   <xsd:element name="CustomerID"  type="xsd:integer" />  
                   <xsd:element name="CompanyName" type="xsd:string" />  
                   <xsd:element name="City"        type="xsd:string" />  
                 </xsd:sequence>  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
          </xsd:complexType>  
         </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleXMLData.xml로 저장합니다. 이 파일에 다음 XML 문서를 추가합니다.  
  
    ```xml  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Sean Chai</CompanyName>  
        <City>New York</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Tom Johnston</CompanyName>  
         <City>Los Angeles</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Institute of Art</CompanyName>  
        <City>Chicago</City>  
      </Customers>  
    </ROOT>  
    ```  
  
4.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 ValidateAndBulkload.vbs로 저장합니다. 이 파일에 이 항목의 시작 부분에 제공된 VBScript 코드를 추가합니다. 연결 문자열을 수정하여 해당 서버 이름을 지정합니다. Execute 메서드에 대 한 매개 변수로 지정 된 파일에 대 한 적절 한 경로를 지정 합니다.  
  
5.  VBScript 코드를 실행합니다. XML 대량 로드가 Cust 테이블에 XML을 로드합니다.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers"  sql:relation="Cust" >  
      <element type="CustomerID"  sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City"        sql:field="City" />  
  
   </ElementType>  
</Schema>  
```  
  
## <a name="b-bulk-loading-xml-data-in-multiple-tables"></a>B. 여러 테이블에 XML 데이터 대량 로드  
 이 예제에서 XML 문서는 ** \<Customer>** 및 ** \<Order>** 요소로 구성 됩니다.  
  
```xml  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Sean Chai</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Tom Johnston</CompanyName>  
     <City>LA</City>    
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Institute of Art</CompanyName>  
    <Order OrderID="4" />  
  </Customers>  
</ROOT>  
```  
  
 이 예에서는 XML 데이터를 **Cust** 및 **CustOrder**라는 두 테이블에 대량 로드 합니다.  
  
-   Cust (CustomerID, CompanyName, City)  
  
-   CustOrder (OrderID, CustomerID)  
  
 다음 XSD 스키마는 이러한 테이블의 XML 뷰를 정의합니다. 이 스키마는 ** \<Customer>** 와 ** \<Order>** 요소 간의 부모-자식 관계를 지정 합니다.  
  
```xml  
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
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
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
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 XML 대량 로드는 ** \<CustOrder>** 요소 ** \<>** 사이에 지정 된 기본 키/외래 키 관계를 사용 하 여 두 테이블에 데이터를 대량으로 로드 합니다.  
  
#### <a name="to-test-a-sample-bulk-load"></a>예제 대량 로드를 테스트하려면  
  
1.  **Tempdb** 데이터베이스에 두 개의 테이블을 만듭니다.  
  
    ```sql  
    USE tempdb;  
    CREATE TABLE Cust(  
           CustomerID  int PRIMARY KEY,  
           CompanyName varchar(20),  
           City        varchar(20));  
    CREATE TABLE CustOrder(        OrderID     int PRIMARY KEY,   
            CustomerID int FOREIGN KEY REFERENCES Cust(CustomerID));  
    ```  
  
2.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleSchema.xml로 저장합니다. 이 예에 제공되는 XSD 스키마를 이 파일에 추가합니다.  
  
3.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleData.xml로 저장합니다. 이 예의 앞부분에 제공된 XML 문서를 이 파일에 추가합니다.  
  
4.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 ValidateAndBulkload.vbs로 저장합니다. 이 파일에 이 항목의 시작 부분에 제공된 VBScript 코드를 추가합니다. 연결 문자열을 수정하여 해당 서버 및 데이터베이스 이름을 지정합니다. Execute 메서드에 대 한 매개 변수로 지정 된 파일에 대 한 적절 한 경로를 지정 합니다.  
  
5.  위의 VBScript 코드를 실행합니다. XML 대량 로드가 Cust 및 CustOrder 테이블에 XML 문서를 로드합니다.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
<sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="c-using-chain-relationships-in-the-schema-to-bulk-load-xml"></a>C. 스키마의 체인 관계를 사용하여 XML 대량 로드  
 이 예에서는 XML 대량 로드에서 매핑 스키마에 지정된 M:N 관계를 사용하여 M:N 관계를 나타내는 테이블에 데이터를 로드하는 방법을 보여 줍니다.  
  
 예를 들어 다음 XSD 스키마를 참조하십시오.  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Ord"  
          parent-key="OrderID"  
          child="OrderDetail"  
          child-key="OrderID" />  
  
    <sql:relationship name="ODProduct"  
          parent="OrderDetail"  
          parent-key="ProductID"  
          child="Product"  
          child-key="ProductID"   
          inverse="true"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Ord"   
                     sql:key-fields="OrderID" >  
          <xsd:complexType>  
            <xsd:sequence>  
             <xsd:element name="Product"  
                          sql:relation="Product"   
                          sql:key-fields="ProductID"  
                          sql:relationship="OrderOD ODProduct">  
               <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
           <xsd:attribute name="OrderID"   type="xsd:integer" />   
           <xsd:attribute name="CustomerID"   type="xsd:string" />  
         </xsd:complexType>  
       </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 이 스키마는 ** \<Product>** 자식 요소와 함께 ** \<Order>** 요소를 지정 합니다. ** \<Order>** 요소는 Ord 테이블에 매핑되고 ** \<product>** 요소는 데이터베이스의 product 테이블에 매핑됩니다. Product>요소에 지정 된 체인 관계는 orderdetail 테이블로 표시 되는 m:n 관계를 식별 합니다. ** \<** 하나의 주문이 여러 제품을 포함할 수 있으며, 하나의 제품은 여러 주문에 포함될 수 있습니다.  
  
 이 스키마를 사용하여 XML 문서를 대량 로드하는 경우 Ord, Product 및 OrderDetail 테이블에 레코드가 추가됩니다.  
  
#### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  다음 3개의 테이블을 만듭니다.  
  
    ```sql  
    CREATE TABLE Ord (  
             OrderID     int  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  이 예의 윗부분에서 제공하는 스키마를 SampleSchema.xml로 저장합니다.  
  
3.  다음 예제 XML 데이터를 SampleXMLData.xml로 저장합니다.  
  
    ```xml  
    <ROOT>    
      <Order OrderID="1" CustomerID="ALFKI">  
        <Product ProductID="1" ProductName="Chai" />  
        <Product ProductID="2" ProductName="Chang" />  
      </Order>  
      <Order OrderID="2" CustomerID="ANATR">  
        <Product ProductID="3" ProductName="Aniseed Syrup" />  
        <Product ProductID="4" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 ValidateAndBulkload.vbs로 저장합니다. 이 파일에 이 항목의 시작 부분에 제공된 VBScript 코드를 추가합니다. 연결 문자열을 수정하여 해당 서버 및 데이터베이스 이름을 지정합니다. 이 예의 원본 코드에서 다음 줄의 주석 처리를 제거합니다.  
  
    ```vbs  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    ```  
  
5.  VBScript 코드를 실행합니다. XML 대량 로드가 Ord 및 Product 테이블에 XML 문서를 로드합니다.  
  
## <a name="d-bulk-loading-in-identity-type-columns"></a>D. ID 유형 열에 대량 로드  
 이 예에서는 대량 로드에서 ID 유형 열이 처리되는 방법을 보여 줍니다. 이 예에서 데이터는 3개의 테이블(Ord, Product 및 OrderDetail)에 대량 로드됩니다.  
  
 이러한 테이블에는 다음이 적용됩니다.  
  
-   Ord 테이블의 OrderID는 ID 유형 열입니다.  
  
-   Product 테이블의 ProductID는 ID 유형 열입니다.  
  
-   OrderDetail의 OrderID 및 ProductID는 Ord 및 Product 테이블의 해당 기본 키 열을 참조하는 외래 키 열입니다.  
  
 다음은 이 예에 대한 테이블 스키마입니다.  
  
```  
Ord (OrderID, CustomerID)  
Product (ProductID, ProductName)  
OrderDetail (OrderID, ProductID)  
```  
  
 이 XML 대량 로드 예제에서 BulkLoad 개체 모델의 KeepIdentity 속성은 false로 설정 됩니다. 따라서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 각각 Product 및 Ord 테이블의 ProductID 및 OrderID 열에 대한 ID 값을 생성합니다(이 문서에서 대량 로드되도록 제공된 모든 값은 무시됨).  
  
 여기에서 XML 대량 로드는 테이블 간의 기본 키/외래 키 관계를 식별합니다. 대량 로드는 먼저 기본 키가 있는 테이블에 레코드를 삽입한 후 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 생성한 ID 값을 외래 키 열이 있는 테이블로 전파합니다. 다음 예의 XML 대량 로드는 다음 순서에 따라 데이터를 테이블에 삽입합니다.  
  
1.  Product  
  
2.  Ord  
  
3.  OrderDetail  
  
    > [!NOTE]  
    >  Products 및 Orders 테이블에 생성된 ID 값을 전파하기 위해 처리 논리는 XML 대량 로드에서 나중에 OrderDetails 테이블에 삽입할 수 있도록 이러한 값을 추적할 것을 요구합니다. 이를 수행하기 위해 XML 대량 로드는 중간 테이블을 만들고 이 테이블에 데이터를 채운 후 나중에 테이블을 제거합니다.  
  
#### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  다음 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleSchema.xml로 저장합니다. 이 파일에 이 XSD 스키마를 추가합니다.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
       <xsd:appinfo>  
        <sql:relationship name="OrderOD"  
              parent="Ord"  
              parent-key="OrderID"  
              child="OrderDetail"  
              child-key="OrderID" />  
        <sql:relationship name="ODProduct"  
              parent="OrderDetail"  
              parent-key="ProductID"  
              child="Product"  
              child-key="ProductID"   
              inverse="true"/>  
       </xsd:appinfo>  
     </xsd:annotation>  
  
      <xsd:element name="Order" sql:relation="Ord"   
                                sql:key-fields="OrderID" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="Product" sql:relation="Product"   
                         sql:key-fields="ProductID"  
                         sql:relationship="OrderOD ODProduct">  
              <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
              </xsd:complexType>  
            </xsd:element>  
         </xsd:sequence>  
            <xsd:attribute name="OrderID"   type="xsd:integer" />   
            <xsd:attribute name="CustomerID"   type="xsd:string" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleXMLData.xml로 저장합니다. 다음 XML 문서를 추가합니다.  
  
    ```  
    <ROOT>    
      <Order OrderID="11" CustomerID="ALFKI">  
        <Product ProductID="11" ProductName="Chai" />  
        <Product ProductID="22" ProductName="Chang" />  
      </Order>  
      <Order OrderID="22" CustomerID="ANATR">  
         <Product ProductID="33" ProductName="Aniseed Syrup" />  
        <Product ProductID="44" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 ValidateAndBulkload.vbs로 저장합니다. 이 파일에 다음 VBScript 코드를 추가합니다. 연결 문자열을 수정하여 해당 서버 및 데이터베이스 이름을 지정합니다. **Execute** 메서드에 대 한 매개 변수로 사용할 파일의 적절 한 경로를 지정 합니다.  
  
    ```  
    Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "C:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction = False  
    objBL.KeepIdentity = False  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    Set objBL = Nothing  
    MsgBox "Done."  
    ```  
  
5.  VBScript 코드를 실행합니다. XML 대량 로드에서 해당 테이블에 데이터를 로드합니다.  
  
## <a name="e-generating-table-schemas-before-bulk-loading"></a>E. 대량 로드 전에 테이블 스키마 생성  
 XML 대량 로드는 대량 로드 전에 테이블이 존재하지 않는 경우 필요에 따라 이러한 테이블을 만들 수 있습니다. SQLXMLBulkLoad 개체의 SchemaGen 속성을 TRUE로 설정 하면이를 수행 합니다. 또한 선택적으로 XML 대량 로드를 요청 하 여 기존 테이블을 삭제 하 고 SGDropTables 속성을 TRUE로 설정 하 여 다시 만들 수 있습니다. 다음 VBScript 예에서는 이러한 속성의 사용 방법을 보여 줍니다.  
  
 또한 이 예에서는 두 개의 추가 속성을 TRUE로 설정합니다.  
  
-   CheckConstraints. 이 속성을 TRUE로 설정하면 테이블에 삽입되는 데이터가 테이블에 지정된 제약 조건을 위반하지 않도록 보장할 수 있습니다(이 예에서는 Cust와 CustOrder 테이블 간에 지정된 PRIMARY KEY/FOREIGN KEY 제약 조건). 제약 조건 위반이 발생하면 대량 로드는 실패합니다.  
  
-   XMLFragment. 예제 XML 문서(데이터 원본)에는 단일 최상위 요소가 없고 따라서 조각이므로 이 속성은 TRUE로 설정해야 합니다.  
  
 다음은 VBScript 코드입니다.  
  
```  
Dim objBL   
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
objBL.CheckConstraints=true  
objBL.XMLFragment = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
```  
  
#### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleSchema.xml로 저장합니다. 앞의 예 "스키마의 체인 관계를 사용하여 XML 대량 로드"에 제공된 XSD 스키마를 파일에 추가합니다.  
  
2.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleXMLData.xml로 저장합니다. 앞의 예 "스키마의 체인 관계를 사용하여 XML 대량 로드"에 제공된 XML 문서를 파일에 추가합니다. 문서에서 \<루트> 요소를 제거 하 여 조각으로 만듭니다.  
  
3.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 ValidateAndBulkload.vbs로 저장합니다. 이 파일에 이 예의 VBScript 코드를 추가합니다. 연결 문자열을 수정하여 해당 서버 및 데이터베이스 이름을 지정합니다. Execute 메서드에 대 한 매개 변수로 지정 된 파일에 대 한 적절 한 경로를 지정 합니다.  
  
4.  VBScript 코드를 실행합니다. XML 대량 로드에서 제공된 매핑 스키마를 기반으로 필요한 테이블을 만들고 이 테이블에 데이터를 대량 로드합니다.  
  
## <a name="f-bulk-loading-from-a-stream"></a>F. 스트림에서 대량 로드  
 XML 대량 로드 개체 모델의 Execute 메서드는 두 개의 매개 변수를 사용 합니다. 첫 번째 매개 변수는 매핑 스키마 파일입니다. 두 번째 매개 변수는 데이터베이스에 로드될 XML 데이터를 제공합니다. Xml 데이터를 XML 대량 로드의 Execute 메서드에 전달 하는 방법에는 두 가지가 있습니다.  
  
-   파일 이름을 매개 변수로 지정합니다.  
  
-   XML 데이터를 포함하는 스트림을 전달합니다.  
  
 이 예에서는 스트림에서 대량 로드하는 방법을 보여 줍니다.  
  
 VBScript는 먼저 SELECT 문을 실행하여 Northwind 데이터베이스의 Customers 테이블에서 고객 정보를 검색합니다. SELECT 문에 FOR XML 절이 지정되므로(ELEMENTS 옵션 사용) 쿼리는 다음 형식의 요소 중심 XML 문서를 반환합니다.  
  
```  
<Customer>  
  <CustomerID>..</CustomerID>  
  <CompanyName>..</CompanyName>  
  <City>..</City>  
</Customer>  
...  
```  
  
 그런 다음 스크립트는 XML을 Execute 메서드에 대 한 스트림으로 두 번째 매개 변수로 전달 합니다. Execute 메서드는 데이터를 Cust 테이블에 대량 로드 합니다.  
  
 이 스크립트는 SchemaGen 속성을 TRUE로 설정 하 고 SGDropTables 속성을 TRUE로 설정 하므로 XML 대량 로드는 지정 된 데이터베이스에 Cust 테이블을 만듭니다. 테이블이 이미 있는 경우 이 테이블을 먼저 삭제한 다음 다시 만듭니다.  
  
 다음은 VBScript 예입니다.  
  
```  
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
Set objCmd = CreateObject("ADODB.Command")  
Set objConn = CreateObject("ADODB.Connection")  
Set objStrmOut = CreateObject ("ADODB.Stream")  
  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile     = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen        = True  
objBL.SGDropTables     = True  
objBL.XMLFragment      = True  
' Open a connection to the instance of SQL Server to get the source data.  
  
objConn.Open "provider=SQLOLEDB;server=(local);database=tempdb;integrated security=SSPI"  
Set objCmd.ActiveConnection = objConn  
objCmd.CommandText = "SELECT CustomerID, CompanyName, City FROM Customers FOR XML AUTO, ELEMENTS"  
  
' Open the return stream and execute the command.  
Const adCRLF = -1  
Const adExecuteStream = 1024  
objStrmOut.Open  
objStrmOut.LineSeparator = adCRLF  
objCmd.Properties("Output Stream").Value = objStrmOut  
objCmd.Execute , , adExecuteStream  
objStrmOut.Position = 0  
  
' Execute bulk load. Read source XML data from the stream.  
objBL.Execute "SampleSchema.xml", objStrmOut  
  
Set objBL = Nothing  
```  
  
 다음 XSD 매핑 스키마는 테이블을 만드는 데 필요한 정보를 제공합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="ROOT" sql:is-constant="true" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customers"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="Customers" sql:relation="Cust" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element name="CustomerID"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(5)"/>  
      <xsd:element name="CompanyName"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
      <xsd:element name="City"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
 다음은 이에 해당하는 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
    </ElementType>  
</Schema>  
```  
  
### <a name="opening-a-stream-on-an-existing-file"></a>기존 파일에서 스트림 열기  
 기존 XML 데이터 파일에서 스트림을 열고 파일 이름을 매개 변수로 전달 하는 대신 Execute 메서드에 스트림으로 전달할 수도 있습니다.  
  
 다음은 스트림을 매개 변수로 전달하는 Visual Basic 예입니다.  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad  
Dim objStrm As New ADODB.Stream  
Dim objFileSystem As New Scripting.FileSystemObject  
Dim objFile As Scripting.TextStream  
  
MsgBox "Begin BulkLoad..."  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
' Here again a stream is specified that contains the source data   
' (instead of the file name). But this is just an illustration.  
' Usually this is useful if you have an XML data   
' stream that is created by some other means that you want to bulk   
' load. This example starts with an XML text file, so it may not be the   
' best to use a stream (you can specify the file name directly).  
' Here you could have specified the file name itself.   
Set objFile = objFileSystem.OpenTextFile("c:\SampleData.xml")  
objStrm.Open  
objStrm.WriteText objFile.ReadAll  
objStrm.Position = 0  
objBL.Execute "c:\SampleSchema.xml", objStrm  
  
Set objBL = Nothing  
MsgBox "Done."  
End Sub  
```  
  
 애플리케이션을 테스트하려면 파일(SampleData.xml)의 다음 XML 문서와 이 예에 제공된 XSD 스키마를 사용하십시오.  
  
 다음은 XML 원본 데이터(SampleData.xml)입니다.  
  
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
    <Order CustomerID= "4444" OrderID="4" />  
</Customers>  
</ROOT>  
```  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="g-bulk-loading-in-overflow-columns"></a>G. 오버플로 열에 대량 로드  
 매핑 스키마가 **sql: 오버플로-필드** 주석을 사용 하 여 오버플로 열을 지정 하는 경우 XML 대량 로드는 원본 문서에서 사용 되지 않은 모든 데이터를이 열에 복사 합니다.  
  
 다음 XSD 스키마를 고려해 보십시오.  
  
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
  <xsd:element name="Customers" sql:relation="Cust"  
                                sql:overflow-field="OverflowColumn" >  
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
          <xsd:attribute name="CustomerID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 스키마는 Cust 테이블에 대한 오버플로 열(OverflowColumn)을 식별합니다. 따라서 각 ** \<Customer>** 요소에 대해 소비 되지 않은 모든 XML 데이터가이 열에 추가 됩니다.  
  
> [!NOTE]  
>  모든 추상 요소 ( **abstract = "true"** 가 지정 된 요소) 및 모든 금지 된 특성 ( **금지 = "true"** 가 지정 된 특성)은 XML 대량 로드에 의해 오버플로로 간주 되 고 지정 된 경우 오버플로 열에 추가 됩니다. 지정되지 않은 경우에는 무시됩니다.  
  
#### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  **Tempdb** 데이터베이스에 두 개의 테이블을 만듭니다.  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle',  
                  OverflowColumn nvarchar(200));  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID    int PRIMARY KEY,  
                  CustomerID int FOREIGN KEY   
                                 REFERENCES Cust(CustomerID));  
    GO  
    ```  
  
2.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleSchema.xml로 저장합니다. 이 예에 제공되는 XSD 스키마를 이 파일에 추가합니다.  
  
3.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleXMLData.xml로 저장합니다. 이 파일에 다음 XML 문서를 추가합니다.  
  
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
         <![CDATA[LA]]>   
        <!-- <xyz><address>111 Maple, Seattle</address></xyz>   -->  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 ValidateAndBulkload.vbs로 저장합니다. 이 파일에 다음 Microsoft Visual Basic Scripting Edition(VBScript) 코드를 추가합니다. 연결 문자열을 수정하여 해당 서버 및 데이터베이스 이름을 지정합니다. Execute 메서드에 대 한 매개 변수로 지정 된 파일에 대 한 적절 한 경로를 지정 합니다.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  VBScript 코드를 실행합니다.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"   
                       sql:overflow-field="OverflowColumn"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="h-specifying-the-file-path-for-temp-files-in-transaction-mode"></a>H 트랜잭션 모드에서 임시 파일에 대한 파일 경로 지정  
 트랜잭션 모드에서 대량 로드 하는 경우, 즉 Transaction 속성이 TRUE로 설정 된 경우 다음 조건 중 하나에 해당 하는 경우에도 TempFilePath 속성을 설정 해야 합니다.  
  
-   원격 서버에 대량 로드하는 경우  
  
-   TEMP 환경 변수에 지정된 경로와 다른 대체 로컬 드라이브 또는 폴더를 사용하여 트랜잭션 모드에서 만들어진 임시 파일을 저장하려는 경우  
  
 예를 들어 다음 VBScript 코드는 트랜잭션 모드에서 SampleXMLData.xml 파일의 데이터를 데이터베이스 테이블에 대량 로드합니다. TempFilePath 속성은 트랜잭션 모드에서 생성 된 임시 파일의 경로를 설정 하는 데 지정 됩니다.  
  
```  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.Transaction=True  
objBL.TempFilePath="\\Server\MyDir"  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
set objBL=Nothing  
```  
  
> [!NOTE]  
>  임시 파일 경로는 대상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 서비스 계정과 대량 로드 애플리케이션을 실행 중인 계정에서 액세스 가능한 공유 위치여야 합니다. 로컬 서버에서 대량 로드 하는 경우가 아니면 임시 파일 경로는 UNC 경로 (예: \\\servername\sharename) 여야 합니다.  
  
#### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  **Tempdb** 데이터베이스에이 테이블을 만듭니다.  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (     CustomerID uniqueidentifier,   
          LastName  varchar(20));  
    GO  
    ```  
  
2.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleSchema.xml로 저장합니다. 다음 XSD 스키마를 파일에 추가합니다.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleXMLData.xml로 저장합니다. 이 파일에 다음 XML 문서를 추가합니다.  
  
    ```  
    <ROOT>  
    <Customers CustomerID="6F9619FF-8B86-D011-B42D-00C04FC964FF"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
4.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 ValidateAndBulkload.vbs로 저장합니다. 이 파일에 다음 VBScript 코드를 추가합니다. 연결 문자열을 수정하여 해당 서버 및 데이터베이스 이름을 지정합니다. Execute 메서드에 대 한 매개 변수로 지정 된 파일에 대 한 적절 한 경로를 지정 합니다. 또한 TempFilePath 속성에 대해 적절 한 경로를 지정 합니다.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.TempFilePath="\\server\folder"  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  VBScript 코드를 실행합니다.  
  
     **Customerid** 의 값이 중괄호 ({및})를 포함 하는 GUID로 지정 된 경우 스키마는 **customerid** 특성에 해당 하는 **sql: datatype** 을 지정 해야 합니다. 예를 들면 다음과 같습니다.  
  
    ```  
    <ROOT>  
    <Customers CustomerID="{6F9619FF-8B86-D011-B42D-00C04FC964FF}"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
     다음은 업데이트된 스키마입니다.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string"   
                        sql:datatype="uniqueidentifier" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
     **Sql: datatype** 이 열 유형을 **uniqueidentifier**로 식별 하도록 지정 된 경우 대량 로드 작업은 열에 삽입 하기 전에 **CustomerID** 값에서 중괄호 ({및})를 제거 합니다.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
<ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
</ElementType>  
<ElementType name="Customers" sql:relation="Cust" >  
  <AttributeType name="CustomerID"  sql:datatype="uniqueidentifier" />  
  <AttributeType name="LastName"   />  
  
  <attribute type="CustomerID" />  
  <attribute type="LastName"   />  
</ElementType>  
</Schema>  
```  
  
## <a name="i-using-an-existing-database-connection-with-the-connectioncommand-property"></a>I. ConnectionCommand 속성으로 기존 데이터베이스 연결 사용  
 기존 ADO 연결을 사용하여 XML을 대량 로드할 수 있습니다. 이 방법은 XML 대량 로드 외에도 많은 작업이 데이터 원본에 대해 수행되는 경우 유용합니다.  
  
 ConnectionCommand 속성을 사용 하면 ADO 명령 개체를 사용 하 여 기존 ADO 연결을 사용할 수 있습니다. 다음 Visual Basic 예에서 확인할 수 있습니다.  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad4  
Dim objCmd As New ADODB.Command  
Dim objConn As New ADODB.Connection  
  
'Open a connection to an instance of SQL Server.  
objConn.Open "provider=SQLOLEDB;data source=(local);database=tempdb;integrated security=SSPI"  
'Ask the Command object to use the connection just established.  
Set objCmd.ActiveConnection = objConn  
  
'Tell Bulk Load to use the active command object that is using the Connection obj.  
objBL.ConnectionCommand = objCmd  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
'The Transaction property must be set to True if you use ConnectionCommand.  
objBL.Transaction = True  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
End Sub  
```  
  
#### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  **Tempdb** 데이터베이스에 두 개의 테이블을 만듭니다.  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust(  
                   CustomerID   varchar(5) PRIMARY KEY,  
                   CompanyName  varchar(30),  
                   City         varchar(20));  
    GO  
    CREATE TABLE CustOrder(  
                   CustomerID  varchar(5) references Cust (CustomerID),  
                   OrderID     varchar(5) PRIMARY KEY);  
    GO  
    ```  
  
2.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleSchema.xml로 저장합니다. 다음 XSD 스키마를 파일에 추가합니다.  
  
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
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
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
              <xsd:attribute name="CustomerID" type="xsd:integer" />  
             </xsd:complexType>  
           </xsd:element>  
         </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleXMLData.xml로 저장합니다. 이 파일에 다음 XML 문서를 추가합니다.  
  
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
  
4.  Visual Basic(표준 EXE) 애플리케이션과 위의 코드를 만듭니다. 프로젝트에 다음 참조를 추가합니다.  
  
    ```  
    Microsoft XML BulkLoad for SQL Server 4.0 Type Library  
    Microsoft ActiveX Data objects 2.6 Library  
    ```  
  
5.  애플리케이션을 실행합니다.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
         <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="j-bulk-loading-in-xml-data-type-columns"></a>J. xml 데이터 형식 열에 대량 로드  
 매핑 스키마가 **sql: datatype = "xml"** 주석을 사용 하 여 [xml 데이터 형식](../../../t-sql/xml/xml-transact-sql.md) 열을 지정 하는 경우 xml 대량 로드는 원본 문서에서 매핑된 필드의 xml 자식 요소를이 열로 복사할 수 있습니다.  
  
 AdventureWorks 예제 데이터베이스에 있는 Production.ProductModel 테이블의 뷰를 매핑하는 다음 XSD 스키마를 고려해 보십시오. 이 테이블에서 **xml** 데이터 형식의 CatalogDescription 필드는 **sql: field** 및 **sql: datatype = "xml"** 주석을 사용 하 여 ** \<Desc>** 요소에 매핑됩니다.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Name" type="xs:string"></xsd:element>  
        <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element name="ProductDescription">  
              <xsd:complexType>  
                <xsd:sequence>  
                  <xsd:element name="Summary" type="xs:anyType"/>  
                </xsd:sequence>  
              </xsd:complexType>  
            </xsd:element>  
          </xsd:sequence>  
        </xsd:complexType>  
        </xsd:element>   
     </xsd:sequence>  
     <xsd:attribute name="ProductModelID" sql:field="ProductModelID" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
#### <a name="to-test-a-working-sample"></a>작업 예제를 테스트하려면  
  
1.  AdventureWorks 예제 데이터베이스가 설치되어 있는지 확인합니다.  
  
2.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleSchema.xml로 저장합니다. 위의 XSD 스키마를 복사하여 파일에 붙여넣고 저장합니다.  
  
3.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 SampleXMLData.xml로 저장합니다. 다음 XML 문서를 복사하여 파일에 붙여넣고 이전 단계에서 사용한 폴더와 동일한 폴더에 저장합니다.  
  
    ```  
    <ProductModel ProductModelID="2005">  
        <Name>Mountain-100 (2005 model)</Name>  
        <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
            <p1:ProductDescription xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
                  xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
                  xmlns:wf="https://www.adventure-works.com/schemas/OtherFeatures"   
                  xmlns:html="http://www.w3.org/1999/xhtml"   
                  xmlns="">  
                <p1:Summary>  
                    <html:p>Our top-of-the-line competition mountain bike.   
          Performance-enhancing options include the innovative HL Frame,   
          super-smooth front suspension, and traction for all terrain.  
                            </html:p>  
                </p1:Summary>  
                <p1:Manufacturer>  
                    <p1:Name>AdventureWorks</p1:Name>  
                    <p1:Copyright>2002-2005</p1:Copyright>  
                    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
                </p1:Manufacturer>  
                <p1:Features>These are the product highlights.   
                     <wm:Warranty>  
                        <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
                        <wm:Description>parts and labor</wm:Description>  
                    </wm:Warranty><wm:Maintenance>  
                        <wm:NoOfYears>10 years</wm:NoOfYears>  
                        <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
                    </wm:Maintenance><wf:wheel>High performance wheels.</wf:wheel><wf:saddle>  
                        <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle><wf:pedal>  
                        <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal><wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter   
          and wall-thickness required of a premium mountain frame.   
          The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame><wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset></p1:Features>  
                <!-- add one or more of these elements... one for each specific product in this product model -->  
                <p1:Picture>  
                    <p1:Angle>front</p1:Angle>  
                    <p1:Size>small</p1:Size>  
                    <p1:ProductPhotoID>118</p1:ProductPhotoID>  
                </p1:Picture>  
                <!-- add any tags in <specifications> -->  
                <p1:Specifications> These are the product specifications.  
                       <Material>Almuminum Alloy</Material><Color>Available in most colors</Color><ProductLine>Mountain bike</ProductLine><Style>Unisex</Style><RiderExperience>Advanced to Professional riders</RiderExperience></p1:Specifications>  
            </p1:ProductDescription>  
        </Desc>  
    </ProductModel>  
    ```  
  
4.  기본 텍스트 편집기 또는 XML 편집기에서 파일을 만든 후 BulkloadXml.vbs로 저장합니다. 다음 VBScript 코드를 복사한 후 파일에 붙여 넣습니다. 이전 XML 데이터 및 스키마 파일에 사용한 폴더와 동일한 폴더에 이 파일을 저장합니다.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=AdventureWorks;integrated security=SSPI"  
  
    Dim fso, sAppPath  
    Set fso = CreateObject("Scripting.FileSystemObject")   
    sAppPath = fso.GetFolder(".")   
  
    objBL.ErrorLogFile = sAppPath & "\error.log"  
  
    'Execute XML bulkload using file.  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  BulkloadXml.vbs 스크립트를 실행합니다.  
  
  
