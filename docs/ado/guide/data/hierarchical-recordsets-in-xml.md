---
title: XML의 계층적 레코드 집합 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 71b28233d8b687eff803a5897b31b2bc59bbd4e2
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700622"
---
# <a name="hierarchical-recordsets-in-xml"></a>XML의 계층적 레코드 집합
ADO는 계층적 레코드 집합 개체의 지 속성 xml을 허용합니다. 계층적 레코드 집합 개체를 부모 레코드 집합에서에서 필드의 값이 다른 레코드 집합입니다. 이러한 필드는 특성 대신 XML 스트림을에 자식 요소로 표시 됩니다.  
  
## <a name="remarks"></a>Remarks  
 다음 예제에서는이 사례를 보여 줍니다.  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 다음은 유지 된 레코드 집합의 XML 형식입니다.  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
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
  
 이 방식으로 유지 될 경우에 부모 레코드 집합의에서 열 순서가 분명 하지 않습니다. 모든 필드는 부모에서 자식 레코드 집합을 포함할 수 있습니다. 지 속성 공급자는 특성으로 먼저 모든 스칼라 열 유지 하 고 부모 행의 자식 요소로 모든 자식 레코드 집합 "열"을 유지 합니다. 부모에서 필드의 서 수 위치 레코드 집합의 스키마 정의 확인 하 여 레코드 집합을 가져올 수 있습니다. 모든 필드에 해당 필드에 대 한 서 수를 포함 하는 레코드 집합 스키마 네임 스페이스에 정의 된 OLE DB 속성 rs: 수 있습니다.  
  
 자식 레코드 집합에서에서 모든 필드의 이름이 부모가이 자식을 포함 하는 레코드 집합의 필드 이름을 사용 하 여 연결 됩니다. 이 부모 및 자식 레코드 집합 이름은 같지만 서로 다른 두 테이블에서 가져온는 필드를 포함 하는 경우 이름 충돌을 확인 하는 것입니다.  
  
 계층적 레코드 집합을 XML로 저장 하는 경우 ado에서 다음 제한 사항에 유의 해야 합니다.  
  
-   보류 중인 업데이트 된 계층적 레코드 집합을 XML로 저장할 수 없습니다.  
  
-   매개 변수가 있는 모양 명령으로 만든 계층적 레코드 집합 ADTG 또는 XML 형식으로 저장할 수 없습니다.  
  
-   ADO는 현재 binary large object (BLOB)으로 부모와 자식 레코드 집합 간의 관계를 저장합니다. 이 관계를 설명 하는 XML 태그 행 집합 스키마 네임 스페이스에 아직 정의 되지 있어야 합니다.  
  
-   계층적 레코드 집합 저장 되 면 모든 하위 레코드 집합 저장 됩니다 함께 합니다. 현재 레코드 집합 다른 레코드 집합의 자식인 경우 부모 저장 되지 않습니다. 모든 자식 현재 레코드 집합의 하위 트리를 형성 하는 레코드 집합이 저장 됩니다.  
  
 경우 계층적 레코드 집합에서에서 다시 열 XML 유지 형식으로 다음 제한 사항을 알고 있어야 합니다.  
  
-   자식 레코드를 해당 부모 레코드가 없는 레코드에 있으면 이러한 행은 계층적 레코드 집합의 XML 표현을으로 기록 되지 않습니다. 따라서 지속 된 위치에서 레코드 집합 다시 열릴 때 이러한 행은 손실 됩니다.  
  
-   자식 레코드를 둘 이상의 부모 레코드에 대 한 참조에 다음 레코드를 다시 열 때 자식 레코드 집합 포함 될 수 있습니다 중복 된 레코드입니다. 그러나 이러한 중복만 사용자 기본 자식 행 집합을 사용 하 여 직접 작동 하는 경우에 볼 수 있습니다. 장에 자식 (즉, ADO를 통해 이동 하는 유일한 방법은) 레코드 집합을 탐색 하는 데, 중복 행은 표시 되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
