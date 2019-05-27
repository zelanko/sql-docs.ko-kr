---
title: Sql:use 사용 하 여 CDATA 섹션 만들기-cdata (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cddde2ed1e40b2ea21cf4ebff75bea3beed8f2ce
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014009"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>sql:use-cdata를 사용하여 CDATA 섹션 만들기(SQLXML 4.0)
  XML에서 CDATA 섹션은 태그 문자로 인식될 문자가 포함된 텍스트 블록을 이스케이프하는 데 사용됩니다.  
  
 Microsoft의 데이터베이스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 파서에서 태그 문자로 처리 됩니다; 예를 들어 꺾쇠 괄호는 문자가 포함 될 수 있습니다 (\< 및 >), 작음 보다-또는-같음 기호 (< =), 및 앰퍼샌드 (&)는 태그 문자로 처리 합니다. 하지만 이러한 유형의 특수 문자를 CDATA 섹션에 래핑하여 태그 문자로 처리되지 않도록 할 수 있습니다. CDATA 섹션 내의 텍스트는 XML 파서에서 일반 텍스트로 처리됩니다.  
  
 `sql:use-cdata` 주석은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 반환된 데이터를 CDATA 섹션에 래핑하도록 지정하는 데 사용됩니다. 즉, `sql:field`로 지정된 열의 값을 CDATA 섹션에 포함할지 여부를 나타냅니다. `sql:use-cdata` 주석은 데이터베이스 열에 매핑되는 요소에만 지정할 수 있습니다.  
  
 `sql:use-cdata` 주석은 부울 값(0=false, 1=true)을 사용합니다. 허용되는 값은 0, 1, true 및 false입니다.  
  
 `sql:url-encode`나 ID, IDREF, IDREFS, NMTOKEN 및 NMTOKENS 특성 유형에는 이 주석을 사용할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예 실행에 대 한 요구 사항](../sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>1. 요소에 sql:use-cdata 지정  
 다음 스키마에서 `sql:use-cdata` 1(true)로 설정 됩니다는  **\<주소란 1, 주소란 >** 내 합니다  **\<주소 >** 요소입니다. 따라서 데이터가 CDATA 섹션으로 반환됩니다.  
  
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
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
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
  
  
