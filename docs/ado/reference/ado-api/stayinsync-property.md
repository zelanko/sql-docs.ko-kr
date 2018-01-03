---
title: "StayInSync 속성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords: StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ef263a54892c31df4c44de8ebdb29308ef3dfb5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="stayinsync-property"></a>StayInSync 속성
계층적 나타냅니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 하는지 여부, 원본 자식 레코드에 대 한 참조 (즉,는 *장*) 부모 행 위치가 변경 될 때 변경 내용을 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **부울** 값입니다. 기본값은 **True**입니다. 경우 **True**, 장 업데이트 됩니다 부모 **레코드 집합** 개체 변경 내용을 행 위치가; 경우 **False**, 장 계속 이전 장에서 데이터 참조 하지만 부모 **레코드 집합** 개체가 행 위치를 변경 합니다.  
  
## <a name="remarks"></a>주의  
 이 속성에서 지 원하는 등의 계층적 레코드 집합에 적용 됩니다.는 [OLE DB에 대 한 Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), 부모에서 설정 해야 하 고 **레코드 집합** 자식 항목 전에  **레코드 집합** 검색 됩니다. 이 속성의 계층적 레코드 집합을 탐색을 간소화 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [StayInSync 속성 예제 (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Microsoft 데이터를 셰이핑 OLE DB (ADO 서비스 공급자)에 대 한 서비스](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
