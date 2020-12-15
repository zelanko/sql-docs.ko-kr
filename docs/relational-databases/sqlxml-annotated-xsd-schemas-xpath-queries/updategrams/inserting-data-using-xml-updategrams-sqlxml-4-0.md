---
title: XML Updategrams을 사용 하 여 데이터 삽입 (SQLXML)
description: SQLXML 4.0에서 XML updategram을 사용 하 여 데이터를 삽입 하는 방법을 알아봅니다.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- xsi:nil attribute
- unique values
- <after> block
- id attribute
- data insertions [SQLXML]
- nil attribute
- <before> block
- updg:guid attribute
- multiple record insertions
- returnid attribute
- updategrams [SQLXML], inserting data
- updg:at-identity attribute
- invalid characters [SQLXML]
- updg:returnid attribute
- updg:id attribute
- namespaces [SQLXML], updategrams
- IDENTITY-type column
- guid attribute
- record insertion [SQLXML]
- null values [SQLXML]
- at-identity attribute
- xml data type [SQL Server], SQLXML
ms.assetid: 4dc48762-bc12-43fb-b356-ea1b9c1e287e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac801a52e89e60bb05d1431de77078fa750f6d34
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473114"
---
# <a name="inserting-data-using-xml-updategrams-sqlxml-40"></a>XML Updategram을 사용하여 데이터 삽입(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Updategram는 레코드 인스턴스가 블록에 나타나지만 **\<after>** 해당 블록에는 없는 경우 삽입 작업을 나타냅니다 **\<before>** . 이 경우 updategram은 블록의 레코드를 **\<after>** 데이터베이스에 삽입 합니다.  
  
 삽입 작업에 대한 Updategram 형식은 다음과 같습니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   [<updg:before>  
   </updg:before>]  
    <updg:after [updg:returnid="x y ...] >  
       <ElementName [updg:id="value"]   
                   [updg:at-identity="x"]   
                   [updg:guid="y"]  
                   attribute="value"   
                   attribute="value"  
                   ...  
       />  
      [<ElementName .../>... ]  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
## <a name="before-block"></a>\<before> 거부  
 **\<before>** 삽입 작업에 대해 블록을 생략할 수 있습니다. 선택적 **매핑 스키마** 특성을 지정 하지 않으면 **\<ElementName>** updategram에 지정 된가 데이터베이스 테이블에 매핑되고 자식 요소 또는 특성은 테이블의 열에 매핑됩니다.  
  
## <a name="after-block"></a>\<after> 거부  
 블록에서 하나 이상의 레코드를 지정할 수 있습니다 **\<after>** .  
  
 **\<after>** 블록이 특정 열에 대 한 값을 제공 하지 않으면 updategram는 주석이 지정 된 스키마 (스키마가 지정 된 경우)에 지정 된 기본값을 사용 합니다. 스키마가 열의 기본값을 지정 하지 않는 경우 updategram는이 열에 명시적 값을 지정 하지 않고 대신 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본값 (지정 된 경우)을이 열에 할당 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본값이 없고 열에서 NULL 값을 허용하는 경우 Updategram에서 열 값을 NULL로 설정합니다. 열에 기본값이 없고 NULL 값을 허용하지도 않는 경우 명령이 실패하고 Updategram에서 오류를 반환합니다. 선택적인 **updg: returnid** 특성은 id 유형 열이 있는 테이블에 레코드가 추가 될 때 시스템에서 생성 하는 id 값을 반환 하는 데 사용 됩니다.  
  
## <a name="updgid-attribute"></a>updg:id 특성  
 Updategram는 레코드만 삽입 하는 경우 updategram에 **updg: id** 특성이 필요 하지 않습니다. **Updg: id** 에 대 한 자세한 내용은 [XML UPDATEGRAMS &#40;SQLXML 4.0&#41;를 사용 하 여 데이터 업데이트](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md)를 참조 하세요.  
  
## <a name="updgat-identity-attribute"></a>updg:at-identity 특성  
 Updategram가 ID 유형 열을 포함 하는 테이블에 레코드를 삽입 하는 경우 updategram는 선택적 **updg: id** 특성을 사용 하 여 시스템 할당 값을 캡처할 수 있습니다. Updategram은 이 값을 이후 작업에 사용할 수 있습니다. Updategram 실행 시 **updg: returnid** 특성을 지정 하 여 생성 된 id 값을 반환할 수 있습니다.  
  
## <a name="updgguid-attribute"></a>updg:guid 특성  
 **Updg: guid** 특성은 guid (globally unique identifier)를 생성 하는 선택적 특성입니다. 이 값은 지정 된 전체 블록의 범위 내에 유지 됩니다 **\<sync>** . 블록의 아무 곳에서 나이 값을 사용할 수 있습니다 **\<sync>** . 특성은 **Newguid ()** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 함수를 호출 하 여 고유 식별자를 생성 합니다.  
  
## <a name="examples"></a>예  
 다음 예제를 사용 하 여 작업 예제를 만들려면 [SQLXML 예를 실행 하기 위한 요구 사항](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)에 지정 된 요구 사항을 충족 해야 합니다.  
  
 Updategram 예를 사용하기 전에 다음 사항을 확인하십시오.  
  
-   대부분의 예에서는 기본 매핑을 사용합니다. 즉, Updategram에 매핑 스키마가 지정되지 않습니다. 매핑 스키마를 사용 하는 updategram의 추가 예제는 [Updategram &#40;SQLXML 4.0&#41;에서 주석이 추가 된 매핑 스키마 지정 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)을 참조 하세요.  
  
-   대부분의 예에서는 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 사용합니다. 모든 업데이트는 이 데이터베이스의 테이블에 적용됩니다.  
  
### <a name="a-inserting-a-record-by-using-an-updategram"></a>A. Updategram을 사용하여 단일 레코드 삽입  
 이 특성 중심 Updategram은 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 데이터베이스의 HumanResources.Employee 테이블에 레코드를 삽입합니다.  
  
 이 예에서 Updategram은 매핑 스키마를 지정하지 않으므로 요소 이름은 테이블 이름에 매핑되고 특성 또는 자식 요소는 해당 테이블의 열에 매핑되는 기본 매핑을 사용합니다.  
  
 HumanResources.Department 테이블에 대한 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 스키마는 모든 열에 'not null' 제한을 적용합니다. 따라서 Updategram은 모든 열에 대해 지정된 값을 포함해야 합니다. DepartmentID는 IDENTITY 유형 열입니다. 따라서 해당 값이 지정되어 있지 않습니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name="New Product Research"   
            GroupName="Research and Development"   
            ModifiedDate="2010-08-31"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 Updategram을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 MyUpdategram.xml로 저장합니다.  
  
2.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 요소 중심 매핑에서 Updategram은 다음과 같이 나타납니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department>  
            <Name> New Product Research </Name>  
            <GroupName> Research and Development </GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 혼합 모드(요소 중심 및 특성 중심) Updategram에서 요소는 다음 Updategram과 같이 특성과 하위 요소를 모두 포함할 수 있습니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name=" New Product Research "   
            <GroupName>Research and Development</GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="b-inserting-multiple-records-by-using-an-updategram"></a>B. Updategram을 사용하여 여러 레코드 삽입  
 이 Updategram은 HumanResources.Shift 테이블에 새 근무조 레코드 두 개를 추가합니다. Updategram는 선택적 블록을 지정 하지 않습니다 **\<before>** .  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 Updategram을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 Updategram-AddShifts.xml로 저장합니다.  
  
2.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 이 예제의 또 다른 버전은 **\<after>** 두 개의 직원을 삽입 하는 한 블록 대신 별도의 두 블록을 사용 하는 updategram입니다. 이 작업은 유효하며 다음과 같이 인코딩할 수 있습니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after >  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="c-working-with-valid-sql-server-characters-that-are-not-valid-in-xml"></a>C. 유효한 XML이 아닌 유효한 SQL Server 문자 작업  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 테이블 이름은 Northwind 데이터베이스의 Order Details 테이블과 같이 공백을 포함할 수 있습니다. 그러나 잘못 된 식별자 인 XML 문자는 유효 하지 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 않지만 잘못 된 xml 식별자는 ' __xHHHH '를 인코딩 값으로 사용 하 여 인코딩할 수 있습니다 \_ \_ . 여기서 HHHH는 가장 중요 한 비트 우선 순서로 문자에 대 한 4 자리 16 진수 UCS-2 코드를 나타냅니다.  
  
> [!NOTE]  
>  이 예에서는 Northwind 데이터베이스를 사용합니다. 이 [Microsoft 웹 사이트](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)에서 다운로드할 수 있는 SQL 스크립트를 사용 하 여 Northwind 데이터베이스를 설치할 수 있습니다.  
  
 또한 요소 이름을 대괄호([ ])로 묶어야 합니다. XML에서 [및] 문자는 유효 하지 않으므로 각각 _x005B 및 _x005D로 인코딩해야 합니다 \_ \_ . 매핑 스키마를 사용하는 경우 공백과 같은 유효하지 않은 문자가 포함된 요소 이름을 제공할 수 있습니다. 매핑 스키마에서 필요한 매핑을 수행하므로 이러한 문자를 인코딩할 필요가 없습니다.  
  
 이 Updategram은 Northwind 데이터베이스의 Order Details 테이블에 레코드를 추가합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <_x005B_Order_x0020_Details_x005D_ OrderID="1"  
            ProductID="11"  
            UnitPrice="$1.0"  
            Quantity="1"  
            Discount="0.0" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Order Details 테이블의 UnitPrice 열은 **money** 형식입니다. **문자열** 형식에서 **money** 형식으로 적절 한 형식 변환을 적용 하려면 달러 기호 문자 ($)를 값의 일부로 추가 해야 합니다. Updategram가 매핑 스키마를 지정 하지 않으면 **문자열** 값의 첫 문자가 계산 됩니다. 첫 문자가 달러 기호($)이면 해당 변환이 적용됩니다.  
  
 열이 **dt: type = "updategram"** 또는 **sql: datatype = "money"** 로 적절 하 게 표시 된 매핑 스키마에 대해 지정 된 경우에는 달러 기호 ($)가 필요 하지 않으며 매핑은 매핑을 통해 처리 됩니다. 적절한 형식 변환을 수행하려는 이 방법을 사용하는 것이 좋습니다.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 Updategram을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 UpdategramSpacesInTableName.xml로 저장합니다.  
  
2.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
### <a name="d-using-the-at-identity-attribute-to-retrieve-the-value-that-has-been-inserted-in-the-identity-type-column"></a>D. at-identity 특성을 사용하여 IDENTITY 유형 열에 삽입된 값 검색  
 다음 Updategram은 두 개의 레코드를 삽입합니다. 하나는 Sales.SalesOrderHeader 테이블에 삽입하고 다른 하나는 Sales.SalesOrderDetail 테이블에 삽입합니다.  
  
 먼저 Updategram은 Sales.SalesOrderHeader 테이블에 레코드를 추가합니다. 이 테이블에서 SalesOrderID 열은 IDENTITY 유형 열입니다. 따라서이 레코드를 테이블에 추가 하면 updategram는 **id** 특성을 사용 하 여 할당 된 SalesOrderID 값을 "x" (자리 표시자 값)로 캡처합니다. 그런 다음 updategam은이 **id** 변수를 요소의 SalesOrderID 특성 값으로 지정 합니다 \<Sales.SalesOrderDetail> .  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
   <Sales.SalesOrderHeader updg:at-identity="x"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00001111-2222-3333-4444-556677889900"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
      <Sales.SalesOrderDetail SalesOrderID="x"  
                LineNumber="1"  
                OrderQty="1"  
                ProductID="776"  
                SpecialOfferID="1"  
                UnitPrice="2429.9928"  
                UnitPriceDiscount="0.00"  
                rowguid="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"  
                ModifiedDate="2001-07-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 **Updg: identity** 특성에 의해 생성 된 id 값을 반환 하려는 경우 **updg: returnid** 특성을 사용할 수 있습니다. 다음은 이 ID 값을 반환하는 수정된 Updategram입니다. 이 Updategram은 예를 좀더 복잡하게 만들기 위해 주문 레코드 두 개와 주문 정보 레코드 두 개를 추가합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync>  
  <updg:before>  
  </updg:before>  
  <updg:after updg:returnid="x y" >  
       <HumanResources.Shift updg:at-identity="x" Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift updg:at-identity="y" Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:after>  
 </updg:sync>  
</ROOT>  
```  
  
 Updategram을 실행하면 생성된 ID 값(테이블 ID에 사용되는 ShiftID 열의 생성된 값)이 포함된 다음과 유사한 결과가 반환됩니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">   
  <returnid>   
    <x>4</x>   
    <y>5</y>   
  </returnid>   
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 Updategram을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 Updategram-returnId.xml로 저장합니다.  
  
2.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
### <a name="e-using-the-updgguid-attribute-to-generate-a-unique-value"></a>E. updg:guid 특성을 사용하여 고유한 값 생성  
 이 예에서 Updategram은 Cust 및 CustOrder 테이블에 레코드를 삽입합니다. 또한 updategram는 **updg: guid** 특성을 사용 하 여 CustomerID 특성에 대 한 고유한 값을 생성 합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after updg:returnid="x" >  
      <Cust updg:guid="x" >  
         <CustID>x</CustID>  
         <LastName>Fuller</LastName>  
      </Cust>  
      <CustOrder>  
         <CustID>x</CustID>  
         <OrderID>1</OrderID>  
      </CustOrder>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Updategram는 **returnid** 특성을 지정 합니다. 따라서 생성된 GUID가 반환됩니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <returnid>  
    <x>7111BD1A-7F0B-4CEE-B411-260DADFEFA2A</x>   
  </returnid>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 Updategram을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 Updategram-GenerateGuid.xml로 저장합니다.  
  
2.  다음 테이블을 만듭니다.  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust (CustID uniqueidentifier, LastName varchar(20))  
    CREATE TABLE CustOrder (CustID uniqueidentifier, OrderID int)  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
### <a name="f-specifying-a-schema-in-an-updategram"></a>F. Updategram에 스키마 지정  
 이 예의 Updategram은 다음 테이블에 레코드를 삽입합니다.  
  
```  
CustOrder(OrderID, EmployeeID, OrderType)  
```  
  
 이 Updategram에는 XSD 스키마가 지정됩니다. 즉, Updategram 요소 및 특성의 기본 매핑이 없습니다. 스키마는 데이터베이스 테이블과 열에 필요한 요소 및 특성의 매핑을 제공합니다.  
  
 다음 스키마 (CustOrderSchema.xml)는 **\<CustOrder>** **OrderID** 및 **EmployeeID** 특성으로 구성 된 요소에 대해 설명 합니다. 스키마를 더 흥미롭게 만들려면 **EmployeeID** 특성에 기본값이 할당 됩니다. Updategram은 삽입 작업에 대해서만 및 Updategram에서 해당 특성을 지정하지 않는 경우에만 특성의 기본값을 사용합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="CustOrder" >  
   <xsd:complexType>  
        <xsd:attribute name="OrderID"     type="xsd:integer" />   
        <xsd:attribute name="EmployeeID"  type="xsd:integer" />  
        <xsd:attribute name="OrderType  " type="xsd:integer" default="1"/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 이 Updategram은 CustOrder 테이블에 레코드를 삽입합니다. Updategram은 OrderID 및 EmployeeID 특성 값만 지정합니다. OrderType 특성 값은 지정하지 않습니다. 따라서 Updategram은 앞의 스키마에 지정된 EmployeeID 특성의 기본값을 사용합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
             xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync mapping-schema='CustOrderSchema.xml'>  
<updg:after>  
       <CustOrder OrderID="98000" EmployeeID="1" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 매핑 스키마를 지정 하는 updategram의 추가 예는 [Updategram &#40;SQLXML 4.0&#41;에서 주석이 추가 된 매핑 스키마 지정 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)을 참조 하세요.  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  **Tempdb** 데이터베이스에이 테이블을 만듭니다.  
  
    ```  
    USE tempdb  
    CREATE TABLE CustOrder(  
                     OrderID int,   
                     EmployeeID int,   
                     OrderType int)  
    ```  
  
2.  위 스키마를 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 CustOrderSchema.xml로 저장합니다.  
  
3.  위 Updategram을 복사한 후 텍스트 파일에 붙여 넣습니다. 이전 단계에 사용된 폴더와 같은 폴더에 CustOrderUpdategram.xml로 파일을 저장합니다.  
  
4.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
 <ElementType name="CustOrder" >  
    <AttributeType name="OrderID" />  
    <AttributeType name="EmployeeID" />  
    <AttributeType name="OrderType" default="1" />  
    <attribute type="OrderID"  />  
    <attribute type="EmployeeID" />  
    <attribute type="OrderType" />  
  </ElementType>  
</Schema>  
```  
  
### <a name="g-using-the-xsinil-attribute-to-insert-null-values-in-a-column"></a>G. xsi:nil 특성을 사용하여 열에 Null 값 삽입  
 테이블의 해당 열에 null 값을 삽입 하려는 경우 updategram의 요소에 **xsi: nil** 특성을 지정할 수 있습니다. 해당 XSD 스키마에서 XSD **nillable** 특성도 지정 해야 합니다.  
  
 예를 들어 다음 XSD 스키마를 참조하십시오.  
  
```  
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="Student" sql:relation="Students">  
  <xsd:complexType>  
    <xsd:all>  
      <xsd:element name="fname" sql:field="first_name"   
                                type="xsd:string"   
                                 nillable="true"/>  
    </xsd:all>  
    <xsd:attribute name="SID"   
                        sql:field="StudentID"  
                        type="xsd:ID"/>      
    <xsd:attribute name="lname"       
                        sql:field="last_name"  
                        type="xsd:string"/>  
    <xsd:attribute name="minitial"    
                        sql:field="middle_initial"   
                        type="xsd:string"/>  
    <xsd:attribute name="years"       
                         sql:field="no_of_years"  
                         type="xsd:integer"/>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 XSD 스키마는 요소에 대해 **nillable = "true"** 를 지정 합니다 **\<fname>** . 다음 Updategram은 이 스키마를 사용합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
      xmlns:updg="urn:schemas-microsoft-com:xml-updategram"  
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  
<updg:sync mapping-schema='StudentSchema.xml'>  
  <updg:before/>  
  <updg:after>  
    <Student SID="S00004" lname="Elmaci" minitial="" years="2">  
      <fname xsi:nil="true">  
    </fname>  
    </Student>  
  </updg:after>  
</updg:sync>  
  
</ROOT>  
```  
  
 Updategram는 블록의 요소에 대해 **xsi: nil** 을 지정 합니다 **\<fname>** **\<after>** . 따라서 이 Updategram을 실행하면 테이블의 first_name 열에 대해 NULL 값이 삽입됩니다.  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  **Tempdb** 데이터베이스에 다음 테이블을 만듭니다.  
  
    ```  
    USE tempdb  
    CREATE TABLE Students (  
       StudentID char(6)NOT NULL ,  
       first_name varchar(50),  
       last_name varchar(50),  
       middle_initial char(1),  
       no_of_years int NULL)  
    GO  
    ```  
  
2.  위 스키마를 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 StudentSchema.xml로 저장합니다.  
  
3.  위 Updategram을 복사한 후 텍스트 파일에 붙여 넣습니다. 이전 단계에서 StudentSchema.xml을 저장한 폴더와 같은 폴더에 StudentUpdategram.xml로 파일을 저장합니다.  
  
4.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
### <a name="h-specifying-namespaces-in-an-updategram"></a>H. Updategram에 네임스페이스 지정  
 Updategram에는 Updategram의 동일한 요소에서 선언된 네임스페이스에 속하는 요소가 있을 수 있습니다. 이 경우 해당 스키마에서도 동일한 네임스페이스를 선언해야 하며 요소가 대상 네임스페이스에 속해야 합니다.  
  
 예를 들어 다음 updategram (UpdateGram-ElementHavingNamespace.xml)에서 **\<Order>** 요소는 요소에 선언 된 네임 스페이스에 속합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema='XSD-ElementHavingNameSpace.xml'>  
    <updg:after>  
       <x:Order  xmlns:x="https://server/xyz/schemas/"  
             updg:at-identity="SalesOrderID"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00009999-8888-7777-6666-554433221100"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 이 경우 스키마에서도 이 스키마와 같이 해당 네임스페이스를 선언해야 합니다.  
  
 다음 스키마(XSD-ElementHavingNamespace.xml)에서는 해당 요소와 특성을 선언하는 방법을 보여 줍니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
     xmlns:dt="urn:schemas-microsoft-com:datatypes"   
     xmlns:sql="urn:schemas-microsoft-com:mapping-schema"    
     xmlns:x="https://server/xyz/schemas/"   
     targetNamespace="https://server/xyz/schemas/" >  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" type="x:Order_type"/>  
  <xsd:complexType name="Order_type">  
    <xsd:attribute name="SalesOrderID"  type="xsd:ID"/>  
    <xsd:attribute name="RevisionNumber" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OrderDate" type="xsd:dateTime"/>  
    <xsd:attribute name="DueDate" type="xsd:dateTime"/>  
    <xsd:attribute name="ShipDate" type="xsd:dateTime"/>  
    <xsd:attribute name="Status" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OnlineOrderFlag" type="xsd:boolean"/>  
    <xsd:attribute name="SalesOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="PurchaseOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="AccountNumber" type="xsd:string"/>  
    <xsd:attribute name="CustomerID" type="xsd:int"/>  
    <xsd:attribute name="ContactID" type="xsd:int"/>  
    <xsd:attribute name="SalesPersonID" type="xsd:int"/>  
    <xsd:attribute name="TerritoryID" type="xsd:int"/>  
    <xsd:attribute name="BillToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipMethodID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardApprovalCode" type="xsd:string"/>  
    <xsd:attribute name="CurrencyRateID" type="xsd:int"/>  
    <xsd:attribute name="SubTotal" type="xsd:decimal"/>  
    <xsd:attribute name="TaxAmt" type="xsd:decimal"/>  
    <xsd:attribute name="Freight" type="xsd:decimal"/>  
    <xsd:attribute name="TotalDue" type="xsd:decimal"/>  
    <xsd:attribute name="Comment" type="xsd:string"/>  
    <xsd:attribute name="rowguid" type="xsd:string"/>  
    <xsd:attribute name="ModifiedDate" type="xsd:dateTime"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 스키마를 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 XSD-ElementHavingNamespace.xml로 저장합니다.  
  
2.  위 Updategram을 복사한 후 텍스트 파일에 붙여 넣습니다. XSD-ElementHavingnamespace.xml을 저장한 폴더와 같은 폴더에 Updategram-ElementHavingNamespace.xml로 파일을 저장합니다.  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
### <a name="i-inserting-data-into-an-xml-data-type-column"></a>9\. XML 데이터 형식 열에 데이터 삽입  
 **Xml** 데이터 형식은에서 도입 되었습니다 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] . Updategram을 사용 하 여 **xml** 데이터 형식 열에 저장 된 데이터를 삽입 하 고 업데이트할 수 있습니다.  
  
-   **Xml** 열은 기존 행을 식별 하는 데 사용할 수 없습니다. 따라서 updategram의 **updg: before** 섹션에 포함할 수 없습니다.  
  
-   **Xml** 열에 삽입 되는 xml 조각 범위 내에 있는 네임 스페이스는 유지 되 고 해당 네임 스페이스 선언이 삽입 된 조각의 최상위 요소에 추가 됩니다.  
  
 예를 들어 다음 updategram (SampleUpdateGram.xml)에서 **\<Desc>** 요소는 샘플 데이터베이스의 Production>제품 모델 테이블에서 제품 설명 열을 업데이트 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 합니다. 이 updategram의 결과는 제품 설명 열의 XML 콘텐츠가 요소의 XML 내용으로 업데이트 된다는 것입니다 **\<Desc>** .  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
       <updg:before>  
<ProductModel ProductModelID="19">  
   <Name>Mountain-100</Name>  
</ProductModel>  
    </updg:before>  
    <updg:after>  
 <ProductModel>  
    <Name>Mountain-100</Name>  
    <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
        <p1:ProductDescription xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
              xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
              xmlns:wf="https://www.adventure-works.com/schemas/OtherFeatures"   
              xmlns:html="http://www.w3.org/1999/xhtml"   
              xmlns="">  
  <p1:Summary>  
     <html:p>Insert Example</html:p>  
  </p1:Summary>  
  <p1:Manufacturer>  
    <p1:Name>AdventureWorks</p1:Name>  
    <p1:Copyright>2002</p1:Copyright>  
    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
  </p1:Manufacturer>  
  <p1:Features>These are the product highlights.   
    <wm:Warranty>  
       <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
       <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
    <wm:Maintenance>  
       <wm:NoOfYears>10 years</wm:NoOfYears>  
       <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
    </wm:Maintenance>  
    <wf:wheel>High performance wheels.</wf:wheel>  
    <wf:saddle>  
      <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle>  
    <wf:pedal>  
       <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal>  
    <wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter and wall-thickness required of a premium mountain frame. The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame>  
    <wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset>  
   </p1:Features>  
   <p1:Picture>  
      <p1:Angle>front</p1:Angle>  
      <p1:Size>small</p1:Size>  
      <p1:ProductPhotoID>118</p1:ProductPhotoID>  
   </p1:Picture>  
   <p1:Specifications> These are the product specifications.  
     <Material>Almuminum Alloy</Material>  
     <Color>Available in most colors</Color>  
     <ProductLine>Mountain bike</ProductLine>  
     <Style>Unisex</Style>  
     <RiderExperience>Advanced to Professional riders</RiderExperience>  
   </p1:Specifications>  
  </p1:ProductDescription>  
 </Desc>  
      </ProductModel>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Updategram은 주석이 추가된 다음 XSD 스키마(SampleSchema.xml)를 참조합니다.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
     <xsd:complexType>  
       <xsd:sequence>  
          <xsd:element name="Name" type="xsd:string"></xsd:element>  
          <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
           <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="ProductDescription">  
                 <xsd:complexType>  
                   <xsd:sequence>  
                     <xsd:element name="Summary" type="xsd:anyType">  
                     </xsd:element>  
                   </xsd:sequence>  
                 </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>   
       </xsd:sequence>  
       <xsd:attribute name="ProductModelID" sql:field="ProductModelID"/>  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 스키마를 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 XSD-SampleSchema.xml로 저장합니다.  
  
    > [!NOTE]  
    >  Updategram은 기본 매핑을 지원 하기 때문에 **xml** 데이터 형식의 시작과 끝을 식별할 수 있는 방법이 없습니다. 이는 **xml** 데이터 형식 열을 사용 하 여 테이블을 삽입 하거나 업데이트할 때 매핑 스키마가 필요 함을 의미 합니다. 스키마를 제공하지 않으면 SQLXML에서 열 중 하나가 테이블에 없음을 나타내는 오류를 반환합니다.  
  
2.  위 Updategram을 복사한 후 텍스트 파일에 붙여 넣습니다. SampleSchema.xml을 저장하는 데 사용된 폴더와 같은 폴더에 SampleUpdategram.xml로 파일을 저장합니다.  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Updategram 보안 고려 사항은 SQLXML 4.0&#41;&#40;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
