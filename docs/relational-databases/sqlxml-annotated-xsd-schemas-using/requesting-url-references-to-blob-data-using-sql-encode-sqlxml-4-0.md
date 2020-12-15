---
title: 'Sql: 인코드 (SQLXML)를 사용 하 여 BLOB 데이터에 대 한 URL 참조 가져오기'
description: 'SQLXML 4.0에 sql: encoding 주석을 지정 하 여 BLOB 데이터에 대 한 URL 참조를 요청 하는 방법에 대해 알아봅니다.'
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:encode
- encode annotation
- URL references to BLOB data [SQLXML]
- references to BLOB data [SQLXML]
- annotated XSD schemas, URL references to BLOB data
- requesting URL references to BLOB data
- BLOBs, URL references
- Base 64-encoded format
ms.assetid: 2f8cd93b-c636-462b-8291-167197233ee0
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 432b1b888392b345038d14bb18909ba90b4d86a7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461754"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>sql:encode를 사용하여 BLOB 데이터에 대한 URL 참조 요청(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  주석이 추가된 XSD 스키마에서 특성(또는 요소)이 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 BLOB 열에 매핑된 경우 XML 내의 Base 64 인코딩 형식으로 데이터가 반환됩니다.  
  
 나중에 이진 형식으로 BLOB 데이터를 검색 하는 데 사용할 수 있는 데이터에 대 한 참조 (URI)를 반환 하려면 **sql:** encoding 주석을 지정 합니다. 단순 형식의 특성 또는 요소에 대해 **sql:** encoding을 지정할 수 있습니다.  
  
 필드 값 대신 필드에 대 한 URL을 반환 하도록 지정 하려면 **sql:** encoding 주석을 지정 합니다. **sql: 인코드** 는 기본 키에 따라 URL에서 단일 select를 생성 합니다. **Sql: 키-필드** 주석을 사용 하 여 기본 키를 지정할 수 있습니다.  
  
 **Sql: 인코드** 주석에는 "url" 또는 "default" 값을 할당할 수 있습니다. "default" 값은 Base 64 인코딩 형식으로 데이터를 반환합니다.  
  
 Sql **: encoding 주석은** **sql: use-cdata** 또는 ID, IDREF, IDREFS, NMTOKEN 또는 NMTOKENS 특성 유형에 사용할 수 없습니다. XSD **fixed** 특성에도 사용할 수 없습니다.  
  
> [!NOTE]  
>  BLOB 유형의 열은 키 또는 외래 키의 일부로 사용할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예를 실행 하기 위한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)을 참조 하세요.  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. sql:encode를 지정하여 BLOB 데이터에 대한 URL 참조 얻기  
 이 예에서 매핑 스키마는 **LargePhoto** 특성에 **sql:** encoding을 지정 하 여 기본 64 인코딩 형식으로 이진 데이터를 검색 하는 대신 특정 제품 사진에 대 한 URI 참조를 검색 합니다.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="ProductPhoto" sql:relation="Production.ProductPhoto"   
               sql:key-fields="ProductPhotoID" >  
   <xsd:complexType>  
      <xsd:attribute name="ProductPhotoID"  type="xsd:int"  />  
     <xsd:attribute name="LargePhoto" type="xsd:string" sql:encode="url" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>스키마에 대해 예제 XPath 쿼리를 테스트하려면  
  
1.  위 스키마 코드를 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 sqlEncode.xml로 저장합니다.  
  
2.  다음 템플릿을 복사한 후 텍스트 파일에 붙여넣습니다. sqlEncode.xml을 저장한 디렉터리와 같은 디렉터리에 sqlEncodeT.xml로 파일을 저장합니다.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sqlEncode.xml">  
            /ProductPhoto[@ProductPhotoID=100]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     매핑 스키마(sqlEncode.xml)에 대해 지정된 디렉터리 경로는 템플릿이 저장된 디렉터리에 상대적입니다. 또한 다음과 같이 절대 경로를 지정할 수 있습니다.  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlEncode.xml"  
    ```  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 템플릿을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
 다음은 결과입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
