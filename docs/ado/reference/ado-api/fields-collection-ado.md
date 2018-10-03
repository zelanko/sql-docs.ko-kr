---
title: 필드 컬렉션 (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74e6deb0caba88e6bbcf2897dcfa4aaaa22f04d0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762601"
---
# <a name="fields-collection-ado"></a>Fields 컬렉션(ADO)
모든 포함 된 [필드](../../../ado/reference/ado-api/field-object.md) 의 개체를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 또는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체.  
  
## <a name="remarks"></a>Remarks  
 A **레코드 집합** 개체에는 **필드** 컬렉션으로 이루어져 **필드** 개체입니다. 각 **필드** 개체의 열에 해당 합니다 **Recordset**합니다. 채울 수 있습니다는 **필드** 열기 전에 컬렉션의 **레코드 집합** 호출 하 여를 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 컬렉션 메서드.  
  
> [!NOTE]
>  참조 된 **필드** 개체를 사용 하는 방법에 대 한 자세한 설명은 항목 **필드** 개체입니다.  
  
 **필드** 컬렉션에는 [추가](../../../ado/reference/ado-api/append-method-ado.md) 일시적으로 만들고 추가 하는 메서드를 **필드** 개체를 컬렉션 및 **업데이트**메서드를 추가 또는 삭제를 종료 합니다.  
  
 A **레코드** 개체에 사용 하 여 인덱싱할 수 있는 두 개의 특수 필드 [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) 상수입니다. 하나의 상수에 대 한 기본 스트림이 포함 된 필드에 액세스 합니다 **레코드**, 하 고 다른 액세스에 대 한 절대 URL 문자열을 포함 하는 필드를 **레코드**.  
  
 특정 공급자 (예를 들어를 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md))을 입력할 수 있습니다를 **필드** 에 대 한 사용 가능한 필드의 하위 집합을 사용 하 여 컬렉션을 **레코드** 나 **레코드 집합**합니다. 다른 필드 이름으로 참조 또는 코드에 의해 인덱싱된 먼저 될 때까지 컬렉션에 추가 되지 됩니다.  
  
 존재 하지 않는 필드 이름으로 참조 하려고 하면 새 **필드** 에 추가할 개체를 **필드** 사용 하 여 컬렉션을 [상태](../../../ado/reference/ado-api/status-property-ado-field.md) 의  **adFieldPendingInsert**합니다. 호출 하는 경우 [업데이트](../../../ado/reference/ado-api/update-method.md), ADO는 새 필드를에서 만들려면 데이터 원본 공급자에서 허용 하는 경우.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [필드 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)
