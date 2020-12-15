---
title: 'Sql: datatype을 사용 하 여 데이터 형식 변환 (SQLXML)'
description: 'SQLXML 4.0의 xsd: type 및 sql: datatype 특성을 사용 하 여 XSD 데이터 형식과 SQL Server 데이터 형식 간의 매핑을 제어 하는 방법에 대해 알아봅니다.'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- type attribute
- sql:datatype
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- xsd:type
- datatype annotation
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XSD schemas [SQLXML], mapping data types
ms.assetid: db192105-e8aa-4392-b812-9d727918c005
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0e457aa6c1d1e16e96682f19898e22813254e9ef
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461804"
---
# <a name="data-type-conversions-and-the-sqldatatype-annotation-sqlxml-40"></a>데이터 형식 변환 및 sql: datatype 주석 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Xsd 스키마에서 **xsd: type** 특성은 요소나 특성의 xsd 데이터 형식을 지정 합니다. XSD 스키마를 사용하여 데이터베이스에서 데이터를 추출할 경우 지정된 데이터 형식이 데이터 서식 지정에 사용됩니다.  
  
 스키마에 XSD 형식을 지정 하는 것 외에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sql: datatype** 주석을 사용 하 여 Microsoft 데이터 형식을 지정할 수 있습니다. **Xsd: type** 및 **sql: DATATYPE** 특성은 xsd 데이터 형식과 데이터 형식 간의 매핑을 제어 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="xsdtype-attribute"></a>xsd:type 특성  
 **Xsd: type** 특성을 사용 하 여 열에 매핑되는 특성 또는 요소의 XML 데이터 형식을 지정할 수 있습니다. **Xsd: type** 은 서버에서 반환 되는 문서 및 실행 되는 XPath 쿼리에 영향을 줍니다. **Xsd: type** 이 포함 된 매핑 스키마에 대해 xpath 쿼리를 실행 하면 xpath는 쿼리를 처리할 때 지정 된 데이터 형식을 사용 합니다. XPath에서 **xsd: type** 을 사용 하는 방법에 대 한 자세한 내용은 [&#40;SQLXML 4.0&#41;Xsd 데이터 형식을 xpath 데이터 형식에 매핑](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)을 참조 하세요.  
  
 반환된 문서에서 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식은 문자열 표현으로 변환됩니다. 일부 데이터 형식에는 추가적인 변환이 필요합니다. 다음 표에서는 다양 한 **xsd: type** 값에 사용 되는 변환을 나열 합니다.  
  
|XSD 데이터 형식|SQL Server 변환|  
|-------------------|---------------------------|  
|부울|CONVERT(bit, COLUMN)|  
|Date|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|decimal|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|시간|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|나머지|추가 변환 없음|  
  
> [!NOTE]  
>  에서 반환 하는 값 중 일부는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xsd: type** 을 사용 하 여 지정 된 XML 데이터 형식과 호환 되지 않을 수 있습니다. 예를 들어 "XYZ"를 **decimal** 데이터 형식으로 변환 하는 것과 같이 변환할 수 없거나 값이 해당 데이터 형식의 범위를 초과 하는 경우 (예:-10만을 **unsignedshort** 않는 xsd 형식으로 변환) 호환되지 않는 형식 변환은 XML 문서를 유효하지 않게 만들거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류를 발생시킬 수 있습니다.  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>SQL Server 데이터 형식에서 XSD 데이터 형식으로의 매핑  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에서 XSD 데이터 형식으로의 명확한 매핑을 보여 줍니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식을 아는 경우 이 표를 통해 XSD 스키마에 지정할 수 있는 해당 XSD 형식을 확인할 수 있습니다.  
  
|SQL Server 데이터 형식|XSD 데이터 형식|  
|--------------------------|-------------------|  
|**bigint**|**long**|  
|**binary**|**base64Binary**|  
|**bit**|**boolean**|  
|**char**|**string**|  
|**datetime**|**dateTime**|  
|**decimal**|**decimal**|  
|**float**|**double**|  
|**image**|**base64Binary**|  
|**int**|**int**|  
|**money**|**decimal**|  
|**nchar**|**string**|  
|**ntext**|**string**|  
|**nvarchar**|**string**|  
|**numeric**|**decimal**|  
|**real**|**float**|  
|**smalldatetime**|**dateTime**|  
|**smallint**|**short**|  
|**smallmoney**|**decimal**|  
|**sql_variant**|**string**|  
|**sysname**|**string**|  
|**text**|**string**|  
|**timestamp**|**dateTime**|  
|**tinyint**|**unsignedByte**|  
|**varbinary**|**base64Binary**|  
|**varchar**|**string**|  
|**uniqueidentifier**|**string**|  
  
## <a name="sqldatatype-annotation"></a>sql:datatype 주석  
 **Sql: datatype** 주석은 데이터 형식을 지정 하는 데 사용 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 경우에는이 주석을 지정 해야 합니다.  
  
-    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XSD **날짜**/시간, **날짜** 또는 **시간** 형식에서 datetime 열로 대량 로드 합니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sql: datatype = "dateTime"** 을 사용 하 여 열 데이터 형식을 식별 해야 합니다. 이 규칙은 updategram에도 적용됩니다.  
  
-   Uniqueidentifier 형식의 열에 대량 로드 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  고 XSD 값은 중괄호 ({및})를 포함 하는 GUID입니다. **Sql: datatype = "uniqueidentifier"** 를 지정 하면 열에 삽입 되기 전에 값에서 중괄호가 제거 됩니다. **Sql: datatype** 을 지정 하지 않으면 값이 중괄호와 함께 전송 되 고 삽입 또는 업데이트가 실패 합니다.  
  
-   XML 데이터 형식 **base64Binary** 는 다양 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 (**binary**, **image** 또는 **varbinary**)에 매핑됩니다. XML 데이터 형식 **base64Binary** 을 특정 데이터 형식에 매핑하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sql: datatype** 주석을 사용 합니다. 이 주석은 특성이 매핑될 열의 명시적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지정합니다. 데이터가 데이터베이스에 저장될 경우 이 주석을 사용하는 것이 좋습니다. **Sql: datatype** 주석을 지정 하 여 명시적 데이터 형식을 식별할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 일반적으로 스키마에서 **sql: datatype** 을 지정 하는 것이 좋습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예를 실행 하기 위한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)을 참조 하세요.  
  
