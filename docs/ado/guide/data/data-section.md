---
title: "데이터 섹션 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fae3df37c9a83bdf97a7ae2a53bc76777b318546
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="data-section"></a>데이터 섹션
데이터 섹션 업데이트, 삽입 또는 삭제 보류 중인 함께 행 집합의 데이터를 정의합니다. 데이터 섹션에는 0 개 이상의 행 포함 될 수 있습니다. 행이 스키마에 정의 되어 있는 행 집합에서 데이터를 포함할 수 있습니다. 또한 앞에서 설명한 것 처럼 모든 데이터가 없는 열을 생략할 수 있습니다. 특성 또는 하위 요소 데이터 섹션에 사용 하는 경우 해당 구문이 스키마 섹션에 정의 되지 않은 자동으로 무시 됩니다.  
  
## <a name="string"></a>문자열  
 적절 한 문자 엔터티가 포함 된 텍스트 데이터에서 예약 된 XML 문자를 바꾸어야 합니다. 예를 들어 "조의 차고" 회사 이름에는 작은따옴표 엔터티에 의해 교체 해야 합니다. 실제 행은 다음과 유사 합니다.  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 다음 문자가 XML에 예약 되어 문자 엔터티 클래스로 바꿔야: {', ", &,\<, >}.  
  
## <a name="binary"></a>이진  
 이진 데이터 (즉, 두 개의 문자를 1 바이트 맵, 한 문자를 니블) 인코딩된 bin.hex입니다.  
  
## <a name="datetime"></a>DateTime  
 Variant VT_DATE 형식 XML 데이터 데이터 형식으로 직접 지원 되지 않습니다. 올바른 데이터와 시간 구성 요소를 포함 하는 날짜 형식은 yyyy-m m-ddThh:mm:ss 합니다.  
  
 XML에 지정 된 날짜 형식에 대 한 자세한 내용은 참조는 [W3C XML 데이터 사양](https://go.microsoft.com/fwlink/?LinkId=5692)합니다.  
  
 지정 된 XML 데이터 유형에 해당 하는 데이터를 정의 하는 경우 (예를 들어 i4 int = =), ADO를 친숙 한 이름을 작성 하지만 모두에서 읽습니다.  
  
## <a name="managing-pending-changes"></a>보류 중인 변경 내용 관리  
 레코드 집합에서 즉시 열 수 나 일괄 업데이트 모드입니다. 클라이언트 쪽 커서가 있는 일괄 처리 업데이트 모드에서 열 때 UpdateBatch 메서드를 호출할 때까지 모든 변경 내용은 레코드 집합을 보류 상태로 됩니다. 보류 중인 변경 내용이 레코드 집합을 저장할 때 유지도 됩니다. Xml에서 나타나는:에 정의 된 "업데이트" 요소를 사용 하 여-microsoft-com:rowset 합니다. 또한 행 집합, 업데이트 하는 경우 업데이트할 수 있는 속성 설정 해야는 행의 정의에 true입니다. 예를 들어 보류 중인 변경 내용이 Shippers 테이블, 행 정의 정의를 모양 유사 다음 합니다.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 ADO는 업데이트할 수 있는 Recordset 개체를 만들 수 있도록 노출 데이터 지 속성 제공자 인지 나타냅니다.  
  
 다음 예제 데이터는 지속된 된 파일에 대 한 삽입, 변경 및 삭제 표시 되는 방식을 보여 줍니다.  
  
```  
<rs:data>  
  <z:row ShipperID="2" CompanyName="United Package"   
    Phone="(503) 555-3199"/>  
<rs:update>  
  <rs:original>  
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>  
  </rs:original>  
  <z:row Phone="(503) 552-7134"/>  
</rs:update>  
<rs:insert>  
  <z:row ShipperID="12" CompanyName="Lightning Shipping"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="13" CompanyName="Thunder Overnight"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="14" CompanyName="Blue Angel Air Delivery"   
    Phone="(505) 111-2222"/>  
</rs:insert>  
<rs:delete>  
  <z:row ShipperID="1" CompanyName="Speedy Express" Phone="(503) 555-9831"/>  
</rs:delete>  
</rs:data>  
```  
  
 업데이트가 변경 된 행이 데이터 전체 원래 행 데이터를 항상 포함 됩니다. 변경된 된 행은 모든 열 이나 실제로 변경 된 열만 포함할 수 있습니다. 이전 예제에서는 운송 업체 2에 대 한 행이 변경 되지 않는 및 Phone 열만 운송 업체 3에 대 한 값 변경 되었으며 변경된 된 행에 포함 하는 유일한 열 되므로 합니다. Shippers 12, 13, 및 14에 대 한 삽입 된 행이 함께 일괄 처리 된 한 rs: 삽입 태그 됩니다. 이 앞의 예제에 표시 되지 않지만 삭제 된 행도 일괄 처리할 수, note 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
