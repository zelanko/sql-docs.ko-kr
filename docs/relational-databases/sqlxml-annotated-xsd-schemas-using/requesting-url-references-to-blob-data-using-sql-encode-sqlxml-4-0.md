---
title: 'BLOB 데이터를 사용 하 여 sql에 대 한 URL 참조 요청: 인코딩 (SQLXML 4.0) | Microsoft 문서'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 5eba5d17938d4bcfce27fb70476cad3e8974a1c0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39543343"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>sql:encode를 사용하여 BLOB 데이터에 대한 URL 참조 요청(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  주석이 추가된 XSD 스키마에서 특성(또는 요소)이 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 BLOB 열에 매핑된 경우 XML 내의 Base 64 인코딩 형식으로 데이터가 반환됩니다.  
  
 데이터에 대 한 참조를 원하는 경우 (URI)를 반환 하는 데 사용할 수 나중에 이진 형식으로 BLOB 데이터 검색을 지정 합니다 **sql: 인코딩** 주석. 지정할 수 있습니다 **sql: 인코딩** 단순 유형의 요소 또는 특성입니다.  
  
 지정 된 **sql: 인코딩** 주석 필드에 대 한 URL 필드 값 대신 반환 되어야 함을 나타냅니다. **sql: 인코딩** URL에 단일 선택을 생성 기본 키에 따라 달라 집니다. 사용 하 여 기본 키를 지정할 수 있습니다 합니다 **sql:-필드** 주석입니다.  
  
 합니다 **sql: 인코딩** 주석에 "url" 또는 "default" 값을 할당할 수 있습니다. "default" 값은 Base 64 인코딩 형식으로 데이터를 반환합니다.  
  
 합니다 **sql: 인코딩** 주석을 사용할 수 없습니다 **sql:use-cdata** 나 ID, IDREF, IDREFS, NMTOKEN 또는 NMTOKENS 특성 유형에 합니다. 것도 사용할 수 없습니다 XSD를 사용 하 여 **고정** 특성입니다.  
  
> [!NOTE]  
>  BLOB 유형의 열은 키 또는 외래 키의 일부로 사용할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예를 사용하여 작업 예제를 만들려면 특정 요구 사항이 충족되어야 합니다. 자세한 내용은 [SQLXML 예 실행에 대 한 요구 사항](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>1. sql:encode를 지정하여 BLOB 데이터에 대한 URL 참조 얻기  
 이 예에서 매핑 스키마 지정 **sql: 인코딩** 에 **LargePhoto** (Base 64-에서 이진 데이터를 검색 하는 대신 특정 제품 사진에 대 한 URI 참조를 검색 하는 특성 인코딩된 형식)입니다.  
  
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
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
 다음은 결과입니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
