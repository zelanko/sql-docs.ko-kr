---
title: XML 지 속성 형식을 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 0f794267904ec1c84595b4b627722a1ca935c15a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211012"
---
# <a name="xml-persistence-format"></a>XML 지속성 형식
ADO 유지 XML 스트림에 대 한 utf-8 인코딩을 사용 합니다.  
  
 ADO XML 형식으로 두 개의 섹션에서는 데이터 섹션 뒤에 스키마 섹션으로 구분 됩니다. 다음은 Northwind 데이터베이스에서 Shippers 테이블에 대 한 예제 XML 파일입니다. 다음 예제에서는 XML의 다양 한 부분 설명 합니다.  
  
## <a name="remarks"></a>Remarks  
  
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
  
 스키마 네임 스페이스, 스키마 섹션 및 데이터 섹션의 선언을 보여 줍니다. 스키마 섹션 행, ShipperID, CompanyName 및 전화 번호에 대 한 정의 포함합니다.  
  
 스키마 정의를 따라야 합니다 [W3C XML 데이터 사양](https://www.w3.org/TR/1998/NOTE-XML-data/) 완벽 하 게 유효성을 검사할 수 (경우에 Internet Explorer 5의 유효성 검사를 발생 하지 것입니다). XML 데이터는 현재만 지원 되는 스키마 형식 레코드 집합 지 속성에 대 한 합니다.  
  
 데이터 섹션에는 운송 업체에 대 한 정보를 포함 하는 세 개의 행에 있습니다. 빈 행 집합에 대 한 데이터 섹션 비어 있을 수 있지만 \<rs: 데이터 > 태그가 있어야 합니다. 데이터가 없는 작성할 수 있습니다 태그 줄임 간단히 \<rs: 데이터 / >입니다. 태그 "rs"를 접두사로 urn: 스키마에 의해 정의 된 네임 스페이스 임을 나타냅니다.-microsoft-com:rowset 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
