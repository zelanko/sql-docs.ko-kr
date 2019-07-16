---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6aebf318652e604c5f5ad4c30ef389fdfd9e78c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925649"
---
# <a name="data-section"></a>데이터 섹션
데이터 섹션을 업데이트, 삽입 또는 삭제를 보류 중인 함께 행 집합의 데이터를 정의합니다. 데이터 섹션 0 개 이상의 행을 포함할 수 있습니다. 행이 스키마에 정의 되어 있는 행 집합의 데이터를 포함할 수 있습니다. 또한 앞에서 설명한 것 처럼 데이터가 없는 열을 생략할 수 있습니다. 데이터 섹션에서 특성 또는 하위 요소는 해당 구문이 스키마 섹션에 정의 되지 않은 경우 자동으로 무시 됩니다.  
  
## <a name="string"></a>String  
 적절 한 문자 엔터티를 사용 하 여 텍스트 데이터에서 예약 된 XML 문자를 바꾸어야 합니다. 예를 들어, "Joe의 Garage" 회사 이름에 작은따옴표 엔터티에 의해 대체 해야 합니다. 실제 행은 다음과 같습니다.  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 문자가 XML에 예약 되어 문자 엔터티로 대체 되어야 합니다. {', ", &,\<, >}.  
  
## <a name="binary"></a>Binary  
 이진 데이터는 bin.hex 인코딩 (즉, 두 개의 문자를 1 바이트 맵, 니블 당 하나의 문자)입니다.  
  
## <a name="datetime"></a>Datetime  
 Variant VT_DATE 형식 XML 데이터 데이터 형식으로 직접 지원 되지 않습니다. 올바른 데이터 및 시간 구성 요소를 사용 하 여 날짜 형식은 yyyy-mm-ddThh:mm:ss 합니다.  
  
 XML에 지정 된 날짜 형식에 대 한 자세한 내용은 참조는 [W3C XML 데이터 사양](https://go.microsoft.com/fwlink/?LinkId=5692)합니다.  
  
 XML 데이터 사양은 유형에 해당 하는 데이터를 정의 하는 경우 (예를 들어, i4 int = =), ADO는 친숙 한 이름을 작성 하지만 모두에서 읽습니다.  
  
## <a name="managing-pending-changes"></a>보류 중인 변경 내용 관리  
 레코드 집합에서 직접 열 수 있습니다 또는 일괄 처리 업데이트 모드입니다. 클라이언트 쪽 커서를 사용 하 여 일괄 처리 업데이트 모드로 열고 UpdateBatch 메서드를 호출할 때까지 레코드 집합에 대 한 모든 변경 내용을 보류 중 상태가 됩니다. 보류 중인 변경 내용 레코드 집합을 저장할 때 유지도 됩니다. Xml에서 urn: 스키마에 정의 된 "업데이트" 요소를 사용 하 여 표시 됩니다-microsoft-com:rowset 합니다. 또한 행 집합을 업데이트할 수 있으면를 업데이트할 수 있는 속성을 설정 해야는 행의 정의에 true입니다. 예를 들어 보류 중인 변경 내용이 Shippers 테이블에 행 정의 정의를 찾습니다 유사 다음입니다.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 이 ADO 업데이트할 수 있는 레코드 집합 개체를 만들 수 있도록 노출 데이터 지 속성 공급자를 나타냅니다.  
  
 다음 예제 데이터는 지속된 된 파일에 삽입, 변경 및 삭제를 확인 하는 방법을 보여 줍니다.  
  
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
  
 업데이트는 항상 전체 원래 행 데이터를 그 뒤에 변경된 행 데이터를 포함 합니다. 변경된 된 행은 모든 열 이나 실제로 변경 된 열만 포함할 수 있습니다. 이전 예제에서는 운송 업체 2에 대 한 행이 변경 되지 않는 고 Phone 열만 전달자 3에 대 한 값을 변경 했습니다 따라서 변경된 된 행에 포함 하는 유일한 열. Shippers 12, 13 및 14에 대해 삽입 된 행을 함께 일괄 처리 태그 아래에 있는 하나의 rs: 삽입 됩니다. 이 표시 되지 않지만 이전 예제에는 삭제 된 행도 일괄 처리할 수, note 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
