---
title: XML Updategrams을 사용 하 여 데이터 업데이트 (SQLXML)
description: SQLXML 4.0에서 XML updategram를 사용 하 여 기존 데이터를 업데이트 하는 방법에 대해 알아봅니다.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREF type attribute [SQLXML]
- before attribute
- <sync> block
- <after> block
- id attribute
- <before> block
- updg:after attribute
- mapping-schema attribute
- IDREFS type attribute [SQLXML]
- updg:id attribute
- multiple record updates
- after attribute
- updategrams [SQLXML], updating data
- updg:before attribute
- record updates [SQLXML]
ms.assetid: 90ef8a33-5ae3-4984-8259-608d2f1d727f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b5539c07b9faab5c426ad9b101d94c683ed665c5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484815"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>XML Updategram을 사용하여 데이터 업데이트(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  기존 데이터를 업데이트 하는 경우 및 블록을 모두 지정 해야 합니다 **\<before>** **\<after>** . 및 블록에 지정 된 요소는 **\<before>** **\<after>** 원하는 변경을 설명 합니다. Updategram은 블록에 지정 된 요소를 사용 하 여 **\<before>** 데이터베이스의 기존 레코드를 식별 합니다. 블록의 해당 요소는 **\<after>** 업데이트 작업을 실행 한 후 레코드를 찾는 방법을 표시 합니다. 이 정보를 통해 updategram는 블록과 일치 하는 SQL 문을 만듭니다 **\<after>** . 그런 다음 Updategram은 이 문을 사용하여 데이터베이스를 업데이트합니다.  
  
 다음은 업데이트 작업을 위한 Updategram 형식입니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
      <ElementName [updg:id="value"] .../>  
      [<ElementName [updg:id="value"] .../> ... ]  
   </updg:before>  
   <updg:after>  
      <ElementName [updg:id="value"] ... />  
      [<ElementName [updg:id="value"] .../> ...]  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 **\<updg:before>**  
 블록의 요소는 **\<before>** 데이터베이스 테이블의 기존 레코드를 식별 합니다.  
  
 **\<updg:after>**  
 블록의 요소는 **\<after>** **\<before>** 업데이트를 적용 한 후 블록에 지정 된 레코드를 확인 하는 방법을 설명 합니다.  
  
 **매핑 스키마** 특성은 updategram에서 사용할 매핑 스키마를 식별 합니다. Updategram가 매핑 스키마를 지정 하는 경우 및 블록에 지정 된 요소 및 특성 이름은 **\<before>** **\<after>** 스키마의 이름과 일치 해야 합니다. 매핑 스키마는 이러한 요소 또는 특성 이름을 데이터베이스 테이블 및 열 이름에 매핑합니다.  
  
 Updategram은 스키마를 지정하지 않을 경우 기본 매핑을 사용합니다. 기본 매핑에서 **\<ElementName>** updategram에 지정 된은 데이터베이스 테이블에 매핑되고 자식 요소 또는 특성은 데이터베이스 열에 매핑됩니다.  
  
 블록의 요소는 **\<before>** 데이터베이스에 있는 하나의 테이블 행과만 일치 해야 합니다. 요소가 여러 테이블 행과 일치 하거나 어떤 테이블 행 과도 일치 하지 않는 경우 updategram는 오류를 반환 하 고 전체 블록을 취소 합니다 **\<sync>** .  
  
 Updategram는 여러 블록을 포함할 수 있습니다 **\<sync>** . 각 **\<sync>** 블록은 트랜잭션으로 처리 됩니다. 각 **\<sync>** 블록에는 여러 **\<before>** 및 블록이 있을 수 있습니다 **\<after>** . 예를 들어 두 개의 기존 레코드를 업데이트 하는 경우 **\<before>** **\<after>** 업데이트 되는 각 레코드에 대해 하나씩 두 개의 및 쌍을 지정할 수 있습니다.  
  
## <a name="using-the-updgid-attribute"></a>updg:id 특성 사용  
 및 블록에 여러 요소가 지정 된 **\<before>** 경우 **\<after>** **updg: id** 특성을 사용 하 여 및 블록의 행을 **\<before>** 표시 **\<after>** 합니다. 처리 논리는이 정보를 사용 하 여 블록에서 블록의 레코드를 사용 하 여 블록 쌍의 레코드를 확인 **\<before>** **\<after>** 합니다.  
  
 다음 중 하나에 해당 하는 경우 **updg: id** 특성은 필요 하지 않습니다 (권장).  
  
