---
description: XML의 계층적 레코드 집합
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3e6180c8aa422c5833234afba7881a1a4c8b9049
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806019"
---
# <a name="hierarchical-recordsets-in-xml"></a>XML의 계층적 레코드 집합
ADO에서는 계층적 레코드 집합 개체를 XML로 지 속성을 사용할 수 있습니다. 계층적 레코드 집합 개체를 사용 하는 경우 부모 레코드 집합의 필드 값은 또 다른 레코드 집합입니다. 이러한 필드는 특성이 아니라 XML 스트림에 자식 요소로 표시 됩니다.  
  
## <a name="remarks"></a>설명  
 다음 예에서는이 경우를 보여 줍니다.  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 다음은 지속형 레코드 집합의 XML 형식입니다.  
  
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
  
 부모 레코드 집합에 있는 열의 정확한 순서는 이러한 방식으로 지속 될 때 명확 하지 않습니다. 부모에 있는 모든 필드에는 자식 레코드 집합이 포함 될 수 있습니다. 지 속성 공급자는 모든 스칼라 열을 먼저 특성으로 유지 한 다음 모든 자식 레코드 집합 "columns"를 부모 행의 자식 요소로 유지 합니다. 레코드 집합의 스키마 정의를 살펴보면 부모 레코드 집합에 있는 필드의 서 수 위치를 가져올 수 있습니다. 모든 필드에는 해당 필드의 서 수 번호를 포함 하는 레코드 집합 스키마 네임 스페이스에 정의 된 rs: number OLE DB 속성이 있습니다.  
  
 자식 레코드 집합에 있는 모든 필드의 이름은이 자식을 포함 하는 부모 레코드 집합의 필드 이름과 연결 됩니다. 이는 부모 및 자식 레코드 집합에 두 개의 서로 다른 테이블에서 가져온 필드가 있지만 이름이 개별 인 경우에는 이름 충돌이 발생 하지 않도록 하기 위한 것입니다.  
  
 계층적 레코드 집합을 XML로 저장 하는 경우 ADO에서 다음과 같은 제한 사항을 알고 있어야 합니다.  
  
-   업데이트 보류 중인 계층적 레코드 집합은 XML로 보관할 수 없습니다.  
  
-   매개 변수가 있는 shape 명령을 사용 하 여 만든 계층적 레코드 집합은 XML 또는 ADTG 형식으로 유지할 수 없습니다.  
  
-   현재 ADO는 부모 및 자식 레코드 집합 간의 관계를 BLOB (binary large object)로 저장 합니다. 이 관계를 설명 하는 XML 태그가 행 집합 스키마 네임 스페이스에 아직 정의 되지 않았습니다.  
  
-   계층적 레코드 집합을 저장 하면 모든 자식 레코드 집합도 함께 저장 됩니다. 현재 레코드 집합이 다른 레코드 집합의 자식인 경우 해당 부모는 저장 되지 않습니다. 현재 레코드 집합의 하위 트리를 구성 하는 모든 자식 레코드 집합이 저장 됩니다.  
  
 계층적 레코드 집합이 XML 지속형 형식에서 다시 열리면 다음과 같은 제한 사항을 알고 있어야 합니다.  
  
-   자식 레코드에 해당 부모 레코드가 없는 레코드가 포함 되어 있는 경우 이러한 행은 계층적 레코드 집합의 XML 표현으로 작성 되지 않습니다. 따라서 이러한 행은 지속형 위치에서 레코드 집합을 다시 열 때 손실 됩니다.  
  
-   자식 레코드에 둘 이상의 부모 레코드에 대 한 참조가 있는 경우 레코드 집합을 다시 열면 자식 레코드 집합에 중복 레코드가 포함 될 수 있습니다. 그러나 이러한 중복은 사용자가 기본 자식 행 집합을 사용 하 여 직접 작업 하는 경우에만 표시 됩니다. 하위 레코드 집합을 탐색 하는 데 챕터를 사용 하는 경우 (ADO를 탐색 하는 유일한 방법) 중복 항목이 표시 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 형식으로 레코드 유지](./persisting-records-in-xml-format.md)