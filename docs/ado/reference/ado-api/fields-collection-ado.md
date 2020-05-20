---
title: Fields 컬렉션 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
author: rothja
ms.author: jroth
ms.openlocfilehash: ecf6d672bd82b6ac532306cd1ca6fc2400b215e8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762564"
---
# <a name="fields-collection-ado"></a>Fields 컬렉션(ADO)
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 또는 [Record](../../../ado/reference/ado-api/record-object-ado.md) 개체의 모든 [필드](../../../ado/reference/ado-api/field-object.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 **레코드 집합** 개체에는 **필드** 개체로 구성 된 **Fields** 컬렉션이 있습니다. 각 **Field** 개체는 **레코드 집합**의 열에 해당 합니다. 컬렉션에서 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드를 호출 하 여 **레코드 집합** 을 열기 전에 **Fields** 컬렉션을 채울 수 있습니다.  
  
> [!NOTE]
>  **Field** 개체를 사용 하는 방법에 대 한 자세한 설명은 **field** object 항목을 참조 하세요.  
  
 **Fields** 컬렉션에는 [추가](../../../ado/reference/ado-api/append-method-ado.md) 메서드가 있습니다 .이 메서드는 되었으면 **필드** 개체를 만들어 컬렉션에 추가 하 고 **업데이트** 메서드를 추가 또는 삭제를 마무리 합니다.  
  
 **Record** 개체에는 [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) 상수를 사용 하 여 인덱싱할 수 있는 두 가지 특수 필드가 있습니다. 한 상수는 **레코드**의 기본 스트림을 포함 하는 필드에 액세스 하 고 다른 하나는 **레코드**의 절대 URL 문자열을 포함 하는 필드에 액세스 합니다.  
  
 특정 공급자 (예: [Internet 게시용 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md))는 **Fields** 컬렉션을 **레코드** 또는 **레코드 집합**에 사용할 수 있는 필드의 하위 집합으로 채울 수 있습니다. 다른 필드는 이름으로 처음 참조 되거나 코드에서 인덱싱되는 경우에만 컬렉션에 추가 됩니다.  
  
 이름으로 존재 하지 않는 필드를 참조 하려고 하면 새 **field** 개체가 **Adfieldpendinginsert** [상태의](../../../ado/reference/ado-api/status-property-ado-field.md) **Fields** 컬렉션에 추가 됩니다. [Update](../../../ado/reference/ado-api/update-method.md)를 호출 하면 공급자가 허용 하는 경우 ADO에서 데이터 원본에 새 필드를 만듭니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Fields 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)
