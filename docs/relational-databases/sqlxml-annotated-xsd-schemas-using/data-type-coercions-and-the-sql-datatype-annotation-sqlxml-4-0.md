---
title: '데이터 형식 강제 변환 및 sql: datatype 주석 (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 21dc355570d5a2778e553924a189ce985513a7cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65981033"
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>데이터 형식 강제 변환 및 sql:datatype 주석(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSD 스키마에 **xsd: type** 특성 요소 또는 특성의 XSD 데이터 형식을 지정 합니다. XSD 스키마를 사용하여 데이터베이스에서 데이터를 추출할 경우 지정된 데이터 형식이 데이터 서식 지정에 사용됩니다.  
  
 XSD 형식 스키마에서를 지정 하는 것 외에도 지정할 수 있습니다 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 사용 하 여 합니다 **sql: datatype** 주석입니다. 합니다 **xsd: type** 하 고 **sql: datatype** 특성에 XSD 데이터 형식 간의 매핑을 제어 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
## <a name="xsdtype-attribute"></a>xsd:type 특성  
 사용할 수는 **xsd: type** XML 데이터 형식의 열에 매핑되는 요소나 특성을 지정 하는 특성입니다. 합니다 **xsd: type** 서버 및 실행 되는 XPath 쿼리에서 반환 되는 문서에 영향을 줍니다. 포함 된 매핑 스키마에 대해 XPath 쿼리를 실행할 때 **xsd: type**, XPath 쿼리를 처리할 때 지정 된 데이터 형식을 사용 합니다. XPath 사용 하는 방법에 대 한 자세한 내용은 **xsd: type**를 참조 하십시오 [XSD 데이터 형식을 XPath 데이터 형식에 매핑 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md).  
  
 반환된 문서에서 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식은 문자열 표현으로 변환됩니다. 일부 데이터 형식에는 추가적인 변환이 필요합니다. 다음 표에서 다양 한에 사용 되는 변환을 **xsd: type** 값입니다.  
  
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
>  반환 하는 값의 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 지정 된 XML 데이터 형식과 호환 되지 않을 수 있습니다 **xsd: type**를 변환이 불가능 하기 때문에 (예를 들어 변환할 "XYZ"는  **10 진수** 데이터 형식) 또는 해당 데이터 형식의 범위를 초과 하는 값 (-100000으로 변환 하는 예를 들어는 **UnsignedShort** XSD 형식). 호환되지 않는 형식 변환은 XML 문서를 유효하지 않게 만들거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류를 발생시킬 수 있습니다.  
  
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
 **sql: datatype** 주석에 지정 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식,이 주석은 지정 해야:  
  
-   에 대량 로드 하는 **날짜/시간** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] xsd에서 열 **dateTime**를 **날짜**, 또는 **시간** 형식입니다. 이 경우 식별 해야 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 열 데이터 형식 **sql: datatype = "dateTime"** 합니다. 이 규칙은 updategram에도 적용됩니다.  
  
-   열으로 대량 로드 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **uniqueidentifier** 형식과 XSD 값은 중괄호를 포함 하는 GUID ({및}). 지정 하는 경우 **sql: datatype = "uniqueidentifier"** , 열에 삽입 하기 전에 중괄호가 값에서 제거 됩니다. 하는 경우 **sql: datatype** 를 지정 하지 않은 값 삽입 이나 업데이트가 실패 하 고 중괄호를 사용 하 여 전송 됩니다.  
  
-   XML 데이터 형식 **base64Binary** 다양 한 매핑됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 (**이진**를 **이미지**, 또는 **varbinary**). XML 데이터 형식에 매핑할 **base64Binary** 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 사용 합니다 **sql: datatype** 주석입니다. 이 주석은 특성이 매핑될 열의 명시적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지정합니다. 데이터가 데이터베이스에 저장될 경우 이 주석을 사용하는 것이 좋습니다. 지정 하 여 합니다 **sql: datatype** 주석이 명시적 식별할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
 지정 하는 것이 좋습니다 **sql: datatype** 스키마에 있습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예 실행에 대 한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-xsdtype"></a>1\. xsd:type 지정  
 이 예에서는 XSD **날짜** 사용 하 여 지정 된 형식에는 **xsd: type** 스키마의 특성 결과 XML 문서에 영향을 줍니다. 이 스키마에서는 AdventureWorks 데이터베이스에 Sales.SalesOrderHeader 테이블의 XML 뷰를 제공합니다.  
  
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
  
-   지정 **xsd: type = 날짜** 에 **OrderDate** 특성을 반환 하는 값의 날짜 부분 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대 한 합니다 **OrderDate** 특성이 표시 됩니다.  
  
-   지정 **xsd: type = 시간** 에 **ShipDate** 특성에 의해 반환 되는 값의 시간 부분 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대 한 합니다 **ShipDate** 특성이 표시 됩니다.  
  
-   지정 하지 않습니다 **xsd: type** 에 **DueDate** 특성에 의해 반환 되는 동일한 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 표시 됩니다.  
  
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
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
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
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>2\. sql:datatype을 사용하여 SQL 데이터 형식 지정  
 작업 샘플은 예제 G를 참조 하세요 [XML 대량 로드 예 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)합니다. 이 예에서는 "{" 및 "}"을 포함하는 GUID 값을 대량 로드합니다. 이 예제에서 스키마 지정 **sql: datatype** 식별 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 **uniqueidentifier**합니다. 이 예제에서는 시기를 보여 줍니다 **sql: datatype** 스키마를 지정 해야 합니다.  
  
  
