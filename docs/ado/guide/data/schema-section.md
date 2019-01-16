---
title: 스키마 섹션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e8e37d8bb85e727771072abda9249b8155076f
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256198"
---
# <a name="schema-section"></a>스키마 섹션
스키마 섹션은 필수입니다. 이전 예제에서 알 수 있듯이, ADO 데이터 값의 의미 체계를 업데이트 하기 위한 최대한 유지 하기 위해 각 열에 대 한 자세한 메타 데이터를 작성 합니다. 그러나 XML을 로드 하려면 ADO 하기만 열 및 속해 있는 행 집합의 이름입니다. 최소 스키마의 예는 다음과 같습니다.  
  
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
  
 이전 예제에서는 ADO는 처리 데이터를 가변 길이 문자열로 형식 정보가 없는 스키마에 포함 되어 있으므로 합니다.  
  
## <a name="creating-aliases-for-column-names"></a>열 이름에 대 한 별칭을 만드는 방법  
 Rs: 이름 특성을 사용 하면 이름을 노출 행 집합에서 열 정보에 나타날 수 있습니다 하 고 더 짧은 이름을 데이터 섹션에서 사용할 수 있도록 열 이름에 대 한 별칭을 만들 수 있습니다. 예를 들어, s1, s2, CompanyName ShipperID 매핑 및 s3 같이 Phone 이전 스키마를 변경할 수 있습니다.  
  
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
  
 그런 다음 데이터 섹션에 행 사용 name 특성 (rs 이름이 아님) 해당 열을 참조 합니다.:  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 열 이름 별칭을 만드는 방법 열 이름을 유효한 특성 또는 xml에서 태그 이름이 없을 때마다 필요 합니다. 예를 들어, "LastName" 별칭이 있어야 공백이 포함된 된 이름은 잘못 된 특성 때문입니다. 다음 줄은 처리 되지 않습니다 올바르게 XML 파서에서 공백이 없는 다른 이름에 대 한 별칭을 만들어야 합니다.  
  
```  
<row last name="Jones"/>  
```  
  
 XML 문서의 스키마 및 데이터 섹션에서 참조 되는 열에는 각 위치에 name 특성에 사용할 값을 일관 되 게 사용 되어야 합니다. 다음 예제에서는 s1의 일관 된 사용을 보여 줍니다.  
  
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
  
 에 대 한 별칭이 없는 정의 되어 있기 때문에 마찬가지로 `CompanyName` 이전 예에서 `CompanyName` 문서 전체에서 일관 되 게 사용 해야 합니다.  
  
## <a name="data-types"></a>데이터 형식  
 Dt: type 특성을 사용 하 여 열 데이터 형식에 적용할 수 있습니다. 허용 되는 XML 형식에 선언적 가이드의 데이터 형식 섹션을 참조 합니다 [W3C XML 데이터 사양](http://www.w3.org/TR/1998/NOTE-XML-data/)합니다. 두 가지 방법으로 데이터 형식을 지정할 수 있습니다: 열 정의 자체가에 직접 dt: type 특성을 지정 하거나 방법 열 정의의 중첩 된 요소로 사용 합니다. 예:  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 위의 식은 아래의 식과 동일합니다.  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 기본적으로 행 정의에서 완전히 dt: type 특성을 생략 하면 가변 길이 문자열 열의 형식이 됩니다.  
  
 간단한 형식 이름 (예를 들어 dt: maxlength) 보다 더 많은 형식 정보에 있는 경우이 있도록 s:datatype 자식 요소를 사용 하는 것이 쉬운 합니다. 그러나이 단순히에서 규칙을 요구 사항이 아니라 있습니다.  
  
 다음 예제에서는 추가 스키마에 형식 정보를 포함 하는 방법을 표시 합니다.  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!-or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!-- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!-- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!-- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 두 번째 예제에서 rs: fixedlength 특성을 사용 하는 미묘한 있습니다. Rs: fixedlength 특성을 가진 열을 데이터 스키마에 정의 된 길이 포함 해야 하는 true로 설정 합니다. 이 경우 title_id에 대 한 유효한 값은 "123456,"는 "123"입니다. 그러나 "123" 해당 길이 3, 6 하지 때문에 하지 유효한 것입니다. Fixedlength 속성 설명은 완료 더에 대 한 OLE DB Programmer's Guide를 참조 하세요.  
  
## <a name="handling-nulls"></a>Null 처리  
 Rs: maybenull 특성으로 null 값 처리 됩니다. 이 특성이로 설정 된 경우 true 이면 열 내용의 수 null 값을 포함 합니다. 또한 열 데이터의 행에 없는 경우 행 집합에서 다시 데이터를 읽는 사용자는 IRowset::GetData()에서 null 상태를을 받게 됩니다. Shippers 테이블에서 다음 열 정의 고려해 야 합니다.  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 정의 사용 하면 `CompanyName` null 일 수 있지만 `ShipperID` null 값을 포함할 수 없습니다. 데이터 섹션에서 다음 행에 포함 하는 경우 지 속성 공급자 설정에 대 한 데이터의 상태는 `CompanyName` OLE DB 상태 상수 DBSTATUS_S_ISNULL 열:  
  
```  
<z:row ShipperID="1"/>  
```  
  
 지 속성 공급자는 OLE DB 상태에 대 한 DBSTATUS_E_UNAVAILABLE의 반환 행 인 경우 완전히 비어 있는 경우 다음과 같이 `ShipperID` 및 DBSTATUS_S_ISNULL CompanyName에 대 한 합니다.  
  
```  
<z:row/>   
```  
  
 길이가 0 인 문자열은 null로 동일한 note 합니다.  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 이전 행에 대 한 지 속성 공급자는 OLE DB 상태 DBSTATUS_S_OK의 두 열 모두에 대 한 반환 합니다. `CompanyName` 여기서는 단순히 "" (빈 문자열)입니다.  
  
 OLE DB에 대 한 자세한 내용은 OLE DB에 대 한 XML 문서의 스키마 내에서 사용 하기 위해 사용할 수 있는 구문을 정의 참조 "urn: 스키마-microsoft-com:rowset" 및 OLE DB 프로그래머 가이드입니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
