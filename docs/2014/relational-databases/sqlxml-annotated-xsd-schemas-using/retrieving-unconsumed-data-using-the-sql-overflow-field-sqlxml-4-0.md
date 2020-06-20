---
title: 'Sql: 오버플로 필드를 사용 하 여 사용 되지 않은 데이터 검색 (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- unconsumed data
- storing unconsumed data
- retrieving unconsumed data
- annotated XSD schemas, unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: 8526998d-b47d-4a32-8dc2-7f50a8d11097
author: rothja
ms.author: jroth
ms.openlocfilehash: e87089d05ec00993900bc8a081ebe43ae3adf448
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003184"
---
# <a name="retrieving-unconsumed-data-using-the-sqloverflow-field-sqlxml-40"></a>sql:overflow-field를 사용하여 사용되지 않은 데이터 검색(SQLXML 4.0)
  [!INCLUDE[tsql](../../includes/tsql-md.md)] OPENXML 함수를 사용하여 XML 문서에서 데이터베이스로 레코드를 삽입하는 경우 원본 XML 문서에서 사용되지 않은 모든 데이터를 한 열에 저장할 수 있습니다. 주석 스키마를 사용하여 데이터베이스에서 데이터를 검색할 때는 `sql:overflow-field` 특성을 지정하여 오버플로 데이터가 저장되어 있는 테이블 열을 식별할 수 있습니다. `sql:overflow-field`에서 특성을 지정할 수 있습니다 **\<element>** .  
  
 이 데이터는 다음과 같은 방법으로 검색할 수 있습니다.  
  
-   오버플로 열에 저장된 특성은 `sql:overflow-field` 주석이 포함된 요소에 추가됩니다.  
  
-   데이터베이스의 오버플로 열에 저장된 자식 요소와 해당 하위 항목은 스키마에 명시적으로 지정된 내용에 따라 자식 요소로 추가되며, 이때 순서는 유지되지 않습니다.  
  
## <a name="examples"></a>예제  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예를 실행 하기 위한 요구 사항](../sqlxml/requirements-for-running-sqlxml-examples.md)을 참조 하세요.  
  
### <a name="a-specifying-sqloverflow-field-for-an-element"></a>A. 요소에 Specifying sql:overflow-field 지정  
 이 예에서는 다음 스크립트를 실행한 결과 tempdb 데이터베이스에 Customers2라는 테이블이 생성되었다고 가정합니다.  
  
```  
USE tempdb  
CREATE TABLE Customers2 (  
CustomerID       VARCHAR(10),   
ContactName    VARCHAR(30),   
AddressOverflow    NVARCHAR(500))  
  
GO  
INSERT INTO Customers2 VALUES (  
'ALFKI',   
'Joe',  
'<Address>  
  <Address1>Maple St.</Address1>  
  <Address2>Apt. E105</Address2>  
  <City>Seattle</City>  
  <State>WA</State>  
  <Zip>98147</Zip>  
 </Address>')  
GO  
```  
  
 또한 tempdb 데이터베이스에 대 한 가상 디렉터리를 만들어야 하며 `template` "template" 이라는 형식의 템플릿 가상 이름도 만들어야 합니다.  
  
 다음 예에서 매핑 스키마는 Customers2 테이블의 AddressOverflow 열에 저장되어 있는 사용되지 않은 데이터를 검색합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customers2" sql:overflow-field="AddressOverflow" >  
    <xsd:complexType>  
      <xsd:attribute name="CustomerID"  type="xsd:integer"/>  
      <xsd:attribute name="ContactName"  type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 Overflow.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 Overflow.xml을 저장한 디렉터리와 같은 디렉터리에 OverflowT.xml로 저장합니다. 템플릿의 쿼리는 Customers2 테이블의 레코드를 선택합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="Overflow.xml">  
            /Customers2  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(Overflow.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\Overflow.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 결과 집합은 다음과 같습니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customers2 CustomerID="ALFKI" ContactName="Joe">  
    <Address1>Maple St.</Address1>   
    <Address2>Apt. E105</Address2>   
    <City>Seattle</City>   
    <State>WA</State>   
    <Zip>98147</Zip>   
  </Customers2>  
</ROOT>  
```  
  
  
