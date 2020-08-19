---
description: 스키마 섹션
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b7d3a82231e31771a6f01dc558feebdc98dcbe1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452895"
---
# <a name="schema-section"></a>스키마 섹션
스키마 섹션이 필요 합니다. 이전 예제에서 볼 수 있듯이 ADO는 각 열에 대 한 자세한 메타 데이터를 작성 하 여 데이터 값의 의미 체계를 업데이트 가능한 한 많이 유지 합니다. 그러나 XML에서 로드 하려면 ADO에 열 이름과 해당 열이 속한 행 집합만 필요 합니다. 최소 스키마의 예는 다음과 같습니다.  
  
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
  
 이전 예제에서 ADO는 스키마에 형식 정보가 포함 되어 있지 않기 때문에 데이터를 가변 길이 문자열로 취급 합니다.  
  
## <a name="creating-aliases-for-column-names"></a>열 이름에 대 한 별칭 만들기  
 Rs: name 특성을 사용 하면 열 이름에 대 한 별칭을 만들어 행 집합에 의해 노출 되는 열 정보에 이름이 표시 될 수 있으며 데이터 섹션에 더 짧은 이름을 사용할 수 있습니다. 예를 들어 앞의 스키마를 수정 하 여 다음과 같이가 나이를 s1, CompanyName을 s2로, Phone을 s 2에 매핑할 수 있습니다.  
  
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
  
 그런 다음 데이터 섹션에서 행은 name 특성 (rs: name 아님)을 사용 하 여 해당 열을 참조 합니다.  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 열 이름이 XML에서 올바른 특성 또는 태그 이름이 아닐 때마다 열 이름에 대 한 별칭을 만드는 것이 필요 합니다. 예를 들어 공백이 포함 된 이름은 잘못 된 특성 이므로 "LastName"은 별칭을 포함 해야 합니다. 다음 줄은 XML 파서에서 올바르게 처리 되지 않으므로 공백을 포함 하지 않는 다른 이름에 대 한 별칭을 만들어야 합니다.  
  
```  
<row last name="Jones"/>  
```  
  
 Name 특성에 사용 하는 모든 값은 XML 문서의 스키마 및 데이터 섹션 모두에서 열이 참조 되는 각 위치의 일관 되 게 사용 되어야 합니다. 다음 예제에서는 s1을 일관 되 게 사용 하는 방법을 보여 줍니다.  
  
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
  
 마찬가지로, 이전 예제에서에 대해 정의 된 별칭이 없기 때문에 `CompanyName` `CompanyName` 문서 전체에서를 일관 되 게 사용 해야 합니다.  
  
## <a name="data-types"></a>데이터 형식  
 Dt: type 특성을 사용 하 여 열에 데이터 형식을 적용할 수 있습니다. 허용 되는 XML 유형에 대 한 명확한 지침은 [W3C XML 데이터 사양의](http://www.w3.org/TR/1998/NOTE-XML-data/)데이터 형식 섹션을 참조 하세요. 다음 두 가지 방법으로 데이터 형식을 지정할 수 있습니다. 열 정의 자체에는 dt: type 특성을 직접 지정 하거나, 열 정의의 중첩 된 요소로는 다음과 같은 두 가지 방법을 사용 합니다. 예를 들면 다음과 같습니다.  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 위의 식은 아래의 식과 동일합니다.  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 행 정의에서 완전히 dt: type 특성을 생략 하는 경우 기본적으로 열의 형식은 가변 길이 문자열이 됩니다.  
  
 형식 이름 (예: dt: maxLength) 보다 더 많은 형식 정보가 있는 경우에는이를 통해 내용 데이터 형식 자식 요소를 보다 읽기 쉽게 만들 수 있습니다. 그러나이는 단순한 규칙 이지만 요구 사항은 아닙니다.  
  
 다음 예제에서는 스키마에 형식 정보를 포함 하는 방법을 자세히 보여 줍니다.  
  
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
  
 두 번째 예제에는 rs: fixedlength 특성의 미묘한 사용이 있습니다. Rs: fixedlength 특성이 true로 설정 된 열은 데이터의 길이가 스키마에 정의 되어 있어야 함을 의미 합니다. 이 경우 title_id의 유효한 값은 "123"와 같이 "123456"입니다. 그러나 "123"은 길이가 6이 아니라 3 이므로 유효 하지 않습니다. Fixedlength 속성에 대 한 자세한 설명은 OLE DB 프로그래머 가이드를 참조 하세요.  
  
## <a name="handling-nulls"></a>Null 처리  
 Null 값은 rs: maybenull 특성에 의해 처리 됩니다. 이 특성을 true로 설정 하면 열의 내용에 null 값이 포함 될 수 있습니다. 또한 데이터 행에서 열을 찾을 수 없는 경우에는 행 집합에서 데이터를 다시 읽는 사용자가 IRowset:: GetData ()에서 null 상태를 가져옵니다. 운송 테이블에서 다음과 같은 열 정의를 고려 합니다.  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 정의는 `CompanyName` null이 될 수 있지만 `ShipperID` null 값을 포함할 수 없습니다. 데이터 섹션에 다음 행이 포함 된 경우 지 속성 공급자는 열에 대 한 데이터의 상태를 `CompanyName` OLE DB 상태 상수 DBSTATUS_S_ISNULL 설정 합니다.  
  
```  
<z:row ShipperID="1"/>  
```  
  
 다음과 같이 행이 완전히 비어 있으면 지 속성 공급자는에 대해 DBSTATUS_E_UNAVAILABLE OLE DB 상태를 반환 `ShipperID` 하 고 CompanyName에 대해 DBSTATUS_S_ISNULL을 반환 합니다.  
  
```  
<z:row/>   
```  
  
 길이가 0 인 문자열은 null과 같지 않습니다.  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 이전 행의 경우 지 속성 공급자는 두 열에 대해 DBSTATUS_S_OK의 OLE DB 상태를 반환 합니다. `CompanyName`이 경우는 단순히 "" (빈 문자열)입니다.  
  
 OLE DB XML 문서 스키마 내에서 사용할 수 있는 OLE DB 구문에 대 한 자세한 내용은 "urn: schema-microsoft-com: rowset"의 정의 및 OLE DB 프로그래머 가이드를 참조 하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
