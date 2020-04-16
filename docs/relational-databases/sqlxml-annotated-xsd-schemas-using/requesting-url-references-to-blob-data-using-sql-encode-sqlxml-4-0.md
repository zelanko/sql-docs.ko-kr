---
title: SQLXML(SQLXML)을 사용하여 BLOB 데이터에 대한 URL 참조 받기
description: SQLXML 4.0에서 sql:encode 별칭을 지정하여 BLOB 데이터에 대한 URL 참조를 요청하는 방법을 알아봅니다.
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 487ed2bbee997db22739bdeecd7e024b817ace80
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388113"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>sql:encode를 사용하여 BLOB 데이터에 대한 URL 참조 요청(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  주석이 추가된 XSD 스키마에서 특성(또는 요소)이 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 BLOB 열에 매핑된 경우 XML 내의 Base 64 인코딩 형식으로 데이터가 반환됩니다.  
  
 나중에 이진 형식으로 BLOB 데이터를 검색하는 데 사용할 수 있는 데이터(URI)에 대한 참조를 반환하려면 **sql:encode** annotation을 지정합니다. 간단한 형식의 특성 또는 요소에 **sql:encode를** 지정할 수 있습니다.  
  
 **sql:encode** 참조를 지정하여 필드의 값 대신 필드에 대한 URL을 반환해야 함을 나타냅니다. **sql:인코딩은** URL에서 단일 선택을 생성하는 기본 키에 따라 다릅니다. 기본 키는 **sql:key 필드** 별표를 사용하여 지정할 수 있습니다.  
  
 **sql:encode** 부포는 "url" 또는 "기본" 값을 할당할 수 있습니다. "default" 값은 Base 64 인코딩 형식으로 데이터를 반환합니다.  
  
 **sql:encode** annotation **sql:use-cdata** 또는 ID, IDREF, IDREFS, NMTOKEN 또는 NMTOKENS 특성 형식에서 사용할 수 없습니다. 또한 XSD **고정** 특성과 함께 사용할 수 없습니다.  
  
> [!NOTE]  
>  BLOB 유형의 열은 키 또는 외래 키의 일부로 사용할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 실행 요구 사항 예제를](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)참조하십시오.  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. sql:encode를 지정하여 BLOB 데이터에 대한 URL 참조 얻기  
 이 예제에서 매핑 스키마는 **LargePhoto** 특성에서 **sql:encode를** 지정하여 Base 64 인코딩 된 형식으로 이진 데이터를 검색하는 대신 특정 제품 사진에 대한 URI 참조를 검색합니다.  
  
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
  
     자세한 내용은 [ADO를 사용하여 SQLXML 4.0 쿼리를 실행합니다.](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)  
  
 다음은 결과입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