-   지정 된 매핑 스키마의 요소에는 **sql: key-fields** 특성이 정의 되어 있습니다.  
  
-   Updategram의 키 필드에 대해 하나 이상의 특정 값이 제공된 경우  
  
 두 경우 모두 updategram는 **sql: key 필드** 에 지정 된 키 열을 사용 하 여 및 블록의 요소를 쌍으로 연결 합니다 **\<before>** **\<after>** .  
  
 매핑 스키마가 키 열을 식별 하지 않는 경우 ( **sql: 키-필드** 를 사용 하 여) 또는 updategram에서 키 열 값을 업데이트 하는 경우 **updg: id** 를 지정 해야 합니다.  
  
 및 블록에서 식별 된 레코드는 **\<before>** **\<after>** 동일한 순서로 지정할 필요가 없습니다. **Updg: id** 특성은 및 블록에 지정 된 요소 간의 연결을 강제로 적용 **\<before>** 합니다 **\<after>** .  
  
 블록에서 하나의 요소를 지정 하 **\<before>** 고 블록에 해당 요소를 하나만 지정 하는 경우 **\<after>** **updg: id** 를 사용 하지 않아도 됩니다. 그러나 모호성을 방지 하려면 **updg: id** 를 지정 하는 것이 좋습니다.  
  
## <a name="examples"></a>예  
 Updategram 예를 사용하기 전에 다음 사항을 확인하십시오.  
  
