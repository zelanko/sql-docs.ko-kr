---
title: "필드 컬렉션 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords: Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 433ce545129e4a0a6ac88238ba3181fade2186bf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="fields-collection-ado"></a>Fields 컬렉션 (ADO)
모든 포함 된 [필드](../../../ado/reference/ado-api/field-object.md) 의 개체는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 또는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체입니다.  
  
## <a name="remarks"></a>주의  
 A **레코드 집합** 개체에는 **필드** 컬렉션으로 이루어져 **필드** 개체입니다. 각 **필드** 의 열에 해당 하는 개체는 **레코드 집합**합니다. 채울 수 있습니다는 **필드** 열기 전에 컬렉션의 **레코드 집합** 호출 하 여는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드는 컬렉션에 있습니다.  
  
> [!NOTE]
>  참조는 **필드** 손쉽게 사용 하는 방법에 대 한 개체 항목 **필드** 개체입니다.  
  
 **필드** 컬렉션에는 [추가](../../../ado/reference/ado-api/append-method-ado.md) 를 일시적으로 만들고 추가 하는 메서드는 **필드** 개체를 컬렉션에는 및 **업데이트**메서드를 추가 또는 삭제 작업을 마무리 합니다.  
  
 A **레코드** 개체에 인덱싱할 수 있는 두 가지 특별 한 필드가 [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) 상수입니다. 하나의 상수에 대 한 기본 스트림이 포함 하는 필드에 액세스 하는 **레코드**, 다른 액세스에 대 한 절대 URL 문자열을 포함 하는 필드는 **레코드**합니다.  
  
 특정 공급자 (예를 들어는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) 이용할 수는 **필드** 에 대 한 사용 가능한 필드의 하위 집합을 사용 하 여 컬렉션의 **레코드** 또는 **레코드 집합**합니다. 다른 필드 이름으로 참조 또는 코드에 의해 인덱싱된 먼저 될 때까지 컬렉션에 추가 되지 않습니다.  
  
 이름으로 존재 하지 않는 필드를 참조 하려고 하면 새 **필드** 개체에 추가 됩니다는 **필드** 사용 하 여 컬렉션을 [상태](../../../ado/reference/ado-api/status-property-ado-field.md) 의  **adFieldPendingInsert**합니다. 호출 하는 경우 [업데이트](../../../ado/reference/ado-api/update-method.md), 해당 공급자가 허용 하는 경우 ADO 데이터 원본에 새 필드를 만들려면 됩니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [필드 컬렉션의 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)
