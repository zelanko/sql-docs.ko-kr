---
description: StayInSync 속성
title: StayInSync 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9677a776273e83ad31fecde3a7ea436138d3784e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988624"
---
# <a name="stayinsync-property"></a>StayInSync 속성
부모 행 위치가 변경 될 때 계층 구조 [레코드 집합](./recordset-object-ado.md) 개체에서 기본 자식 레코드에 대 한 참조 (즉, *장*)가 변경 되는지 여부를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **부울** 값을 설정 하거나 반환 합니다. 기본값은 **True**입니다. **True**이면 부모 **레코드 집합** 개체가 행 위치를 변경 하는 경우 챕터가 업데이트 됩니다. **False**이면 부모 **레코드 집합** 개체가 행 위치를 변경한 경우에도 장이 이전 챕터의 데이터를 계속 참조 합니다.  
  
## <a name="remarks"></a>설명  
 이 속성은 [OLE DB에 대해 Microsoft 데이터 셰이핑 서비스](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)에서 지 원하는 것과 같은 계층적 레코드 집합에 적용 되며, 자식 **레코드 집합** 을 검색 하기 전에 부모 **레코드** 집합에서 설정 해야 합니다. 이 속성은 계층적 레코드 집합 탐색을 간소화 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [StayInSync 속성 예제 (VB)](./stayinsync-property-example-vb.md)   
 [OLE DB 용 Microsoft 데이터 셰이핑 서비스 (ADO 서비스 공급자)](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)