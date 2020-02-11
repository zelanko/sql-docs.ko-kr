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
ms.openlocfilehash: 18d17e0a761fe03053ba90b8ff1ef87f3067df76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67930742"
---
# <a name="stayinsync-property"></a>StayInSync 속성
부모 행 위치가 변경 될 때 계층 구조 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에서 기본 자식 레코드에 대 한 참조 (즉, *장*)가 변경 되는지 여부를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **부울** 값을 설정 하거나 반환 합니다. 기본값은 **True**입니다. **True**이면 부모 **레코드 집합** 개체가 행 위치를 변경 하는 경우 챕터가 업데이트 됩니다. **False**이면 부모 **레코드 집합** 개체가 행 위치를 변경한 경우에도 장이 이전 챕터의 데이터를 계속 참조 합니다.  
  
## <a name="remarks"></a>설명  
 이 속성은 [OLE DB에 대해 Microsoft 데이터 셰이핑 서비스](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)에서 지 원하는 것과 같은 계층적 레코드 집합에 적용 되며, 자식 **레코드 집합** 을 검색 하기 전에 부모 **레코드** 집합에서 설정 해야 합니다. 이 속성은 계층적 레코드 집합 탐색을 간소화 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [StayInSync 속성 예제 (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [OLE DB 용 Microsoft 데이터 셰이핑 서비스 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
