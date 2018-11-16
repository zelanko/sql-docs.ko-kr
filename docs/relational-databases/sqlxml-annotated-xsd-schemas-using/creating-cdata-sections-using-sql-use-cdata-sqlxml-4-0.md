---
title: Sql:use 사용 하 여 CDATA 섹션 만들기-cdata (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ed36a17744c9626b54de7439af20cdd76c2bc18
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51667402"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>sql:use-cdata를 사용하여 CDATA 섹션 만들기(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML에서 CDATA 섹션은 태그 문자로 인식될 문자가 포함된 텍스트 블록을 이스케이프하는 데 사용됩니다.  
  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터베이스에는 XML 파서에서 태그 문자로 처리되는 문자가 포함될 수 있습니다. 예를 들어 꺾쇠 괄호(< 및 >), 작거나 같음 기호(<=) 및 앰퍼샌드(&)는 태그 문자로 처리됩니다. 하지만 이러한 유형의 특수 문자를 CDATA 섹션에 래핑하여 태그 문자로 처리되지 않도록 할 수 있습니다. CDATA 섹션 내의 텍스트는 XML 파서에서 일반 텍스트로 처리됩니다.  
  
 합니다 **sql:use-cdata** 주석에서 반환 된 데이터를 지정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDATA 섹션에 래핑해야 합니다 (열에서 값을 인지 여부는 나타냅니다 즉, 지정 된 **sql: field** CDATA 섹션으로 묶어야 합니다). 합니다 **sql:use-cdata** 주석은 데이터베이스 열에 매핑되는 요소에 대해서만 지정할 수 있습니다.  
  
 합니다 **sql:use-cdata** 주석은 부울 값 (0 = false, 1 = true). 허용되는 값은 0, 1, true 및 false입니다.  
  
 이 주석을 사용할 수 없습니다 **sql:url-인코딩** ID, IDREF, IDREFS, NMTOKEN 및 NMTOKENS 특성 유형에 또는 합니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예 실행에 대 한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>1. 요소에 sql:use-cdata 지정  
 다음 스키마에서 **sql:use-cdata** 1(true)로 설정 됩니다는  **\<주소란 1, 주소란 >** 내는  **\<주소 >** 요소입니다. 따라서 데이터가 CDATA 섹션으로 반환됩니다.  
  
```  
<xsd:schema xmlns:xsd="https://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 UseCData.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. UseCData.xml을 저장한 디렉터리와 같은 디렉터리에 UseCDataT.xml로 파일을 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(UseCData.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리를 기준으로 합니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 결과 집합의 일부입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