### <a name="a-specifying-xsdtype"></a>A. xsd:type 지정  
 이 예에서는 스키마의 **xsd: type** 특성을 사용 하 여 지정 된 xsd **날짜** 유형이 결과 XML 문서에 주는 영향을 보여 줍니다. 이 스키마에서는 AdventureWorks 데이터베이스에 Sales.SalesOrderHeader 테이블의 XML 뷰를 제공합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader">  
     <xsd:complexType>  
       <xsd:attribute name="SalesOrderID" type="xsd:string" />   
       <xsd:attribute name="CustomerID"   type="xsd:string" />   
       <xsd:attribute name="OrderDate"    type="xsd:date" />   
       <xsd:attribute name="DueDate"  />   
       <xsd:attribute name="ShipDate"  type="xsd:time" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 이 XSD 스키마에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜 값을 반환하는 세 가지 특성이 있습니다. 스키마에서 다음을 확인하십시오.  
  
-   **Orderdate** 특성에서 **xsd: type = date** 를 지정 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **orderdate** 특성에 대해에서 반환 하는 값의 날짜 부분을 표시 합니다.  
  
-   **ShipDate** 특성에 대해 **xsd: type = time** 을 지정 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ShipDate** 특성에 대해에서 반환 하는 값의 시간 부분이 표시 됩니다.  
  
-   **DueDate** 특성에 **xsd: type** 을 지정 하지 않으면에서 반환 하는 것과 동일한 값 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 표시 됩니다.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 xsdType.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 xsdType.xml을 저장한 디렉터리와 같은 디렉터리에 xsdTypeT.xml로 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="xsdType.xml">  
        /Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(xsdType.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\xsdType.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  

     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43659"   
         CustomerID="676"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
  <Order SalesOrderID="43660"   
         CustomerID="117"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
 ...  
</ROOT>  
```  
  
 다음은 동등한 XDR 스키마입니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader">  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="CustomerID"  />  
    <AttributeType name="OrderDate" dt:type="date" />  
    <AttributeType name="DueDate" />  
    <AttributeType name="ShipDate" dt:type="time" />  
  
    <attribute type="SalesOrderID" sql:field="OrderID" />  
    <attribute type="CustomerID" sql:field="CustomerID" />  
    <attribute type="OrderDate" sql:field="OrderDate" />  
    <attribute type="DueDate" sql:field="DueDate" />  
    <attribute type="ShipDate" sql:field="ShipDate" />  
</ElementType>  
</Schema>  
```  
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>B. sql:datatype을 사용하여 SQL 데이터 형식 지정  
 작업 샘플은 [SQLXML 4.0&#41;&#40;XML 대량 로드 예제의 ](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)예제 G를 참조 하세요. 이 예에서는 "{" 및 "}"을 포함하는 GUID 값을 대량 로드합니다. 이 예의 스키마는 **sql: datatype** 을 지정 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 **uniqueidentifier** 로 식별 합니다. 이 예에서는 스키마에 **sql: datatype** 을 지정 해야 하는 경우를 보여 줍니다.  
  
  
