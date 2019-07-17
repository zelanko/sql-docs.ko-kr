---
title: Sql:use 사용 하 여 CDATA 섹션 만들기-cdata (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d2c0e81c6a497f9377d04adc94f3a9e221758f81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126568"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>sql:use-cdata를 사용하여 CDATA 섹션 만들기(SQLXML 4.0)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML에서 CDATA 섹션은 태그 문자로 인식될 문자가 포함된 텍스트 블록을 이스케이프하는 데 사용됩니다.  
  
 데이터베이스에 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 태그 문자 XML 파서에서 처리는; 예를 들어, 괄호 (< 및 >), 덜-보다-또는-같음 기호 각도 문자를 포함할 수 있습니다 때로는 (< =), 앰퍼샌드 (&)는 처리 태그 문자입니다. 하지만 이러한 유형의 특수 문자를 CDATA 섹션에 래핑하여 태그 문자로 처리되지 않도록 할 수 있습니다. CDATA 섹션 내의 텍스트는 XML 파서에서 일반 텍스트로 처리됩니다.  
  
 합니다 **sql:use-cdata** 주석에서 반환 된 데이터를 지정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDATA 섹션에 래핑해야 합니다 (열에서 값을 인지 여부는 나타냅니다 즉, 지정 된 **sql: field** CDATA 섹션으로 묶어야 합니다). 합니다 **sql:use-cdata** 주석은 데이터베이스 열에 매핑되는 요소에 대해서만 지정할 수 있습니다.  
  
 합니다 **sql:use-cdata** 주석은 부울 값 (0 = false, 1 = true). 허용되는 값은 0, 1, true 및 false입니다.  
  
 이 주석을 사용할 수 없습니다 **sql:url-인코딩** ID, IDREF, IDREFS, NMTOKEN 및 NMTOKENS 특성 유형에 또는 합니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예 실행에 대 한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. 요소에 sql:use-cdata 지정  
 다음 스키마에서 **sql:use-cdata** 1(true)로 설정 됩니다는  **\<주소란 1, 주소란 >** 내는  **\<주소 >** 요소입니다. 따라서 데이터가 CDATA 섹션으로 반환됩니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
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
  
  