-   대부분의 예에서는 기본 매핑을 사용합니다. 즉, Updategram에 매핑 스키마가 지정되지 않습니다. 매핑 스키마를 사용 하는 updategram의 추가 예제는 [Updategram &#40;SQLXML 4.0&#41;에서 주석이 추가 된 매핑 스키마 지정 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)을 참조 하세요.  
  
-   대부분의 예에서는 AdventureWorks 예제 데이터베이스를 사용합니다. 모든 업데이트는 이 데이터베이스의 테이블에 적용됩니다. AdventureWorks 데이터베이스를 복원할 수 있습니다.  
  
### <a name="a-updating-a-record"></a>A. 레코드 업데이트  
 다음 Updategram은 AdventureWorks 데이터베이스의 Person.Contact 테이블에서 직원 성을 Fuller로 업데이트합니다. Updategram은 매핑 스키마를 지정하지 않으므로 기본 매핑을 사용합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact LastName="Abel-Achong" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 블록에 설명 된 레코드는 **\<before>** 데이터베이스의 현재 레코드를 나타냅니다. Updategram은 블록에 지정 된 모든 열 값을 사용 하 여 **\<before>** 레코드를 검색 합니다. 이 updategram **\<before>** 블록은 ContactID 열만 제공 하므로 updategram는 값만 사용 하 여 레코드를 검색 합니다. 이 블록에 LastName 값을 추가하면 Updategram은 ContactID와 LastName을 모두 사용하여 검색합니다.  
  
 이 updategram에서 블록은 **\<after>** 변경 되는 유일한 값 이므로 LastName 열 값만 제공 합니다.  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 Updategram 템플릿을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 UpdateLastName.xml로 저장합니다.  
  
2.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  

     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. updg:id 특성을 사용하여 여러 레코드 업데이트  
 이 예에서 Updategram은 AdventureWorks 데이터베이스의 HumanResources.Shift 테이블에 다음과 같은 두 가지 업데이트를 수행합니다.  
  
-   오전 7시에 시작하는 원래의 주간 근무 이름을 "Day"에서 "Early Morning"으로 변경합니다.  
  
-   오전 10시에 시작하는 "Late Morning"이라는 새 근무 시간을 삽입합니다.  
  
 Updategram에서 **updg: id** 특성은 및 블록의 요소 간 연결을 만듭니다 **\<before>** **\<after>** .  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift updg:id="x" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift updg:id="y" Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
      <HumanResources.Shift updg:id="x" Name="Early Morning" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 **Updg: id** 특성이 블록에 있는 요소의 첫 번째 인스턴스를 \<HumanResources.Shift> **\<before>** 블록에 있는 요소의 두 번째 인스턴스와 쌍으로 표시 하는 방법을 확인 \<HumanResources.Shift> **\<after>** 합니다.  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 Updategram 템플릿을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 UpdateMultipleRecords.xml로 저장합니다.  
  
2.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. 여러 \<before> 및 \<after> 블록 지정  
 모호성을 피하려면 여러 개의 **\<before>** 및 블록 쌍을 사용 하 여 예제 B에서 updategram를 작성할 수 있습니다 **\<after>** . 및 쌍을 지정 하는 **\<before>** **\<after>** 방법은 혼동을 최소화 하면서 여러 업데이트를 지정 하는 한 가지 방법입니다. 또한 각 **\<before>** 및 **\<after>** 블록이 최대 하나의 요소를 지정 하는 경우 **updg: id** 특성을 사용할 필요가 없습니다.  
  
> [!NOTE]  
>  쌍을 형성 하려면 **\<after>** 태그가 해당 태그 바로 뒤에와 야 합니다 **\<before>** .  
  
 다음 updategram에서 첫 번째 **\<before>** 및 쌍은 **\<after>** 일 교대의 교대조 이름을 업데이트 합니다. 두 번째 쌍은 새 근무 시간 레코드를 삽입합니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Early Morning" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 Updategram 템플릿을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 UpdateMultipleBeforeAfter.xml로 저장합니다.  
  
2.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. 여러 \<sync> 블록 지정  
 Updategram에서 여러 블록을 지정할 수 있습니다 **\<sync>** . 지정 된 각 **\<sync>** 블록은 독립적인 트랜잭션입니다.  
  
 다음 updategram에서 첫 번째 블록은 **\<sync>** Sales. Customer 테이블의 레코드를 업데이트 합니다. 간단하게 보여 주기 위해 이 Updategram은 필수 열 값, 즉 ID 값(CustomerID)과 업데이트되는 값(SalesPersonID)만 지정합니다.  
  
 두 번째 **\<sync>** 블록은 SalesOrderHeader 테이블에 두 개의 레코드를 추가 합니다. 이 테이블의 경우 SalesOrderID는 IDENTITY 형식 열입니다. 따라서 updategram는 각 요소에 SalesOrderID 값을 지정 하지 않습니다 \<Sales.SalesOrderHeader> .  
  
 여러 블록을 지정 하는 **\<sync>** 것은 두 번째 **\<sync>** 블록 (트랜잭션)이 SalesOrderHeader 테이블에 레코드를 추가 하는 데 실패 하는 경우에도 유용 합니다. 첫 번째 **\<sync>** 블록은 sales. customer 테이블의 고객 레코드를 업데이트할 수 있습니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
      <Sales.Customer CustomerID="1" SalesPersonID="280" />  
    </updg:before>  
    <updg:after>  
      <Sales.Customer CustomerID="1" SalesPersonID="283" />  
    </updg:after>  
  </updg:sync>  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
   <Sales.SalesOrderHeader   
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="01010101-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-08 00:00:00.000" />  
   <Sales.SalesOrderHeader  
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="1000.0000"  
             TaxAmt="0.0000"  
             Freight="0.0000"  
             rowguid="10101010-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-09 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 Updategram 템플릿을 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 UpdateMultipleSyncs.xml로 저장합니다.  
  
2.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
### <a name="e-using-a-mapping-schema"></a>E. 매핑 스키마 사용  
 이 예제에서 updategram는 **매핑** 스키마 특성을 사용 하 여 매핑 스키마를 지정 합니다. 기본 매핑은 없습니다. 즉, 매핑 스키마가 데이터베이스 테이블 및 열에 대한 Updategram의 필요한 요소 및 특성 매핑을 제공합니다.  
  
 Updategram에 지정된 요소와 특성은 매핑 스키마의 요소와 특성을 참조합니다.  
  
 다음 XSD 매핑 스키마에는 **\<Customer>** **\<Order>** **\<OD>** 데이터베이스의 sales. Customer, SalesOrderHeader 및 SalesOrderDetail 테이블에 매핑되는, 및 요소가 있습니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustomerOrder"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustomerOrder" >  
           <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OD"   
                             sql:relation="Sales.SalesOrderDetail"  
                             sql:relationship="OrderOD" >  
                 <xsd:complexType>  
                  <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                  <xsd:attribute name="ProductID" type="xsd:integer" />  
                  <xsd:attribute name="UnitPrice" type="xsd:decimal" />  
                  <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  <xsd:attribute name="UnitPriceDiscount" type="xsd:decimal" />   
                 </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
           </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 이 매핑 스키마(UpdategramMappingSchema.xml)는 다음 Updategram에 지정됩니다. Updategram은 특정 주문에 대한 Sales.SalesOrderDetail 테이블에 주문 세부 정보 항목을 추가합니다. Updategram에는 요소 내에 중첩 된 요소가 포함 됩니다. **\<OD>** **\<Order>** 이 두 요소 간의 기본 키/외래 키 관계는 매핑 스키마에 지정됩니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="UpdategramMappingSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43659" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43659" >  
          <OD ProductID="776" UnitPrice="2329.0000"  
              OrderQty="2" UnitPriceDiscount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  위 매핑 스키마를 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 UpdategramMappingSchema.xml로 저장합니다.  
  
2.  위 Updategram 템플릿을 복사한 후 텍스트 파일에 붙여 넣습니다. 매핑 스키마(UpdategramMappingSchema.xml)를 저장할 때 사용한 폴더와 동일한 폴더에 UpdateWithMappingSchema.xml로 파일을 저장합니다.  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 매핑 스키마를 사용 하는 updategram의 추가 예제는 [Updategram &#40;SQLXML 4.0&#41;에서 주석이 추가 된 매핑 스키마 지정 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)을 참조 하세요.  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. 매핑 스키마와 IDREFS 특성 함께 사용  
 이 예에서는 Updategram이 매핑 스키마에서 IDREFS 특성을 사용하여 여러 테이블의 레코드를 업데이트하는 방법을 보여 줍니다. 이 예에서는 데이터베이스가 다음 테이블로 구성되어 있다고 가정합니다.  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 한 명의 학생이 다수의 과목에 등록할 수 있고, 하나의 과목은 다수의 학생을 가질 수 있으므로 이 M:N 관계를 나타내기 위해 세 번째 테이블인 Enrollment 테이블이 필요합니다.  
  
 다음 XSD 매핑 스키마는 **\<Student>** , 및 요소를 사용 하 여 테이블의 XML 뷰를 제공 합니다 **\<Course>** **\<Enrollment>** . 매핑 스키마의 **IDREFS** 특성은 이러한 요소 간의 관계를 지정 합니다. 요소의 **StudentIDList** 특성은 **\<Course>** 등록 테이블의 StudentID 열을 참조 하는 **IDREFS** 유형 특성입니다. 마찬가지로 요소의 **EnrolledIn** 특성은 **\<Student>** 등록 테이블의 CourseID 열을 참조 하는 **IDREFS** 유형 특성입니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="StudentEnrollment"  
          parent="Student"  
          parent-key="StudentID"  
          child="Enrollment"  
          child-key="StudentID" />  
  
    <sql:relationship name="CourseEnrollment"  
          parent="Course"  
          parent-key="CourseID"  
          child="Enrollment"  
          child-key="CourseID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Course" sql:relation="Course"   
                             sql:key-fields="CourseID" >  
    <xsd:complexType>  
    <xsd:attribute name="CourseID"  type="xsd:string" />   
    <xsd:attribute name="CourseName"   type="xsd:string" />   
    <xsd:attribute name="StudentIDList" sql:relation="Enrollment"  
                 sql:field="StudentID"  
                 sql:relationship="CourseEnrollment"   
                                     type="xsd:IDREFS" />  
  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name="Student" sql:relation="Student" >  
    <xsd:complexType>  
    <xsd:attribute name="StudentID"  type="xsd:string" />   
    <xsd:attribute name="LastName"   type="xsd:string" />   
    <xsd:attribute name="EnrolledIn" sql:relation="Enrollment"  
                 sql:field="CourseID"  
                 sql:relationship="StudentEnrollment"   
                                     type="xsd:IDREFS" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Updategram에 이 스키마를 지정하고 Course 테이블에 레코드를 삽입할 때마다 Updategram은 Course 테이블에 새 과목 레코드를 삽입합니다. 또한 StudentIDList 특성에 대해 하나 이상의 새 학생 ID를 지정하면 Updategram은 각 새 학생에 대해 Enrollment 테이블에 레코드를 삽입합니다. Updategram은 Enrollment 테이블에 중복 항목이 추가되지 않도록 합니다.  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  가상 루트에 지정된 데이터베이스에 다음과 같이 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE Student(StudentID varchar(10) primary key,   
                         LastName varchar(25))  
    CREATE TABLE Course(CourseID varchar(10) primary key,   
                        CourseName varchar(25))  
    CREATE TABLE Enrollment(StudentID varchar(10)   
                                      references Student(StudentID),  
                           CourseID varchar(10)   
                                      references Course(CourseID))  
    ```  
  
2.  다음 예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Student VALUES ('S1','Davoli')  
    INSERT INTO Student VALUES ('S2','Fuller')  
  
    INSERT INTO Course VALUES  ('CS101', 'C Programming')  
    INSERT INTO Course VALUES  ('CS102', 'Understanding XML')  
  
    INSERT INTO Enrollment VALUES ('S1', 'CS101')  
    INSERT INTO Enrollment VALUES ('S1', 'CS102')  
    ```  
  
3.  위 매핑 스키마를 복사한 후 텍스트 파일에 붙여 넣습니다. 파일을 SampleSchema.xml로 저장합니다.  
  
4.  이전 단계에서 매핑 스키마를 저장하는 데 사용한 폴더와 동일한 폴더에 Updategram(SampleUpdategram)을 저장합니다. 이 Updategram은 CS102 과목에서 StudentID="1"인 학생을 삭제합니다.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
5.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
6.  다음 Updategram을 이전 단계에서 설명된 대로 저장하고 실행합니다. Updategram은 Enrollment 테이블에 레코드를 추가하여 StudentID="1"인 학생을 CS102 과목에 다시 추가합니다.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
7.  이 다음 Updategram을 이전 단계에서 설명된 대로 저장하고 실행합니다. 이 Updategram은 3명의 새 학생을 삽입하고 CS101 과목에 등록합니다. IDREFS 관계는 다시 Enrollment 테이블에 레코드를 삽입합니다.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
           <Course updg:id="y" CourseID="CS101"   
                               CourseName="C Programming" />  
        </updg:before>  
        <updg:after >  
           <Student updg:id="x1" StudentID="S3" LastName="Leverling" />  
           <Student updg:id="x2" StudentID="S4" LastName="Pecock" />  
           <Student updg:id="x3" StudentID="S5" LastName="Buchanan" />  
           <Course updg:id="y" CourseID="CS101"  
                               CourseName="C Programming"  
                               StudentIDList="S3 S4 S5" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ElementType name="Enrollment" sql:relation="Enrollment" sql:key-fields="StudentID CourseID">  
    <AttributeType name="StudentID" dt:type="id" />  
    <AttributeType name="CourseID" dt:type="id" />  
  
    <attribute type="StudentID" />  
    <attribute type="CourseID" />  
  </ElementType>  
  <ElementType name="Course" sql:relation="Course" sql:key-fields="CourseID">  
    <AttributeType name="CourseID" dt:type="id" />  
    <AttributeType name="CourseName" />  
  
    <attribute type="CourseID" />  
    <attribute type="CourseName" />  
  
    <AttributeType name="StudentIDList" dt:type="idrefs" />  
    <attribute type="StudentIDList" sql:relation="Enrollment" sql:field="StudentID" >  
        <sql:relationship  
                key-relation="Course"  
                key="CourseID"  
                foreign-relation="Enrollment"  
                foreign-key="CourseID" />  
    </attribute>  
  
  </ElementType>  
  <ElementType name="Student" sql:relation="Student">  
    <AttributeType name="StudentID" dt:type="id" />  
     <AttributeType name="LastName" />  
  
    <attribute type="StudentID" />  
    <attribute type="LastName" />  
  
    <AttributeType name="EnrolledIn" dt:type="idrefs" />  
    <attribute type="EnrolledIn" sql:relation="Enrollment" sql:field="CourseID" >  
        <sql:relationship  
                key-relation="Student"  
                key="StudentID"  
                foreign-relation="Enrollment"  
                foreign-key="StudentID" />  
    </attribute>  
  
    <element type="Enrollment" sql:relation="Enrollment" >  
        <sql:relationship key-relation="Student"  
                          key="StudentID"  
                          foreign-relation="Enrollment"  
                          foreign-key="StudentID" />  
    </element>  
  </ElementType>  
  
</Schema>  
```  
  
 매핑 스키마를 사용 하는 updategram의 추가 예제는 [Updategram &#40;SQLXML 4.0&#41;에서 주석이 추가 된 매핑 스키마 지정 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Updategram 보안 고려 사항은 SQLXML 4.0&#41;&#40;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
