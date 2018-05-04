---
title: 스키마 섹션 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7614a2c23d21d88652c32fef480367df4db65be8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="schema-section"></a>스키마 섹션
스키마 섹션이 필요 합니다. 이전 예제와 같이 ADO 업데이트에 대 한 가능한 한 데이터 값의 의미 체계를 유지 하기 위해 각 열에 대 한 메타 데이터를 작성 합니다. 그러나 XML을 로드 하려면 ADO 하기만 열과 소속 된 행 집합의 이름을 합니다. 다음은 최소한의 스키마의 예가입니다.  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 이전 예에서 ADO은 처리 데이터를 가변 길이 문자열로 스키마에 형식 정보가 없기 때문에 합니다.  
  
## <a name="creating-aliases-for-column-names"></a>열 이름에 대 한 별칭 만들기  
 Rs: name 특성을 사용 하면 이름을 행 집합에 나와 있는 열 정보에 나타날 수 있습니다 하 고 데이터 섹션에 더 짧은 이름을 사용할 수 있도록 열 이름에 대 한 별칭을 만들 수 있습니다. 예를 들어, s1, s2, CompanyName ShipperID 매핑한 다음과 같이 s 3에 전화를 이전 스키마를 변경할 수 있습니다.  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 다음 행의 데이터 섹션에서 해당 열을 참조할 name 특성 (rs 이름 아님)를 사용 합니다.:  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 열 이름이 유효한 특성 또는 xml에서 태그 이름이 없을 때마다에 열 이름에 대 한 별칭을 만들 필요는 좋습니다. 예를 들어 "LastName" 별칭이 있어야 공백이 포함된 된 이름이 잘못 된 특성 때문에 있습니다. 다음 줄은 올바르게를 처리할 수는 XML 파서에서 다른 이름으로 포함 된 공간에 대 한 별칭을 만들어야 합니다.  
  
```  
<row last name="Jones"/>  
```  
  
 XML 문서의 스키마와 데이터 섹션에 참조 되는 열은 각 위치에 name 특성에 사용 하는 값을 일관성 있게 사용 되어야 합니다. 다음 예에서는 s 1의 일관 된 사용을 보여 줍니다.  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 마찬가지로, 있기 때문에 없는 별칭에 대해 정의 `CompanyName` 이전 예에서 `CompanyName` 문서 전체에서 일관 되 게 사용 해야 합니다.  
  
## <a name="data-types"></a>데이터 형식  
 Dt: type 특성을 가진 열에는 데이터 형식에 적용할 수 있습니다. 허용 되는 XML 형식은 하기 위한 최선의 가이드의 데이터 형식 섹션을 참조 하십시오.는 [W3C XML 데이터 사양](http://www.w3.org/TR/1998/NOTE-XML-data/)합니다. 두 가지 방법으로 데이터 형식을 지정할 수 있습니다: 열 정의 자체에서 직접 dt: type 특성을 지정 하거나 열 정의의 중첩 요소로 방법 사용 합니다. 예를 들면 다음과 같습니다.  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 가 같음  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 기본적으로 행 정의에서 완전히 dt: type 특성을 생략 하면 열의 형식을 가변 길이 문자열 됩니다.  
  
 단순히 형식 이름 (예를 들어 dt: maxlength) 보다 더 많은 형식 정보가 있는 경우 이렇게 하면 더 읽기 쉬운 s:datatype 자식 요소를 사용 합니다. 그러나이 단지는 규칙, 및 요구 사항은 아닙니다.  
  
 다음 예에서는 스키마에서 형식 정보를 포함 하는 방법을 보여 추가 합니다.  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!—or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!—- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!—- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!—- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 두 번째 예에서 rs: fixedlength 특성을 사용 하는 미묘한 있습니다. Rs: fixedlength 특성을 가진 열에는 데이터에는 스키마에 정의 된 길이 사용 해야 합니다. true로 설정 합니다. 이 경우 title_id에 대 한 유효한 값은 "123456" 됩니다 "123"입니다. 그러나 "123" 사용할 수 없습니다 길이 3, 6 하지 때문에 있습니다. Fixedlength 속성 설명을 완료 읅 OLE DB Programmer's Guide를 참조 하십시오.  
  
## <a name="handling-nulls"></a>Null을 처리  
 Rs: maybenull 특성으로 null 값 처리 됩니다. 이 특성이로 설정 된 경우 true 이면 열 내용의 수 null 값을 포함 합니다. 또한 열 데이터의 행에 없는 경우 행 집합에서 다시 데이터를 읽는 사용자는 IRowset::GetData()에서 null 상태를 받게 됩니다. Shippers 테이블에서 다음 열 정의 고려 합니다.  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 정의 사용 하면 `CompanyName` , null이 될 수 있지만 `ShipperID` null 값을 포함할 수 없습니다. 데이터 섹션에서 다음 행에 포함 된 경우 지 속성 공급자 설정에 대 한 데이터의 상태는 `CompanyName` OLE DB 상태 상수 DBSTATUS_S_ISNULL 열:  
  
```  
<z:row ShipperID="1"/>  
```  
  
 행이 다음과 같이 완전히 비어 있는 경우, 하는 경우 지 속성 공급자는는 OLE DB의 반환 상태에 대 한 dbstatus_e_unavailable로 `ShipperID` 및 DBSTATUS_S_ISNULL CompanyName에 대 한 합니다.  
  
```  
<z:row/>   
```  
  
 Note 길이가 0 인 문자열은 null과 동일 합니다.  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 이전 행에 대 한 지 속성 공급자는 두 열 모두에 대 한 DBSTATUS_S_OK의 OLE DB 상태를 반환 합니다. `CompanyName` 이 경우에 단순히 "" (빈 문자열)입니다.  
  
 OLE DB에 대 한 자세한 내용은 OLE DB에 대 한 XML 문서의 스키마 내에서 사용 하기 위해 사용할 수 있는 구문에 대 한 참조의 정의 ":-microsoft-com:rowset" 및 OLE DB 프로그래머 가이드입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
