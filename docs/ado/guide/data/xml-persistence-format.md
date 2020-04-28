---
title: XML 지 속성 형식 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e2d1c30546a8466ba9950f31cffdfb9447bd89ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923384"
---
# <a name="xml-persistence-format"></a>XML 지속성 형식
ADO는 유지 되는 XML 스트림에 UTF-8 인코딩을 사용 합니다.  
  
 ADO XML 형식은 두 개의 섹션, 즉 스키마 섹션과 데이터 섹션으로 구분 됩니다. 다음은 Northwind 데이터베이스의 운송 테이블에 대 한 예제 XML 파일입니다. XML의 여러 부분에 대해서는 예제 다음에 설명 되어 있습니다.  
  
## <a name="remarks"></a>설명  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"   
xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"   
xmlns:rs="urn:schemas-microsoft-com:rowset"   
xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="ShipperID" rs:number="1"   
        rs:basetable="shippers" rs:basecolumn="ShipperID"  
        rs:keycolumn="true">   
        <s:datatype dt:type="int" dt:maxLength="4" rs:precision="10"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="CompanyName" rs:number="2"   
        rs:nullable="true" rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="CompanyName">   
        <s:datatype dt:type="string" dt:maxLength="40" />   
      </s:AttributeType>   
      <s:AttributeType name="Phone" rs:number="3" rs:nullable="true"   
        rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="Phone">   
        <s:datatype dt:type="string" dt:maxLength="24"/>   
      </s:AttributeType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  
  <rs:data>   
    <z:row ShipperID="1" CompanyName="Speedy Express"   
      Phone="(503) 555-9831"/>   
    <z:row ShipperID="2" CompanyName="United Package"   
      Phone="(503) 555-3199"/>   
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>   
  </rs:data>   
</xml>  
```  
  
 스키마는 네임 스페이스, 스키마 섹션 및 데이터 섹션의 선언을 보여 줍니다. Schema 섹션에는 row,와 함께 Id, CompanyName 및 Phone에 대 한 정의가 포함 되어 있습니다.  
  
 스키마 정의는 [W3C XML 데이터 사양을](http://www.w3.org/TR/1998/NOTE-XML-data/) 따르며 완전히 유효성을 검사할 수 있습니다. 그러나 Internet Explorer 5에서는 유효성 검사가 수행 되지 않습니다. 현재 XML 데이터는 레코드 집합 지 속성에 대해 지원 되는 유일한 스키마 형식입니다.  
  
 데이터 섹션에는 운송 정보를 포함 하는 3 개의 행이 있습니다. 빈 행 집합의 경우 데이터 섹션이 비어 있을 수 있지만 \<rs: data> 태그가 있어야 합니다. 데이터가 없는 경우 간단한 \<rs: data/> 태그를 작성할 수 있습니다. "Rs" 접두사가 붙은 태그는 urn: 스키마-microsoft-com: rowset에서 정의 된 네임 스페이스에 있음을 나타냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
