---
title: "동적 속성 (ADO) 다시 동기화를 업데이트 합니다. | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c43bd5b60fef002d4fad9cc6fc6842d602d5673
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="update-resync-property-dynamic-ado"></a>동적 속성 (ADO) 다시 동기화를 업데이트 합니다.
지정 여부는 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드 뒤 암시적 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드 작업 그리고 있다면 해당 작업의 범위입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 하나 이상의 반환 된 [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) 값입니다.  
  
## <a name="remarks"></a>주의  
 나머지 값의 조합에 이미 나타내는 adResyncAll 제외한 ADCPROP_UPDATERESYNC_ENUM 값 결합할 수 있습니다.  
  
 상수 **adResyncConflicts** 기본 값으로 다시 동기화 값을 저장 하지만 보류 중인 변경 내용이 재정의 하지 않습니다.  
  
 **재 동기화 업데이트** 동적 속성에 추가 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 때는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성 **adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

