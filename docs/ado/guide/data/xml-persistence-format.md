---
title: "XML 지 속성 형식 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8694aac4f8699d102d94664862f5ad357579eab9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="xml-persistence-format"></a>XML 지 속성 형식
ADO 혹시 계속 될 XML 스트림에 대 한 utf-8 인코딩을 사용 합니다.  
  
 ADO XML 형식의 스키마 section 다음 데이터 섹션에 두 개의 섹션으로 구분 됩니다. 다음은 Northwind 데이터베이스에서 Shippers 테이블에 대 한 예제 XML 파일입니다. 다음 예제는 XML의 다양 한 부분 설명 되어 있습니다.  
  
## <a name="remarks"></a>주의  
  
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
  
 스키마 정의 준수 하는 [W3C XML 데이터 사양](http://www.w3.org/TR/1998/NOTE-XML-data/) 완벽 하 게 유효성을 검사할 수 (경우에 유효성 검사에서 Internet Explorer 5 발생 하지 것입니다). XML 데이터는 현재 레코드 집합 지 속성에 대 한 지원 되는 유일한 스키마 형식입니다.  
  
 데이터 섹션에는 운송 업체에 대 한 정보를 포함 하는 3 개의 행에 있습니다. 빈 행 집합에 대 한 데이터 섹션 비어 있을 수 있지만 \<rs: 데이터 > 태그가 있어야 합니다. 데이터가 없는 작성할 수 태그 줄임 간단 하 게 \<rs: 데이터 / >입니다. 모든 태그 "rs" 접두사로 urn: 스키마에 의해 정의 된 네임 스페이스 임을 나타냅니다.-microsoft-com:rowset 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)

