---
title: 사용 되지 않은 데이터를 사용 하 여 sql:overflow 검색-(SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- unconsumed data
- storing unconsumed data
- retrieving unconsumed data
- annotated XSD schemas, unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: 8526998d-b47d-4a32-8dc2-7f50a8d11097
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c82c157d5d76a2b6dfd005bf7984bd3e60cb69e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="retrieving-unconsumed-data-using-the-sqloverflow-field-sqlxml-40"></a>sql:overflow-field를 사용하여 사용되지 않은 데이터 검색(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] OPENXML 함수를 사용하여 XML 문서에서 데이터베이스로 레코드를 삽입하는 경우 원본 XML 문서에서 사용되지 않은 모든 데이터를 한 열에 저장할 수 있습니다. 주석이 추가 된 스키마를 사용 하 여 데이터베이스에서 데이터를 검색할 때 지정할 수 있습니다는 **sql:overflow-필드** 오버플로 데이터가 저장 되어 있는 테이블의 열을 식별 하는 특성입니다. **sql:overflow-필드** 특성에 지정할 수 있으며  **\<요소 >**합니다.  
  
 이 데이터는 다음과 같은 방법으로 검색할 수 있습니다.  
  
-   오버플로 열에 저장 된 특성이 포함 된 요소에 추가 되는 **sql:overflow-필드** 주석입니다.  
  
-   데이터베이스의 오버플로 열에 저장된 자식 요소와 해당 하위 항목은 스키마에 명시적으로 지정된 내용에 따라 자식 요소로 추가되며, 이때 순서는 유지되지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 참조 [SQLXML 예 실행에 대 한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-sqloverflow-field-for-an-element"></a>1. 요소에 Specifying sql:overflow-field 지정  
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
  
 또한 tempdb 데이터베이스에 대 한 가상 디렉터리를 만들어야-및의 템플릿 가상 이름도 **템플릿** "template" 이라는 형식입니다.  
  
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
  
     자세한 내용은 참조 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
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
  
  
