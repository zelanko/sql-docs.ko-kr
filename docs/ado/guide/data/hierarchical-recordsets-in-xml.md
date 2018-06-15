---
title: XML에서 계층적 레코드 집합 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 697305c34e1906c95b20a2f33866bc57c1a1d019
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272062"
---
# <a name="hierarchical-recordsets-in-xml"></a>XML에서 계층적 레코드 집합
ADO는 계층적 레코드 집합 개체의 지 속성을 XML로 수 있습니다. 계층적 Recordset 개체 부모 레코드 집합에에서 있는 필드의 값이 다른 레코드 집합입니다. 이러한 필드는 특성 대신 XML 스트림을에 자식 요소로 표시 됩니다.  
  
## <a name="remarks"></a>Remarks  
 다음 예제에서는이 사례를 보여 줍니다.  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 다음은 유지 된 레코드 집합의 XML 형식입니다.  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
    xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="stor_id" rs:number="1"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="4"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="stor_name" rs:number="2" rs:nullable="true"   
        rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="40"/>   
      </s:AttributeType>   
      <s:AttributeType name="state" rs:number="3" rs:nullable="true"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="2"   
          rs:fixedlength="true"/>   
      </s:AttributeType>   
      <s:ElementType name="rsSales" content="eltOnly"   
        rs:updatable="true" rs:relation="010000000100000000000000">   
        <s:AttributeType name="stor_id" rs:number="1"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="4"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_num" rs:number="2"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="20"   
            rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_date" rs:number="3"   
          rs:writeunknown="true">   
            <s:datatype dt:type="dateTime" dt:maxLength="16"   
              rs:scale="3" rs:precision="23" rs:fixedlength="true"   
              rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="qty" rs:number="4" rs:writeunknown="true">   
          <s:datatype dt:type="i2" dt:maxLength="2" rs:precision="5"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:extends type="rs:rowbase"/>   
      </s:ElementType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  <rs:data>   
    <z:row stor_id="6380" stor_name="Eric the Read Books" state="WA">   
      <rsSales stor_id="6380" ord_num="6871"   
        ord_date="1994-09-14T00:00:00" qty="5"/>   
      <rsSales stor_id="6380" ord_num="722a"   
        ord_date="1994-09-13T00:00:00" qty="3"/>   
    </z:row>   
    <z:row stor_id="7066" stor_name="Barnum's" state="CA">   
      <rsSales stor_id="7066" ord_num="A2976"   
        ord_date="1993-05-24T00:00:00" qty="50"/>   
      <rsSales stor_id="7066" ord_num="QA7442.3"   
        ord_date="1994-09-13T00:00:00" qty="75"/>   
    </z:row>   
    <z:row stor_id="7067" stor_name="News & Brews" state="CA">   
      <rsSales stor_id="7067" ord_num="D4482"   
        ord_date="1994-09-14T00:00:00" qty="10"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="40"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
    </z:row>   
  </rs:data>   
</xml>   
```  
  
 이러한 방식으로 유지 될 경우에 부모 레코드 집합의에서 열 순서가 분명 하지 않습니다. 필드 부모에서 자식 레코드 집합을 포함할 수 있습니다. 지 속성 공급자는 모든 스칼라 열 먼저 특성으로 지속 되 면 하 고 부모 행의 자식 요소로 모든 자식 레코드 집합 "열"을 유지 합니다. 부모 필드의 서 수 위치 레코드 집합의 스키마 정의 확인 하 여 레코드 집합을 가져올 수 있습니다. 모든 필드에 해당 필드에 대 한 서 수를 포함 하는 레코드 집합 스키마 네임 스페이스에 정의 된 OLE DB 속성인 rs: 수 있습니다.  
  
 자식 레코드 집합의에서 모든 필드의 이름은 부모이 자식이 포함 된 레코드 집합에서에서 필드의 이름으로 연결 됩니다. 이 부모 및 자식 레코드 집합 필드 이름은 같지만 서로 다른 두 테이블에서 가져온를 포함 하는 경우 이름 충돌을 확인 합니다.  
  
 계층적 레코드 집합을 XML로 저장할 때 ADO에서 다음과 같은 제한 사항을 알고 있어야 합니다.  
  
-   보류 중인 업데이트 된 계층적 레코드 집합을 XML로 저장할 수 없습니다.  
  
-   XML 또는 ADTG 형식 매개 변수가 있는 shape 명령으로 만든는 계층적 레코드 집합을 유지할 수 없습니다.  
  
-   ADO는 현재 binary large object (BLOB)으로 부모 및 자식 레코드 집합 간 관계를 저장합니다. 이 관계를 설명 하는 XML 태그 행 집합 스키마 네임 스페이스에 아직 정의 되지 않은 합니다.  
  
-   계층적 레코드 집합을 저장 하는 경우 모든 하위 레코드 집합 저장 됩니다 함께 합니다. 현재 레코드 집합 다른 레코드 집합의 자식인 경우 부모 저장 되지 않습니다. 모든 하위 현재 레코드 집합의 하위 트리를 구성 하는 레코드 집합 저장 됩니다.  
  
 때 계층적 레코드 집합에서에서 다시 열 해당 XML 유지 형식 다음과 같은 제한 사항을 알고 있어야 합니다.  
  
-   해당 부모 레코드가 없는 레코드를 포함 하는 자식 레코드를 하는 경우 이러한 행은 계층적 레코드 집합의 XML 표현으로 기록 되지 않습니다. 따라서 지속 된 위치에서 레코드 집합 다시 열릴 때 이러한 행은 손실 됩니다.  
  
-   자식 레코드에 둘 이상의 부모 레코드에 대 한 참조가 있는 경우 다음 레코드 집합을 다시 열 때 자식 레코드 집합이 포함 될 수 있습니다 중복 레코드입니다. 그러나 이러한 중복 사용자 기본 자식 행 집합와 직접 통신 하는 경우에 표시 됩니다. 자식 (즉, ADO를 통해 이동 하는 유일한 방법은) 레코드 집합을 탐색 하는 장 사용 하는 경우에 중복 항목은 표시 되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
