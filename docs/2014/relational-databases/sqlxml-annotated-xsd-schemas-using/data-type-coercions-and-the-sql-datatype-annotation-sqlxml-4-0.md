---
title: '데이터 형식 강제 변환 및 sql: datatype 주석 (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 095df15d5a917b54e1a518445f49a7ab1f351378
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297943"
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>데이터 형식 강제 변환 및 sql:datatype 주석(SQLXML 4.0)
  XSD 스키마에서 `xsd:type` 특성은 요소 또는 특성의 XSD 데이터 형식을 지정합니다. XSD 스키마를 사용하여 데이터베이스에서 데이터를 추출할 경우 지정된 데이터 형식이 데이터 서식 지정에 사용됩니다.  
  
 `sql:datatype` 주석을 사용하면 스키마에 XSD 형식을 지정할 수 있을 뿐만 아니라 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식도 지정할 수 있습니다. `xsd:type` 및 `sql:datatype` 특성은 XSD 데이터 형식과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 간의 매핑을 제어합니다.  
  
## <a name="xsdtype-attribute"></a>xsd:type 특성  
 `xsd:type` 특성을 사용하여 열에 매핑되는 특성이나 요소의 XML 데이터 형식을 지정할 수 있습니다. `xsd:type`은 서버에서 반환되는 문서뿐만 아니라 실행되는 XPath 쿼리에도 영향을 미칩니다. `xsd:type`이 포함된 매핑 스키마를 기준으로 XPath 쿼리가 실행될 때 XPath는 지정된 데이터 형식을 사용하여 쿼리를 처리합니다. XPath 사용 하는 방법에 대 한 자세한 내용은 `xsd:type`를 참조 하세요 [XSD 데이터 형식을 XPath 데이터 형식에 매핑 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)합니다.  
  
 반환된 문서에서 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식은 문자열 표현으로 변환됩니다. 일부 데이터 형식에는 추가적인 변환이 필요합니다. 다음 표에서는 다양한 `xsd:type` 값에 사용되는 변환을 보여 줍니다.  
  
|XSD 데이터 형식|SQL Server 변환|  
|-------------------|---------------------------|  
|Boolean|CONVERT(bit, COLUMN)|  
|Date|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|Decimal|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|Time|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|나머지|추가 변환 없음|  
  
> [!NOTE]  
>  "XYZ"를 `xsd:type` 데이터 형식으로 변환하는 경우처럼 변환이 가능하지 않거나 -100000을 `decimal` XSD 형식으로 변환하는 경우처럼 값이 데이터 형식의 범위를 초과하는 경우와 같이, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 반환되는 일부 값이 `UnsignedShort`을 사용하여 지정한 XML 데이터 형식과 호환되지 않을 수 있습니다. 호환되지 않는 형식 변환은 XML 문서를 유효하지 않게 만들거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류를 발생시킬 수 있습니다.  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>SQL Server 데이터 형식에서 XSD 데이터 형식으로의 매핑  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에서 XSD 데이터 형식으로의 명확한 매핑을 보여 줍니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식을 아는 경우 이 표를 통해 XSD 스키마에 지정할 수 있는 해당 XSD 형식을 확인할 수 있습니다.  
  
|SQL Server 데이터 형식|XSD 데이터 형식|  
|--------------------------|-------------------|  
|`bigint`|`long`|  
|`binary`|`base64Binary`|  
|`bit`|`boolean`|  
|`char`|`string`|  
|`datetime`|`dateTime`|  
|`decimal`|`decimal`|  
|`float`|`double`|  
|`image`|`base64Binary`|  
|`int`|`int`|  
|`money`|`decimal`|  
|`nchar`|`string`|  
|`ntext`|`string`|  
|`nvarchar`|`string`|  
|`numeric`|`decimal`|  
|`real`|`float`|  
|`smalldatetime`|`dateTime`|  
|`smallint`|`short`|  
|`smallmoney`|`decimal`|  
|`sql_variant`|`string`|  
|`sysname`|`string`|  
|`text`|`string`|  
|`timestamp`|`dateTime`|  
|`tinyint`|`unsignedByte`|  
|`varbinary`|`base64Binary`|  
|`varchar`|`string`|  
|`uniqueidentifier`|`string`|  
  
## <a name="sqldatatype-annotation"></a>sql:datatype 주석  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지정하는 데에는 `sql:datatype` 주석이 사용됩니다. 다음 경우에 이 주석을 지정해야 합니다.  
  
-   에 대량 로드 하는 한 `dateTime` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XSD에서 열 `dateTime`, `date`, 또는 `time` 형식. 이 경우에는 `sql:datatype="dateTime"`을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열 데이터 형식을 식별해야 합니다. 이 규칙은 updategram에도 적용됩니다.  
  
-   열으로 대량 로드 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `uniqueidentifier` 형식과 XSD 값은 중괄호를 포함 하는 GUID ({및}). `sql:datatype="uniqueidentifier"`를 지정하면 열에 값을 삽입하기 전에 중괄호가 제거됩니다. `sql:datatype`을 지정하지 않으면 값이 중괄호와 함께 보내지므로 삽입이나 업데이트가 실패합니다.  
  
-   XML 데이터 형식 `base64Binary`는 다양한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식(`binary`, `image` 또는 `varbinary`)에 매핑됩니다. XML 데이터 형식 `base64Binary`를 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 매핑하려면 `sql:datatype` 주석을 사용합니다. 이 주석은 특성이 매핑될 열의 명시적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지정합니다. 데이터가 데이터베이스에 저장될 경우 이 주석을 사용하는 것이 좋습니다. `sql:datatype` 주석을 지정하면 명시적 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 식별할 수 있습니다.  
  
 일반적으로 스키마에 `sql:datatype`을 지정하는 것이 좋습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예 실행에 대 한 요구 사항](../sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-xsdtype"></a>1. xsd:type 지정  
 이 예에서는 스키마에서 `date` 특성을 사용하여 지정한 XSD `xsd:type` 형식이 결과 XML 문서에 미치는 영향을 보여 줍니다. 이 스키마에서는 AdventureWorks 데이터베이스에 Sales.SalesOrderHeader 테이블의 XML 뷰를 제공합니다.  
  
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
  
-   지정 `xsd:type=date` 에 **OrderDate** 특성을 반환 하는 값의 날짜 부분 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대 한 합니다 **OrderDate** 특성이 표시 됩니다.  
  
-   지정 `xsd:type=time` 에 **ShipDate** 특성에 의해 반환 되는 값의 시간 부분 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대 한 합니다 **ShipDate** 특성이 표시 됩니다.  
  
-   지정 하지 않습니다 `xsd:type` 에 **DueDate** 특성에 의해 반환 되는 동일한 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 표시 됩니다.  
  
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
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
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
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>2. sql:datatype을 사용하여 SQL 데이터 형식 지정  
 작업 샘플은 예제 G를 참조 하세요 [XML 대량 로드 예 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)합니다. 이 예에서는 "{" 및 "}"을 포함하는 GUID 값을 대량 로드합니다. 이 예의 스키마는 `sql:datatype`을 지정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 `uniqueidentifier`로 식별합니다. 이 예에서는 스키마에서 `sql:datatype`을 지정해야 하는 경우를 설명합니다.  
  
  
