---
title: StayInSync 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords:
- StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 98a0cc1df12f905cd0d22d05b162983742d0f355
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710782"
---
# <a name="stayinsync-property"></a>StayInSync 속성
계층적 나타냅니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 하는지 여부, 기본 자식 레코드에 대 한 참조 (즉, 합니다 *장*) 부모 행 위치를 변경 하는 경우의 변경 내용입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **부울** 값입니다. 기본값은 **True**입니다. 경우 **True**, 장 업데이트할 경우 부모 **레코드 집합** 개체 변경 하는 경우 위치를 행 **False**, 장에서 계속 이전 장에서 데이터를 참조 하지만 부모 **레코드 집합** 개체가 행 위치를 변경 합니다.  
  
## <a name="remarks"></a>Remarks  
 이 속성에서 지원 되는 것과 같은 계층적 레코드 집합에 적용 됩니다는 [OLE DB에 대 한 Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), 및 부모에 설정 되어 있어야 **레코드 집합** 자식 전에  **레코드 집합** 검색 됩니다. 이 속성의 계층적 레코드 집합을 탐색을 간소화 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [StayInSync 속성 예제 (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Microsoft 데이터 셰이핑 OLE DB (ADO 서비스 공급자)에 대 한 서비스](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
