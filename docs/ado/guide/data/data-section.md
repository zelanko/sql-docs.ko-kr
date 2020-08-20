---
description: 데이터 섹션
title: 데이터 섹션 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
author: rothja
ms.author: jroth
ms.openlocfilehash: abf0202e75ef64825d6dc815624adc1c1d337174
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453575"
---
# <a name="data-section"></a>데이터 섹션
데이터 섹션은 보류 중인 모든 업데이트, 삽입 또는 삭제와 함께 행 집합의 데이터를 정의 합니다. 데이터 섹션에는 0 개 이상의 행이 포함 될 수 있습니다. 행이 스키마에 의해 정의 되는 한 행 집합의 데이터만 포함할 수 있습니다. 또한 앞에서 설명한 것 처럼 데이터를 포함 하지 않는 열은 생략할 수 있습니다. 데이터 섹션에서 특성 또는 하위 요소를 사용 하 고 해당 구문이 schema 섹션에서 정의 되지 않은 경우 자동으로 무시 됩니다.  
  
## <a name="string"></a>String  
 텍스트 데이터의 예약 된 XML 문자를 적절 한 문자 엔터티로 바꾸어야 합니다. 예를 들어 회사 이름 "Joe의 중고품"에서 작은따옴표는 엔터티로 바꾸어야 합니다. 실제 행은 다음과 유사 합니다.  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 다음 문자는 XML에서 예약 되며 문자 엔터티로 바꾸어야 합니다: {', ", &, \<,> }.  
  
## <a name="binary"></a>이진  
 이진 데이터는 bin입니다. hex로 인코드 됩니다. 즉, 1 바이트는 니블 당 한 문자씩 두 문자로 매핑됩니다.  
  
## <a name="datetime"></a>DateTime  
 Variant VT_DATE 형식은 XML 데이터 데이터 형식에서 직접 지원 되지 않습니다. 데이터 및 시간 구성 요소가 모두 포함 된 날짜의 올바른 형식은 yyyy-mm-dd: mm: ss입니다.  
  
 XML로 지정 된 날짜 형식에 대 한 자세한 내용은 [W3C XML 데이터 사양](https://go.microsoft.com/fwlink/?LinkId=5692)을 참조 하십시오.  
  
 XML 데이터 사양에서 두 개의 동일한 데이터 형식 (예: i4 = = int)을 정의 하는 경우 ADO는 친숙 한 이름을 작성 하지만 양쪽에서 읽습니다.  
  
## <a name="managing-pending-changes"></a>보류 중인 변경 내용 관리  
 즉시 또는 일괄 업데이트 모드에서 레코드 집합을 열 수 있습니다. 클라이언트 쪽 커서를 사용 하 여 일괄 업데이트 모드에서 열 경우에는 UpdateBatch 메서드가 호출 될 때까지 레코드 집합에 대 한 모든 변경 내용이 보류 중 상태가 됩니다. 보류 중인 변경 내용도 레코드 집합을 저장할 때 유지 됩니다. XML에서는 urn: 스키마-microsoft-com: 행 집합에 정의 된 "업데이트" 요소를 사용 하 여 표시 됩니다. 또한 행 집합을 업데이트할 수 있는 경우 행 정의에서 업데이트할 수 있는 속성을 true로 설정 해야 합니다. 예를 들어, 운송 테이블에 보류 중인 변경 내용이 포함 되어 있음을 정의 하기 위해 행 정의는 다음과 같습니다.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 이는 ADO에서 업데이트할 수 있는 레코드 집합 개체를 생성할 수 있도록 지 속성 공급자에 게 데이터를 노출 하도록 지시 합니다.  
  
 다음 샘플 데이터는 저장 된 파일에서 삽입, 변경 및 삭제를 확인 하는 방법을 보여 줍니다.  
  
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
  
 업데이트에는 항상 원래 행 데이터와 변경 된 행 데이터가 모두 포함 됩니다. 변경 된 행에는 모든 열 또는 실제로 변경 된 열만 포함 될 수 있습니다. 이전 예에서는 전달자 2에 대 한 행이 변경 되지 않으며 Phone 열만 전달자 3의 값이 변경 되었으므로 변경 된 행에는 유일한 열이 포함 됩니다. 운송 업체 12, 13, 14에 삽입 된 행은 하나의 rs: insert 태그에서 함께 일괄 처리 됩니다. 이전 예제에는 표시 되지 않지만 삭제 된 행도 함께 일괄 처리할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
